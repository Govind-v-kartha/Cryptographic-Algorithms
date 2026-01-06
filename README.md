# Cryptography Assignment Collection

A comprehensive collection of cryptographic algorithms and implementations demonstrating key concepts in modern cryptography, including symmetric ciphers, asymmetric encryption, key exchange protocols, and hash functions.

---

## Table of Contents

1. [Overview](#overview)
2. [Algorithms](#algorithms)
   - [Symmetric Encryption](#symmetric-encryption)
   - [Asymmetric Encryption](#asymmetric-encryption)
   - [Key Exchange](#key-exchange)
   - [Hash Functions](#hash-functions)
3. [File Structure](#file-structure)
4. [Technologies Used](#technologies-used)
5. [Installation & Usage](#installation--usage)

---

## Overview

This collection contains implementations and analysis of 10 major cryptographic algorithms, covering:
- **Block Ciphers**: AES, DES, Toy Block Cipher
- **Stream Ciphers**: RC4, ChaCha20
- **Public-Key Cryptography**: RSA, ElGamal, ECC, Diffie-Hellman
- **Hash Functions**: SHA-256, SHA-512, HMAC

Each algorithm is presented with:
- ✅ Complete implementation
- ✅ Encryption/Decryption examples
- ✅ Performance analysis
- ✅ Security evaluation
- ✅ Key variation and avalanche effect analysis

---

## Algorithms

### Symmetric Encryption

#### 1. **AES (Advanced Encryption Standard)**

**What it is:**
AES is a symmetric encryption algorithm and is the current standard for secure data encryption adopted by the U.S. government.

**How it works:**
- Uses a block size of 128 bits (16 bytes)
- Supports key sizes of 128, 192, or 256 bits
- Operates in multiple modes: ECB, CBC, CTR, GCM, etc.
- **Process:**
  1. **Key Expansion**: Derives round keys from the original key
  2. **Initial Round**: XOR plaintext with first round key
  3. **Main Rounds** (9-13 rounds depending on key size):
     - SubBytes: Non-linear byte substitution using S-box
     - ShiftRows: Permutation of byte positions
     - MixColumns: Mixing columns for diffusion
     - AddRoundKey: XOR with round key
  4. **Final Round**: Same as main rounds but without MixColumns

**Key Properties:**
- **Block Size**: 128 bits
- **Key Sizes**: 128, 192, 256 bits
- **Rounds**: 10, 12, 14 (depending on key size)
- **Mode**: CBC (Cipher Block Chaining) commonly used
- **Security**: Highly secure, no practical attacks known

**Applications:**
- Secure file storage
- Database encryption
- Network communication (TLS/SSL)
- Government classified information

**File**: `AES_Encryption.ipynb`

---

#### 2. **DES (Data Encryption Standard)**

**What it is:**
DES is a symmetric block cipher that was the standard encryption method for many years. Now considered outdated due to small key size.

**How it works:**
- Block size: 64 bits (8 bytes)
- Key size: 56 bits (64 bits with parity)
- **Process:**
  1. **Initial Permutation (IP)**: Rearrange input bits
  2. **16 Rounds** of Feistel Network:
     - Divide block into left (L) and right (R) halves
     - Apply function f to R with round key
     - XOR result with L
     - Swap L and R
  3. **Final Permutation (IP⁻¹)**: Inverse of initial permutation

**Key Properties:**
- **Block Size**: 64 bits
- **Key Size**: 56 effective bits
- **Rounds**: 16
- **Security**: WEAK - vulnerable to brute force attacks

**Why it's outdated:**
- Small key size (56 bits) - can be brute-forced
- Block size (64 bits) - creates vulnerabilities with large datasets
- Takes only ~22 hours to crack on modern hardware

**Historical Use:**
- Banking (legacy systems)
- Government (before AES)
- Legacy encryption in older systems

**Note**: 3DES (Triple DES) was developed to address weaknesses by applying DES three times, but AES is now the standard.

**File**: `DES_Block_Cipher.ipynb`

---

#### 3. **ChaCha20 Stream Cipher**

**What it is:**
ChaCha20 is a modern stream cipher designed to be faster than AES on software and suitable for various platforms.

**How it works:**
- **Key Size**: 256 bits
- **Nonce Size**: 96 bits (or 64 bits in original)
- **Counter**: 32-bit counter
- **Process:**
  1. Initialize state with key, nonce, and counter
  2. Apply 20 rounds of operations (hence "ChaCha20")
  3. Generate keystream block (512 bits)
  4. XOR plaintext with keystream
  5. Increment counter for next block

**Key Properties:**
- **Stream Cipher**: Generates keystream independently
- **Parallelizable**: Each block can be computed independently
- **No Padding**: Works with any message length
- **Fast**: Extremely fast on software implementations

**Advantages:**
- Simpler than AES
- Better performance on resource-constrained devices
- Resistant to timing attacks

**Applications:**
- Mobile devices and embedded systems
- Internet protocols (IETF RFC 7539)
- TLS 1.3 encryption
- Wireless networks

**File**: `ChaCha20_Cipher.ipynb`

---

#### 4. **RC4 Stream Cipher**

**What it is:**
RC4 is a historical stream cipher, once widely used but now considered weak and should not be used for new systems.

**How it works:**
- **Key Size**: 40-2048 bits (typically 128 bits)
- **Process:**
  1. **Key Scheduling Algorithm (KSA)**:
     - Initialize permutation array S with values 0-255
     - Use key to permute the array
  2. **Pseudo-Random Generation Algorithm (PRGA)**:
     - Generate keystream bytes using state permutation
     - XOR plaintext with keystream
     - Update state for each byte

**Key Properties:**
- **Stream Cipher**: Variable output
- **Simple**: Easy to implement
- **Fast**: Byte-by-byte generation

**Security Issues:**
- Weak key scheduling: Some keys produce biased output
- Keystream bias: Not truly random
- Known plaintext attacks
- Vulnerability to FMS (Fluhrer, Mantin, Shamir) attack

**Why it's deprecated:**
- Multiple practical attacks demonstrated
- Biased keystream output
- Weak against modern attackers

**Legacy Use:**
- WEP (WiFi) - broken
- TLS/SSL - removed in TLS 1.3

**File**: `RC4_Stream_Cipher.ipynb`

---

#### 5. **Toy Block Cipher**

**What it is:**
A simplified, educational block cipher demonstrating fundamental encryption principles (not for real-world use).

**How it works:**
- **Block Size**: 16 bits
- **Key Size**: 16 bits
- **Components:**
  1. **S-Box**: Simple substitution table (4-bit input/output)
  2. **Permutation**: Bit rearrangement
  3. **Key XOR**: Add key bytes to block

**Process:**
```
Encryption:
  1. XOR block with key
  2. Apply S-box substitution
  3. Apply permutation
  4. XOR again with key

Decryption (reverse):
  1. XOR block with key
  2. Apply inverse permutation
  3. Apply inverse S-box
  4. XOR again with key
```

**Modes Demonstrated:**
- **ECB (Electronic CodeBook)**: Simple mode, reveals patterns
- **CBC (Cipher Block Chaining)**: Uses initialization vector
- **CFB (Cipher Feedback)**: Stream cipher mode

**Purpose:**
- Educational tool to understand block ciphers
- Demonstrates S-boxes and permutations
- Not suitable for real encryption (too small block size)

**File**: `Toy_Block_Cipher.ipynb`

---

### Asymmetric Encryption

#### 6. **RSA & Hybrid Encryption**

**What it is:**
RSA is the most widely used public-key cryptosystem, combining public-key encryption with symmetric encryption for practical use.

**How it works:**

**RSA Key Generation:**
```
1. Select two large prime numbers p and q
2. Compute n = p × q
3. Compute φ(n) = (p-1) × (q-1)
4. Select e (1 < e < φ(n)) where gcd(e, φ(n)) = 1
5. Compute d = e⁻¹ mod φ(n)
6. Public Key: (n, e)
7. Private Key: (n, d)
```

**RSA Encryption:**
```
Ciphertext = Plaintext^e mod n
```

**RSA Decryption:**
```
Plaintext = Ciphertext^d mod n
```

**Hybrid Encryption (RSA + AES):**
1. Generate session key (random 128-bit AES key)
2. Encrypt session key with RSA public key
3. Encrypt message with AES and session key
4. Generate HMAC for authentication
5. Send: [Encrypted Session Key] + [Ciphertext] + [HMAC]

**Key Properties:**
- **Key Sizes**: 1024, 2048, 4096 bits (minimum 2048 bits recommended)
- **Public Key Operations**: Used for encryption/signature verification
- **Private Key Operations**: Used for decryption/signature creation
- **Security**: Based on difficulty of factoring large numbers

**Advantages:**
- Solves key distribution problem
- Enables digital signatures
- Secure key establishment

**Disadvantages:**
- Slow encryption (not for large data)
- Requires key size to be large
- Hybrid approach needed for practical use

**Applications:**
- Email encryption (PGP)
- Digital signatures
- SSL/TLS handshake
- Key establishment
- Bitcoin and cryptocurrency

**File**: `RSA_and_Hybrid_Encryption.py`

---

#### 7. **ElGamal Encryption**

**What it is:**
ElGamal is a public-key encryption scheme based on the Diffie-Hellman key exchange, providing semantic security.

**How it works:**

**Key Generation:**
```
1. Select large prime p
2. Find primitive root g of p
3. Select random private key x (1 < x < p-1)
4. Compute public key y = g^x mod p
5. Public Key: (p, g, y)
6. Private Key: x
```

**Encryption:**
```
1. Generate random session key k
2. Compute C1 = g^k mod p
3. Compute shared secret S = y^k mod p
4. Compute C2 = M × S mod p (M is plaintext)
5. Ciphertext: (C1, C2)
```

**Decryption:**
```
1. Compute S = C1^x mod p
2. Compute S⁻¹ = S^(p-2) mod p (Fermat's little theorem)
3. Plaintext M = C2 × S⁻¹ mod p
```

**Key Properties:**
- **Probabilistic**: Same plaintext produces different ciphertexts
- **Semantic Security**: Provides IND-CPA security
- **Key Size**: Large primes needed (e.g., 1024-2048 bits)
- **Ciphertext Expansion**: 2× plaintext size

**Advantages:**
- Semantic security
- Provably secure under Discrete Log assumption
- Efficient compared to RSA

**Disadvantages:**
- Slower than RSA for same security level
- Larger ciphertext
- Requires Discrete Log assumption (different from RSA)

**Applications:**
- Educational purposes
- Digital signatures (ElGamal signatures)
- Key agreement
- Some secure multiparty computation schemes

**File**: `ElGamal_Encryption.py`

---

#### 8. **ECC & ECDH (Elliptic Curve Cryptography)**

**What it is:**
ECC uses elliptic curves over finite fields, providing equivalent security to RSA with much smaller key sizes (256-bit ECC ≈ 2048-bit RSA).

**Elliptic Curve Basics:**
An elliptic curve is defined by the equation: **y² = x³ + ax + b (mod p)**

**Key Operations:**
- **Point Addition**: A + B = C (adding two points on curve)
- **Scalar Multiplication**: k × P = Q (adding point P to itself k times)
- **Discrete Log Problem**: Given Q = k × P, find k (hard problem)

**ECC Key Generation:**
```
1. Select curve parameters (a, b, p, G, n)
2. G: Base point (generator)
3. n: Order of base point
4. Private Key: d (random integer < n)
5. Public Key: Q = d × G (point on curve)
```

**ECDH Key Exchange:**
```
Alice:
  - Private key: a, Public key: A = a × G
  - Receives Bob's public key: B
  - Computes shared secret: S = a × B

Bob:
  - Private key: b, Public key: B = b × G
  - Receives Alice's public key: A
  - Computes shared secret: S = b × A

Both get: S = a × b × G (same shared secret)
```

**ECC-Based ElGamal Encryption:**
```
1. Ephemeral key pair: (k, C1 = k × G)
2. Shared secret from recipient's public key: S = k × Q
3. Encrypt: C2 = Message + S (or XOR)
4. Decrypt using private key: S = d × C1, Message = C2 - S
```

**Key Properties:**
- **256-bit ECC ≈ 2048-bit RSA** in security
- **Smaller Keys**: More efficient storage and transmission
- **Faster**: Smaller modulus means faster operations
- **Standards**: P-256, P-384, P-521, Curve25519

**Advantages:**
- Much smaller key sizes
- Faster computations
- Lower bandwidth requirements
- Suitable for mobile and IoT devices

**Disadvantages:**
- More complex mathematics
- Patent concerns (legacy)
- Smaller installed base than RSA

**Applications:**
- Modern TLS/SSL (TLS 1.3 default)
- Bitcoin and cryptocurrency (ECDSA)
- Mobile devices and IoT
- Signal protocol messaging
- DNSSEC

**File**: `ECC_ECDH_Encryption.ipynb`

---

### Key Exchange Protocols

#### 9. **Diffie-Hellman Key Exchange**

**What it is:**
Diffie-Hellman (DH) is a protocol for two parties to establish a shared secret over an insecure channel, enabling subsequent symmetric encryption.

**How it works:**

**Protocol Steps:**
```
Public Parameters:
  - Large prime p
  - Primitive root g

Alice:
  1. Generate random private key a (1 < a < p-1)
  2. Compute public value A = g^a mod p
  3. Send A to Bob

Bob:
  1. Generate random private key b (1 < b < p-1)
  2. Compute public value B = g^b mod p
  3. Send B to Alice

Shared Secret Computation:
  Alice: S = B^a mod p = g^(ab) mod p
  Bob:   S = A^b mod p = g^(ab) mod p
  Both get the same shared secret S!
```

**Key Properties:**
- **Asymmetry**: Attacker cannot compute S from A, B, p, g
- **Basis**: Discrete Logarithm Problem
- **Key Size**: Large primes (1024-2048 bits)
- **Security Against Eavesdropping**: YES
- **Security Against MITM**: NO (requires authentication)

**Why DH Alone Isn't Secure:**
- Vulnerable to man-in-the-middle attack
- Attacker can impersonate both parties
- **Solution**: Combine with digital signatures for authentication

**Variants:**
- **ECDH**: Elliptic Curve Diffie-Hellman (smaller keys, same security)
- **DHE**: Ephemeral DH (fresh keys for each session)

**Applications:**
- TLS/SSL handshake
- SSH key exchange
- VPN protocols (IPsec)
- Cryptocurrency protocols
- Signal protocol messaging

**Modern Use:**
- Forward Secrecy: Use DHE or ECDHE for each session
- Prevents compromise of long-term keys from breaking past sessions

**File**: `Diffie_Hellman_Key_Exchange.ipynb`

---

### Hash Functions

#### 10. **Cryptographic Hash Functions (SHA-256, SHA-512)**

**What it is:**
Hash functions produce fixed-size fingerprints of any input data. Cryptographic hashes have special properties making them suitable for security applications.

**SHA-256 vs SHA-512:**
| Property | SHA-256 | SHA-512 |
|----------|---------|---------|
| **Output Size** | 256 bits (32 bytes) | 512 bits (64 bytes) |
| **Block Size** | 512 bits | 1024 bits |
| **Word Size** | 32 bits | 64 bits |
| **Rounds** | 64 | 80 |

**How SHA-256 Works:**
```
1. **Preprocessing**:
   - Convert message to bits
   - Append '1' bit and pad to length ≡ 448 (mod 512)
   - Append original message length as 64-bit number

2. **Initialize Hash Values**: 8 initial values (A-H)

3. **Main Processing** (for each 512-bit block):
   - Expand block into 64 words (32 bits each)
   - Initialize working variables from hash values
   - Perform 64 rounds of:
     * Bitwise operations (AND, OR, XOR, NOT)
     * Addition modulo 2³²
     * Rotation and shifting

4. **Produce Hash**: Concatenate final hash values
```

**Key Properties:**
- **Deterministic**: Same input → same hash
- **Quick**: Fast to compute
- **Avalanche Effect**: Tiny input change → completely different hash
- **One-way**: Impossible to reverse from hash to input
- **Collision Resistance**: Infeasible to find two inputs with same hash
- **Pre-image Resistance**: Infeasible to find input from hash

**Cryptographic Properties:**
- **Pre-image Resistance**: Cannot find M from H(M)
- **Second Pre-image Resistance**: Cannot find M₂ ≠ M₁ where H(M₁) = H(M₂)
- **Collision Resistance**: Cannot find any M₁ ≠ M₂ where H(M₁) = H(M₂)

**Applications:**

**Message Authentication Code (MAC):**
```
MAC = Hash(Key || Message)
Verify by recomputing and comparing
```

**HMAC (Hash-based MAC):**
```
HMAC = Hash(Key ⊕ opad || Hash(Key ⊕ ipad || Message))
- opad: Outer padding constant
- ipad: Inner padding constant
Provides authentication and integrity
```

**Uses:**
- **Data Integrity**: Verify files haven't been corrupted
- **Digital Signatures**: Sign hash instead of entire file
- **Password Storage**: Hash passwords instead of storing plaintext
- **Blockchain**: Bitcoin uses SHA-256 for block hashes
- **HMAC**: Message authentication and integrity
- **Key Derivation**: Derive keys from passwords
- **Proof of Work**: Mining in cryptocurrency

**Security:**
- **SHA-256**: Currently secure (no practical attacks)
- **SHA-1**: DEPRECATED (collisions found in 2017)
- **MD5**: BROKEN (collisions trivial to find)

**File**: `Cryptographic_Hash_Functions.ipynb`

---

## File Structure

```
Cryptography/Assignment/
│
├── 📄 README.md (this file)
│
├── 📘 Python Scripts (2 unique files)
│   ├── ElGamal_Encryption.py
│   └── RSA_and_Hybrid_Encryption.py
│
├── 📓 Jupyter Notebooks (8 core algorithms)
│   ├── AES_Encryption.ipynb
│   ├── ChaCha20_Cipher.ipynb
│   ├── Cryptographic_Hash_Functions.ipynb
│   ├── DES_Block_Cipher.ipynb
│   ├── Diffie_Hellman_Key_Exchange.ipynb
│   ├── ECC_ECDH_Encryption.ipynb
│   ├── RC4_Stream_Cipher.ipynb
│   └── Toy_Block_Cipher.ipynb
│
└── 📊 Documentation (4 cleanup reports)
    ├── FILE_COMPARISON.txt
    ├── NOTEBOOK_ANALYSIS.txt
    ├── FINAL_DEDUPLICATION_REPORT.txt
    └── COMPLETE_CLEANUP_FINAL_REPORT.txt
```

---

## Technologies Used

### Core Libraries
- **PyCryptodome**: Industry-standard cryptographic library for Python
- **hashlib**: Standard Python library for hash functions
- **cryptography**: High-level cryptography recipes and primitives

### Algorithms Implemented
| Algorithm | Type | Key Size | Security |
|-----------|------|----------|----------|
| AES | Block Cipher | 128/192/256 | Excellent ✅ |
| DES | Block Cipher | 56 | Weak ❌ |
| ChaCha20 | Stream Cipher | 256 | Excellent ✅ |
| RC4 | Stream Cipher | 40-2048 | Weak ❌ |
| Toy Cipher | Educational | 16 | N/A (educational) |
| RSA | Public Key | 2048+ | Excellent ✅ |
| ElGamal | Public Key | 1024+ | Good ✅ |
| ECC | Public Key | 256 | Excellent ✅ |
| DH | Key Exchange | 1024+ | Good ✅ |
| SHA-256/512 | Hash | N/A | Excellent ✅ |

---

## Installation & Usage

### Prerequisites
```bash
pip install pycryptodome cryptography
```

### Running Python Scripts
```bash
python ElGamal_Encryption.py
python RSA_and_Hybrid_Encryption.py
```

### Running Jupyter Notebooks
```bash
jupyter notebook AES_Encryption.ipynb
jupyter notebook DES_Block_Cipher.ipynb
jupyter notebook ChaCha20_Cipher.ipynb
jupyter notebook Cryptographic_Hash_Functions.ipynb
jupyter notebook Diffie_Hellman_Key_Exchange.ipynb
jupyter notebook ECC_ECDH_Encryption.ipynb
jupyter notebook RC4_Stream_Cipher.ipynb
jupyter notebook Toy_Block_Cipher.ipynb
```

### Example Usage in Code

**AES Encryption:**
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad

key = b'0123456789abcdef0123456789abcdef'  # 32-byte key
iv = b'0123456789abcdef'
plaintext = b"Secret message"

cipher = AES.new(key, AES.MODE_CBC, iv)
ciphertext = cipher.encrypt(pad(plaintext, AES.block_size))
```

**SHA-256 Hash:**
```python
import hashlib

message = b"Hello, World!"
hash_obj = hashlib.sha256(message)
digest = hash_obj.hexdigest()
print(digest)  # a591a6d40bf420404a011733cfb7b190...
```

**HMAC Authentication:**
```python
import hmac
import hashlib

key = b"secret_key"
message = b"Message to authenticate"
hmac_tag = hmac.new(key, message, hashlib.sha256).digest()
```

---

## Security Best Practices

### ✅ Recommended for Production
- ✅ **AES-256** with CBC/GCM mode
- ✅ **ChaCha20-Poly1305** for streaming
- ✅ **RSA-2048+** for key exchange (with OAEP padding)
- ✅ **ECDH** with P-256 or Curve25519
- ✅ **SHA-256/SHA-512** for hashing
- ✅ **HMAC-SHA256** for authentication

### ❌ Never Use in Production
- ❌ **DES** - Use AES instead
- ❌ **RC4** - Use ChaCha20 or AES instead
- ❌ **SHA-1** - Use SHA-256 instead
- ❌ **MD5** - Use SHA-256 instead
- ❌ **ECB Mode** - Use CBC/GCM instead

### General Guidelines
1. **Always use authenticated encryption** (GCM, ChaCha20-Poly1305)
2. **Use strong key sizes** (256-bit symmetric, 2048+ RSA, 256-bit ECC)
3. **Use random IVs/nonces** for each encryption
4. **Implement Forward Secrecy** using ephemeral keys
5. **Use TLS 1.3+** for transport security
6. **Hash passwords** with bcrypt/Argon2, not SHA256
7. **Keep cryptographic libraries updated**

---

## Learning Outcomes

After studying this collection, you will understand:

### Symmetric Cryptography
- How block ciphers work (substitution, permutation, rounds)
- Difference between stream and block ciphers
- Modes of operation and their security implications
- Performance trade-offs between security and speed

### Asymmetric Cryptography
- Public-key infrastructure and how it solves key distribution
- Mathematical foundations (modular arithmetic, discrete logarithm)
- How different algorithms achieve security
- Practical hybrid encryption approaches

### Key Exchange & Agreement
- How parties establish shared secrets over insecure channels
- Man-in-the-middle attacks and mitigation
- Importance of forward secrecy in modern protocols

### Hash Functions & Authentication
- One-way properties and avalanche effect
- Message authentication codes and their role
- Digital signatures and their applications
- Password security and proper hashing

---

## References & Further Reading

### Standards & RFCs
- [NIST FIPS 197: AES Standard](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)
- [FIPS 46-3: DES (Legacy)](https://nvlpubs.nist.gov/nistpubs/Legacy/FIPS/nistfips46-3.pdf)
- [RFC 3394: AES Key Wrap](https://tools.ietf.org/html/rfc3394)
- [RFC 7539: ChaCha20-Poly1305](https://tools.ietf.org/html/rfc7539)
- [RFC 8446: TLS 1.3](https://tools.ietf.org/html/rfc8446)

### Textbooks
- "Cryptography and Network Security" - William Stallings
- "Handbook of Applied Cryptography" - Menezes, van Oorschot, Vanstone
- "Introduction to Modern Cryptography" - Katz & Lindell

### Online Resources
- [Cryptopals Challenges](https://cryptopals.com/) - Practical cryptography
- [CrypTool](https://www.cryptool.org/) - Educational cryptography software
- [keylength.com](https://www.keylength.com/) - Key length recommendations

---

## Educational Use

This collection is designed for:
- 🎓 University cryptography courses
- 📚 Self-study of cryptographic algorithms
- 🔬 Research and experimentation
- 💻 Implementation understanding
- ✏️ Competitive programming practice

---

## Status & Maintenance

**Current State**: ✅ Complete and Cleaned
- All algorithms properly named and organized
- No duplicate code or files
- Well-documented implementations
- Ready for educational and reference use

**Last Updated**: January 6, 2026

---

## License & Usage

These implementations are provided for **educational purposes**. 

**⚠️ Important Security Notice:**
- These implementations are for learning purposes
- Do NOT use Toy Block Cipher, RC4, or DES in production
- For production systems, use reviewed cryptographic libraries
- Always validate security requirements with experts

---

**Happy Learning! 🚀**

For questions, improvements, or suggestions, feel free to contribute to this educational collection.
