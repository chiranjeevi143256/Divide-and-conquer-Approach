# Divide-and-conquer-Approach

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void swap(char **a, char **b) {
    char *temp = *a;
    *a = *b;
    *b = temp;
}

int partition(char **names, int low, int high) {
    char *pivot = names[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (strcmp(names[j], pivot) < 0) {
            i++;
            swap(&names[i], &names[j]);
        }
    }

    swap(&names[i + 1], &names[high]);
    return i + 1;
}

void quicksort(char **names, int low, int high) {
    if (low < high) {
        int pi = partition(names, low, high);
        quicksort(names, low, pi - 1);
        quicksort(names, pi + 1, high);
    }
}

int main() {
    int num_names;
    printf("Enter the number of names: ");
    scanf("%d", &num_names);

    char **names = (char **)malloc(num_names * sizeof(char *));
    for (int i = 0; i < num_names; i++) {
        names[i] = (char *)malloc(100 * sizeof(char));
        printf("Enter name %d: ", i + 1);
        scanf("%s", names[i]);
    }

    quicksort(names, 0, num_names - 1);

    printf("\nSorted names:\n");
    for (int i = 0; i < num_names; i++) {
        printf("%s\n", names[i]);
    }

    for (int i = 0; i < num_names; i++) {
        free(names[i]);
    }
    free(names);

    return 0;
}
    for (int i = 0; i < num_names; i++) {
        free(names[i]);
    }
    free(names);

    return 0;
