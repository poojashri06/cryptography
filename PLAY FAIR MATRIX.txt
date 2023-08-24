#include <stdio.h>
#include <string.h>

#define MATRIX_SIZE 5

void removeDuplicates(char *str) {
    int len = strlen(str);
    int index = 0;

    for (int i = 0; i < len; i++) {
        int j;
        for (j = 0; j < i; j++) {
            if (str[i] == str[j]) {
                break;
            }
        }
        if (j == i) {
            str[index++] = str[i];
        }
    }
    str[index] = '\0';
}

void fillMatrix(char matrix[MATRIX_SIZE][MATRIX_SIZE], const char *keyword) {
    char uniqueKeyword[26];
    strcpy(uniqueKeyword, keyword);
    strcat(uniqueKeyword, "ABCDEFGHIKLMNOPQRSTUVWXYZ");

    removeDuplicates(uniqueKeyword);

    int len = strlen(uniqueKeyword);

    for (int i = 0; i < MATRIX_SIZE; i++) {
        for (int j = 0; j < MATRIX_SIZE; j++) {
            matrix[i][j] = uniqueKeyword[i * MATRIX_SIZE + j];
        }
    }
}

void printMatrix(const char matrix[MATRIX_SIZE][MATRIX_SIZE]) {
    printf("Playfair Matrix:\n");
    for (int i = 0; i < MATRIX_SIZE; i++) {
        for (int j = 0; j < MATRIX_SIZE; j++) {
            printf("%c ", matrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    const char keyword[] = "MFHIJKUNOPQZVWXYELARSGDTBC";
    char playfairMatrix[MATRIX_SIZE][MATRIX_SIZE];

    fillMatrix(playfairMatrix, keyword);
    printMatrix(playfairMatrix);

    return 0;
}
