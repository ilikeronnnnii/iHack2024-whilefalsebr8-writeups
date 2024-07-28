first of all we were given a url, together with the credentials `employee01:password`

![Pasted image 20240727230933](https://github.com/user-attachments/assets/25eacc64-7e33-478c-9e94-6928902f5cdc)

once logged in, you can press download button to get the data of employee attendance sorted by month, and the request will be `GET /download?month={insert_month}.json`

![image](https://github.com/user-attachments/assets/9179036c-063d-4782-b3ea-f39dcf97fc30)

now looking at page source code on `index.html` there is an interesting path

```html
<button onclick="downloadJSON()">Download JSON</button>
<button onclick="logout()">Logout</button>
<button href="/admin/flag.html" hidden>Flag</button>
```

when visiting to `admin/flag.html`, the request is unauthorized

![image](https://github.com/user-attachments/assets/7bfe0a28-c32b-4e25-81e6-3c09e99c4d73)

from the previous feature of downloading employee attendance, we can alter the request to download the flag.html file, by doing the path traversal attack `GET /download?month=../admin/flag.html`

![Pasted image 20240727231035](https://github.com/user-attachments/assets/c9a5cf34-b21c-4893-b577-5e117fb51c9b)

now unzip the file, and take a look at the content of flag.html

![Pasted image 20240727231311](https://github.com/user-attachments/assets/13667987-7357-4254-99fd-ff0a889f3593)

![Pasted image 20240727231341](https://github.com/user-attachments/assets/1befef80-6508-4619-b0d5-376152a80f38)

flag `ihack24{8d1f757aa744f459ac7ef07ebe0e2651}`

