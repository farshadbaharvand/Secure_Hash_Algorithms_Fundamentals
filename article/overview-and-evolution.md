## 2. The Secure Hash Algorithm (SHA) Family: Overview and Evolution

The **Secure Hash Algorithm (SHA)** family is a set of cryptographic hash functions designed and standardized by the **National Institute of Standards and Technology (NIST)**, in collaboration with the **National Security Agency (NSA)**. The SHA family has evolved through multiple versions, each addressing the limitations and vulnerabilities discovered in its predecessors.

### 2.1 Members of the SHA Family

The SHA family consists of the following primary variants:

| SHA Variant | Year Introduced | Digest Length | Status |
|-------------|-----------------|---------------|--------|
| **SHA-0**   | 1993            | 160 bits      | Deprecated (flawed) |
| **SHA-1**   | 1995            | 160 bits      | Broken (collisions found) |
| **SHA-2**   | 2001            | 224, 256, 384, 512 bits | Secure (widely used) |
| **SHA-3**   | 2015            | 224, 256, 384, 512 bits | Secure (new design approach) |

### 2.2 SHA-0 and SHA-1

- **SHA-0** was the original version, published in 1993. It was quickly replaced due to undisclosed flaws in its design.
- **SHA-1**, published in 1995, was a revised version with minor changes to improve security. However, practical collision attacks were demonstrated:
  - In 2017, the **SHAttered** attack successfully produced real-world collisions, rendering SHA-1 unsuitable for cryptographic applications.
  - Modern cryptographic standards no longer consider SHA-1 secure.

### 2.3 The SHA-2 Family

SHA-2, introduced in 2001, is not a single algorithm but a family of hash functions with varying digest lengths:
- **SHA-224**
- **SHA-256**
- **SHA-384**
- **SHA-512**
- **SHA-512/224**
- **SHA-512/256**

SHA-2 functions are based on the **Merkle–Damgård construction** and use the **Davies–Meyer compression function** with a one-way compression based on the SHA-1 design, but with larger internal state sizes and different constants.

**SHA-256** and **SHA-512** are the most commonly used, especially in applications like:
- TLS certificates
- Blockchain systems (e.g., Bitcoin uses SHA-256)
- Digital signatures (e.g., RSA, ECDSA with SHA-2)

### 2.4 The SHA-3 Family

SHA-3, standardized in 2015, differs significantly from SHA-1 and SHA-2 in its internal design:
- Based on the **Keccak** sponge construction, SHA-3 provides resistance against length extension attacks and other vulnerabilities inherent in Merkle–Damgård-based hashes.
- Offers the same output sizes as SHA-2: 224, 256, 384, and 512 bits.

Advantages of SHA-3:
- Provides **cryptographic diversity** in case unforeseen weaknesses are found in SHA-2.
- More flexible due to its sponge construction, enabling other cryptographic primitives like extendable output functions (XOFs).

Despite its robust design, SHA-3 adoption has been gradual since SHA-2 remains sufficiently secure for most applications.

### 2.5 Evolution and Motivation

The progression from SHA-0 to SHA-3 was driven by the following factors:
- Discovery of cryptanalytic attacks (collisions, length-extension, pre-image attacks).
- Need for increased digest lengths to match growing computational power.
- Desire for alternative designs resistant to structural attacks on Merkle–Damgård construction.

The SHA family’s evolution reflects the continuous effort to maintain data security in the face of advancing attack techniques and growing computational resources.

### 2.6 Current Status of SHA Algorithms

| Algorithm | Current Security Status | Recommended Usage |
|-----------|-------------------------|------------------|
| SHA-0     | Broken (vulnerable to collisions) | Do not use |
| SHA-1     | Broken (practical collisions) | Deprecated, do not use |
| SHA-2     | Secure | Recommended for most applications |
| SHA-3     | Secure | Alternative to SHA-2 for future-proofing |

Modern security standards (e.g., NIST SP 800-107) strongly recommend SHA-2 or SHA-3 for all cryptographic applications.

