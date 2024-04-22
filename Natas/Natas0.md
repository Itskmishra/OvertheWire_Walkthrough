# Natas 0

## Description
*No description*

## Provided Information
	Username: natas0
	Password: natas0
	URL:      http://natas0.natas.labs.overthewire.org
 
## Solution
Upon visiting the provided URL, a login dialog box appears where we can use the provided username and password to log in successfully. Once logged in, a message appears on the page. 

![natas0-message](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/0fdccbac-9780-4ef3-80fe-1814c489f89a)

But there is no other text on the screen except message. To enumerate any website, it is important to check its source code for any information disclosure. We can use the inspect tool or right-click to view the page source code. 

![natas0-page-source-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/ffcc2ce8-46a6-491a-8890-e932373b578e)

In the page source, the password for natas1 is disclosed. 

## Conclusion
Checking the page source is an important step when testing web applications. Sometimes people make mistakes, and we, as ethical hackers, can leverage those mistakes.

###### Happy Hacking :)
