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


# c) Encrypt a message

First, update. Then, installing the 'gpg'

<img width="624" height="89" alt="image" src="https://github.com/user-attachments/assets/75c4fab1-5f41-4e90-9eb1-d6acb8e14187" />

Going with these settings.. Name, KARI FOO, with an example email

<img width="484" height="143" alt="image" src="https://github.com/user-attachments/assets/50184083-2f29-4761-8efc-259c69e33ba4" />

Adding password (don't know should I...)
<img width="322" height="246" alt="image" src="https://github.com/user-attachments/assets/06b3ab92-9c56-4ca7-80a1-9f3dfdda8346" />

<img width="652" height="201" alt="image" src="https://github.com/user-attachments/assets/70a91842-d3fc-490b-9db4-7cc1af824425" />


















