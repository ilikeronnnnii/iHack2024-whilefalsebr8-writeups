For this challenge we were given a `auth` text file.

![image](https://github.com/user-attachments/assets/f1c7535b-b769-48c6-be2a-69c8917a7814)

After opening it in splunk, I could see multiple instances of ip addresses being brute forced. 

![image](https://github.com/user-attachments/assets/5a4945df-0af1-49b1-9249-4df0f84ba506)

I saw the logs and the ip address `149.102.244.68` was getting handled by invalid user, so this ip address must be the compromised one. 

![image](https://github.com/user-attachments/assets/3ef65fda-8d1d-4bcf-a2a7-759e9b28b895)
 
This log seems interesting as right after the authentication was failed, the connection was closed by the user `sysadmin`, so the flag  is `ihack24{149.102.244.68_ sysadmin}`
