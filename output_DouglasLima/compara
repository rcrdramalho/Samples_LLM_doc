#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LINE_LENGTH 1024

int main(int argc, char *argv[]) {
    if (argc != 3) {
        fprintf(stderr, "Usage: %s <file1> <file2>\n", argv[0]);
        return 1;
    }

    FILE *file1 = fopen(argv[1], "r");
    FILE *file2 = fopen(argv[2], "r");

    if (!file1 || !file2) {
        perror("Error opening files");
        return 1;
    }

    char line1[MAX_LINE_LENGTH];
    char line2[MAX_LINE_LENGTH];
    int line_number = 1;
    int differences_found = 0;

    while (fgets(line1, MAX_LINE_LENGTH, file1) && fgets(line2, MAX_LINE_LENGTH, file2)) {
        // Remove newline characters for cleaner comparison
        line1[strcspn(line1, "\n")] = 0;
        line2[strcspn(line2, "\n")] = 0;

        if (strcmp(line1, line2) != 0) {
            printf("Difference at line %d:\n", line_number);
            printf("File1: %s\n", line1);
            printf("File2: %s\n\n", line2);
            differences_found = 1;
        }

        line_number++;
    }

    // Check if one file has extra lines
    while (fgets(line1, MAX_LINE_LENGTH, file1)) {
        line1[strcspn(line1, "\n")] = 0;
        printf("Extra line in %s at line %d:\n%s\n\n", argv[1], line_number, line1);
        line_number++;
        differences_found = 1;
    }

    while (fgets(line2, MAX_LINE_LENGTH, file2)) {
        line2[strcspn(line2, "\n")] = 0;
        printf("Extra line in %s at line %d:\n%s\n\n", argv[2], line_number, line2);
        line_number++;
        differences_found = 1;
    }

    if (!differences_found) {
        printf("The files are identical.\n");
    }

    fclose(file1);
    fclose(file2);
    return 0;
}
