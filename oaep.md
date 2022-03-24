# Optimal Asymmetric Encryption Padding (OAEP)

Optimal Asymmetric Encryption padding (OAEP) is one of the Padding Schemes which is employed with RSA. It was officially published in [RFC2437](https://datatracker.ietf.org/doc/html/rfc2437) in October 1998. OAEP is the preferred padding scheme since it is considered to be [IND-CCA2](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability) secure. However, there have been studies which contradict this claim stating OAEP is only [IND-CCA1](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability) secure. OAEP also employs a Hash function and a [Mask generation function](https://en.wikipedia.org/wiki/Mask_generation_function) while forming the encoded message.

## Encoding using OAEP

OAEP has the following key components when encoding the message:-
- Hash function Hash() with length `hlen` bytes.
- Mask Generation Function(MGF) mask() which produces masked output of given length.
  - MGF functions as: `mask(ip, n) = op` where `len(op) = n`.
- Optional Label for each message. In our case, we consider label is always empty string.

OAEP Encoding works as follows:-
- Length checking message(m):-
  - If `len(m) > k - 2 - 2 * hLen`, report error and stop.
- Create data block (DB):-
  - Append Hash(L) as start of string.
  - Append (k - len(m) - 2 * hLen - 2) 0x00 bytes.
  - Append 0x01 as seperation byte to mark end of 0x00 bytes.
  - Append message to form DB of length k - hLen - 1.
- Generate random seed (s) where len(s) = hLen bytes.
- Generate `DBmask = mask(s, k - hLen - 1)`
- Generate `MaskedDB = DBMask xor DB`
- Generate `seedMask = mask(DB, hLen)`
- Generate `MaskedSeed = seedMask xor seed`
- Generate Encoded message `(EM) = 0x00 || maskedSeed || maskedDB`
