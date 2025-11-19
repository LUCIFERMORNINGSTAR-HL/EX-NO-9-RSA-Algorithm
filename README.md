# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```python
# rsa_demo.py
# Simple RSA demo for learning. Works with small integers (not secure for real use).

def egcd(a, b):
    # extended gcd: returns (g, x, y) with a*x + b*y = g = gcd(a,b)
    if b == 0:
        return (a, 1, 0)
    g, x1, y1 = egcd(b, a % b)
    return (g, y1, x1 - (a // b) * y1)

def modinv(a, m):
    g, x, _ = egcd(a, m)
    if g != 1:
        raise Exception("modular inverse does not exist")
    return x % m

def generate_keys():
    # small example primes (educational only)
    p = 61
    q = 53
    n = p * q
    phi = (p - 1) * (q - 1)

    e = 17                     # choose e (1 < e < phi) and gcd(e, phi) == 1
    d = modinv(e, phi)         # compute d, the modular inverse of e mod phi
    return (n, e, d)

def encrypt(m, e, n):
    return pow(m, e, n)

def decrypt(c, d, n):
    return pow(c, d, n)

if __name__ == "__main__":
    n, e, d = generate_keys()
    print("Public key: (n={}, e={})".format(n, e))
    print("Private key: d={}".format(d))

    # Example: message must be 0 <= m < n
    m = 65
    print("Plaintext m:", m)

    c = encrypt(m, e, n)
    print("Encrypted c:", c)

    m2 = decrypt(c, d, n)
    print("Decrypted m:", m2)
```
## Output:
<img width="359" height="207" alt="Screenshot 2025-11-19 111821" src="https://github.com/user-attachments/assets/704f727f-4f5f-4eaf-9905-c3b3bd50404e" />

## Result:
 The program is executed successfully.
