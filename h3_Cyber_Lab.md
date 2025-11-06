# X) Cyber Lab
## Summarizing the articles
Here is my summary for the "Command Line Basics Revisited" by Tero: https://terokarvinen.com/2020/command-line-basics-revisited/
- Command line prompting is all about writing commands for the computer
- You can command the computer to move within the system by using specific key words to get in to folders and files
- You can also create and delete files and folders (all caps preferred)
- Additionally you can call for help and check the history
- It is also used for installations (softwares and updates), such as games or hacking console

## Cracking Passwords with Hashcat
Here is my summary for the "Cracking Passwords with Hashcat" by Tero: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/
- Passwords are stored in the system hashed, so it is very high in entropy, and you can not reverse engineer it back. But you can guess it by using some words in the dictionary and see if it matches.
- First we need to install the Hashcat. It will help to download already a list of most common passwords.
- The hashed string is set as -m. The Hashcat then brings different options to choose what mode you want to use to crack the password. The MD5 is common one, and in the code, you refer to the mode with the referenced number after "Hashcat Mode", which is 0 in this case.


# d) 
The goal is to crack the password "6b1628b016dff46e6fa35684be6acc96". For this, we need to install hashcat. Let's see how it goes.

- Ok, I've started by installing the hashid hashcat, ne directory, 
$ sudo apt-get -y install hashid hashcat wget
$ mkdir hashed
$ cd hashed
<img width="811" height="144" alt="image" src="https://github.com/user-attachments/assets/de14dd66-e9fd-4389-b33b-ae1df60bc21c" />

- Then we get the dictionary of most common passwords
$ wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
$ tar xf rockyou.txt.tar.gz
$ rm rockyou.txt.tar.gz

<img width="684" height="207" alt="image" src="https://github.com/user-attachments/assets/7f1939a6-fb6b-4d71-92ab-134b51847bed" />

- we can check the file content (top ones from the file)
<img width="363" height="122" alt="image" src="https://github.com/user-attachments/assets/20dd1e92-0b76-4665-b40d-195ad2a1df61" />

- 


