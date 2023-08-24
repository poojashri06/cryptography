#include <stdio.h>

void bitwise_xor(char *a, char *b, int n) {
    for (int i = 0; i < n; i++) {
        if (a[i] == b[i]) {
            a[i] = '0';
        } else {
            a[i] = '1';
        }
    }
}

void sdes_encrypt(char *plaintext, char *key) {
    int n = 8; // Number of bits in the plaintext and key
    bitwise_xor(plaintext, key, n);
}

void sdes_decrypt(char *ciphertext, char *key) {

    int n = 8; // Number of bits in the ciphertext and key
    bitwise_xor(ciphertext, key, n);
}

int main() {
    char plaintext[] = "0000000100100011"; 
    char key[] = "0111111101"; 
    char iv[] = "10101010"; 

    printf("Plaintext: %s\n", plaintext);

    int n = 16; // Total number of bits in the plaintext (two blocks)
    for (int i = 0; i < n; i += 8) {
        char block[9]; // 8 bits for each block, plus 1 for null terminator
        for (int j = 0; j < 8; j++) {
            block[j] = plaintext[i + j];
        }
        block[8] = '\0';
        if (i == 0) {

            bitwise_xor(block, iv, 8);
        } else {

            bitwise_xor(block, plaintext + i - 8, 8);
        }


        sdes_encrypt(block, key);


        printf("Ciphertext: %s\n", block);


        for (int j = 0; j < 8; j++) {
            plaintext[i + j] = block[j];
        }
    }


    for (int i = 0; i < n; i += 8) {
        char block[9]; // 8 bits for each block, plus 1 for null terminator
        for (int j = 0; j < 8; j++) {
            block[j] = plaintext[i + j];
        }
        block[8] = '\0';


        sdes_decrypt(block, key);


        if (i != 0) {
            bitwise_xor(block, plaintext + i - 8, 8);
        }

        printf("Decrypted: %s\n", block);

        for (int j = 0; j < 8; j++) {
            plaintext[i + j] = block[j];
        }
    }

    return 0;
}
