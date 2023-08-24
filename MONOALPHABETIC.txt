#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

char encryptChar(char ch, char* key) {
    if (isalpha(ch)) {
        char base = islower(ch) ? 'a' : 'A';
        return key[ch - base];
    }
    return ch;
}

int main() {
    char plaintext[] = "This is a simple substitution cipher example.";
    char key[] = "ZYXWVUTSRQPONMLKJIHGFEDCBAzyxwvutsrqponmlkjihgfedcba";
    char ciphertext[sizeof(plaintext)];

    for (int i = 0; plaintext[i]; i++) {
        ciphertext[i] = encryptChar(plaintext[i], key);
    }
    ciphertext[sizeof(plaintext) - 1] = '\0';

    printf("Plaintext: %s\n", plaintext);
    printf("Ciphertext: %s\n", ciphertext);

    return 0;
}
