Leviathan 0
-----------

Leviathan 0 first level of the leviathan war game (over the wire).

## Introduction 
There is no information provided on the level page, so we don't have a starting point. Except the credentails provided on the home screen.

## Tool and commands used
*   ls
*   ssh
*   cat
*   grep
*   wc ( optional )
*   cd 

## Solution

### STEP 1:
The first step is to login to the machine using the provided credentials on the homepage of the war game.

```text-x-sh
ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```


After logging in, we need to understand our environment better to locate the flag. Listing all the files in the current folder is an effective way to do this.

![image](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/bb741933-a91d-42da-9d07-f4cb47cba2ca)


```text-x-sh
ls -al
```

### STEP 2:
When listing the files in the folder, we find a folder called ".backup".

```text-x-sh
cd .backup
```

Exploring it further, we find another file called "bookmarks.html."

![image](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/087d0235-18e2-4bc6-b214-6fe650678872)

```text-x-sh
ls -al
```

### STEP 3:

This file is a very long HTML file with dt tags, and have something inside in every tag. let's check how many lines are there to get a good understanding with file length and size.

![image](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/5d5e0d3f-4457-4156-b2a1-e5ddaa9f45c3)


```text-x-sh
wc bookmark.html
```


It requires a lot of effort to go through it manually. Instead, we can quickly search for lines that contain the word "leviathan.".

### STEP 4:
By combining the cat and grep commands, we can locate the file. In the result, we can see the password for the next level. We have successfully found our flag.

![image](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/ffaa378d-1270-4b55-88f7-0231c6b583f1)


```text-x-sh
cat bookmarks.html | grep leviathan
```



## Conculsion
Before starting any CTF, it is crucial to understand the base environment, including the shell we're using, the environment variables available, and the files in the current directory. This knowledge provides a path to proceed ahead.

HAPPY HACKING :)
