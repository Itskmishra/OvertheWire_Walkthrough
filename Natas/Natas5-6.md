# Natas 5-6

## Description
*No description*
## Provided Information
	Username: natas6
	URL:      http://natas6.natas.labs.overthewire.org
## Solution
After visiting the page, we can see an input field that asks for a secret and a button to view the page source code.

![natas6-home-page](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/cd53dd6a-52ce-4a82-8377-39ae8728770c)

Clicking on the button opens up the page source code, which contains a simple script. 
 
 ![natas6-page-source-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/a29ea38f-a962-48b0-adb1-25e3f6e0b90b)

Let's try to understand this script line by line. Firstly, the script imports a file called "secret.inc" using the command `include "includes/secret.inc"`. This tells us that the script is likely a PHP script and is importing the "secret.inc" file. Next, we notice that there is an if-else condition that checks if the form has been submitted. If it has, then the script compares the inputted secret to the secret variable, which is probably coming from the "secret.inc" file. 

To access the file, we can try entering the URL path `URL?includes/secret.inc` into the address bar. 

![natas6-url](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/f6e9bff4-1297-4eaf-88a7-031325400592)

Upon loading the file, we see that there is nothing on the page.

![natas6-secret-file](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/942a4160-b9b9-4ee1-91e8-27f565748f58)

However, we should check the source code to see if there is any hidden content.

![natas6-secret-file-sourec-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/5e7506a9-350f-4129-b957-3d63e538d17f)

In the source code, we notice a PHP script that defines a variable called "secret" and assigns it a string value. This is the secret we need to enter into the input field to get the password for natas7. 

![natas6-home-page](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/e3555625-5ee6-46f6-9343-0a38c16e409e)

## Conclusion
Understanding programming and development is helpful in cybersecurity as it allows us to understand scripts and sometimes even write our own.

###### Happy Hacking :)
