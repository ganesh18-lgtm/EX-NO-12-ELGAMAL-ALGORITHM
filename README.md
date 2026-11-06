# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <math.h>

// Function to compute modular exponentiation (base^exp % mod)
long long int modExp(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = ((__int128)result * base) % mod; // Prevent overflow
        }
        base = ((__int128)base * base) % mod; // Prevent overflow
        exp = exp / 2;
    }
    return result;
}

int main() {
    long long int p, g, privateKeyA, publicKeyA;
    long long int k, message, c1, c2, decryptedMessage;

    // Step 1: Input a large prime number (p) and a generator (g)
    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);
    printf("Enter a generator (g): ");
    scanf("%lld", &g);

    // Step 2: Ganesh inputs his private key
    printf("Enter Ganesh's private key: ");
    scanf("%lld", &privateKeyA);

    // Step 3: Compute Ganesh's public key (publicKey = g^privateKeyA mod p)
    publicKeyA = modExp(g, privateKeyA, p);
    printf("Ganesh's public key: %lld\n", publicKeyA);

    // Step 4: Input message and random number k
    printf("Enter the message to encrypt (must be less than %lld): ", p);
    scanf("%lld", &message);

    if (message >= p) {
        printf("Error: Message (%lld) must be smaller than prime number p (%lld).\n", message, p);
        return 1;
    }

    printf("Enter a random number k: ");
    scanf("%lld", &k);

    // Step 5: Compute ciphertext (c1 = g^k mod p, c2 = (message * publicKeyA^k) mod p)
    c1 = modExp(g, k, p);
    long long int sharedSecret = modExp(publicKeyA, k, p);
    c2 = ((__int128)message * sharedSecret) % p; // Prevent overflow

    printf("Encrypted message (c1, c2): (%lld, %lld)\n", c1, c2);

    // Step 6: Decrypt the message (decryptedMessage = (c2 * c1^(p-1-privateKeyA)) mod p)
    long long int s_inv = modExp(c1, p - 1 - privateKeyA, p);
    decryptedMessage = ((__int128)c2 * s_inv) % p; // Prevent overflow

    printf("Decrypted message: %lld\n", decryptedMessage);

    return 0;
}
```

## Output:

<img width="700" height="347" alt="image" src="https://github.com/user-attachments/assets/34ebdfb6-fd1b-4e0a-a8eb-56d75a7611e2" />


## Result:
The program is executed successfully.
