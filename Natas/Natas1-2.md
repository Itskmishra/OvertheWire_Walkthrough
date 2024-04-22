# Natas 1-2

## Description
*No description*
## Provided Information

	Username: natas2
	URL:      http://natas2.natas.labs.overthewire.org

## Solution
We can use the password from the last challenge to log in, just as we did in the previous challenge. However, upon logging in, we are greeted with a message that says there is nothing on the page. 

![Message](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas2-message.png)

We checked the source code, but there was nothing useful there either.

![sourcecode](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas2-page-source-code.png)

However, there is an image file in the source code that we noticed. By adding "/files/pixel.png" after the URL, we can see that this is an image of a pixel, and there is nothing else on the page.

![pixel-img](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas2-pixel-img.png)

Despite this, we can still manipulate the URL. When we add or remove values from it, it is called "path traversal." We removed "pixel.png" from the URL to test it for path traversal. 

![file-indexing](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas2-file-indexing.png)

On visiting "URL/files," we can see that there are two files: "pixel.png" and "users.txt." We already know what "pixel.png" is, so we decided to check out "users.txt." 

![users-file](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas2-users-file.png)

When we visited the file, we found a list of usernames and passwords for users, including the natas3 password that we needed to retrieve. 

## Conclusion

It is essential to consider every piece of information when testing web applications. There are various methods and attacks that can be performed, so we should be careful not to make any simple mistakes that could lead to getting hacked.

###### Happy Hacking :)

