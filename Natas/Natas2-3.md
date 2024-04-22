# Natas 2-3 

## Description
*No description*
## Provided Information

	Username: natas3
	URL:      http://natas3.natas.labs.overthewire.org

## Solution

Upon using the credentials found in the last challenge to log in, we are greeted with a message on the page that says "nothing on this page".



![message](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas3-message.png)


To proceed, we can follow the same methods we used in the previous challenges - such as looking at the source code and checking for information leaks. 


![sourcecode](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas3-page-source-code.png)

Although we don't find any information leaks in the source code, we do find a comment that says "no information leaks, and not even Google will find it this time".



If we have knowledge about Google and website crawling, we can easily figure out what it means. For those who are not familiar with crawlers, let me explain. Google web crawlers crawl all websites on the internet to improve their website indexing and user research. To prevent these web crawlers from accessing sensitive information or URL routes on a website (such as '/admin' and more), websites usually use various methods like setting headers, using special files like 'robots.txt', and many more. As hackers, we can also use these files to know about sensitive URLs and routes of a website.

![robotsfile](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas3-robots-file.png)

Upon visiting '/robots.txt', we find a URL route - '/s3cr3t'. 


![secretpath](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas3-file-indexing.png)
Visiting this route, we find a file named 'users.txt'. 

![usersfile](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas3-user-file.png)
Inside this file, we can find the password for natas4, which is our next challenge.


## Conclusion
Sometimes, with an understanding of a website's configuration, sensitive information can be accessed without much effort.

###### Happy Hacking :)

