#include <stdio.h>
#include <stdlib.h>
#include <openssl/dsa.h>
#include <openssl/rsa.h>
#include <openssl/sha.h>

#define MESSAGE "Hello, DSA and RSA!"


void dsa_sign(DSA *dsa, const unsigned char *message, int message_len, unsigned char *signature, unsigned int *signature_len) {
    DSA_SIG *sig = DSA_do_sign(message, message_len, dsa);
    *signature_len = i2d_DSA_SIG(sig, &signature);
    DSA_SIG_free(sig);
}

void rsa_sign(RSA *rsa, const unsigned char *message, int message_len, unsigned char *signature, unsigned int *signature_len) {
    RSA_sign(NID_sha256, message, message_len, signature, signature_len, rsa);
}

void print_signature(const unsigned char *signature, unsigned int signature_len) {
    for (unsigned int i = 0; i < signature_len; i++) {
        printf("%02x", signature[i]);
    }
    printf("\n");
}

int main() {
   
    DSA *dsa = DSA_generate_parameters(1024, NULL, 0, NULL, NULL, NULL, NULL);
    DSA_generate_key(dsa);

    RSA *rsa = RSA_generate_key(1024, RSA_F4, NULL, NULL);

    unsigned char message[SHA256_DIGEST_LENGTH];
    unsigned int message_len = SHA256_DIGEST_LENGTH;
    SHA256(MESSAGE, sizeof(MESSAGE) - 1, message);

    unsigned char dsa_signature[512]; // DSA signature can be larger
    unsigned int dsa_signature_len;
    dsa_sign(dsa, message, message_len, dsa_signature, &dsa_signature_len);

    unsigned char rsa_signature[128]; // RSA signature size is fixed
    unsigned int rsa_signature_len;
    rsa_sign(rsa, message, message_len, rsa_signature, &rsa_signature_len);

    printf("DSA Signature: ");
    print_signature(dsa_signature, dsa_signature_len);

    printf("RSA Signature: ");
    print_signature(rsa_signature, rsa_signature_len);

    DSA_free(dsa);
    RSA_free(rsa);

    return 0;
}
