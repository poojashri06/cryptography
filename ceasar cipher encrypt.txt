#include <stdio.h>
#include <string.h>
void encryptCaesarCipher(char message[], int key) {
    int i;
    char ch;
    for (i = 0; message[i] != '\0'; ++i) {
        ch = message[i];
        if (ch >= 'A' && ch <= 'Z') {
            ch = ch + key;
            if (ch > 'Z') {
                ch = ch - 'Z' + 'A' - 1;
            }
            message[i] = ch;
        }
        else if (ch >= 'a' && ch <= 'z') {
            ch = ch + key;
            if (ch > 'z') {
                ch = ch - 'z' + 'a' - 1;
            }
            message[i] = ch;
        }
    }
}
int main() {
    char message[100];
    int key;
    printf("Enter a message to encrypt: ");
    fgets(message, sizeof(message), stdin);
    printf("Enter the key (0-25): ");
    scanf("%d", &key);
    encryptCaesarCipher(message, key);
	printf("Encrypted message: %s", message);
}
