#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_BIRDS 100
#define NAME_LENGTH 50
#define FILENAME "birds_data.txt"

// Structure to hold bird information
typedef struct {
    char name[NAME_LENGTH];
    char species[NAME_LENGTH];
    char habitat[NAME_LENGTH];
    char color[NAME_LENGTH];
    char diet[NAME_LENGTH];
    char conservationStatus[NAME_LENGTH];
    char locationFound[NAME_LENGTH];
    int wingspan; // in cm
} Bird;

// Function prototypes
void addBird(Bird birds[], int *count);
void displayBirds(Bird birds[], int count);
void searchBirdByList(Bird birds[], int count);
void editBird(Bird birds[], int count);
void deleteBird(Bird birds[], int *count);
void saveToFile(Bird birds[], int count);
void loadFromFile(Bird birds[], int *count);

int main() {
    Bird birds[MAX_BIRDS];
    int count = 0;
    int choice;

    loadFromFile(birds, &count); // Load existing data from file

    do {
        printf("\nBird Information System\n");
        printf("1. Add Bird\n");
        printf("2. Display Birds\n");
        printf("3. Search Bird by List\n");
        printf("4. Edit Bird\n");
        printf("5. Delete Bird\n");
        printf("6. Save and Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // Consume newline character

        switch (choice) {
            case 1:
                addBird(birds, &count);
                break;
            case 2:
                displayBirds(birds, count);
                break;
            case 3:
                searchBirdByList(birds, count);
                break;
            case 4:
                editBird(birds, count);
                break;
            case 5:
                deleteBird(birds, &count);
                break;
            case 6:
                saveToFile(birds, count);
                printf("Exiting the system.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 6);

    return 0;
}

// Function to add a bird
void addBird(Bird birds[], int *count) {
    if (*count >= MAX_BIRDS) {
        printf("Cannot add more birds. Maximum limit reached.\n");
        return;
    }

    printf("Enter bird name: ");
    fgets(birds[*count].name, NAME_LENGTH, stdin);
    strtok(birds[*count].name, "\n"); // Remove newline character

    printf("Enter species: ");
    fgets(birds[*count].species, NAME_LENGTH, stdin);
    strtok(birds[*count].species, "\n");

    printf("Enter habitat: ");
    fgets(birds[*count].habitat, NAME_LENGTH, stdin);
    strtok(birds[*count].habitat, "\n");

    printf("Enter color: ");
    fgets(birds[*count].color, NAME_LENGTH, stdin);
    strtok(birds[*count].color, "\n");

    printf("Enter diet: ");
    fgets(birds[*count].diet, NAME_LENGTH, stdin);
    strtok(birds[*count].diet, "\n");

    printf("Enter conservation status: ");
    fgets(birds[*count].conservationStatus, NAME_LENGTH, stdin);
    strtok(birds[*count].conservationStatus, "\n");

    printf("Enter location found: ");
    fgets(birds[*count].locationFound, NAME_LENGTH, stdin);
    strtok(birds[*count].locationFound, "\n");

    printf("Enter wingspan (in cm): ");
    scanf("%d", &birds[*count].wingspan);
    getchar(); // Consume newline character

    (*count)++;
    printf("Bird added successfully!\n");
}

// Function to display all birds
void displayBirds(Bird birds[], int count) {
    if (count == 0) {
        printf("No birds to display.\n");
        return;
    }

    printf("\nList of Birds:\n");
    for (int i = 0; i < count; i++) {
        printf("Bird %d: \n", i + 1);
        printf("  Name: %s\n", birds[i].name);
        printf("  Species: %s\n", birds[i].species);
        printf("  Habitat: %s\n", birds[i].habitat);
        printf("  Color: %s\n", birds[i].color);
        printf("  Diet: %s \n", birds[i].diet);
        printf("  Conservation Status: %s\n", birds[i].conservationStatus);
        printf("  Location Found: %s\n", birds[i].locationFound);
        printf("  Wingspan: %d cm\n", birds[i].wingspan);
    }
}

// Function to search for a bird by displaying only names
void searchBirdByList(Bird birds[], int count) {
    if (count == 0) {
        printf("No birds available to search.\n");
        return;
    }

    printf("\nList of Bird Names:\n");
    for (int i = 0; i < count; i++) {
        printf("%d. %s\n", i + 1, birds[i].name);
    }

    int index;
    printf("Enter the index of the bird to view details (1 to %d): ", count);
    scanf("%d", &index);
    getchar(); // Consume newline character

    if (index < 1 || index > count) {
        printf("Invalid index. Please try again.\n");
        return;
    }

    printf("Bird details:\n");
    printf("  Name: %s\n", birds[index - 1].name);
    printf("  Species: %s\n", birds[index - 1].species);
    printf("  Habitat: %s\n", birds[index - 1].habitat);
    printf("  Color: %s\n", birds[index - 1].color);
    printf("  Diet: %s\n", birds[index - 1].diet);
    printf("  Conservation Status: %s\n", birds[index - 1].conservationStatus);
    printf("  Location Found: %s\n", birds[index - 1].locationFound);
    printf("  Wingspan: %d cm\n", birds[index - 1].wingspan);
}

// Function to edit a bird's information
void editBird(Bird birds[], int count) {
    char name[NAME_LENGTH];
    printf("Enter the name of the bird to edit: ");
    fgets(name, NAME_LENGTH, stdin);
    strtok(name, "\n"); // Remove newline character

    for (int i = 0; i < count; i++) {
        if (strcmp(birds[i].name, name) == 0) {
            printf("Editing bird: %s\n", birds[i].name);
            printf("Enter new species: ");
            fgets(birds[i].species, NAME_LENGTH, stdin);
            strtok(birds[i].species, "\n");

            printf("Enter new habitat: ");
            fgets(birds[i].habitat, NAME_LENGTH, stdin);
            strtok(birds[i].habitat, "\n");

            printf("Enter new color: ");
            fgets(birds[i].color, NAME_LENGTH, stdin);
            strtok(birds[i].color, "\n");

            printf("Enter new diet: ");
            fgets(birds[i].diet, NAME_LENGTH, stdin);
            strtok(birds[i].diet, "\n");

            printf("Enter new conservation status: ");
            fgets(birds[i].conservationStatus, NAME_LENGTH, stdin);
            strtok(birds[i].conservationStatus, "\n");

            printf("Enter new location found: ");
            fgets(birds[i].locationFound, NAME_LENGTH, stdin);
            strtok(birds[i].locationFound, "\n");

            printf("Enter new wingspan (in cm): ");
            scanf("%d", &birds[i].wingspan);
            getchar(); // Consume newline character

            printf("Bird information updated successfully!\n");
            return;
        }
    }
    printf("Bird not found.\n");
}

// Function to delete a bird
void deleteBird(Bird birds[], int *count) {
    char name[NAME_LENGTH];
    printf("Enter the name of the bird to delete: ");
    fgets(name, NAME_LENGTH, stdin);
    strtok(name, "\n"); // Remove newline character

    for (int i = 0; i < *count; i++) {
        if (strcmp(birds[i].name, name) == 0) {
            for (int j = i; j < *count - 1; j++) {
                birds[j] = birds[j + 1]; // Shift birds down
            }
            (*count)--; // Decrease the count
            printf("Bird deleted successfully!\n");
            return;
        }
    }
    printf("Bird not found.\n");
}

// Function to save birds to a file
void saveToFile(Bird birds[], int count) {
    FILE *file = fopen(FILENAME, "w");
    if (file == NULL) {
        printf("Error opening file for writing.\n");
        return;
    }
    for (int i = 0; i < count ; i++) {
        fprintf(file, "%s\n%s\n%s\n%s\n%s\n%s\n%s\n%d\n",
                birds[i].name,
                birds[i].species,
                birds[i].habitat,
                birds[i].color,
                birds[i].diet,
                birds[i].conservationStatus,
                birds[i].locationFound,
                birds[i].wingspan);
    }
    fclose(file);
    printf("Data saved successfully!\n");
}

// Function to load birds from a file
void loadFromFile(Bird birds[], int *count) {
    FILE *file = fopen(FILENAME, "r");
    if (file == NULL) {
        printf("No existing data found. Starting fresh.\n");
        return;
    }
    while (fscanf(file, "%[^\n]\n%[^\n]\n%[^\n]\n%[^\n]\n%[^\n]\n%[^\n]\n%[^\n]\n%d\n",
                  birds[*count].name,
                  birds[*count].species,
                  birds[*count].habitat,
                  birds[*count].color,
                  birds[*count].diet,
                  birds[*count].conservationStatus,
                  birds[*count].locationFound,
                  &birds[*count].wingspan) == 8) {
        (*count)++;
    }
    fclose(file);
    printf("Data loaded successfully!\n");
}
