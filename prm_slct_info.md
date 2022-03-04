# Parameter Selection Algorithm

## Environment and Implementation Specifications
### Device Specifications
- Personal Laptop will be used for development and testing.
- Specifications for Laptop:
  - CPU: [AMD Ryzen 9 5900HS](https://www.amd.com/en/products/apu/amd-ryzen-9-5900hs)
  - RAM: 16 GB

### Development Specifications
- Language used: Java 11
- IDE used: [Visual Studio Code](https://code.visualstudio.com/)
- Storage and mathematical operations on large primes are performed using [java.math.BigInteger](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/math/BigInteger.html).

### Implementation Specifications
- Final implementation for algorithm is in accordacne with [FIPS 186-4](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-4.pdf) and [FIPS 185-5(Draft)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-5-draft.pdf).
- Prime numbers are generated for the following bit lengths:
  - 512-bit (RSA-1024)
  - 647-bit (RSA-1294)
  - 768-bit (RSA-1536)
  - 813-bit (RSA-1626)
  - 1024-bit (RSA-2048)
  - 2048-bit (RSA-4096)
- Prime number bit lengths are chosen from bit lengths not currently factorised by [RSA Factoring Challenge](https://en.wikipedia.org/wiki/RSA_Factoring_Challenge).
- Public exponent is chosen as *e*=65537.

### What are Safe primes?

#### A prime number *p* is a safe prime if *p-1* is such that *p-1 = 2 x (prime number)*. For example:
    Let *p* = 227 hence *p-1* = 226.
    Now *(p-1)/2* = 113.
    Since 113 is prime, 227 is a safe prime.

#### [Pollard's p-1 Algorithm](https://en.wikipedia.org/wiki/Pollard%27s_p_%E2%88%92_1_algorithm)
    The basic idea of this algorithm is that for finding prime number p, we can use p-1. If p-1 has many small prime factors, we can factor 
    it to then find p. Since RSA uses (prime - 1) to calculate ϕ(n), the RSA primes should be safe primes. Pollards algorithm usually 
    doesn't work with cryptographic random primes but if it does, it could be detrimental to RSA as one could easily find p or q. Thus, as 
    part of the parameter selection process we also check for safe primes.

### The original parameter selection algorithm for generating primes/safe primes: 
    - Generate seed value for random bit generation
    - Generate random bits for given bit length
    - Set least and most significant bit to 1, thus generating large odd number
    - Check if number is prime using following primality tests:
        - Miller-Rabin Primality test
        - Lucas-lehmer Primality test
     - If number is prime record it, else check for next number.
     - If safe prime check is enabled, check if recorded prime number is safe prime and save.
     - If safe prime check is not enabled, save recorded prime.
     
### Refined parameter selection algorithm for generating primes: 
    - Generate primes for given bit length as follows:-
        - Generate seed value for random bit generation
        - Generate random bits for given bit length
        - Set least and most significant bit to 1, thus generating large odd number
        - Check if number has factors within 1st million numbers, if yes discard and check for next number.
        - Check if number is prime using following primality tests:
            - Miller-Rabin Primality test
            - Lucas-lehmer Primality test
        - If number is prime save it, else check for next number.
    
    - Once all primes are generated, segregate primes as safe and basic primes.

> This page is still under construction
