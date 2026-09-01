**EXP. NO: 3: IMPLEMENTATION OF HILL CIPHER**

**Name:** Shrenidhi

**Reg No:** 212223040196

**Dept:** CSE

**AIM:**

To write a C program to implement the Hill Cipher substitution technique.

**DESCRIPTION:**

Each letter is represented by a number modulo 26. The commonly used scheme is **A = 0, B = 1, ..., Z = 25**.

To encrypt a message, each block of **n letters** is multiplied by an invertible **n × n matrix modulo 26**. To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption.

The matrix used for encryption is called the **cipher key**, and it should be chosen from the set of invertible **n × n matrices modulo 26**.

**ALGORITHM:**

**STEP 1:** Read the plain text from the user.

**STEP 2:** Convert the plain text into groups of length three.

**STEP 3:** Arrange the key values in a 3 × 3 matrix.

**STEP 4:** Multiply the plaintext matrix with the key matrix modulo 26 to obtain the cipher text.

**STEP 5:** Combine all the encrypted groups to obtain the complete cipher text.

**STEP 6:** Use the inverse key matrix to decrypt the cipher text and obtain the original plaintext.

**PROGRAM:**

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int key[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

/* Correct inverse of key matrix modulo 26 */
int inverseKey[3][3] = {
    {25, 0, 1},
    {2, 25, 0},
    {24, 2, 25}
};

/* Encryption */
void encrypt(char text[], char cipher[])
{
    int len = strlen(text);

    /* Add X padding */
    while (len % 3 != 0)
    {
        text[len] = 'X';
        len++;
    }

    text[len] = '\0';

    for (int i = 0; i < len; i += 3)
    {
        int p1 = text[i] - 'A';
        int p2 = text[i + 1] - 'A';
        int p3 = text[i + 2] - 'A';

        int c1 = (key[0][0] * p1 +
                  key[0][1] * p2 +
                  key[0][2] * p3) % 26;

        int c2 = (key[1][0] * p1 +
                  key[1][1] * p2 +
                  key[1][2] * p3) % 26;

        int c3 = (key[2][0] * p1 +
                  key[2][1] * p2 +
                  key[2][2] * p3) % 26;

        cipher[i] = c1 + 'A';
        cipher[i + 1] = c2 + 'A';
        cipher[i + 2] = c3 + 'A';
    }

    cipher[len] = '\0';
}

/* Decryption */
void decrypt(char cipher[], char plain[])
{
    int len = strlen(cipher);

    for (int i = 0; i < len; i += 3)
    {
        int c1 = cipher[i] - 'A';
        int c2 = cipher[i + 1] - 'A';
        int c3 = cipher[i + 2] - 'A';

        int p1 = (inverseKey[0][0] * c1 +
                  inverseKey[0][1] * c2 +
                  inverseKey[0][2] * c3) % 26;

        int p2 = (inverseKey[1][0] * c1 +
                  inverseKey[1][1] * c2 +
                  inverseKey[1][2] * c3) % 26;

        int p3 = (inverseKey[2][0] * c1 +
                  inverseKey[2][1] * c2 +
                  inverseKey[2][2] * c3) % 26;

        if (p1 < 0) p1 += 26;
        if (p2 < 0) p2 += 26;
        if (p3 < 0) p3 += 26;

        plain[i] = p1 + 'A';
        plain[i + 1] = p2 + 'A';
        plain[i + 2] = p3 + 'A';
    }

    plain[len] = '\0';
}

int main()
{
    char text[100];
    char cipher[100];
    char plain[100];

    printf("Enter Plain Text : ");
    scanf("%99s", text);

    /* Convert to uppercase */
    for (int i = 0; text[i] != '\0'; i++)
    {
        text[i] = toupper((unsigned char)text[i]);
    }

    printf("Input Message     : %s\n", text);

    /* Encryption */
    encrypt(text, cipher);

    printf("\nEncrypted Message : %s\n", cipher);

    /* Decryption */
    decrypt(cipher, plain);

    printf("Decrypted Message : %s\n", plain);

    return 0;
}
```

**OUTPUT:**

<img width="698" height="291" alt="image" src="https://github.com/user-attachments/assets/3502cd3c-e237-4231-ab65-2219c3786e89" />

**RESULT:**

Thus, the Hill Cipher algorithm was successfully implemented using the C language, and the plaintext was encrypted and decrypted using the given key matrix.
