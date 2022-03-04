# Padding Schemes for RSA and their Security

## Project information
   - **Faculty Advisor:** [Prof. Stanisław Radziszowski](https://www.cs.rit.edu/~spr/)
   - Weekly status updates for the project can be found [**here**](weeklyStatus.md).
   - Current status of Project Paper draft can be viewed [**here**](ppaper.pdf).


## Project Description
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The **Rivest-Shamir-Adleman** algorithm commonly known as the RSA Algorithm is widely used in today’s world. RSA is mainly used with digital signatures for authenticating users. It is based on the factoring problem. In simple words, the crux of RSA works with 2 large prime numbers and their product. The security of RSA is based on the fact that factoring the product to find the 2 large prime numbers is extremely difficult. However, there are attacks that could break RSA, if the prime numbers are not chosen wisely. There are also attacks on the nature of RSA (For e.g. RSA is deterministic), which contribute to the algortihm being susceptible to attacks.
   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To overcome these shortcomings, RSA is often used with a Padding Scheme. Some examples are **PKCS v1.5** and **Optimal Asymmetric Encryption Padding (OAEP)**. These padding schemes make RSA **probabilistic in nature** by applying **randomized padding** to the plaintext before it is encrypted using RSA. As part of this project, I will review the properties of RSA and study how the padding schemes strengthen RSA. Since practical RSA works with very large prime numbers, RSA is a computationally expensive algorithm. Thus, adding padding to the entire encryption process increases the computational overhead. The project aims to research and analyze the trade-off between security and computational cost while implementing RSA in various scenarios. Using this analysis, the project aims to comment on whether using RSA with/without padding is favorable.


## Milestone Roadmap
### Milestone 1 (10<sup>th</sup> Jan. 2022 - 4<sup>th</sup> Feb. 2022)
      - Review literature on the RSA and Padding Schemes.
         - Review the RSA algorithm
         - Review parameter selection methods for the RSA
         - Review Padding schemes for the RSA

      - Implement RSA and its parameter selection algorithm.

### Milestone 2 (7<sup>th</sup> Feb. 2022 - 4<sup>th</sup> Mar. 2022)
      - Study malleability of RSA
         - Review literature on vulnerabilites of the RSA
         - Review literature on attacks performed on the RSA

      - Review literature for Probabilistic versions of RSA
         - Review more literature on Padding Schemes for RSA.
         - Review how probabilistic versions of RSA help mitigate/prevent attacks.
         - Review literature on current research for Padding Schemes of RSA.

      - Implement Padding schemes for RSA
         - Implement RSA using PKCS #1 v1.5.
         - Implement RSA with Optimal Asymmetric Encryption Padding (OAEP).
         - Implement RSA with other* Padding schemes chosen for analysis.

### Milestone 3 (7<sup>th</sup> Mar. 2022 - 15<sup>th</sup> Apr. 2022)
      - Perform experiments on the following to analyze security and performance:-
         - RSA without Padding schemes.
         - RSA implemented using PKCS #1 v1.5.
         - RSA implemented using OAEP.
         - RSA implemented using other* padding schemes

      - Report findings for the following:-
         - Security for RSA implemented with/without Padding schemes
         - Computational cost for each implementation of RSA

> **Note:** other* padding schemes for RSA will be selected as part of research performed in Milestone 2. The plan for the project will be updated accordingly.

## Project Progress
   - [What is RSA? Why are Padding Schemes required?](rsa_info.md)
   - [Parameter Selection Algorithm development process](prm_slct_info.md)

## Presentations
   - [Project Overview Presentation](pop.pdf)
   - [Milestone 1 Progress Presentation](ppt_021022.pdf)

## References
### Online References
   - [RSA Wikipedia Page](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
   - [RSA Encryption v1.5](https://datatracker.ietf.org/doc/html/rfc2313)
   - [RSA Cryptography Specifications v2.0](https://datatracker.ietf.org/doc/html/rfc2437)
   - [RSA Cryptography Specifications v2.2](https://datatracker.ietf.org/doc/html/rfc8017)
   - [SHA-3 Standard: Permutation-Based Hash and Extendable-Output Functions](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.202.pdf)
   - [FIPS PUB 186-4, Digital Signature Standard](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-4.pdf)
   - [FIPS PUB 186-5, Digital Signature Standard (Draft)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-5-draft.pdf)

### Literature References
   - Eiichiro Fujisaki, Tatsuaki Okamoto, David Pointcheval, and Jacques Stern. RSA-- OAEP is secure under the RSA assumption. In J. Kilian, ed., Advances in Cryptology -- CRYPTO 2001, vol. 2139 of Lecture Notes in Computer Science, SpringerVerlag, 2001.
   - Nemec, Matus; Sys, Marek; Svenda, Petr; Klinec, Dusan; Matyas, Vashek (November 2017). “The Return of Coppersmith's Attack: Practical Factorization of Widely Used RSA Moduli”.
   - Coron, Jean-Sébastien; Joye, Marc; Naccache, David; Paillier, Pascal (2000). Preneel, Bart (ed.). “New Attacks on PKCS#1 v1.5 Encryption”.
   - Victor Shoup. OAEP Reconsidered. IBM Zurich Research Lab, Saumerstr. 4, 8803 Ruschlikon, Switzerland. September 18, 2001.
   - Alexandra Boldyreva, Hideki Imai, Life Fellow, IEEE, and Kazukuni Kobara. How to Strengthen the Security of RSA-OAEP. IEEE TRANSACTIONS ON INFORMATION THEORY, VOL. 56, NO. 11, NOVEMBER 2010.
   - Fatma Mallouli, Aya Hellal, Nahla Sharief Saeed, Fatimah Abdulraheem Alzahrani. A Survey on Cryptography: comparative study between RSA vs ECC Algorithms, and RSA vs El-Gamal Algorithms. 2019 6th IEEE International Conference on Cyber Security and Cloud Computing (CSCloud)/ 2019 5th IEEE International Conference on Edge Computing and Scalable Cloud (EdgeCom).
   - P. Paillier and J. Villar, Trading One-Wayness against Chosen-Ciphertext Security in Factoring-Based Encryption, Advances in Cryptology - Asiacrypt 2006.
   - Brown, Daniel R. L. (2006). "What Hashes Make RSA-OAEP Secure?". IACR Cryptology ePrint Archive.



