#include <stdio.h>
#include <string.h>

#define MAX 100

struct Book {
    int id;
    char name[50];
    char author[50];
    int quantity;
};

struct Book library[MAX];
int count = 0;

// Function declarations
void addBook();
void displayBooks();
void searchBook();
void issueBook();
void returnBook();
void deleteBook();

int main() {
    int choice;

    do {
        printf("\n===== Library Management System =====\n");
        printf("1. Add Book\n");
        printf("2. Display All Books\n");
        printf("3. Search Book\n");
        printf("4. Issue Book\n");
        printf("5. Return Book\n");
        printf("6. Delete Book\n");
        printf("7. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1: addBook(); break;
            case 2: displayBooks(); break;
            case 3: searchBook(); break;
            case 4: issueBook(); break;
            case 5: returnBook(); break;
            case 6: deleteBook(); break;
            case 7: printf("Exiting program...\n"); break;
            default: printf("Invalid choice!\n");
        }
    } while(choice != 7);

    return 0;
}

// Add Book
void addBook() {
    if(count >= MAX) {
        printf("Library is full!\n");
        return;
    }

    printf("Enter Book ID: ");
    scanf("%d", &library[count].id);

    printf("Enter Book Name: ");
    scanf(" %[^\n]", library[count].name);

    printf("Enter Author Name: ");
    scanf(" %[^\n]", library[count].author);

    printf("Enter Quantity: ");
    scanf("%d", &library[count].quantity);

    count++;
    printf("Book added successfully!\n");
}

// Display Books
void displayBooks() {
    if(count == 0) {
        printf("No books available.\n");
        return;
    }

    printf("\nID\tName\t\tAuthor\t\tQuantity\n");
    for(int i = 0; i < count; i++) {
        printf("%d\t%s\t\t%s\t\t%d\n",
               library[i].id,
               library[i].name,
               library[i].author,
               library[i].quantity);
    }
}

// Search Book
void searchBook() {
    int id, found = 0;
    printf("Enter Book ID to search: ");
    scanf("%d", &id);

    for(int i = 0; i < count; i++) {
        if(library[i].id == id) {
            printf("Book Found!\n");
            printf("Name: %s\nAuthor: %s\nQuantity: %d\n",
                   library[i].name,
                   library[i].author,
                   library[i].quantity);
            found = 1;
            break;
        }
    }

    if(!found)
        printf("Book not found!\n");
}

// Issue Book
void issueBook() {
    int id;
    printf("Enter Book ID to issue: ");
    scanf("%d", &id);

    for(int i = 0; i < count; i++) {
        if(library[i].id == id) {
            if(library[i].quantity > 0) {
                library[i].quantity--;
                printf("Book issued successfully!\n");
            } else {
                printf("Book not available!\n");
            }
            return;
        }
    }
    printf("Book not found!\n");
}

// Return Book
void returnBook() {
    int id;
    printf("Enter Book ID to return: ");
    scanf("%d", &id);

    for(int i = 0; i < count; i++) {
        if(library[i].id == id) {
            library[i].quantity++;
            printf("Book returned successfully!\n");
            return;
        }
    }
    printf("Book not found!\n");
}

// Delete Book
void deleteBook() {
    int id, found = 0;
    printf("Enter Book ID to delete: ");
    scanf("%d", &id);

    for(int i = 0; i < count; i++) {
        if(library[i].id == id) {
            for(int j = i; j < count - 1; j++) {
                library[j] = library[j + 1];
            }
            count--;
            found = 1;
            printf("Book deleted successfully!\n");
            break;
        }
    }

    if(!found)
        printf("Book not found!\n");
}

