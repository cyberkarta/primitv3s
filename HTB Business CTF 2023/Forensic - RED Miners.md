#forensic #strings
#writeup_sipoer
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