### Bandit0 -> Bandit1
##### objective
retrieve the password for bandit1 from the readme file located in the home directory of the user.
##### Solution
`cat` command used to read files in terminal.
##### command

	$ cat readme.txt

---
### Bandit1 -> Bandit2
##### objective
retrieve password from a file named - in the home directory.
##### Solution
If we want to read a special name files we need to specify it with its path.
##### command

	$ cat ./-
---
### Bandit2 -> Bandit3
##### objective
retrieve password from a file called spaces in the filename
##### Solution
For reading files spaces in names. We can use `/` .Example: `hello world` can be read like this `cat hello/ world` .
##### command 
	
	$ cat spaces/ in/ the/ filename/
---
### Bandit3 -> Bandit4
##### objective
retrieve password from a hidden file in inhere directory.
##### Solution
In this we need to change dir which can be done use 'cd' command in terminal. For listing hidden files we need to use special flags. `ls -al` which means all and long list.
##### command 

	$ cd inhere
	$ ls -al
	$ cat .filename
---
### Bandit5 -> Bandit6
##### objective
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
human-readable
1033 bytes in size
not executable
##### Solution
We can use `find` to search the file.
##### command

	$ find ./inhere -size 1033c -type f -readable

---
### Bandit6 -> Bandit7
##### objective
The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size
##### Solution
We can find the files using `find` tool. 
##### command

	$ find / -type f -size 33c  -user bandit7 2> /dev/null

---
### Bandit7 -> Bandit8
##### objective
The password for the next level is stored in the file data.txt next to the word millionth
##### Solution
Our password for bandit8 is next to word millionth. So we can `cat` the file and use grep to get the line of millionth.
##### command

	$ cat data.txt | grep millionth

---
### Bandit8 -> Bandit9
##### objective
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
##### Solution
We can get this using `cat`, `sort`, and `uniq`. `sort` to sort and `uniq` to get a unique one.
##### command

	$ cat data.txt | sort | uniq -u

---
### Bandit9 -> Bandit10
##### objective
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
##### Solution
We can use strings to get a human-readable string from a file with grep to get only line with `=`
##### command

	$ strings data.txt | grep ===============

---
### Bandit10 -> Bandit11
##### objective
The password for the next level is stored in the file data.txt, which contains base64 encoded data
##### Solution
We can decode this using `base64`.
##### command

	$ base64 -d data.txt

---
### Bandit11 -> Bandit12
##### objective
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
##### Solution
We can use online decoder or `echo`, `tr`, with some regex to decode.
##### command

	$ echo "<dat.txt data>" | tr 'A-Za-z' 'N-ZA-Mn-za-m'

---
### Bandit12 -> Bandit13
##### objective
The password for the next level is stored in the file data.txt, which is a hex dump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under `/tmp` in which you can work using `mkdir`. For example: `mkdir /tmp/myname123 ` . Then copy the datafile using cp, and rename it using mv (read the man pages!).
Additional details: We will create a dir in `/tmp` folder then copy our data.txt file to `/tmp/<dir>` .
##### Solution
Create a dir in the `/tmp` folder and copy the file data.txt to `/tmp/<createdDirName>`. Then reverse the hash dump using the `xxd` tool and save it in a file without any extension. Then use the `file` tool to check what type of file is. According to file type change the extension and decompress it. Repeat this step until we get our flag.
##### command

	// Command to create a dir in /tmp folder.
	$ mkdir /tmp/<dir_name> // dir name can be anything which we want.
	$ cp ~/data.txt /tmp/<dir_name>
	$ cd /tmp/<dir_name>

After this we will reverse the data.txt file using xxd command and save it without any extension. Then we use file command to check what file type of the file is.

	$ xxd -r data.txt > hashdump
	// this command will reverse the data.txt file and save it to a file name hashdump in current folder.
	$ file hashdump
		hashdump gzip compressed data, was "data2.bin", last modified: Sun Apr 23 18:04:23 2023, max compression, from Unix, original size modulo 2^32 581
	// Now we can change file name hashdump to data2.gz then we can decompress the file and check its file type again. 
	$ mv hashdump data2.gz
	$ gzip -d data2.gz
	$ file data2
		data2 bzip2 compressed data, block size = 900k
	// Now We repeatedly change the extension and decompress the file again. We will perform this same step utill we get file type ASCII text


---

### Bandit13 -> Bandit14
##### objective
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.
##### Solution 
Copy the ssh key file to your local machine and then ssh to the machine using the ssh key.
##### command

	$ cat sshkey.private
	// Copy the content of the file and past it in your local file. then change permission of the file.
	$ chmod 600 <file>
	# ssh <host> -p <port> -l bandit14 -i <file>


---
### Bandit14 -> Bandit15
##### objective
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
##### Solution
Retrieve password of  bandit14 from /etc/bandit_pass/bandit14 Then connect to localhost 3000 using nc or telnet put bandit14 password we get password for bandit15
##### command

	$ cat /etc/bandit_pass/bandit14
	$ nc localhost 3000
	<bandit 14 password>
		<bandit 15 password>

---
### Bandit15 -> Bandit16
##### objective
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
##### Solution
In this we need to connect on localhost port 30001 with ssl encryption. We can use `openssl s_client` which is used to connect hosts using `ssl/tls` .
##### command

	$ openssl s_client -host localhost -port 30001
		// put bandit15 password and press enter.



---

### Bandit16 -> Bandit17
##### objective
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
##### Solution
This one is similar to the previous one but now we need to find on which port a ssl server running. We can use a great tool nmap to scan ports and services. If you want to know more visit nmap official website
##### command

	$ nmap -p31000-32000 localhost -sV
		// this command says scan ports from 31000 to 32000 on localhost and '-sV' scan their services and version.
		// In result we can see their is only one server which is not an echo server lets use openssl s_clien to connect to the server
	$ openssl s_client -host localhost -port <server port>
		// connection successful.
		// put password of bandit 16 it will return a ssh private key for bandit17 so copy the return and store into a file with permissions 600.

---

### Bandit17 -> Bandit18
##### objective
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
##### Solution
By connect to the bandit17 using ssh private key found in previous CTF. Now we can use a tool `diff` to find difference between two files.
##### command

	$ diff password.new password.old
		// out the differnt of password.new and password.old.

---

### Bandit18 -> Bandit19
##### objective
The password for the next level is stored in a file readme in the home directory. Unfortunately, someone has modified `.bashrc` to log you out when you log in with SSH.
##### Solution
We cannot login to the bandit18. But we can read files using ssh. In ssh we can read files directly with user creds. 
##### command

	# ssh -p <port> bandit18@<host> "cat /home/bandit/readme"
		// enter password for bandit18
		// content of readme get printed of connection.

---
### Bandit19 -> Bandit20
##### objective
To gain access to the next level, you should use the setuid binary in the home directory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the set uid binary.
##### Solution
We have a program which we can use after running that without any `args` as instructed we can see its says run command as other another. And execute the example command of the program we can see our `euid=20` means we can access resource owned by bandit20. That means we can read bandit password in `/etc/bandti_pass` file
##### command

	$ ./bandit20-do id
		// euid=(bandit20)
	$ ./bandit20-do cat /etc/bandit_pass/bandit20
		// password

---
### Bandit20 -> Bandit21
##### objective
There is a setuid binary in the home directory that does the following: it makes a connection to localhost on the port you specify as a command line argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
##### Solution
After checking processes I find no server is running on the machine. Which means we need to start our own server which we can do using `netcat`. 
Lets start a server and try to connect using the program. After trying to connect and pasting password of bandit20 it returns nothing. Which means we need to pass password on connection. after chaining echo and netcat we can get our password.
##### command

	$ ps -aux
		// Checking if there any server running.
	$ echo "bandit20_password" | nc -l localhost <we_can_use_any_port> & 
		// this command start a server and echo the password on connect, "&" using this to run the process in background.
	$ ./suconnect <specified_port>
		 // password.

---
### Bandit21 -> Bandit22
##### objective
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
##### Solution
In this we just need to reverse engineer the cronjob for bandit_22 to get his password. look at cronjob, read the script motioned in it then cat the directory mentioned in the script.
##### command

	$ ls -al /etc/cron.d
		// jobs.
	$ cat /etc/cron.d/cronjob_bandit22
		// cronjob which executes.
	$ cat <mentioned_script_in_the_cronjob>
		// password stores to a different directory on the execution of script.
	$ cat <dir_path>
		// password

---
### Bandit22 -> Bandit23
##### objective
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
##### Solution
After reverse engineering the cronjob we got a script which runs and store the password of user who executed it in /tmp directory with name of  md5 hash of `I am user <executed_user_username>`. If we try to execute it. It stores our bandit22 password in `/tmp/<md5hash of I am user bandit22>`. Now looking at this we can create a hash for user bandit23 and directly read its password.
##### command

	$ cat /etc/cron.d/cronjob_bandit23
		// cronjobs of bandit23.
	$ cat /usr/bin/<script_name>
		// script 
	$ bash /usr/bin/<script_name>
		// stored password of bandit22 to  /tmp/<hash>
		// from this line  "mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)" copy from echo to 1 and change $myname to bandit23
	$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
		// hash of I am user bandit23 generated lets try reading the directory where its password get stored.
	$ cat /tmp/<generated_hash>
		// password of bandit23

---
### Bandit23 -> Bandit24
##### objective
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
##### Solution
After reading the script. We get to know that if last if condition the file is getting executed. So if we have a script that will get executed by bandit24 So we as we know all the pass in bandit_pass we can create a script to execute and store the password in our specified folder. We cannot create a file in home so we need to create a dir in /tmp folder then we can create our script and move it to `<bandit24_dir_path_in_the_script.>`
##### command

	$ cat /etc/cron.d/cronjob_bandit24
		// cron job
	$ cat <corn_job_script>
		// script content. Analyse
	$ mkdir /tmp/test
		// create a dir name test in /tmp
	$ cd /tmp/test
	$ touch getbandit24pass.sh
	$ echo "cat /etc/bandit_pass/bandit24 > /tmp/test/bandit24Password" >> getbandit24pass.sh
		// adding cat command to read password and store in our /tmp/test folder in a file called bandit24Password
	$ chmod 777 getbandit24pass.sh
		// this will make this file executable by anyone.
	// No we will cp our file to the folder.
	$ cp getbandit24pass.sh /var/spool/bandit24/foo/
		// if this command get executed without error means our file is copied to bandit24 folder
	// After a little wait we can see a file in our /tmp/test dir called bandit24Password
	$ cat bandit24Password
		 // bandit24 password

---
### Bandit24 -> Bandit25
##### objective
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time
##### Solution
In this, we need to pass to the server our password and a code like this `<pass> <code>`. It looks like we can use a shell script to automate this and get the password.
##### command

	$ mkdir /tmp/test
	$ cd /tmp/test
	$ touch script.sh
	$ vim script.sh
		// create a for loop which loop from 0000-9999 and concat it with our password to make it passable and store it to a file pos_pass.txt.
		*script code*
		// for i in {0000..9999}; do
			echo <password> $ i >> pos_pass.txt 
		  done
		  cat pos_pass.txt | nc localhost 30002 > result.txt
		// save the script 
	$ chmod +x script.sh
		// make it executable
	$ ./script.sh
		// It will take some time after complete if we ls we can see our result.txt
	$ sort result.txt | grep -v "Wrong"
		// this say sort the result file alphabetically and print only those line without Wrong keyword
		// password printed.


---
### Bandit25 -> Bandit26
##### objective
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.
##### Solution
This is a tricky one I also need to get help from others after a certain point. We need to find what shell bandit26 using we can do it by checking the `/etc/password` file where we can see it's not a simple shell after looking at the shell file we get to know that it executes a file with more commands that's it. If we try to connect to the user using ssh private key we find at bandit25 home on connection it prints a text.txt file which says bandit26 and after that, the connection gets closed. So if we read more about `more` we can see it used to show length files using screens. But in this case, our file is very short. After a little help from other users, I get to know if we smaller our terminal size it will open in more interactive mode. In a more interactive mode, we can use different keys to do certain things. If we press V more will open the editor at the current line. after we use Vim to get what we want. first set shell to /bin/bash using ": set shell=/bin/bash" <- this will set our shell to bash for temporary. then use ": shell" to get shell. Now can read the password and proceed.
##### command

	$ cat <bandit26_sshkey>
	$ cat /etc/passwd
		// check for the bandit 26 shell
	$ cat <bandit26_shell>
		// A script.
	// we can try to run it.
	$ /usr/bin/showtext
		// No file text.txt in bandit25
	// copy the banidt26 ssh key to your local machine and then try to connect to using ssh key
	# chmod 600 <sshkey>
	# ssh -p <port> <user>@<host> -i <sshkey>
		// on connect text.txt file get executed and connection get closed.
	// make you terminal size smaller 
	# ssh -p <port> <user>@<host> -i <sshkey>
		// opened text.txt file in intractive mode.
		// press V to opne editer
		// then press ESC => `:set shell=/bin/bash`
		// then again press ESC => `:shell`
		// Now we can use bandit26 shell in bash and read fill and proceed for bandit17


---
### Bandit26 -> Bandit27
##### objective
Good job getting a shell! Now hurry and grab the password for bandit27!
##### Solution
In our bandit26 home dir we have a executable binary after executing it we get to know using this script we can run command as bandit27. Which means we can read password of bandit27.
##### command

	$ ./<exe_binary_name>
		// Run command as someone else
		// an example
	$ ./<exe_binary_name> cat /etc/bandit_pass/bandit27
		// password

---
### Bandit27 -> Bandit28
##### objective
There is a git repository at `ssh://bandit27-git@localhost/home/bandit27-git/repo` via the port 2220. The password for the user bandit27-git is the same as for the user bandit27. Clone the repository and find the password for the next level.
##### Solution
NOTE: Git and GitHub knowledge must.
We need to clone this repository and read the content for bandit28 password. First create a dir in tmp dir and clone this repo there and read its content. For understanding this CTF you need to have a basic understanding of GitHub and git.
##### command

	$ mkdir /tmp/<dir_name>
	$ cd /tmp/<dir_name>
	$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
		// This command will copy the repo in current dir.
	$ cd repo
	$ cat README
		// password
---
### Bandit28 -> Bandit29
##### objective
There is a git repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo ` via the port 2220. The password for the user bandit28-git is the same as for the user bandit28. Clone the repository and find the password for the next level.
##### Solution
NOTE: Git and GitHub knowledge must.
After clone repo as we did in the last one. If we cat readme file we can see the username is there but password it in XXXXXXXXX this. let check git logs to see what change are made on this repo so far. In git log we can see last commit with message info leaked fixed. Maybe this is about the password. If we try to revert last commit in the repo and then read the readme file we can get our password.
##### command

	$ mkdir /tmp/<dir_name>
	$ cd /tmp/<dir_name>
	$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
	$ cd repo 
	$ cat README.md
		// the password is not there.
	// let check git log's
	$ git log
		// if we execute this command in repo dir we can see the commits made to this dir so far.
		// now we can see the last commit say info leak let's revert the commit and check.
	$ git revert <commit_id(Hash value about the commit message)>
		// It say's one file changed
	$ cat README.md
		// password

---

### Bandit29 -> Bandit30
##### objective
There is a git repository at `ssh://bandit29-git@localhost/home/bandit29-git/repo` via the port 2220. The password for the user bandit29-git is the same as for the user bandit29. Clone the repository and find the password for the next level.
##### Solution
We perform the same steps as last last on to clone the repo. On checking Readme.md file its say's no password in production. May there is more than one branch on this repo. After list the branches we can see a branch name dev. We can switch our branch to dev and read password.
##### command

	$ mkdir /tmp/<dir_name>
	$ cd /tmp/<dir_name>
	$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
	$ cd repo 
	$ cat README.md
		// No password in production.
	$ git log
		// nothing interesting . We can check by reverting changes.
	$ git branch -a
		// list's all the branches. We can see other branches maybe the password canbe in one of them
	$ git switch -c <branch_full_path(remote/origin/<branch name>)>
		// This command will switch our branch
	$ cat Readme.md 
		// password

---
### Bandit30 -> Bandit31
##### objective
There is a git repository at `ssh://bandit30-git@localhost/home/bandit30-git/repo` via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.
##### Solution
clone the repo similar to previous one. Now our readme files is empty. Let's enumerate further. If we check logs and branches we get nothing. But git is full of features. Git has a feature called tag to tag specific point in git history ex: If I chance something important I need to make a separate mark on that to access to more quickly rather than going through my commits and reverting it to see. We can check git tag user `git tag`  and we can see a tag by using `git show 'tag name'`.
##### command

	$ mkdir /tmp/<dir_name>
	$ cd /tmp/<dir_name>
	$ git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
	$ cd repo 
	$ cat README.md
		// Just an empty file.... muhaha
	$ git branch -a
		// nothing here
	$ git log
		// nothing here
	$ git tag
		// a tag shows
	$ git show <tag_name>
		// password

---
### Bandit31 -> Bandit32
##### objective
There is a git repository at `ssh://bandit31-git@localhost/home/bandit31-git/repo` via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.
##### Solution
In readme file we get instructed to create a file called key.txt with given content and push this repo. It's fairly simple create a file key.txt
then add the given content in it and save it. Add the file in git for file tracking. On try to add key.txt we are unable to perform that because in .gitignore its ignoring all .txt file we can remote from it and save it. Now we can add file and commit it and push it to the repo.
##### command

	$ mkdir /tmp/<dir_name>
	$ cd /tmp/<dir_name>
	$ git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
	$ cd repo 
	$ cat README.md
		// Instruction to create a file key.txt and the given content and push it to main repo.
	$ touch key.txt
		// create file key.txt
	$ echo <given_content> >> key.txt
		// dont change anything with the given content. Make sure to copy it without quotes from readme.
	$ git add key.txt
		// unable to add giving .gitignore error
	$ cat .gitignore
		// can see its ignoring all .txt files.
	$ vi .gitignore 
		// remote the line from .gitignore and save it.
	$ git add key.txt 
		// successfully added
	$ git commit -m "adding key.txt"
		// 'git commit -m' measn commit the changes with the prvodied message(You can provide anything)
	$ git push
		// password

---
### Bandit32 -> Bandit33
##### objective
After all this git stuff its time for another escape. Good luck!
##### Solution
This is a shell escape level. In this I am a little weak so I took help of internet to get what we can do. In this level we connected to a shell where whatever we type get converted to uppercase. But for escaping restricted shells there are few ways to do it. `https://0xffsec.com/handbook/shells/restricted-shells/` You can read this get a better idea of this. And In future I will try to create a good handbook on this. We can try using env Variables. $0 is a special env variable because this store our shell path. If we try this we get a proper `sh` shell as bandit33. Now we can read bandit33 pass from etc bandit_pass.
##### command

	>> $0
	$ whoami
		bandit33
	$ cat /etc/bandit_pass/bandit33
		// pass

---
### Bandit33

After logging over the wire congratulate us for complete this wargame.
