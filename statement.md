#include <stdio.h>
#include <math.h>

#define SIZE 4

int grid[SIZE][SIZE] = {0};
int rowTarget[SIZE] = {5, 9, 6, 10};   // Example targets
int colTarget[SIZE] = {7, 8, 5, 10};

// Convert binary row to decimal
int binaryToDecimalRow(int row[]) {
    int decimal = 0;
    for (int i = 0; i < SIZE; i++) {
        decimal += row[i] * pow(2, SIZE - i - 1);
    }
    return decimal;
}

// Convert binary column to decimal
int binaryToDecimalCol(int colIndex) {
    int decimal = 0;
    for (int i = 0; i < SIZE; i++) {
        decimal += grid[i][colIndex] * pow(2, SIZE - i - 1);
    }
    return decimal;
}

// Display board
void displayGrid() {
    printf("\nCurrent Grid:\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%d ", grid[i][j]);
        }
        printf("| %d\n", rowTarget[i]);
    }

    printf("-----------------\n");

    for (int j = 0; j < SIZE; j++) {
        printf("%d ", colTarget[j]);
    }
    printf("\n");
}

// Check if puzzle solved
int checkWin() {
    for (int i = 0; i < SIZE; i++) {
        if (binaryToDecimalRow(grid[i]) != rowTarget[i])
            return 0;
    }

    for (int j = 0; j < SIZE; j++) {
        if (binaryToDecimalCol(j) != colTarget[j])
            return 0;
    }

    return 1;
}

int main() {
    int row, col, value;

    printf("=== ZERO ONE QUEST ===\n");
    printf("Fill grid with 0 or 1\n");

    while (1) {
        displayGrid();

        printf("\nEnter row (0-%d), column (0-%d), value (0/1): ", SIZE-1, SIZE-1);
        scanf("%d %d %d", &row, &col, &value);

        if (row < 0 || row >= SIZE || col < 0 || col >= SIZE || (value != 0 && value != 1)) {
            printf("Invalid input! Try again.\n");
            continue;
        }

        grid[row][col] = value;

        if (checkWin()) {
            displayGrid();
            printf("\n🎉 Congratulations! You solved the puzzle!\n");
            break;
        }
    }

    return 0;
}
