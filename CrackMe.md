CrackMe

![image](https://github.com/user-attachments/assets/77218433-cff2-4cda-9a16-06821e39492b)
![image](https://github.com/user-attachments/assets/e4d77b6b-19ec-4b8f-96f1-14a7dd7a4e37)

So, in this challenge we were given multiple files, I just opened the application saw what needed to do and then I just opened the crackme.dll file using ILSpy. Here I saw form1 under crackme which functions like `btnsubmit`, `validateLicenseKey` and `secretkey` sounding like something that is usen in the given program. I then took a look into the functions. 

`Secretkey:`                                                                                            

![image](https://github.com/user-attachments/assets/e26843d3-b384-43ce-9229-b9d134d411c6) 

`ValidateLicensekey:`

![image](https://github.com/user-attachments/assets/6e2ea4e6-5ce5-40e0-b514-940c1aea0c14)


From this both functions secret key: `1724-2321-NBSI-HACK`
Making the flag: `ihack24{1724-2321-NBSI-HACK}`
