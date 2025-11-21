# x) Read and summarize

## Schneier 2015

### Chapter 1

- Text can be read, but if you want to hide the message, you encrypt (enchipher) it. This text you call ciphertext. On the otherhand decryption (decipher) is the process to make the ciphertext readible again. Cryptography is the art and science behind the solutions to make the message secure, unreadible, an turn it back to readible format (by those who are privileged to read it).
- In mathematical terms, the encryption function (E) operates on message (M) resulting in ciphertext (C), or **E(M)=C**. On the otherhand, the reverce process would be that decryption function (D) would operate on ciphertext (C) resulting in a message (M), or in mathematical function: **D(C)=M**.

- Cryptography is also used in authentication, integrity (message has not been modified during transit), and nonrepudiation (proof of sending a message)
- Modern cryptography uses **key** (K) to solve problem of some drawbacks of restricted algorithms. Key basically adds an extra security layer to the encryption. Even if you know the algorithm you need the key to decypher the message, because key was used also the encrypt it. Key is denoted by the K subscript in the function,n and depending on a situation can be K1, K2, and so forth:
<img width="90" height="34" alt="image" src="https://github.com/user-attachments/assets/2cfeb9ec-d660-467b-b101-2be1caa0d589" /> and <img width="92" height="25" alt="image" src="https://github.com/user-attachments/assets/52757049-822a-4fde-bd73-3222eddbb0df" />
- There are also symmetric algorithms (where encryption key can be calculated from the deciphered key, and other way around too) and public-key algorithms (key used for encryption differs from the key used for decryption). Symmetric algorithm is like a safe, which you can open if you have the combination, and then close again. Public-key algorithm works basically so, that two persons have agreed on a public-key cryptosystem. Person A sends person B that public key. Person B can encrypt the message with the key person A has sent, and sends the message. Person A can now decrypt person B message by using own private key. In network the key is fetched from the database, so the person A or B does not need to send it to each other.
- In hybrid cryptosystem keys are used with symmetric algorithms to secure the traffic where message runs. So from the previous example perspective, Person A now sends Person B the public key. Person B generates a random session key, and that is encrypted using Person A's public key, and then sends it to Person A. Person A can read Person B message using its private key to recover the session key. Now both of them can encrypt their communication using same session key. So in this case the data encryption key is waiting until it is used.
- Merkle's technique then again is based on so called "puzzles" that eavesdroppers can find hard to crack, but for sender and receiver easy.


Source: [Applied Cryptography: Protocols, Algorithms and Source Code in C, 20th Anniversary Edition]([url](https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001)), 
Chapter 1.1 Terminology & Chapter 2.5 Communication using public-key cryptography



## PGP - Send Encrypted and Signed Message

- Article is about how to use PGP encryption with a 'gpg' tool, which is a popular way to encrypt as well as to decipher.
- We install with following command
$ sudo apt-get update
$ sudo apt-get install gpg micro psmisc

Sudo is the super user (admin) rights. Then we get the updates and install gpg.

$ gpg --gen-key
This creates a keypair. I guess this is related to the example "Person A send a key to Person B" I described above, but in order to send the key, we need to create it first.

$ gpg --fingerprint
Tero get the keypair from the command prompt, but to be honest, I got lost what is he doing in practice. Apparently you give a name and the email address, but I don't know why... Or maybe the system offers it?

Exporting your public key, which you can share with another one, is done with the following commands:
$ cd
$ gpg --export --armor --output publickey.pub
cd is for home directory
'gpg' is the program.  ----export' is I would assume self-explanatory, '--armor' uses only ASCII characters so that the out can be viewed and copied. I wonder why this is not always used (what's the difference to use it this time... I don't remember using it before). '--output publickey.pub' saves the output in to a file called "publickey"

$ ls
publickey.pub

$ head -4 publickey.pub

This should provide the public key, which is just a hash of letters and numbers.

$ cd
$ mkdir alice/
$ chmod og-rwx alice/
Then we should create a folder a folder. Let's call the folder Alice. We can of course create another user... but this will do.

Then we should save some gpg files in the folder.

$ gpg --homedir . --gen-key
Then we create Alice own keypair.

We also create some name and email address for "Alice" who can also send a message to me with some lines of codes. The lines of codes are a bit long and technical...

But basically the enryption is set between to points by sharing the public key with eache other. Alice in this case would verify and sign the key sent, and can proceed encrypting messages back. But for that, Alice needs to sends the key to me.

$ gpg --homedir . --export --armor --output alice.pub
$ cp -v alice/alice.pub .
'alice/alice.pub' -> './alice.pub'
So in this we use gpg again, we go to our home folder and export alice.pub file. 

$ cd 
$ cp -v alice/alice.pub .
I think then we need to send the key in alice.pub file.

$ gpg --import alice.pub
And then import that key

$ gpg --sign-key "B20F D80B 705C 791D C878  0030 7BAA 4F13 2645 134F"
$ gpg --fingerprint
uid           [  full  ] Alice <alice@example.com.invalid>
Then I uess we would have the established the secure connection!

Following codes in the article shows how to formulate a message, write it, and...
$ gpg --homedir . --encrypt --recipient tero@example.com.invalid --sign --output encrypted.pgp --armor message.txt
Enrypt it! So again using the 'gpg', navigating to working directory, naming the recipient, signing (with the Alice's secret message), and then encrypt it with printable ASCII characters.

The article continues with instructions how to formulate encrypted messages. Overall the article is an interesting example how the public and secret key works in practice, from techical perspective. It demonstrates how it is actually possible to create your own key and share it with the receiver to start encrypted messaging. The concept looks actually quite "simple" in the end. Just as above described how Person A and Person B would share the keys, we do this now in practice to establish a secure connection between two.

Good that Tero has some troubleshooting instructions, because I'm already getting panicked infront of this assignment. Getting quite technical... Phew...


Source: Karvinen, T. 2023. PGP - Send Encrypted and Signed Message - gpg


x) Pubkey today

Instantly when I started to read about the encryption, decryption, abd keys, it reminded me of Signal messaging app, which uses end-to-end encryption (E2EE) protocol. I use Signal on my phone. It has sometimes a message im the chat saying "Your safety number with XXX changed, likely because they reinstalled Signal or changed devices. Tap Verify to confirm the new safety number. This is optional.", and by pressing "Verify" it shows me random numbers infront of my screen (and a QR code). 

This is how Signal sees it: "Your messages with Signal are end-to-end encrypted which is like having locks and keys for each message. When the safety number changes it's as if you have changed the locks and keys for your messages." I assume this is the public key (as its publicly visible).

According to Truong Luu (Medium 2025), this E2EE combines symmetric and asymmetric encrytion. So first Person A generates symmetric key to encrypt the message. The Person A then encrypts the key using the Person B's public key. This way only the Person B's private key can decrypt it. So what happens is, that symmetric key is sent with the encrypted message from Person A to Person B. Only Person B can open it. Sounds familiar? It's because I was writing about this earlier :-)


Sources: 

Signal. https://signal.org/

Signal. https://support.signal.org/hc/en-us/articles/360007060632-What-is-a-safety-number-and-why-do-I-see-that-it-changed#:~:text=Each%20Signal%20one%2Dto%2Done%20chat%20has%20a%20unique,manually%20approved%20before%20sending%20a%20new%20message.

Medium. 2025. End-to-end encryption explained: how the Signal app secured your messages. https://medium.com/@jackluucoding/end-to-end-encryption-explained-how-the-signal-app-secured-your-messages-d57e2ecd5d6d


# b-c) Encrypt a message

First, update. Then, installing the 'gpg'

<img width="624" height="89" alt="image" src="https://github.com/user-attachments/assets/75c4fab1-5f41-4e90-9eb1-d6acb8e14187" />

Going with these settings.. Name, KARI FOO, with an example email

<img width="484" height="143" alt="image" src="https://github.com/user-attachments/assets/50184083-2f29-4761-8efc-259c69e33ba4" />

Adding password (don't know should I...). Won't share my screenshot of this...

<img width="652" height="201" alt="image" src="https://github.com/user-attachments/assets/70a91842-d3fc-490b-9db4-7cc1af824425" />

So... Now I got a key. There is now my public key to encrypt my messages later on. I think its that long string of codes 4390AAF8... and so forth.

Then let's exort the key to a file named karifoo.pub
<img width="650" height="57" alt="image" src="https://github.com/user-attachments/assets/4a820482-906a-45d9-97a0-c9ec30d24920" />

There is the public key (in the file I think)
<img width="632" height="288" alt="image" src="https://github.com/user-attachments/assets/cf4be170-ef85-44bb-8b59-6fba2e81ebe7" />

Let's create a receiving folder for Alice so we can send a message and test our encrypted messaging
<img width="647" height="408" alt="image" src="https://github.com/user-attachments/assets/26f7a813-4486-42f2-8ed2-459de42c6203" />

Alice doesn't need any passwords...
<img width="567" height="195" alt="image" src="https://github.com/user-attachments/assets/54d9827d-9d19-4c3c-97b4-51a25a0470b4" />

But Alice needs own key, so let's genereate one.
<img width="632" height="281" alt="image" src="https://github.com/user-attachments/assets/322cbcd1-87cb-4ba0-b48d-44e2649680a7" />

Let's share the public key with Alice
<img width="631" height="245" alt="image" src="https://github.com/user-attachments/assets/9cd4223d-2d05-4de2-b604-2a0379062dab" />

We can compare the public keys now with Alice. The Alice key is above (CD75 2C66)...  so forth. My key is below (4390 AAF8...)
<img width="630" height="235" alt="image" src="https://github.com/user-attachments/assets/b3a9cdb9-6d5a-4a0f-80b4-2499cfe115a8" />

Now Alice will sign the code sent from me ("4390 AAF8 1537...") to basically establish a secure messaging between us. That is because I have createad a key for Alice. Alice has a key for me. Alice now signs the key from me and makes it trusted. 

And that's a yes! Match made in heaven.

<img width="637" height="468" alt="image" src="https://github.com/user-attachments/assets/2814bb9f-c8de-41be-b6c2-ce46c7beee21" />

Now we need to make Alice's key trustworthy also for me. So let's do it with similar steps.

Ok... I rant into some technical problem and I can't get out of this one... The problem is just looping...

<img width="632" height="501" alt="image" src="https://github.com/user-attachments/assets/8c08a1fe-b829-477e-a26d-4c31bd3dc7fa" />

So... While I try to export alice.pub again and again, it asks me to overwrite it again and again, and I say everytime yes.. So, from my view it's an indication that there is a file there... But the 'cp -v alice/alice.pub' doesn't work... If I check the files in the directory, it seems 'alice.pub' is there...

<img width="635" height="140" alt="image" src="https://github.com/user-attachments/assets/f241518f-43ef-44a3-b493-be1fb5c36606" />

I don't know... I'll just try and hope it works, if I just continue with the instructions...
<img width="649" height="194" alt="image" src="https://github.com/user-attachments/assets/c2a71330-3ad9-48dd-98d4-d3b937ad0b7a" />

After one hour of solving this I already lost what I was doing here... Oh jeez... But I think now I imported Alice's key. I think the problem was with my command that as I was already in the "/alice" directory, I couldn't clal the the "alice/alice.pub .".
<img width="653" height="285" alt="image" src="https://github.com/user-attachments/assets/baa081bc-367b-428b-8858-06587bf4e812" />


All right... Alice is writing me a message
<img width="634" height="625" alt="image" src="https://github.com/user-attachments/assets/33704f17-3b91-48d3-b0d2-5dce84be7845" />

Had a bit of a problem, but managed to restore my message... I didn't know how to save the .txt file and I didn't see that the answer was all along in the instructions... And then I actually accidentally shut the whole terminal and you can imagine the frustration... So I opened it back and got this point where I try to enter the message.txt file back. It says there is a recovery, so I recover by pressing 'r' and press enter.
<img width="657" height="455" alt="image" src="https://github.com/user-attachments/assets/519a7b0f-ae2d-4e40-a972-1f61784f4d87" />

So, let's send it then.. The encryption better work... For some reason Linkin Park - 'In the End' song started to play in my head... I've tried so hard, and got so far...
<img width="635" height="98" alt="image" src="https://github.com/user-attachments/assets/4eef48b3-73e6-4493-bb33-7ce7d665ec1a" />

Nothing happened?
<img width="630" height="101" alt="image" src="https://github.com/user-attachments/assets/15e2107b-cda1-4a5a-9ffd-52d3cbc30680" />

Phew... It's there... Should it open?
<img width="624" height="236" alt="image" src="https://github.com/user-attachments/assets/ca1834bc-10a6-42ed-afbc-2744a50ef912" />

Let's try a bit more...
<img width="626" height="311" alt="image" src="https://github.com/user-attachments/assets/129edf18-85b3-4d07-9f6b-a69b18f48c81" />

Again this error... I already forgot how I solved it after one hour of smashing my head on the table... :-)
<img width="639" height="167" alt="image" src="https://github.com/user-attachments/assets/081e9cea-b68b-4f86-8d11-83e76d3e7c32" />

So I had to exit Alice directory..?
<img width="626" height="160" alt="image" src="https://github.com/user-attachments/assets/0ab9d0d7-dc9d-4223-9fe5-fdbf7fb65079" />

Yup... It worked.. Maybe? (Linkin Park playing in the head even harder now...)

I almost forgot the password... Jeez... Good that I didn't have to start over...
<img width="882" height="318" alt="image" src="https://github.com/user-attachments/assets/ca7a8925-f0a1-474f-b9e1-31ff78a6759d" />

Holy moly... I opened it... And the message!
<img width="647" height="575" alt="image" src="https://github.com/user-attachments/assets/3e0b8c38-c320-4b06-958e-ce9dd773dafb" />

So in the end, what I did in simple words...
1. I createad a key
2. Alice created a key.
3. We exhcanged the public key info. Alice saved my key as trustworthy. She writes me a message and encrypts it before sending it to me.
4. I managed to open the message and encrypt the message with my key (after Alice encrypted it, only I can open it).

This was quite hard assignment... I was lost for quite a while with the error there... But with some trial and error, I learned a bit mode how to code in the terminal.

So let's say an eavesdropper would try to interfere the messages... Well that person wouldn't be able to decypher the message that Alice wrote to me. That is because Alice used the key to encrypt the message. After encrypting the message, you need a key to decrypt it. If you don't have the key, the message is just random looking letters. It is the private key as I've understood that allows to decrypt the message.


# d) Password management
Password managers can create passwords for you, but also store them in a safe place digitally. It is protected by a one password. There can be password manager applications or one can be in the browser. 

The problem is that you might need to use various web services and resources daily and remember many passwords. It is only human trying to simplify them because of the ability to remember limited amount of such passwords. So what typically happens is that we might use the same password or connected passwords in multiple services. And if one password gets compromised, well, then it puts all servicdes using the same password at risk. 

So... Let's download one. I chose this KeyPassXC (download here: https://keepassxc.org/download/#windows). I'll guide you through the installation. So, download the file, and install it.
<img width="496" height="387" alt="image" src="https://github.com/user-attachments/assets/cc9b7ef1-3758-4479-9ea8-39a9ba76d6f3" />

Accept the terms, and click Next. Just finish te setup (directory, shortcut) and click 'Next'. Then 'Install', and after installation let it update the latest updates. I guess there is a security functionality, but I can't take screenshots of the application.

1) First we need to create a database (my app is in Finnish, but I try to translate it to English. It seems I can't change the language).
2) Name the database as "Passwords".
3) I use the recommended database type: KDBX 4.0
4) You can keep everything else as is and press continue.
5) Enter the password with which you want to open the password manager, press 'Ready'.
6) Save the kdbx file into computer
7) You can then add a new entry by pressing 'Add a new entry' (+ sign circulated)
8) Add following information
   - Name of the entry (example: GitHub)
   - username
   - password
   - URL address where the login happens
   - Tags (e.g. Cyber; Cyber Security)
   - Expiry date (optional)
   - Notes (E.g. After graduation from Haaga-Helia University of Applied Sciences this username will stop working)
9) Now you can click on the page where you want to login (like GitHub)
10) Then have KeyPass open and press 'execute automatic fill'. It will then go to the page where you had the cursor last time clicked (I hope on the username) and fill username and password automatically.

I wanted to record my screen while doing this. Even when using collaboration tools such as Google Meet and sharing the screen, the KeyPass is somehow protected from such tools... So I can't see the whole application in the video when recording.. So no screenshots, no video... 


Sources:

Jyoti & Jeyanthi, 2023. Jyoti, M. & Jeyanthi, N. 2023. A Review of Modern Authentication Methods in Digital Systems. IEEE.

Kaspersky. [How to protect your data online by using a password manager]([url](https://www.kaspersky.com/resource-center/preemptive-safety/protecting-your-data-online-password-manager)).
