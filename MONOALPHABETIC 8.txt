#include <stdio.h>
#include <string.h>
#include <ctype.h>
void generateCipher(char keyword[], char cipher[]) {
    char alphabet[29] = "abcdefghijklmnopqrstuvwxyz";
    int i, j, len = strlen(keyword);
    int used[26] = {0};
    for (i = 0; i < len; i++) {
        cipher[i] = toupper(keyword[i]);
        used[tolower(keyword[i]) - 'a'] = 1;
    }
    j = 0;
    for (i = 0; i < 26; i++) {
        if (!used[i]) {
            cipher[len + j] = alphabet[i];
            j++;
        }
    }
    cipher[26] = '\0'; 
}
void encrypt(char plaintext[], char cipher[], char ciphertext[]) {
    int i, len = strlen(plaintext);
    for (i = 0; i < len; i++) {
        char c = plaintext[i];
        if (isalpha(c)) {
            if (islower(c))
                ciphertext[i] = tolower(cipher[c - 'a']);
            else
                ciphertext[i] = toupper(cipher[c - 'A']);
        } else {
            ciphertext[i] = c;
        }
    }
    ciphertext[len] = '\0'; 
}
int main() {
    char keyword[] = "CIPHER";
    char cipher[27];
    char plaintext[100];
    char ciphertext[100];
    generateCipher(keyword, cipher);
    printf("Enter the plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    encrypt(plaintext, cipher, ciphertext);
    printf("Cipher sequence: %s\n", cipher);
    printf("Encrypted text: %s\n", ciphertext);
}
