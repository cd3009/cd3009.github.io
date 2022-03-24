# Optimal Asymmetric Encryption Padding (OAEP)

Optimal Asymmetric Encryption padding (OAEP) is one of the Padding Schemes which is employed with RSA. It was officially published in [RFC2437](https://datatracker.ietf.org/doc/html/rfc2437) in October 1998. OAEP is the preferred padding scheme since it is considered to be [IND-CCA2](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability) secure. However, there have been studies which contradict this claim stating OAEP is only [IND-CCA1](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability) secure. OAEP also employs a Hash function and a [Mask generation function](https://en.wikipedia.org/wiki/Mask_generation_function) while forming the encoded message.

> page is under construction
