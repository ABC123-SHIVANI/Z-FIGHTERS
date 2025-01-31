# Z-FIGHTERS
INNOTHON 2025 
#include <stdio.h>
#include <string.h>

#define MAX_CONTRACTS 100

// Structure to store contract details
typedef struct {
    int id;
    char type[50];
    char party[100];
    float value;
    char status[20];
} Contract;

Contract contracts[MAX_CONTRACTS]; // Contract database
int contract_count = 0; // Number of contracts stored

// Function to add a new contract
void add_contract() {
    if (contract_count >= MAX_CONTRACTS) {
        printf("Contract database is full!\n");
        return;
    }

    Contract c;
    printf("Enter Contract ID: ");
    scanf("%d", &c.id);
    getchar(); // Consume newline character

    printf("Enter Contract Type (e.g., Provider, Insurance): ");
    fgets(c.type, sizeof(c.type), stdin);
    c.type[strcspn(c.type, "\n")] = 0; // Remove newline

    printf("Enter Party Name: ");
    fgets(c.party, sizeof(c.party), stdin);
    c.party[strcspn(c.party, "\n")] = 0;

    printf("Enter Contract Value ($): ");
    scanf("%f", &c.value);
    getchar();

    printf("Enter Status (Active/Pending/Expired): ");
    fgets(c.status, sizeof(c.status), stdin);
    c.status[strcspn(c.status, "\n")] = 0;

    contracts[contract_count++] = c;
    printf("Contract added successfully!\n");
}

// Function to display all contracts
void view_contracts() {
    if (contract_count == 0) {
        printf("No contracts available.\n");
        return;
    }

    printf("\n%-5s %-20s %-30s %-10s %-10s\n", "ID", "Type", "Party", "Value($)", "Status");
    printf("--------------------------------------------------------------\n");

    for (int i = 0; i < contract_count; i++) {
        printf("%-5d %-20s %-30s %-10.2f %-10s\n",
               contracts[i].id, contracts[i].type, contracts[i].party,
               contracts[i].value, contracts[i].status);
    }
}

// Function to search for a contract by ID
void search_contract() {
    int search_id;
    printf("Enter Contract ID to search: ");
    scanf("%d", &search_id);

    for (int i = 0; i < contract_count; i++) {
        if (contracts[i].id == search_id) {
            printf("\nContract Found:\n");
            printf("ID: %d\nType: %s\nParty: %s\nValue: $%.2f\nStatus: %s\n",
                   contracts[i].id, contracts[i].type, contracts[i].party,
                   contracts[i].value, contracts[i].status);
            return;
        }
    }
    printf("Contract not found.\n");
}

// Main function to run the program
int main() {
    int choice;
    while (1) {
        printf("\nHealthcare Contract Management System\n");
        printf("1. Add Contract\n2. View Contracts\n3. Search Contract\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // Consume newline character

        switch (choice) {
            case 1:
                add_contract();
                break;
            case 2:
                view_contracts();
                break;
            case 3:
                search_contract();
                break;
            case 4:
                printf("Exiting system...\n");
                return 0;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }
}
