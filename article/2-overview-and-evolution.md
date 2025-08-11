# 2. The Secure Hash Algorithm (SHA) Family: Overview and Evolution

The **Secure Hash Algorithm (SHA)** family is a set of cryptographic hash functions designed and standardized by the **National Institute of Standards and Technology (NIST)**, in collaboration with the **National Security Agency (NSA)**.  
These algorithms are widely used for data integrity, digital signatures, password hashing, and blockchain technologies.  
Over the years, SHA has evolved through multiple versions to address **performance needs, discovered vulnerabilities, and advances in cryptanalysis**.

---

## 2.1 Generational Timeline of SHA

~~~~mermaid

gantt
    title SHA Family Evolution Timeline
    dateFormat  YYYY
    axisFormat  %Y
    excludes    weekends

    section SHA Versions
    SHA-0: active, 1993, 1993
    SHA-1: done, 1995, 1995
    SHA-2: done, 2001, 2001
    SHA-512/224 & 512/256: done, 2008, 2008
    SHA-3: crit, 2015, 2015
%% Colors:
%% active: light blue, done: green, crit: red

~~~~

---

## 2.2 Members of the SHA Family

| SHA Variant   | Year | Digest Length (bits) | Internal State Size | Status       | Notes                               |
|---------------|------|---------------------|---------------------|--------------|-----------------------------------|
| SHA-0         | 1993 | 160                 | 512                 | ❌ Deprecated | Withdrawn due to flaws.            |
| SHA-1         | 1995 | 160                 | 512                 | ❌ Broken    | SHAttered collision in 2017.      |
| SHA-224       | 2001 | 224                 | 512                 | ✅ Secure   | SHA-256 truncated.                 |
| SHA-256       | 2001 | 256                 | 512                 | ✅ Secure   | Used in Bitcoin, TLS.              |
| SHA-384       | 2001 | 384                 | 1024                | ✅ Secure   | SHA-512 truncated.                 |
| SHA-512       | 2001 | 512                 | 1024                | ✅ Secure   | Used in high-security apps.        |
| SHA-512/224   | 2008 | 224                 | 1024                | ✅ Secure   | Alternative truncation.            |
| SHA-512/256   | 2008 | 256                 | 1024                | ✅ Secure   | Alternative truncation.            |
| SHA-3         | 2015 | 224–512             | — (Sponge)          | ✅ Secure   | Keccak-based.                     |

## 2.3 Evolution Drivers

**Why new versions emerged:**

- **SHA-0 → SHA-1**  
  Fixed internal weakness (susceptible to differential cryptanalysis).

- **SHA-1 → SHA-2**  
  Larger digest lengths, different constants, and more rounds to resist collision attacks.

- **SHA-2 → SHA-3**  
  Different design paradigm (sponge construction) to avoid any Merkle–Damgård-specific flaws.


--- 

## 2.4 Internal Architecture

### SHA-2 Workflow

```mermaid
flowchart LR
    A[Input Message] --> B[Padding \ (length adjusted\)]
    B --> C[Block Parsing \ (512 or 1024 bits\)]
    C --> D[Message Schedule Expansion]
    D --> E[Compression Function]
    E --> F[State Update]
    F --> G[Final Digest Output]

```


- **Padding:** Ensures message length ≡ 448 (mod 512) for SHA-256 (or equivalent for SHA-512).
- **Message Schedule:** Expands input into multiple 32-bit or 64-bit words.
- **Compression:** Uses bitwise operations, modular addition, and constants.
- **Output:** Fixed-size hash digest.

---

## 2.5 Security Status (2025)

| Algorithm | Collision Resistance | Preimage Resistance | Status     |
|-----------|----------------------|---------------------|------------|
| SHA-0     | ❌ Weak              | ❌ Weak             | Broken     |
| SHA-1     | ❌ Broken            | ⚠ Partial           | Deprecated |
| SHA-2     | ✅ Strong            | ✅ Strong           | Active     |
| SHA-3     | ✅ Strong            | ✅ Strong           | Active     |

> **Note:** SHA-3 adoption is still slower than SHA-2 due to compatibility and migration costs, not because of security concerns.

---

## 2.6 Adoption Trends (Estimated 2025)

~~~~mermaid
pie
    title SHA Adoption Share (2025 Estimate)
    "SHA-1 (Legacy)" : 5
    "SHA-2 Family" : 70
    "SHA-3 Family" : 20
    "Other Hash Functions" : 5
~~~~

---

## 2.7 Key Application Examples

- **SHA-256:** Bitcoin mining, TLS 1.3 certificates.
- **SHA-512:** High-security file integrity checks, password hashing.
- **SHA-3:** IoT device security, post-quantum cryptographic protocols.

---

## 2.8 Benchmarking SHA-2 vs SHA-3 in JavaScript

This benchmark compares the speed of SHA-256 (from SHA-2) and SHA-3 hashing using the `js-sha3` library and Node.js crypto module.

~~~~javascript
const crypto = require('crypto');
const { sha3_256 } = require('js-sha3');

const input = "The quick brown fox jumps over the lazy dog";

function benchmarkSHA256(iterations = 10000) {
  console.time('SHA-256');
  for(let i = 0; i < iterations; i++) {
    crypto.createHash('sha256').update(input).digest('hex');
  }
  console.timeEnd('SHA-256');
}

function benchmarkSHA3_256(iterations = 10000) {
  console.time('SHA3-256');
  for(let i = 0; i < iterations; i++) {
    sha3_256(input);
  }
  console.timeEnd('SHA3-256');
}

benchmarkSHA256();
benchmarkSHA3_256();
~~~~

**Interpretation:**  
Typically, SHA-256 is faster due to native implementation in crypto modules, while SHA-3 is slower but offers different security properties. Actual times vary by hardware.

---

## 2.9 Takeaways

- SHA family evolved to address cryptanalysis breakthroughs and computational needs.
- SHA-2 remains the dominant standard but SHA-3 provides a valuable alternative design.
- Developers should choose algorithms based on security requirements, compatibility, and performance.
