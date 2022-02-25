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
- Final implementation for algorithm is in accordacne with [FIPS 186-4](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-4.pdf) and [FIPS 185-5(Draft)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-5-draft.pdf)
- Prime numbers are generated for the following bit lengths:
  - 512-bit (RSA-1024)
  - 647-bit (RSA-1294)
  - 768-bit (RSA-1536)
  - 813-bit (RSA-1626)
  - 1024-bit (RSA-2048)
  - 2048-bit (RSA-4096)
- Prime number bit lengths are chosen from bit lengths not currently factorised by [RSA Factoring Challenge](https://en.wikipedia.org/wiki/RSA_Factoring_Challenge).
- Public exponent is chosen as *e*=65537.

> This page is still under construction
