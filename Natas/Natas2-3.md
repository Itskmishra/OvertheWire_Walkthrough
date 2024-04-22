# Natas 2-3 

## Description
*No description*
## Provided Information

	Username: natas3
	URL:      http://natas3.natas.labs.overthewire.org

## Solution

Upon using the credentials found in the last challenge to log in, we are greeted with a message on the page that says "nothing on this page".

![natas3-message](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/c97a5cec-48bc-4edc-84b9-cac9935e171c)


To proceed, we can follow the same methods we used in the previous challenges - such as looking at the source code and checking for information leaks. 



![natas3-page-source-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/df801706-ef43-4ee7-a1e0-b55549aab6a8)

Although we don't find any information leaks in the source code, we do find a comment that says "no information leaks, and not even Google will find it this time".



If we have knowledge about Google and website crawling, we can easily figure out what it means. For those who are not familiar with crawlers, let me explain. Google web crawlers crawl all websites on the internet to improve their website indexing and user research. To prevent these web crawlers from accessing sensitive information or URL routes on a website (such as '/admin' and more), websites usually use various methods like setting headers, using special files like 'robots.txt', and many more. As hackers, we can also use these files to know about sensitive URLs and routes of a website.


![natas3-robots-file](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/ac63b455-3979-4863-b49a-6c4b0e6bc183)

Upon visiting '/robots.txt', we find a URL route - '/s3cr3t'. 



![natas3-file-indexing](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/94e1d7c4-91f5-44ef-a659-301dfe07a2c8)

Visiting this route, we find a file named 'users.txt'. 

![natas3-user-file](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/4af8f453-f1a0-4fce-b633-7b7188cf4a25)

Inside this file, we can find the password for natas4, which is our next challenge.


## Conclusion
Sometimes, with an understanding of a website's configuration, sensitive information can be accessed without much effort.

###### Happy Hacking :)

