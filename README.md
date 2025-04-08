# Cryptography---19CS412-classical-techqniques
# EX-1:Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:

```
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <ctype.h>
void main()

{
    char plain[10],cipher[10];
    int key,i,length;
    int result;
    printf("\n Enter the plain text:");
    scanf("%s", plain);
    printf("\n Enter the key value:");
    scanf("%d", &key);
    printf("\n \n \t PLAIN TEXt: %s", plain);
    printf("\n \n \t ENCRYPTED TEXT:");
    for(i=0, length = strlen(plain); i<length; i++)
    {
        
        cipher[i]=plain[i] + key;
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
        cipher[i] = cipher[i] - 26;
        if (islower(plain[i]) && (cipher[i] > 'z'))
        cipher[i] = cipher[i] - 26;
        printf("%c", cipher[i]);

    }
    printf("\n \n \t AFTER DECRYPTION : ");
    for(i=0;i<length;i++)
    {
        
        plain[i]=cipher[i]-key;
        if(isupper(cipher[i])&&(plain[i]<'A'))
        plain[i]=plain[i]+26;
        if(islower(cipher[i])&&(plain[i]<'a'))
        plain[i]=plain[i]+26;
        printf("%c",plain[i]);
    }
    getch();

    
}

```
## OUTPUT:

![Screenshot 2025-03-18 142450](https://github.com/user-attachments/assets/42fac8f9-29d9-4039-af6e-428927e80bea)

## RESULT:
The program is executed successfully

---------------------------------
# EXP-2:PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define MX 5

void encryptPair(char ch1, char ch2, char key[MX][MX])
{
    int i, j, row1 = -1, col1 = -1, row2 = -1, col2 = -1;
    for (i = 0; i < MX; i++)
    {
        for (j = 0; j < MX; j++)
        {
            if (key[i][j] == ch1)
            {
                row1 = i;
                col1 = j;
            }
            else if (key[i][j] == ch2)
            {
                row2 = i;
                col2 = j;
            }
        }
    }
    if (row1 == row2)
        printf("%c%c", key[row1][(col1 + 1) % 5], key[row2][(col2 + 1) % 5]);
    else if (col1 == col2)
        printf("%c%c", key[(row1 + 1) % 5][col1], key[(row2 + 1) % 5][col2]);
    else
        printf("%c%c", key[row1][col2], key[row2][col1]);
}

void decryptPair(char ch1, char ch2, char key[MX][MX])
{
    int i, j, row1 = -1, col1 = -1, row2 = -1, col2 = -1;
    for (i = 0; i < MX; i++)
    {
        for (j = 0; j < MX; j++)
        {
            if (key[i][j] == ch1)
            {
                row1 = i;
                col1 = j;
            }
            else if (key[i][j] == ch2)
            {
                row2 = i;
                col2 = j;
            }
        }
    }
    if (row1 == row2)
        printf("%c%c", key[row1][(col1 + 4) % 5], key[row2][(col2 + 4) % 5]);
    else if (col1 == col2)
        printf("%c%c", key[(row1 + 4) % 5][col1], key[(row2 + 4) % 5][col2]);
    else
        printf("%c%c", key[row1][col2], key[row2][col1]);
}

int main()
{
    int i, j, k = 0, m = 0;
    char key[MX][MX], keyminus[25], keystr[25], plaintext[100];
    char alpha[26] = "ABCDEFGHIKLMNOPQRSTUVWXYZ";

    printf("Simulating Playfair Cipher\n");
    printf("Key text: ");
    fgets(keystr, sizeof(keystr), stdin);
    keystr[strcspn(keystr, "\n")] = 0;

    printf("Plain text: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = 0;

    for (i = 0; i < strlen(keystr); i++)
    {
        if (tolower(keystr[i]) == 'j')
            keystr[i] = 'I';
        keystr[i] = toupper(keystr[i]);
    }

    for (i = 0; i < strlen(plaintext); i++)
    {
        if (tolower(plaintext[i]) == 'j')
            plaintext[i] = 'I';
        plaintext[i] = toupper(plaintext[i]);
    }

    int n = strlen(keystr), found;
    for (i = 0; i < 25; i++)
    {
        found = 0;
        for (j = 0; j < n; j++)
        {
            if (keystr[j] == alpha[i])
            {
                found = 1;
                break;
            }
        }
        if (!found)
            keyminus[m++] = alpha[i];
    }

    k = 0;
    m = 0;
    for (i = 0; i < MX; i++)
    {
        for (j = 0; j < MX; j++)
        {
            if (k < n)
                key[i][j] = keystr[k++];
            else
                key[i][j] = keyminus[m++];
        }
    }

    printf("Cipher text: ");
    for (i = 0; i < strlen(plaintext); i++)
    {
        if (plaintext[i + 1] == '\0')
        {
            encryptPair(plaintext[i], 'X', key);
        }
        else if (plaintext[i] == plaintext[i + 1])
        {
            encryptPair(plaintext[i], 'X', key);
        }
        else
        {
            encryptPair(plaintext[i], plaintext[i + 1], key);
            i++;
        }
    }

    printf("\nDecrypted text: %s\n", plaintext);
    return 0;
}
```

## OUTPUT:

![Screenshot 2025-03-24 102740](https://github.com/user-attachments/assets/a058e0b5-4525-48b6-8c4b-c89e78043ac9)

## RESULT:
The program is executed successfully


---------------------------

## EXP-3: Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

void encipher();
void decipher();

int main() {
    int choice;
    while (1) {
        printf("\n1. ENCRYPT TEXT");
        printf("\t2. DECRYPED TEXT");
        printf("\t3. EXIT");
        printf("\n\nENTER YOUR CHOICE: ");
        scanf("%d", &choice);
        getchar(); // Consume newline character after scanf
        
        if (choice == 3)
        { 
            printf("\nEXIT\n");
            return 0;
        }
        else if (choice == 1)
            encipher();
        else if (choice == 2)
            decipher();
        else
            printf("PLEASE ENTER A VALID OPTION.\n");
    }
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];
    printf("\nENCRYPTION\n");

    printf("\nENTER PLAIN TEXT: ");
    scanf("%49s", input); // Prevent buffer overflow

    printf("\nENTER KEY VALUE: ");
    scanf("%9s", key); // Prevent buffer overflow

    printf("\nRESULTANT CIPHER TEXT: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0; // Reset key index if it exceeds the key length
        }
        printf("%c", 65 + (((toupper(input[i]) - 65) + (toupper(key[j]) - 65)) % 26)); // Encryption formula
    }
    printf("\n"); // New line after output
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;
    printf("\nDECRYPTION\n");

    printf("\nENTER CIPHER TEXT: ");
    scanf("%49s", input); // Prevent buffer overflow

    printf("\nENTER THE KEY VALUE: ");
    scanf("%9s", key); // Prevent buffer overflow

    printf("\nDECRYPTED PLAIN TEXT: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0; // Reset key index if it exceeds the key length
        }
        // Decryption formula
        value = (toupper(input[i]) - 65) - (toupper(key[j]) - 65);
        if (value < 0) {
            value += 26; // Correct the negative wrap-around in the alphabet
        }
        printf("%c", 65 + (value % 26));
    }
    printf("\n"); // New line after output
}
```

## OUTPUT:

![Screenshot 2025-04-08 230559](https://github.com/user-attachments/assets/ec793bf6-bb4c-459f-8769-e18137fe02e2)

![Screenshot 2025-04-08 230617](https://github.com/user-attachments/assets/9039f555-1455-4b3b-91f5-a65f1bbaadad)


## RESULT:
The program is executed successfully

-------------------------------------------------

## Exp:4 Vigenere Cipher
Vigenere Cipher using with different key values

## AIM:
To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:
Step 1:
Design of Vigenere Cipher algorithnm

Step 2:
Implementation using C or pyhton code

Step 3:
Testing algorithm with different key values. ALGORITHM DESCRIPTION: The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.

## PROGRAM:
```

#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

void encipher();
void decipher();

int main() {
    int choice;
    while (1) {
        printf("\n1. ENCRYPT TEXT");
        printf("\t2. DECRYPED TEXT");
        printf("\t3. EXIT");
        printf("\n\nENTER YOUR CHOICE: ");
        scanf("%d", &choice);
        getchar(); // Consume newline character after scanf
        
        if (choice == 3)
        { 
            printf("\nEXIT\n");
            return 0;
        }
        else if (choice == 1)
            encipher();
        else if (choice == 2)
            decipher();
        else
            printf("PLEASE ENTER A VALID OPTION.\n");
    }
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];
    printf("\nENCRYPTION\n");

    printf("\nENTER PLAIN TEXT: ");
    scanf("%49s", input); // Prevent buffer overflow

    printf("\nENTER KEY VALUE: ");
    scanf("%9s", key); // Prevent buffer overflow

    printf("\nRESULTANT CIPHER TEXT: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0; // Reset key index if it exceeds the key length
        }
        printf("%c", 65 + (((toupper(input[i]) - 65) + (toupper(key[j]) - 65)) % 26)); // Encryption formula
    }
    printf("\n"); // New line after output
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;
    printf("\nDECRYPTION\n");

    printf("\nENTER CIPHER TEXT: ");
    scanf("%49s", input); // Prevent buffer overflow

    printf("\nENTER THE KEY VALUE: ");
    scanf("%9s", key); // Prevent buffer overflow

    printf("\nDECRYPTED PLAIN TEXT: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0; // Reset key index if it exceeds the key length
        }
        // Decryption formula
        value = (toupper(input[i]) - 65) - (toupper(key[j]) - 65);
        if (value < 0) {
            value += 26; // Correct the negative wrap-around in the alphabet
        }
        printf("%c", 65 + (value % 26));
    }
    printf("\n"); // New line after output
}

```

## OUTPUT:

![Screenshot 2025-04-08 230559](https://github.com/user-attachments/assets/b70e1a8d-90ca-485e-afd2-c3ecf644ffb1)

![Screenshot 2025-04-08 230617](https://github.com/user-attachments/assets/4af99bcf-5660-45f2-90c8-bf2cb247497c)


## RESULT:
The program is executed successfully..
