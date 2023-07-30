#crypto #cyberchef
#writeup_sipoer 
![[attachments/Pasted image 20230717234109.png]]
![[attachments/Pasted image 20230717234357.png]]
`Cipher target xor cipher known xor plaintext known`
FLAG = HTB{unpr0t3cted_bl0ckch41n_s3cur1ty_p4r4m3t3rs!!!} 

Rationale
diketahui masing masing plaintext menggunakan kunci yang sama dalam proses enkripsi. hal itu dapat diketahui dari script python yang disertakan. mode yang dipakai untuk mengenkripsi adalah AES_CTR. sehingga metode untuk memecahkannya adalah sebagai berikut:

Asumsi
Key= key yang digunakan.
Plaintext_Known= plaintext yang diketahui hasil menjadi ciphertext. karena kesamaan penggunaan kunci
plaintext_result = hasil yang dicari
ciphertext_target = cipher teks yang ingin dibongkar

dengan demikian

Plaintext X Key >>>ciphertext
Plaintext_known X Key >>>Ciphertext_known


untuk memecahkannnya adalah(working in bit realm)
Ciphertext_target XOR Ciphertext_known >>>Processed_text
akan menghasilkan text baru dengan asumsi perlu untuk dibandingkan dengan plaintext_known untuk mengekstrak plaintext_target. kunci dapat diabaikan, seolah olah proses ini merupakan menyertakan kunci yang didapat dari ciphertext_known

kemudian untuk itu lakukan 1 kali proses lagi
Processed_text XOR Plaintext_known >>> Plaintext target
hal ini dilakukan untuk menghilangkan Plaintext_known dari processed_text.

