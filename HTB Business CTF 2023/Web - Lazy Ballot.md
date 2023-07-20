#webex #burpsuite
#writeup_sipoer
**![](https://lh4.googleusercontent.com/JFIXQ2A5XAKvHPpChPqM__sYuyEdTDBRlw3ML80AU7tMMXmhRS2-kgSlEXXNy8uhnddf2KFOUYJFkQHQXLAdz0NytxfKAwMDYZiUm9mQ1S4OuXekMVBPbadAfs3YbY-1KM54K0YWLXTyXaTu63a2JLs)**

**Tampilan web**
**![](https://lh4.googleusercontent.com/iTVFaEBfaQv6W9IQ_6lLj9WptAUpxhAZbCgpgjBIsmZn75WgfyTjq1dk_QjxjNK_5GVji95ZXt7PMutknmhklqf6UDUwFSf0bfIK__TCJjvGcNr-Nvn6d36sd2jgHPqypcrXthaRbGtpiCPFUwJQQPQ)**
1. dikarenakan chall ini white box, kita bisa membaca source codenya. saya akan membaca routes (index.js), disini terdapat beberapa informasi path seperti path `/login`, `/dashboard`, `/api/votes/list`, `/api/login`.
**![](https://lh6.googleusercontent.com/vM7F4l7_p1Ob2hzGSjflvRedoUAeYpnVIf_UMZdfSb0lMz587JGNff7XRmbc0fyHzOTH7H4W7IyIVkarmwi1OKAGh8jNbFqPmih3L00eJ91XSmB5l5iqW-9ME87wT6pkgtEY75GysvveBpNP5IB2DHw)**
2. Selanjutnya kita akan masuk ke path login melalui web, disini terdapat tempat untuk memasukan username dan password 
**![](https://lh4.googleusercontent.com/Nch8H_nF3xl70BG4zUg-Rge1olatV4xTAKweFtOuzqJeY5RacSDKVrAR54djuWLaYXDITX1-V3rW-Pqzbf7Z3hGMc9gW17WxInlwj9eZ7uaUGcLwOY3-jAMWTMF0VmH5XvFzMmtJNGyfNbZ8d_o120Y)**
3. kemudian saya akan membaca source pada helpers /database.js, saya mendapatkan data yang menyatakan bahwa username admin dan passwordnya pass.
![[attachments/Pasted image 20230717225149.png]]
4.  disini saya tau bahwa database menggunakan coughdb atau nosql. sehingga saya akan mencoba bypass paswordnya itu menggunakan nosql injection (referensi = https://book.hacktricks.xyz/pentesting-web/nosql-injection).
```
{"username": {"$ne": "foo"}, "password": {"$ne": "bar"} }
```
**![](https://lh5.googleusercontent.com/ZZgManmWE_eHkG3270kf12mCBFvjVZpPkHWi2rIADgRh5f_aRvEE7s5WRZ8LAAL9lhvaQSYX8aOiphaLP7bTjRif5BUx4l2cYciMOAzAn9Jj6PqSQeZsSVp6YsdsQKI1C0CvwkzUKJucgHmVBsTNZ38)**
5. Terdapat format nosql yang dapat kita jadikan nosql injection, kita akan memasukannya ke repeater dan saya akan menggati password menjadi `{"$ne":"bar"}}`, kemudian kita send
**![](https://lh4.googleusercontent.com/GHUlPOLwxwqXsPOeXzZmcGcIkSPrlWoA4IQ35eS_9bOI2RhhvL04U_h7NnxVYssNNeHiU9NdlKYx53sFp3Bx_VO8oNNGMjM9XqHDMX8I4sMuJgZBh-krYM7UnMiyu0mLWelk_YVpbJtaRQdgw5Ua2Hs)**
6. Authentifikasi berhasil dan kita mendapatkan session cookiee, kemudian kita akan mengakses halaman dasboard dengan session cookie yang diberikan 
**![](https://lh6.googleusercontent.com/Ai1smu08eNMMNXSS2eKtGxMW_E_6aDbGFMszhEsOPk4MTV2Esww-d2z0UhVPFU6Jnm8H65U0mimBe5mm4s79yrxBR2p89qeoz8pNEU2uQqpkG6fJswBBBteJZC0CTeqOdFReAsVprIURAby0rV03x2U)** 7. **Kita akan searching flagnya, ternyata flag terdapat pada kolom 9** 
**![](https://lh3.googleusercontent.com/kL4NYhP3jB_4Y5endxoWt31uuesuMDQC8dY1ooNwqEBglCHf3mVvmKaROt40SpXITRpzgUNA3cWgpmrhtbvJ8K9Fu-HfIUamDDDzilBwfmsuUxhkLPMM605X6d3K4W0s76YH4iNWHZubnGE3fXNiq54)**

FLAG = **HTB{c0rrupt3d_c0uch_b4ll0t}** 

