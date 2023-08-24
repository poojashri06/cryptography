#include <stdio.h>
int gcd(int a, int b) {
    if (b == 0) {
        return a;
    }
    return gcd(b, a % b);
}
int main() {
    int a;
    printf("Allowed values of 'a' for the affine Caesar cipher: ");
    for (a = 1; a < 26; a++) {
        if (gcd(a, 26) == 1) {
            printf("%d ", a);
        }
    }
    printf("\n");
}
