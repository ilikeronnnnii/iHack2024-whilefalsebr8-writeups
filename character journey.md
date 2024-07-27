when visiting the url `character-journey.ihack24.capturextheflag.io` we were presented with a login form

![Pasted image 20240727212737](https://github.com/user-attachments/assets/c6e79f03-e148-446b-83a8-1d0462f3e440)

like always, to login you need to first register

![Pasted image 20240727212749](https://github.com/user-attachments/assets/1c21485c-a979-4338-99d6-27a556468aab)

once registered, try to login again, and you will be given a dashboard page 

![Pasted image 20240727212809](https://github.com/user-attachments/assets/40f7cbc7-c47f-4d5d-824c-b7621303eeff)

choosing My Account menu will create a new GET request to profile.php page with a parameter `userId=xxx`

![Pasted image 20240727213046](https://github.com/user-attachments/assets/6585e87e-567a-4e9b-94c5-0459a252a8f9)

therefore, changing the userId parameter values leads to a different webpage thus conclude that this webpage is vulnerable to IDOR Attack. To obtain the flag just snipe it using burp suite, the flag is at parameter value of `userId=53`

![Pasted image 20240727213304](https://github.com/user-attachments/assets/281ecd36-6676-4acc-836a-0f446dfc4ecb)

flag `ihack24{655b7b7ae4c62d726a568eff8914573e}`
