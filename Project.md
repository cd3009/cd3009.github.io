# Padding schemes for the RSA and its Security
## Project information
   - **Faculty Advisor:** Prof. Stanisław Radziszowski

## Project Description
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The **Rivest-Shamir-Adleman** algorithm commonly known as the RSA Algorithm is widely used in today’s world. RSA is mainly used with digital signatures for authenticating users. It is based on the factoring problem. In simple words, the crux of RSA works with 2 large prime numbers and their product. The security of RSA is based on the fact that factoring the product to find the 2 large prime numbers is extremely difficult. However, there are attacks that could break RSA, if the prime numbers are not chosen wisely. There are also attacks on the nature of RSA (For e.g. RSA is deterministic), which contribute to the algortihm being susceptible to attacks.
   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To overcome these shortcomings, RSA is often used with a Padding Scheme. Some examples are **PKCS v1.5** and **Optimal Asymmetric Encryption Padding (OAEP)**. These padding schemes make RSA **probabilistic in nature** by applying **randomized padding** to the plaintext before it is encrypted using RSA. As part of this project, I will review the properties of RSA and study how the padding schemes strengthen RSA. Since practical RSA works with very large prime numbers, RSA is a computationally expensive algorithm. Thus, adding padding to the entire encryption process increases the computational overhead. The project aims to research and analyze the trade-off between security and computational cost while implementing RSA in various scenarios. Using this analysis, the project aims to comment on whether using RSA with/without padding is favorable.

## Milestone Roadmap
### Milestone 1
   - Review literature on the RSA and Padding Schemes.
      - Review the RSA algorithm
      - Review parameter selection methods for the RSA
      - Review Padding schemes for the RSA

   - Implement RSA and its parameter selection algorithm.

### Milestone 2
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

### Milestone 3
   - Perform experiments on the following to analyze security and performance:-
      - RSA without Padding schemes.
      - RSA implemented using PKCS #1 v1.5.
      - RSA implemented using OAEP.
      - RSA implemented using other* padding schemes

   - Report findings for the following:-
      - Security for RSA implemented with/without Padding schemes
      - Computational cost for each implementation of RSA

**Note:** other* padding schemes for RSA will be selected as part of research performed in Milestone 2. The plan for the project will be updated accordingly.

## Weekly Progress Report
### Milestone 1
   - [Week 1 & 2 Progress](Week1&2.md)
   
## References
### Online References
   - [RSA Cryptosystem Wikipedia page] (https://en.wikipedia.org/wiki/RSA_(cryptosystem))
   - [RSA Encryption v1.5] (https://datatracker.ietf.org/doc/html/rfc2313)
   - [RSA Cryptography Specifications v2.0] (https://datatracker.ietf.org/doc/html/rfc2437)
   - [RSA Cryptography Specifications v2.2] (https://datatracker.ietf.org/doc/html/rfc8017)

## Literature References
This secction will be populated as the project progresses.
