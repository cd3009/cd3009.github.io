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

### Performance Analysis of Algorithms
#### Old Parameter algorithm disadvantages:
- The old parameter algorithm was very fast in case of basic primes but very poor when it came to safe primes.
- Directly generating safe primes was very expensive. This is because randomly generating a prime and checking for it being safe in the same loop proves to be computatationally costly.
- The average times for the old algorithm:
  - 2primes/sec for basic primes
  - 1prime/2min for safe primes.
- These times are when prime numbers for variable lengths are generated together. 
- The generation times for safe primes of higher bit length values were poorer than above highlighted times.

#### New Parameter algorithm performance:
- Thus, the decision to split generation of safe primes as a filtering process was chosen.
- In this case, a bunch of basic prime numbers are generated and then safe primes are filtered out of them. This created a significant performance increase.
- Since higher bit numbers have lower rounds in primality tests, a filtering process was chosen.
- The filtering process checks the odd number for factors within 3..2<sup>20</sup>-1. If any factors are present, the odd number is disacrded from primality tests.
- This affected the performance of the new algorithm but not by much. The average time for generating primes is approx 1 prime/2 mins.
- Due to the filtering process, more odd numbers are filtered but better quality of odd numbers are chosen for primality tests.

#### Comments on Java and java.math.BigInteger:
- Since Java uses a garbage collector, memory is cleared at regular intervals rather than being immediately cleared when not required.
- Also, BigInteger holds metadata about the number rather than just the number. This causes additional memory stress on the program.
- The above points surely affect the performance of the new algorithm. A probable performance increase would be implementing the algorithm in Rust.
- Rust is a compiled language and also clears memory based on scope. This may reduce the memory stress and provide for aa more meory efficient algorithm
