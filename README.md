# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_LEN 100

// Function to encrypt the plaintext
void vigenereEncrypt(char plaintext[], char keyword[], char ciphertext[]) {
    int ptLen = strlen(plaintext);
    int kwLen = strlen(keyword);
    int i, j = 0;

    for (i = 0; i < ptLen; i++) {
        if (isalpha(plaintext[i])) {
            char ptChar = toupper(plaintext[i]);
            char kwChar = toupper(keyword[j % kwLen]);

            // STEP-6 & 7: Encryption math -> (P + K) % 26
            char cipherChar = ((ptChar - 'A') + (kwChar - 'A')) % 26 + 'A';
            
            if (islower(plaintext[i])) {
                ciphertext[i] = tolower(cipherChar);
            } else {
                ciphertext[i] = cipherChar;
            }
            j++;
        } else {
            ciphertext[i] = plaintext[i];
        }
    }
    ciphertext[ptLen] = '\0';
}

// Function to decrypt the ciphertext back to plaintext
void vigenereDecrypt(char ciphertext[], char keyword[], char decryptedtext[]) {
    int ctLen = strlen(ciphertext);
    int kwLen = strlen(keyword);
    int i, j = 0;

    for (i = 0; i < ctLen; i++) {
        if (isalpha(ciphertext[i])) {
            char ctChar = toupper(ciphertext[i]);
            char kwChar = toupper(keyword[j % kwLen]);

            // Decryption math -> (C - K + 26) % 26
            // We add 26 to handle negative results gracefully in C
            char decChar = ((ctChar - 'A') - (kwChar - 'A') + 26) % 26 + 'A';
            
            if (islower(ciphertext[i])) {
                decryptedtext[i] = tolower(decChar);
            } else {
                decryptedtext[i] = decChar;
            }
            j++;
        } else {
            decryptedtext[i] = ciphertext[i];
        }
    }
    decryptedtext[ctLen] = '\0';
}

int main() {
    char plaintext[MAX_LEN];
    char keyword[MAX_LEN];
    char ciphertext[MAX_LEN];
    char decryptedtext[MAX_LEN];

    // Read inputs
    printf("Enter the plain text: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("Enter the key : ");
    fgets(keyword, sizeof(keyword), stdin);
    keyword[strcspn(keyword, "\n")] = '\0';

    // 1. Run Encryption
    vigenereEncrypt(plaintext, keyword, ciphertext);

    // 2. Run Decryption using the generated ciphertext
    vigenereDecrypt(ciphertext, keyword, decryptedtext);

    // Output Results
    printf("\nOriginal Plain Text: %s\n", plaintext);
    printf("Key:             %s\n", keyword);
    printf("Encrypted Cipher:    %s\n", ciphertext);
    printf("Decrypted Text:      %s\n", decryptedtext);

    return 0;
}
```

## OUTPUT
<img width="1872" height="964" alt="Crypto Exp-4" src="https://github.com/user-attachments/assets/9d71da63-556d-42b6-bcdf-fef4e05d4608" />



## RESULT
The program implementing the Vigenère cipher for encryption and decryption has been successfully executed, and the results have been verified.
