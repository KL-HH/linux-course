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


# d) Cracking the password
The goal is to crack the password "6b1628b016dff46e6fa35684be6acc96". For this, we need to install hashcat. Let's see how it goes.

Ok, I've started by installing the hashcat directory. 
- $ sudo apt-get -y install hashid hashcat wget
- $ mkdir hashed
- Let's start the haschat by typing '$ cd hashed'
<img width="811" height="144" alt="image" src="https://github.com/user-attachments/assets/de14dd66-e9fd-4389-b33b-ae1df60bc21c" />

Then we get the dictionary of most common passwords
- $ wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
- (Dont write 'rm rockyou.txt.tar.gz' as it will delete the file, I think)

<img width="584" height="108" alt="image" src="https://github.com/user-attachments/assets/27b1fe55-1071-4ddc-b9fb-bd504b0eb947" />


we can check the file content (top ones from the file)

<img width="363" height="122" alt="image" src="https://github.com/user-attachments/assets/20dd1e92-0b76-4665-b40d-195ad2a1df61" />

Next, the Hashcat offers different methods to crack the code. We use the common one, MD5, and in code you can see me refer to that mode by selecting 0 before typing the actual hashed value. 

<img width="632" height="389" alt="image" src="https://github.com/user-attachments/assets/de9c3d45-5daa-4f14-8bf5-b2ff6c2203e2" />

So, let's put that hashed string back just after "-m 0", where 0 refers to MD5 mode. We put the hashed value inside single quoation in case of special characters. We also ask to look for the value from the rockyou.txt file. We save the solution in file named "solved" by using command -o solved

<img width="800" height="43" alt="image" src="https://github.com/user-attachments/assets/cefcb941-0a81-4005-a861-a2688ec98baf" />


As a sidenote... I encountered several times error messages, and the reason was in my settings. At this time I had to shut down the virtual machine and start over, increase RAM to 4gb and video memory to 128MB. After that I repeated some steps to get back here, and then got this message:

<img width="763" height="511" alt="image" src="https://github.com/user-attachments/assets/4fe07f2f-7b3b-4911-b2fb-2bcd6be4f15f" />

I cracked the password! Let's see what it is by typing 'cat solved' in the terminal

And there you have it... 
summer 


<img width="812" height="46" alt="image" src="https://github.com/user-attachments/assets/53ca66f3-5444-4656-bbac-3a497a6eb1a7" />

I don't know why it says it couldn't find the file 'rockyou.txt', when it read the file and provided me the answer. But that's not the weirdest part... Seriously... Who uses 'summer' as password? 
