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
```
#include <stdio.h>

// Function to compute GCD
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to compute modular exponentiation
int mod_exp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp / 2;
        base = (base * base) % mod;
    }
    return result;
}

// Function to find multiplicative inverse of e mod phi
int mod_inverse(int e, int phi) {
    int d = 1;
    while ((d * e) % phi != 1) {
        d++;
    }
    return d;
}

int main() {
    int p, q, e;
    printf("Enter two prime numbers (p and q): ");
    scanf("%d %d", &p, &q);

    int n = p * q;
    int phi = (p - 1) * (q - 1);

    // User inputs e
    printf("Enter value of e (1 < e < %d) such that gcd(e, %d) = 1: ", phi, phi);
    scanf("%d", &e);

    if (gcd(e, phi) != 1) {
        printf("Invalid e! It must be coprime with %d.\n", phi);
        return 1;
    }

    // Compute d
    int d = mod_inverse(e, phi);

    printf("Public Key: (e=%d, n=%d)\n", e, n);
    printf("Private Key: (d=%d, n=%d)\n", d, n);

    // Encryption
    int msg;
    printf("Enter message (as an integer < %d): ", n);
    scanf("%d", &msg);

    int cipher = mod_exp(msg, e, n);
    printf("Encrypted message: %d\n", cipher);

    // Decryption
    int decrypted = mod_exp(cipher, d, n);
    printf("Decrypted message: %d\n", decrypted);

    return 0;
}

```
## Output:

<img width="844" height="291" alt="image" src="https://github.com/user-attachments/assets/70d6b4ae-31ac-41e1-a04d-df3f5b4d4749" />


## Result:
 The program is executed successfully.
