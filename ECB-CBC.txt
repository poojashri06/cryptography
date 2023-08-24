#include <stdio.h>
#include <string.h>

void aes_encrypt(char *plaintext, char *key, char *ciphertext) {
    // AES encryption logic here (implementation not included)
    strcpy(ciphertext, "AES_ENCRYPTED"); // Dummy implementation
}

void aes_decrypt(char *ciphertext, char *key, char *plaintext) {
    // AES decryption logic here (implementation not included)
    strcpy(plaintext, "AES_DECRYPTED"); // Dummy implementation
}

void simulate_bit_error(char *block, int block_size, int bit_position) {
    block[bit_position / 8] ^= (1 << (bit_position % 8));
}

int main() {
    char key[] = "SECRET_KEY123456"; // 128-bit key (16 bytes)
    char plaintext[] = "HELLO_WORLD123456"; // 128-bit plaintext (16 bytes)
    char ciphertext_ecb[17]; // 128-bit ciphertext in ECB mode (16 bytes + null terminator)
    char ciphertext_cbc[17]; // 128-bit ciphertext in CBC mode (16 bytes + null terminator)
    char decrypted_ecb[17]; // Decrypted plaintext in ECB mode (16 bytes + null terminator)
    char decrypted_cbc[17]; // Decrypted plaintext in CBC mode (16 bytes + null terminator)

    aes_encrypt(plaintext, key, ciphertext_ecb);

    char iv[] = "INITIAL_VECTOR1234"; // 128-bit IV (16 bytes)
    char previous_ciphertext[17]; // Previous ciphertext block in CBC mode (16 bytes + null terminator)
    strcpy(previous_ciphertext, iv); // Initialize the previous ciphertext block

    int bit_error_position = 7; // Bit error position (modify this to test different positions)

    simulate_bit_error(plaintext, 16, bit_error_position);

    aes_encrypt(plaintext, key, ciphertext_cbc);
    simulate_bit_error(ciphertext_cbc, 16, bit_error_position); // Simulate error in C1 block (ciphertext)

    aes_decrypt(ciphertext_ecb, key, decrypted_ecb);

    aes_decrypt(ciphertext_cbc, key, decrypted_cbc);

    printf("Original Plaintext: %s\n", plaintext);
    printf("ECB Ciphertext: %s\n", ciphertext_ecb);
    printf("CBC Ciphertext: %s\n", ciphertext_cbc);
    printf("Decrypted ECB: %s\n", decrypted_ecb);
    printf("Decrypted CBC: %s\n", decrypted_cbc);

    return 0;
}
