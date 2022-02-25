# RSA and why padding schemes are required

## What is RSA?
Rivest-Shamir-Adleman (RSA) is a widely used [public-key cryptosystem](https://en.wikipedia.org/wiki/Public-key_cryptography) which relies on the ["factoring problem"](https://en.wikipedia.org/wiki/Integer_factorization). In simple words, the crux of RSA works with 2 large prime numbers and their product. The security of RSA is based on the fact that factoring the product to find the 2 large prime numbers is extremely difficult. Since RSA works with large (2048/4096 bit) prime numbers it is computationally expensive to implement. Thus, it is often used in transmission of shared keys for Symmetric Key Algorithms. It is also used for signing messages as a Digitial Signature. 

The RSA encyrption scheme (m bit) is implemented as follows:-

### Key Generation:
  - Choose two large distinct prime numbers of length m/2 bits (*p* and *q*).
      - These prime numbers should be generated using a random number generator.
      - The numbers should have equal number of bits but may differ in number of digits.
      - The primality of the number is checked using primality tests. The primality tests usually used are:
          - [Miller-Rabin Primality test](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test)
          - [Lucas-Lehmer Prinality test](https://en.wikipedia.org/wiki/Lucas%E2%80%93Lehmer_primality_test)
      - The numbers *p* and *q* are kept secret.
  
  - Compute the product of two prime numbers as *n = pq*.
      - The product *n* is used as the modulus for encryption and decrytion operations.
      - *n* is an *m* bit number. Thus, an *m*-bit RSA refers to length of the modulus used.
      - The number *n* is used as part of public key.
  
  - Compute ϕ(n) = (*p*-1)(*q*-1). This number is kept secret and is usually calculated using the [Euclidians Algorithm](https://en.wikipedia.org/wiki/Euclidean_algorithm).
  
  - Choose a number *e* as the **public exponent**.
      - *e* must be 1 < e < ϕ(n)
      - GCD(ϕ(n), *e*) must be 1.
      - *e* is broadcasted as part of public key.
  
  - Calculate *d* as the **private exponent**.
      - *d* is the [modular multiplicative inverse](https://en.wikipedia.org/wiki/Modular_multiplicative_inverse) of e.
      - It is calculated as *d* ≡ e<sup>-1</sup> mod ϕ(n).
      - *d* is kept secret since it is part of the private key.
   
   - The private and public keys for RSA are as follows:-
      - **Public Key** = (*e*,*n*)
      - **Private Key** = (*d*,*n*)

### Key distribution and Encryption/Decryption operations:
As any public-key cryptosystem, the public key is broadcasted by the owner and used for encrypting messages sent to them. The owner then decrypts these messages using the private key. The encryption (plaintext = *m*) and decryption (ciphertext = *c*) steps are as follows:
   - **Encryption**: *c* = *m<sup>e</sup> mod n*
   - **Decryption**: *m* = *c<sup>d</sup> mod n*

### Example:
#### Key Generation
   - Let the prime numbers chosen be *p*=3 and *q*=11.
   - *n* = *p*.*q* = 33
   - ϕ(n) = (*p*-1)(*q*-1) = 20
   - Let e = 3 (1 < 3 < 20 and GCD(3,20) = 1)
   - d ≡ 3<sup>-1</sup> mod 20 ≡ 7 mod 20, Hence, d = 7.
   - Thus, public key = (3,33) and private key = (7,33)

#### Encrytion and Decrytion
   - Encrytion:
      - Let plaintext *m* = 4, public key = (3,33).
      - Ciphertext (*c*) ≡ 4<sup>3</sup> mod 33 ≡ 31 mod 33
      - Thus, *c* = 31
  
   - Decryption:
      - Private key = (7,33).
      - *m* ≡ 32<sup>7</sup> mod 33 ≡ 4 mod 33
      - Thus, *m* = 4

## Why Padding schemes are required?
As seen from the above, RSA is [deterministic](https://en.wikipedia.org/wiki/Deterministic_algorithm) in nature. In simple mathematical terms, RSA(x) is always = y for plaintext x. This deterministic nature of RSA can be exploited using chosen plaintext attacks without knowing the private key.

### Chosen-plaintext attacks against textbook RSA
Consider an application which uses RSA as its ecnryption scheme for messages sent over the network. Let Alice be the owner of the application and Bob be a user sending messages to Alice. Let every message start with "Hello", "Hi" or "Hey". Let *h(x)* be an publicly available invertible function used for converting a word from string to number and vice versa.
Let Eve be the eavesdropper intercepting messages and trying to decrypt the messages over the network. the network looks as follows:


![Network looks like this](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Finterstices.info%2Fupload%2Fcodes-secrets%2Falice-et-bob1.jpg&f=1&nofb=1)


Since, RSA and *h(x)* are deterministic, the starting messages will always be encryted as follows (using public key):
   - RSA(h("Hi")) = 1678
   - RSA(h("Hey")) = 1798
   - RSA(h("Hello")) = 2768
 
Note, that Eve does not know what the starting messages are, but knows how the application works. Also, the public key *(e,n)* is publicly avaliable and Eve has access to it. Eve can only see 1678, 1798 and 2768 over the network and requires the secret private key to decrypt these messages. However, there is a hack to this. Since Eve has access to *h(x)* and *(e,n)*, Eve can try encrypting plaintexts that she feels may be this ciphertext and match them against the ones she has.

Thus, Eve could perform RSA(h("Hey")) and get the value 1798 and match it cipherext 1798 and know the plaintext is "Hey". The RSA algorithm explained above is referred to as textbook RSA and not recommended for use in real-world applications. The above example shows that textbook RSA is not [semantically secure](https://en.wikipedia.org/wiki/Semantic_security). Textbook RSA would semantically secure if Eve despite having the ciphertexts, couldn't launch the chosen plaintext attack described successfully. To make textbook RSA semantically secure it is used along with Padding schemes.

### Padding Schemes to the rescue!
Padding schemes help introduce a random component to textbook RSA, thus making it [probabilistic/randomized](https://en.wikipedia.org/wiki/Randomized_algorithm) in nature. Commonly used Padding Schemes for RSA are [PKCS #1 v1.5](https://en.wikipedia.org/wiki/PKCS_1) and [Optimal Asymmetric Encrytion Padding (OAEP)](https://en.wikipedia.org/wiki/Optimal_asymmetric_encryption_padding). A more detailed description for how these Padding schemes should be implemented can be found in [RFC8017](https://datatracker.ietf.org/doc/html/rfc8017).

To elaborate how a basic padding scheme works, lets return to our example. Except now Alice and Bob decide to prefix a random 4 digit number to the message before encrypting it. After decryption, the random number is simply discarded and the message is retreived. Thus, even though the 1st three messages are fixed as "Hello", "Hi" and "Hey", the cipher text generated each time would be different. For example, consider 4 new converstaions initiated by Bob using "Hi". The encrypted text would be as follows:-
   - RSA(h("1234RSA")) = 12789
   - RSA(h("4334RSA")) = 34389
   - RSA(h("1634RSA")) = 23367
   - RSA(h("0034RSA")) = 99983

Now, Eve would have 4 different ciphertexts for "Hi" alone and will not able to match RSA(h("Hi")) to these ciphertexts. Eve does not know of the random padding and thus cannot decrypt the messages. Since, paddings schemes are usually public, lets say the encryption scheme generated uses a variable length number. Thus, even though Eve knows that the text is padded, she doesn't know the variable length used. This encryption scheme is not practical in a real-world application, but one gets an idea of how a padding scheme works and helps make RSA semantically secure. Multiple ciphertexts are generated for a single plaintext and thus the attacker canot match the chosen plaintexts to acquired ciphertexts without knowing the random component.

In real-world applications, RSA is implemented using 2048/4096 bit number modulus' and thus the padding string used with above mentioned Padding schemes is of a high bit length too. This helps make RSA even more resilient with padding schemes, since higher bit numbers lead to more permutations of ciphertext. The number of permutations is usually large and brute force attacks prove to infeasible against the random component.
