#scada #wireshark 
#writeup_sipoer
1. Diberikan sebuah file zip dengan nama ics_wacth_tower.zip, kemudian kita akan melakukan extract dan mengeluarkan file tower_logs.pcapng
**![](https://lh6.googleusercontent.com/iUAqVADoxVk21u3fWLIaloWKmun98yBBf7Oewd1F99yrIYXGsE-_pNQvxIPambvQmKnNJ-CQKO-hEVVSxpjO_ZVwfGW18OOb6Va1R8nTA8UEdC5wLJxsJ1cWMhLGnsYqMwfYqeULnk8o9p4P-zGMwz4)**
2. selanjutnya, kita akan membuka file pcapng dengan menggunakan tools wireshark, dan terdapat logs dari scada dengan protokol modbus
**![](https://lh3.googleusercontent.com/Y8EV6RHM4XZNAHaUvZNNhNZLy6oLjFpzeNYWg3xvutSrIaD8U-vRgrCx6hsFzPrOxgBBv8Cmz1yhYcGKfdP7F9xZpS2Jku0CMDCLmH61kIvP_1Ix7kstZNM8popxZFedCQCvZ53tSm_olisLqR_kfwE)**
3. kemudian kita akan melakukan analyze dari logs dengan menggunakan opsi Analyze > Follow > TCP Stream
![[attachments/Pasted image 20230717222613.png]]
**![](https://lh5.googleusercontent.com/Q53cPVElluGh86fl4DYThombYbiOQfFFBBqm7YBpFgBxd-DayvRb3lJ6voxa3EoUjErtOQ_n8hVHuHpdxkNp4M7Afqcs6S39qs7XKmFd6kVCV3ZEXhK6ZGvosuvIAEm7yaqKy8h1jx4p82nsUI7_tss)**
4. kemudian kita akan melihat data dengan format selain ascii, disini saya coba beberapa format dan ketemu format yang cocok yaitu Hex Dump
**![](https://lh4.googleusercontent.com/WUQq289ed5u5IokR_gOQt1G3DVDz4fAJQJkrsy2VVapp7bNt-uqD_5smTQMZcZd70MfrC03FShSWj9BZRzh5t2uYr4_EGPERgsz3AHCXGk_mnF9ptbBtttUbSa1gS4Lfgn0oJ7d3-cC-A5x2-c4bJjA)**

**FLAG = HTB{m0d8u5_724ff1c_15_un3nc2yp73d!@^}** 



