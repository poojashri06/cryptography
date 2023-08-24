#include <stdio.h>
#include <stdlib.h>
#include <math.h>
unsigned long long mod_exp(unsigned long long base, unsigned long long exp, unsigned long long modulus) {
    unsigned long long result = 1;
    base %= modulus;
    while (exp > 0) {
        if (exp & 1) {
            result = (result * base) % modulus;
        }
        base = (base * base) % modulus;
        exp >>= 1;
    }
    return result;
}

int main() {
    unsigned long long q, a, xA, xB, YA, YB, K1, K2;
    q = 23;
    a = 5;  

  
    xA = 4; // Alice's secret number
    xB = 3; // Bob's secret number

    YA = mod_exp(a, xA, q); // Alice sends YA to Bob
    YB = mod_exp(a, xB, q); // Bob sends YB to Alice

    K1 = mod_exp(YB, xA, q); // Alice calculates the shared secret key
    K2 = mod_exp(YA, xB, q); // Bob calculates the shared secret key

    printf("Shared secret key for Alice: %llu\n", K1);
    printf("Shared secret key for Bob: %llu\n", K2);

    return 0;
}
