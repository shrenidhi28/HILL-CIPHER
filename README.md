# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int key[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

void encrypt(char text[])
{
    int len = strlen(text);

    // Padding with X
    while(len % 3 != 0)
    {
        text[len] = 'X';
        len++;
    }
    text[len] = '\0';

    char cipher[100];

    for(int i = 0; i < len; i += 3)
    {
        int p1 = text[i] - 'A';
        int p2 = text[i+1] - 'A';
        int p3 = text[i+2] - 'A';

        int c1 = (key[0][0]*p1 + key[0][1]*p2 + key[0][2]*p3) % 26;
        int c2 = (key[1][0]*p1 + key[1][1]*p2 + key[1][2]*p3) % 26;
        int c3 = (key[2][0]*p1 + key[2][1]*p2 + key[2][2]*p3) % 26;

        cipher[i]   = c1 + 'A';
        cipher[i+1] = c2 + 'A';
        cipher[i+2] = c3 + 'A';
    }

    cipher[len] = '\0';

    printf("\nEncrypted Message : %s\n", cipher);
}

int main()
{
    char text[100];

    printf("Enter Plain Text : ");
    scanf("%s", text);

    for(int i = 0; text[i] != '\0'; i++)
        text[i] = toupper(text[i]);

    printf("Input Message     : %s\n", text);

    encrypt(text);

    return 0;
}
```

## OUTPUT
<img width="544" height="410" alt="image" src="https://github.com/user-attachments/assets/2f52956c-4263-4dbe-b301-ebc63385c328" />


## RESULT

Thus, the Hill Cipher algorithm was successfully implemented using C language, and the plaintext was encrypted using the given key matrix.

