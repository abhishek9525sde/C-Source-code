# C-Source-code
Laptop repair system


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
// Define structures for client, laptop, and expert
typedef struct {
    int id;
    char name[70];
    char address[100];
    char phone[20];
} client;

typedef struct {
    int id;
    char brand[50];
    char model[50];
    char problem[100];
    char status[20];
    int expert_id;
} laptop;

typedef struct {
    int id;
    char name[50];
    char expertise[50];
} expert;

// Define global arrays for storing records
client clients[100];
int num_clients = 0;
laptop laptops[100];
int num_laptops = 0;
expert experts[10] = {{1, "Aditya", "Hardware"}, {2, "Arus", "Software"}};
int num_experts = 2;

// Function to add a new client record
void add_client() {
    printf("Enter client name: ");
    scanf("%s", clients[num_clients].name);
    printf("Enter client address: ");
    scanf("%s", clients[num_clients].address);
    printf("Enter client phone number: ");
    scanf("%s", clients[num_clients].phone);
    clients[num_clients].id = num_clients + 1;
    num_clients++;
    printf("Client's Id : %d\n\n",num_clients);
    printf("Client record added successfully!\n\n");
}

// Function to add a new laptop record
void add_laptop() {
    printf("Enter laptop brand: ");
    scanf("%s", laptops[num_laptops].brand);
    printf("Enter laptop model: ");
    scanf("%s", laptops[num_laptops].model);
    printf("Enter laptop problem: ");
    scanf("%s", laptops[num_laptops].problem);
    laptops[num_laptops].status[0] = 'N'; // N = not repaired
    laptops[num_laptops].status[1] = '\0';
    laptops[num_laptops].id = num_laptops + 1;
    num_laptops++;
    printf("Laptop record added successfully!\n\n\n");
}

// Function to display all client records
void display_clients() {
    printf("\nClient records:");
    printf("\nID\tName\t\tAddress\t\tPhone\n");
    for (int i = 0; i < num_clients; i++) {
        printf("%d\t%s\t\t%s\t\t%s\n", clients[i].id, clients[i].name, clients[i].address, clients[i].phone);
    }
}

// Function to display all laptop records
void display_laptops() {
    printf("\nLaptop records: ");
    printf("\nID\tBrand\tModel\tProblem\t\tStatus\tExpert ID\n\n");
    for (int i = 0; i < num_laptops; i++) {
        printf("%d\t%s\t%s\t%s\t%s\t%d\n", laptops[i].id, laptops[i].brand, laptops[i].model, laptops[i].problem, laptops[i].status, laptops[i].expert_id);
    }
}

// Function to update a client record
void update_client(int id) {
	printf("Enter previous client Id");
	scanf("%d",&id);
    for (int i = 0; i < num_clients; i++) {
        if (clients[i].id == id) {
            printf("\nEnter new client name: ");
            scanf("%s", clients[i].name);
            printf("Enter new client address: ");
            scanf("%s", clients[i].address);
            printf("Enter new client phone number: ");
            scanf("%s", clients[i].phone);
            printf("Client record updated successfully!\n\n\n");
            return;
        }
    }
    printf("Client record not found!\n");
}

// Function to delete a client record
void delete_client(int id) {
	printf("Enter client's Id : ");
	scanf("%d",&id);
    for (int i = 0; i < num_clients; i++) {
        if (clients[i].id == id) {
            // Shift all records after the deleted one one position to the left
            for (int j = i; j < num_clients - 1; j++) {
                clients[j] = clients[j + 1];
            }
            num_clients--;
            printf("\nClient record deleted successfully!\n\n\n");
            return;
        }
    }
    printf("\nClient record not found!\n\n\n");
}

// Function to update a laptop record
void update_laptop(int id) {
	printf("Enter laptop's Id :");
	scanf("%d",&id);
    for (int i = 0; i < num_laptops; i++) {
        if (laptops[i].id == id) {
            printf("Enter new laptop brand: ");
            scanf("%s", laptops[i].brand);
            printf("Enter new laptop model: ");
            scanf("%s", laptops[i].model);
            printf("Enter new laptop problem: ");
            scanf("%s", laptops[i].problem);
            printf("Laptop record updated successfully!\n\n\n");
            return;
        }
    }
    printf("\nLaptop record not found!\n\n\n");
}

// Function to delete a laptop record
void delete_laptop(int id) {
	printf("Enter laptop's Id : ");
	scanf("%d",&id);
    for (int i = 0; i < num_laptops; i++) {
        if (laptops[i].id == id) {
            // Shift all records after the deleted one one position to the left
            for (int j = i; j < num_laptops - 1; j++) {
                laptops[j] = laptops[j + 1];
            }
            num_laptops--;
            printf("\nLaptop record deleted successfully!\n\n\n");
            return;
        }
    }
    printf("\nLaptop record not found!\n\n\n");
}

// Function to display all expert records
void display_experts() {
    printf("\nExpert records:\n");
    printf("ID\tName\tExpertise\n");
    for (int i = 0; i < num_experts; i++) {
        printf("%d\t%s\t%s\n\n\n", experts[i].id, experts[i].name, experts[i].expertise);
    }
}

// Function to assign an expert to a laptop
void assign_expert(int laptop_id, int expert_id) {
	printf("\nEnter laptop's Id : ");
	scanf("%d",&laptop_id);
	printf("\nEnter expert Id : ");
	scanf("%d",&expert_id);
    for (int i = 0; i < num_laptops; i++) {
        if (laptops[i].id == laptop_id) {
            laptops[i].expert_id = expert_id;
            laptops[i].status[0] = 'R'; // R = repaired
            printf("\nExpert assigned successfully!\n\n\n");
            return;
        }
    }
    printf("\nLaptop record not found!\n\n\n");
}
int main() 
{
    int choice;
    int id,i;
    int laptop_id;
    int expert_id;
    char input;
    char ch;

    doit:
        printf("Laptop Repair System\n");
        printf("1. Add client record\n");
        printf("2. Add laptop record\n");
        printf("3. Update client record\n");
        printf("4. Delete client record\n");
        printf("5. Update laptop record\n");
        printf("6. Delete laptop record\n");
        printf("7. Display expert records\n");
        printf("8. Assign expert to laptop\n");
        printf("9. Display client records\n");
        printf("10. Display laptop records\n");
        printf("11. Exit\n\n\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                add_client();
                break;
            case 2:
                add_laptop();
                break;
            case 3:
            	update_client( id);
            	break;
            case 4 :
            	delete_client(id);
				break;
			case 5:
				update_laptop(id);
				break;
			case 6:
				delete_laptop(id);
				break;
			case 7:
				display_experts();
				break;
			case 8:
				assign_expert( laptop_id,  expert_id);
				break;
			case 9:
				display_clients() ;
				break;
			case 10:
				display_laptops();
				break;
			case 11:
				printf("\nStay happy ! \n\n");	
				break;
			
			default:
			
			printf("\nInvalid Input\n \n ");
		}
	
	
	printf("\nDo you want to do another operation (y/n): ");
	fflush(stdin);
	scanf("%c",&ch);
	
	if (ch=='y' || ch=='Y')
	goto doit;
	
}
