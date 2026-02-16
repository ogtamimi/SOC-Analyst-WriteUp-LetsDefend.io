# LECTURE6: Detecting Web Attacks - 2
## 1) Detecting Open Redirection Attacks

```
What is Open Redirection?

Open redirection is a web security vulnerability that occurs when a website or web application redirects users
to a different URL without proper validation or sanitization of the target URL. Attackers can 
exploit Open Redirection to trick users into visiting malicious websites or performing actions unintended by the website owner.

In an open redirection attack, an attacker typically crafts a legitimate URL hosted on the vulnerable website, 
but includes a malicious URL as a parameter or query string. When a user clicks on the crafted URL, the website's 
redirect mechanism automatically redirects the user to the malicious URL, which can lead to various malicious activities, 
such as phishing attacks, spreading malware, or stealing sensitive information.

Open redirection vulnerabilities commonly occur when websites use user-supplied input, such as URLs, as part of their 
redirect mechanism without proper validation or sanitization. To prevent open redirection attacks, web developers should 
validate and sanitize all user-supplied input used in redirections, and ensure that only trusted and whitelisted URLs 
are allowed for redirection. Additionally, it's important to implement proper authentication and authorization mechanisms 
to ensure that only authenticated and authorized users can perform redirects. Regular security testing, including 
vulnerability scanning and penetration testing, can also help identify and fix open redirection vulnerabilities in web 
applications.
```

Open Redirection Types:
* URL-based open redirection: This is the most common type of open redirection
vulnerability. It occurs when a website takes a URL or a URL parameter as input 
and uses it in a redirect without proper validation or sanitization. An attacker 
can craft a malicious URL that includes a different domain or malicious URL as 
a parameter which will be included in the redirect, leading to an unintended 
redirection to a malicious website.
* JavaScript-based open redirection: This type of open redirection vulnerability 
occurs when a website uses JavaScript to perform a redirect .
* Meta refresh-based open redirection: This type of open redirection vulnerability 
occurs when a website uses the HTML "meta refresh" tag to redirect users to another 
URL automatically .
* Header-based open redirection: This type of open redirection vulnerability 
occurs when a website uses HTTP headers, such as "Location" header, to perform a 
redirect .
* Parameter-based open redirection: This type of open redirection vulnerability 
occurs when a website uses a parameter in the URL or in a form submission as part 
of the redirect process.

```
to Prevention Methods for Open Redirection : 

-Validate and sanitize input
-Use a whitelist approach NOT A BLACKLIST!
-Avoid using user-controlled data in redirects
-Implement proper authorization and authentication
-Implement proper authorization and authentication

```

### LAB 

```
Detecting Open Redirect Attacks
What was described in Part 1 was a list of things to do from the perspective of a hacker/attacker. At the 
same time, the issues that a developer should pay attention to while developing were also mentioned.

So in this part, let’s have a look at how to detect Open Redirection attacks with an example. But, before 
moving, let’s quickly recap some of the important things to detect Open Redirection attacks;

If there is a consecutive requests to query string parameters such as ?next (http://website.com/param.php?next=), 
or ?url ( http://website.com/…?url=), with payloads like http://attacker.com or attacker.com (URL structure)
For the WAF or other middleware products, sometimes payloads can have bypass techniques like;

* Localhost
http://[::]:25/
http://①②⑦.⓪.⓪.⓪

* CDIR
http://127.0.0.0

* Decimal Bypass
http://2130706433/ = http://127.0.0.1

* Hexadecimal Bypass
http://0x7f000001/ = http://127.0.0.1

* Encoded characters like %2f = /
Of course it’s not possible to detect or analyze web server logs without using automated detection methods. 
For an easier way, any SOC analyst can use the following regex to detect open redirection attacks. 

/^.*"GET.*\?.*=(https%3a%2f%2f[a-z0-9-]+%2e[a-z]{2,}).+?.*HTTP\/.*".*$/gm

This regex will match any log entry where the HTTP method is GET, the request contains a query parameter 
with https://x.com, and the request is using HTTP version 1.0 or 1.1. This should match the most common open 
redirection attack patterns.

You can customize this regex to match specific query parameters or HTTP methods that are relevant to your 
web application. Remember that this regex is just one part of an overall security monitoring strategy and 
should be used in conjunction with other security tools and best practices.
```

### lets solve it :
1. Open /root/Desktop/QuestionFiles/Open-Redirection/access.log and check All users 
![alt text](..\Assets\lab6\1.png)

2. this IP: 254.198.150.19 Indicators:
* Massive repeated requests in milliseconds
* Many 499 status codes
* Rapid repeated retries

What This Suggests:
Automated enumeration / brute force testing

![alt text](..\Assets\lab6\2.png)



3. Using the regrex Method to Filtering the Log to Confirm
![alt text](..\Assets\lab6\3.png)

4. Check this User 86.236.188.85:
+ URL-encoded payloads
+ Attempting external domain injection
+ Trying path traversal / open redirect tricks 
![alt text](..\Assets\lab6\4.png)

5. Results

| IP             | Behavior                       | Classification    |
| -------------- | ------------------------------ | ----------------- |
| 178.78.113.5   | Normal browsing                | Benign            |
| 206.52.45.12   | Comment + browsing             | Benign            |
| 254.198.150.19 | Enumeration + rapid retries    | Automated Attack  |
| 86.236.188.85  | Encoded URL injection attempts | Injection Testing |



#### What date did the exploitation phase of Open Redirection start? Format: dd/MMM/yyyy HH:mm:ss
> **ANSWER: 27/Apr/2023 15:45:22**
#### What is the IP address of the attacker who performed the Open Redirect attack?
> **ANSWER: 86.236.188.85**
#### What was the parameter that attacked?
> **ANSWER: postId**


## 2) Detecting Directory Traversal Attacks 
