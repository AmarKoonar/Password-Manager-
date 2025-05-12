#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/sha.h>
#include <sys/stat.h>

#define MAX_PASSWORD_LEN 128
#define HASH_FILE "master.hash"

// ==================== Utilities ====================

void print_banner() {
    printf("====================================\n");
    printf("      C Password Manager \n");
    printf("====================================\n");
    printf("Store your passwords securely.\n\n");
}

int file_exists(const char *filename) {
    struct stat buffer;
    return (stat(filename, &buffer) == 0);
}

void prompt_password(char *buffer, size_t size, const char *msg) {
    printf("%s", msg);
    if (fgets(buffer, size, stdin) == NULL) {
        fprintf(stderr, "Error reading input.\n");
        exit(1);
    }

    size_t len = strlen(buffer);
    if (len > 0 && buffer[len - 1] == '\n') buffer[len - 1] = '\0';
}

void sha256_string(const char *str, unsigned char hash[SHA256_DIGEST_LENGTH]) {
    SHA256((const unsigned char *)str, strlen(str), hash);
}

int compare_hashes(unsigned char *a, unsigned char *b) {
    return memcmp(a, b, SHA256_DIGEST_LENGTH) == 0;
}

void print_hex(unsigned char hash[SHA256_DIGEST_LENGTH]) {
    for (int i = 0; i < SHA256_DIGEST_LENGTH; i++) {
        printf("%02x", hash[i]);
    }
    printf("\n");
}

// ==================== Main Logic ====================

int main() {
    char password[MAX_PASSWORD_LEN];
    unsigned char hash[SHA256_DIGEST_LENGTH];

    print_banner();

    if (!file_exists(HASH_FILE)) {
        prompt_password(password, sizeof(password), "No master password set. Please create one: ");
        sha256_string(password, hash);

        FILE *fp = fopen(HASH_FILE, "wb");
        if (!fp) {
            perror("Failed to save hash");
            exit(1);
        }
        fwrite(hash, 1, SHA256_DIGEST_LENGTH, fp);
        fclose(fp);

        printf("[✔] Master password set successfully.\n");
    } else {
        FILE *fp = fopen(HASH_FILE, "rb");
        if (!fp) {
            perror("Failed to open hash file");
            exit(1);
        }

        unsigned char stored_hash[SHA256_DIGEST_LENGTH];
        fread(stored_hash, 1, SHA256_DIGEST_LENGTH, fp);
        fclose(fp);

        prompt_password(password, sizeof(password), "Enter Master Password: ");
        sha256_string(password, hash);

        if (compare_hashes(stored_hash, hash)) {
            printf("[✔] Access granted.\n");
        } else {
            printf("[✘] Incorrect password. Access denied.\n");
            exit(1);
        }
    }

    // 🔐 Continue to vault logic...
    return 0;
}
