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






