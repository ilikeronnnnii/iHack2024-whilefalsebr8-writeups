Lock?

![image](https://github.com/user-attachments/assets/63471007-5ae4-4e26-9b07-d0cbf7561b0e)

So first we were given three event logs windows and one disc image file. The log files and thousands of entries, I decided to just use Hayabusa to help me filter the logs. 
`.\hayabusa-2.16.0-win-x64.exe csv-timeline -d D:\iHack2024\lock -p verbose -o D:\iHack2024\lock\results.csv`

![image](https://github.com/user-attachments/assets/3142e0a2-e69b-443d-b5df-b8381eee9ba3)
![image](https://github.com/user-attachments/assets/09770109-500d-4c55-9414-7d959fbfa7b9)

This was the result summary showing 4 events. Then I open timeline with the result.csv from Hayabusa and checked them. 

 ![image](https://github.com/user-attachments/assets/4600532b-f416-46b3-8114-050a25395505)

Here in timeline, I found an event with password and went to dismount the disk image that was given in Linux. When mount, it needs a passphrase, and I used pa55iPOjLKbMN as the passphrase. 

![image](https://github.com/user-attachments/assets/b7b558df-83c7-4833-a4a0-9cd83dbeca47)
  
After entering the password: 

![image](https://github.com/user-attachments/assets/ea4d7abf-178a-4bc1-8a47-c1be172a0c8b)
![image](https://github.com/user-attachments/assets/3e9093d2-a153-429a-a693-729d1ff3b4c3)

Then open the flag.txt that has the flag: `ihack24{6f6450f1695e405557486a2be402dc27}`

