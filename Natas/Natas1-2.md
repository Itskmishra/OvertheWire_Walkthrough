# Natas 1-2

## Description
*No description*
## Provided Information

	Username: natas2
	URL:      http://natas2.natas.labs.overthewire.org

## Solution
We can use the password from the last challenge to log in, just as we did in the previous challenge. However, upon logging in, we are greeted with a message that says there is nothing on the page. 

![natas2-message](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/3d477df1-3afd-4c6e-88ed-6ee98aa293ea)

We checked the source code, but there was nothing useful there either.

![natas2-page-source-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/339c6841-4d6f-4163-ba1b-855febb3c4d6)

However, there is an image file in the source code that we noticed. By adding "/files/pixel.png" after the URL, we can see that this is an image of a pixel, and there is nothing else on the page.


![natas2-pixel-img](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/205aa2a3-3bcc-4163-b0c6-f8456df195c8)

Despite this, we can still manipulate the URL. When we add or remove values from it, it is called "path traversal." We removed "pixel.png" from the URL to test it for path traversal. 

![natas2-file-indexing](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/7aa0d81b-95d0-472d-a26f-8b0d3bbdd6d7)

On visiting "URL/files," we can see that there are two files: "pixel.png" and "users.txt." We already know what "pixel.png" is, so we decided to check out "users.txt." 

![natas2-users-file](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/2104f408-bb73-4a44-a390-7cfb492e8889)

When we visited the file, we found a list of usernames and passwords for users, including the natas3 password that we needed to retrieve. 

## Conclusion

It is essential to consider every piece of information when testing web applications. There are various methods and attacks that can be performed, so we should be careful not to make any simple mistakes that could lead to getting hacked.

###### Happy Hacking :)

