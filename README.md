# DSL-7
// Practical No -07
// Problem Statement: Department of Computer Engineering has student's club named 'Pinnacle Club'. Students of second, third and final year of department can be granted membership on request. Similarly one may cancel the membership of club. First node is reserved for president of club and last node is reserved for secretary of club. Write C++ program to maintain club member‘s information using singly linked list. Store student PRN and Name. Write functions to:
// a) Add and delete the members as well as president or even secretary.
// b) Compute total number of members of club 
// c) Display members 
// d) Two linked lists exists for two divisions. Concatenate two lists.
// Program:-
#include <iostream>
#include <string>
using namespace std;

// Node structure
struct Node {
    int prn;
    string name;
    Node* next;
};

// Linked list class
class ClubList {
    Node* head;

public:
    ClubList() {
        head = nullptr;
    }

    // Function to create a new node
    Node* createNode(int prn, string name) {
        Node* newNode = new Node;
        if (!newNode) {
            cout << "Memory allocation failed!" << endl;
            return nullptr;
        }
        newNode->prn = prn;
        newNode->name = name;
        newNode->next = nullptr;
        return newNode;
    }

    // Function to add a member at the end (Secretary)
    void addMemberEnd() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        if (!head) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "Member added!" << endl;
    }

    // Function to add a member at the beginning (President)
    void addMemberBeginning() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        newNode->next = head;
        head = newNode;
        cout << "New President added!" << endl;
    }

    // Function to delete a member at a specific position
    void deleteMember(int pos) {
        if (pos == 1) {
            if (head) {
                Node* temp = head;
                head = head->next;
                delete temp;
                cout << "President deleted!" << endl;
            } else {
                cout << "No members to delete!" << endl;
            }
        } else {
            Node* temp = head;
            int count = 1;
            while (temp && count < pos - 1) {
                temp = temp->next;
                count++;
            }
            if (temp && temp->next) {
                Node* deleteNode = temp->next;
                temp->next = temp->next->next;
                delete deleteNode;
                cout << "Member at position " << pos << " deleted!" << endl;
            } else {
                cout << "Position out of range!" << endl;
            }
        }
    }

    // Function to display the members
    void displayMembers() {
        if (!head) {
            cout << "No members in the club!" << endl;
            return;
        }
        Node* temp = head;
        cout << "President: " << temp->prn << " - " << temp->name << endl;
        temp = temp->next;
        while (temp) {
            cout << "Member: " << temp->prn << " - " << temp->name << endl;
            temp = temp->next;
        }
    }

    // Function to count the total number of members
    int countMembers() {
        int count = 0;
        Node* temp = head;
        while (temp) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    // Function to concatenate two lists
    void concatenate(ClubList& listB) {
        if (!head) {
            head = listB.head;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = listB.head;
        }
        listB.head = nullptr;
        cout << "Lists concatenated!" << endl;
    }
};

// Main function
int main() {
    ClubList listA, listB;
    int choice;
    
    while (true) {
        cout << "\nEnter your choice:\n1. Add member to List A\n2. Add member to List B\n3. Concatenate Lists\n4. Display List A\n5. Display List B\n6. Delete member from List A\n7. Delete member from List B\n8. Count members in List A\n9. Count members in List B\n0. Exit" << endl;
        cin >> choice;

        switch (choice) {
            case 1: {
                listA.addMemberEnd();
                break;
            }
            case 2: {
                listB.addMemberEnd();
                break;
            }
            case 3: {
                listA.concatenate(listB);
                break;
            }
            case 4: {
                listA.displayMembers();
                break;
            }
            case 5: {
                listB.displayMembers();
                break;
            }
            case 6: {
                int pos;
                cout << "Enter position to delete in List A: ";
                cin >> pos;
                listA.deleteMember(pos);
                break;
            }
            case 7: {
                int pos;
                cout << "Enter position to delete in List B: ";
                cin >> pos;
                listB.deleteMember(pos);
                break;
            }
            case 8: {
                cout << "Total members in List A: " << listA.countMembers() << endl;
                break;
            }
            case 9: {
                cout << "Total members in List B: " << listB.countMembers() << endl;
                break;
            }
            case 0: {
                cout << "Exiting program..." << endl;
                return 0;
            }
            default: {
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
}
// Output:
// Enter: 
// 1. List A 
// 2. List B 
// 3. Concatenate
// 0. Exit
// 1

// List A:
// Enter: 
// 1. Add 
// 2. Delete 
// 3. Member's Count 
// 4. Display 
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// a
// Enter PRN: 12345
// Enter Name: abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 2

// Enter:
// A. Delete President
// B. Delete Secretary
// C. Delete Member
// a

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 3
// Count: 1

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 4
// President: 12345 ΓÇö abcd -> Secretary: 12345 ΓÇö abcd -> NULL

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 12345 ΓÇö abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 2

// List B:
// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// b
// Enter PRN: 34567
// Enter Name: defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 34567 ΓÇö defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 3
// President: 12345 ΓÇö abcd -> Secretary: 34567 ΓÇö defg -> NULL
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit

// Practical No -07
// Problem Statement: Department of Computer Engineering has student's club named 'Pinnacle Club'. Students of second, third and final year of department can be granted membership on request. Similarly one may cancel the membership of club. First node is reserved for president of club and last node is reserved for secretary of club. Write C++ program to maintain club member‘s information using singly linked list. Store student PRN and Name. Write functions to:
// a) Add and delete the members as well as president or even secretary.
// b) Compute total number of members of club 
// c) Display members 
// d) Two linked lists exists for two divisions. Concatenate two lists.
// Program:-
#include <iostream>
#include <string>
using namespace std;

// Node structure
struct Node {
    int prn;
    string name;
    Node* next;
};

// Linked list class
class ClubList {
    Node* head;

public:
    ClubList() {
        head = nullptr;
    }

    // Function to create a new node
    Node* createNode(int prn, string name) {
        Node* newNode = new Node;
        if (!newNode) {
            cout << "Memory allocation failed!" << endl;
            return nullptr;
        }
        newNode->prn = prn;
        newNode->name = name;
        newNode->next = nullptr;
        return newNode;
    }

    // Function to add a member at the end (Secretary)
    void addMemberEnd() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        if (!head) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "Member added!" << endl;
    }

    // Function to add a member at the beginning (President)
    void addMemberBeginning() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        newNode->next = head;
        head = newNode;
        cout << "New President added!" << endl;
    }

    // Function to delete a member at a specific position
    void deleteMember(int pos) {
        if (pos == 1) {
            if (head) {
                Node* temp = head;
                head = head->next;
                delete temp;
                cout << "President deleted!" << endl;
            } else {
                cout << "No members to delete!" << endl;
            }
        } else {
            Node* temp = head;
            int count = 1;
            while (temp && count < pos - 1) {
                temp = temp->next;
                count++;
            }
            if (temp && temp->next) {
                Node* deleteNode = temp->next;
                temp->next = temp->next->next;
                delete deleteNode;
                cout << "Member at position " << pos << " deleted!" << endl;
            } else {
                cout << "Position out of range!" << endl;
            }
        }
    }

    // Function to display the members
    void displayMembers() {
        if (!head) {
            cout << "No members in the club!" << endl;
            return;
        }
        Node* temp = head;
        cout << "President: " << temp->prn << " - " << temp->name << endl;
        temp = temp->next;
        while (temp) {
            cout << "Member: " << temp->prn << " - " << temp->name << endl;
            temp = temp->next;
        }
    }

    // Function to count the total number of members
    int countMembers() {
        int count = 0;
        Node* temp = head;
        while (temp) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    // Function to concatenate two lists
    void concatenate(ClubList& listB) {
        if (!head) {
            head = listB.head;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = listB.head;
        }
        listB.head = nullptr;
        cout << "Lists concatenated!" << endl;
    }
};

// Main function
int main() {
    ClubList listA, listB;
    int choice;
    
    while (true) {
        cout << "\nEnter your choice:\n1. Add member to List A\n2. Add member to List B\n3. Concatenate Lists\n4. Display List A\n5. Display List B\n6. Delete member from List A\n7. Delete member from List B\n8. Count members in List A\n9. Count members in List B\n0. Exit" << endl;
        cin >> choice;

        switch (choice) {
            case 1: {
                listA.addMemberEnd();
                break;
            }
            case 2: {
                listB.addMemberEnd();
                break;
            }
            case 3: {
                listA.concatenate(listB);
                break;
            }
            case 4: {
                listA.displayMembers();
                break;
            }
            case 5: {
                listB.displayMembers();
                break;
            }
            case 6: {
                int pos;
                cout << "Enter position to delete in List A: ";
                cin >> pos;
                listA.deleteMember(pos);
                break;
            }
            case 7: {
                int pos;
                cout << "Enter position to delete in List B: ";
                cin >> pos;
                listB.deleteMember(pos);
                break;
            }
            case 8: {
                cout << "Total members in List A: " << listA.countMembers() << endl;
                break;
            }
            case 9: {
                cout << "Total members in List B: " << listB.countMembers() << endl;
                break;
            }
            case 0: {
                cout << "Exiting program..." << endl;
                return 0;
            }
            default: {
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
}
// Output:
// Enter: 
// 1. List A 
// 2. List B 
// 3. Concatenate
// 0. Exit
// 1

// List A:
// Enter: 
// 1. Add 
// 2. Delete 
// 3. Member's Count 
// 4. Display 
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// a
// Enter PRN: 12345
// Enter Name: abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 2

// Enter:
// A. Delete President
// B. Delete Secretary
// C. Delete Member
// a

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 3
// Count: 1

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 4
// President: 12345 ΓÇö abcd -> Secretary: 12345 ΓÇö abcd -> NULL

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 12345 ΓÇö abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 2

// List B:
// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// b
// Enter PRN: 34567
// Enter Name: defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 34567 ΓÇö defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 3
// President: 12345 ΓÇö abcd -> Secretary: 34567 ΓÇö defg -> NULL
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit

// Practical No -07
// Problem Statement: Department of Computer Engineering has student's club named 'Pinnacle Club'. Students of second, third and final year of department can be granted membership on request. Similarly one may cancel the membership of club. First node is reserved for president of club and last node is reserved for secretary of club. Write C++ program to maintain club member‘s information using singly linked list. Store student PRN and Name. Write functions to:
// a) Add and delete the members as well as president or even secretary.
// b) Compute total number of members of club 
// c) Display members 
// d) Two linked lists exists for two divisions. Concatenate two lists.
// Program:-
#include <iostream>
#include <string>
using namespace std;

// Node structure
struct Node {
    int prn;
    string name;
    Node* next;
};

// Linked list class
class ClubList {
    Node* head;

public:
    ClubList() {
        head = nullptr;
    }

    // Function to create a new node
    Node* createNode(int prn, string name) {
        Node* newNode = new Node;
        if (!newNode) {
            cout << "Memory allocation failed!" << endl;
            return nullptr;
        }
        newNode->prn = prn;
        newNode->name = name;
        newNode->next = nullptr;
        return newNode;
    }

    // Function to add a member at the end (Secretary)
    void addMemberEnd() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        if (!head) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "Member added!" << endl;
    }

    // Function to add a member at the beginning (President)
    void addMemberBeginning() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        newNode->next = head;
        head = newNode;
        cout << "New President added!" << endl;
    }

    // Function to delete a member at a specific position
    void deleteMember(int pos) {
        if (pos == 1) {
            if (head) {
                Node* temp = head;
                head = head->next;
                delete temp;
                cout << "President deleted!" << endl;
            } else {
                cout << "No members to delete!" << endl;
            }
        } else {
            Node* temp = head;
            int count = 1;
            while (temp && count < pos - 1) {
                temp = temp->next;
                count++;
            }
            if (temp && temp->next) {
                Node* deleteNode = temp->next;
                temp->next = temp->next->next;
                delete deleteNode;
                cout << "Member at position " << pos << " deleted!" << endl;
            } else {
                cout << "Position out of range!" << endl;
            }
        }
    }

    // Function to display the members
    void displayMembers() {
        if (!head) {
            cout << "No members in the club!" << endl;
            return;
        }
        Node* temp = head;
        cout << "President: " << temp->prn << " - " << temp->name << endl;
        temp = temp->next;
        while (temp) {
            cout << "Member: " << temp->prn << " - " << temp->name << endl;
            temp = temp->next;
        }
    }

    // Function to count the total number of members
    int countMembers() {
        int count = 0;
        Node* temp = head;
        while (temp) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    // Function to concatenate two lists
    void concatenate(ClubList& listB) {
        if (!head) {
            head = listB.head;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = listB.head;
        }
        listB.head = nullptr;
        cout << "Lists concatenated!" << endl;
    }
};

// Main function
int main() {
    ClubList listA, listB;
    int choice;
    
    while (true) {
        cout << "\nEnter your choice:\n1. Add member to List A\n2. Add member to List B\n3. Concatenate Lists\n4. Display List A\n5. Display List B\n6. Delete member from List A\n7. Delete member from List B\n8. Count members in List A\n9. Count members in List B\n0. Exit" << endl;
        cin >> choice;

        switch (choice) {
            case 1: {
                listA.addMemberEnd();
                break;
            }
            case 2: {
                listB.addMemberEnd();
                break;
            }
            case 3: {
                listA.concatenate(listB);
                break;
            }
            case 4: {
                listA.displayMembers();
                break;
            }
            case 5: {
                listB.displayMembers();
                break;
            }
            case 6: {
                int pos;
                cout << "Enter position to delete in List A: ";
                cin >> pos;
                listA.deleteMember(pos);
                break;
            }
            case 7: {
                int pos;
                cout << "Enter position to delete in List B: ";
                cin >> pos;
                listB.deleteMember(pos);
                break;
            }
            case 8: {
                cout << "Total members in List A: " << listA.countMembers() << endl;
                break;
            }
            case 9: {
                cout << "Total members in List B: " << listB.countMembers() << endl;
                break;
            }
            case 0: {
                cout << "Exiting program..." << endl;
                return 0;
            }
            default: {
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
}
// Output:
// Enter: 
// 1. List A 
// 2. List B 
// 3. Concatenate
// 0. Exit
// 1

// List A:
// Enter: 
// 1. Add 
// 2. Delete 
// 3. Member's Count 
// 4. Display 
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// a
// Enter PRN: 12345
// Enter Name: abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 2

// Enter:
// A. Delete President
// B. Delete Secretary
// C. Delete Member
// a

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 3
// Count: 1

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 4
// President: 12345 ΓÇö abcd -> Secretary: 12345 ΓÇö abcd -> NULL

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 12345 ΓÇö abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 2

// List B:
// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// b
// Enter PRN: 34567
// Enter Name: defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 34567 ΓÇö defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 3
// President: 12345 ΓÇö abcd -> Secretary: 34567 ΓÇö defg -> NULL
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit

// Practical No -07
// Problem Statement: Department of Computer Engineering has student's club named 'Pinnacle Club'. Students of second, third and final year of department can be granted membership on request. Similarly one may cancel the membership of club. First node is reserved for president of club and last node is reserved for secretary of club. Write C++ program to maintain club member‘s information using singly linked list. Store student PRN and Name. Write functions to:
// a) Add and delete the members as well as president or even secretary.
// b) Compute total number of members of club 
// c) Display members 
// d) Two linked lists exists for two divisions. Concatenate two lists.
// Program:-
#include <iostream>
#include <string>
using namespace std;

// Node structure
struct Node {
    int prn;
    string name;
    Node* next;
};

// Linked list class
class ClubList {
    Node* head;

public:
    ClubList() {
        head = nullptr;
    }

    // Function to create a new node
    Node* createNode(int prn, string name) {
        Node* newNode = new Node;
        if (!newNode) {
            cout << "Memory allocation failed!" << endl;
            return nullptr;
        }
        newNode->prn = prn;
        newNode->name = name;
        newNode->next = nullptr;
        return newNode;
    }

    // Function to add a member at the end (Secretary)
    void addMemberEnd() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        if (!head) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        cout << "Member added!" << endl;
    }

    // Function to add a member at the beginning (President)
    void addMemberBeginning() {
        int prn;
        string name;
        cout << "Enter PRN: ";
        cin >> prn;
        cout << "Enter Name: ";
        cin >> name;

        Node* newNode = createNode(prn, name);
        newNode->next = head;
        head = newNode;
        cout << "New President added!" << endl;
    }

    // Function to delete a member at a specific position
    void deleteMember(int pos) {
        if (pos == 1) {
            if (head) {
                Node* temp = head;
                head = head->next;
                delete temp;
                cout << "President deleted!" << endl;
            } else {
                cout << "No members to delete!" << endl;
            }
        } else {
            Node* temp = head;
            int count = 1;
            while (temp && count < pos - 1) {
                temp = temp->next;
                count++;
            }
            if (temp && temp->next) {
                Node* deleteNode = temp->next;
                temp->next = temp->next->next;
                delete deleteNode;
                cout << "Member at position " << pos << " deleted!" << endl;
            } else {
                cout << "Position out of range!" << endl;
            }
        }
    }

    // Function to display the members
    void displayMembers() {
        if (!head) {
            cout << "No members in the club!" << endl;
            return;
        }
        Node* temp = head;
        cout << "President: " << temp->prn << " - " << temp->name << endl;
        temp = temp->next;
        while (temp) {
            cout << "Member: " << temp->prn << " - " << temp->name << endl;
            temp = temp->next;
        }
    }

    // Function to count the total number of members
    int countMembers() {
        int count = 0;
        Node* temp = head;
        while (temp) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    // Function to concatenate two lists
    void concatenate(ClubList& listB) {
        if (!head) {
            head = listB.head;
        } else {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = listB.head;
        }
        listB.head = nullptr;
        cout << "Lists concatenated!" << endl;
    }
};

// Main function
int main() {
    ClubList listA, listB;
    int choice;
    
    while (true) {
        cout << "\nEnter your choice:\n1. Add member to List A\n2. Add member to List B\n3. Concatenate Lists\n4. Display List A\n5. Display List B\n6. Delete member from List A\n7. Delete member from List B\n8. Count members in List A\n9. Count members in List B\n0. Exit" << endl;
        cin >> choice;

        switch (choice) {
            case 1: {
                listA.addMemberEnd();
                break;
            }
            case 2: {
                listB.addMemberEnd();
                break;
            }
            case 3: {
                listA.concatenate(listB);
                break;
            }
            case 4: {
                listA.displayMembers();
                break;
            }
            case 5: {
                listB.displayMembers();
                break;
            }
            case 6: {
                int pos;
                cout << "Enter position to delete in List A: ";
                cin >> pos;
                listA.deleteMember(pos);
                break;
            }
            case 7: {
                int pos;
                cout << "Enter position to delete in List B: ";
                cin >> pos;
                listB.deleteMember(pos);
                break;
            }
            case 8: {
                cout << "Total members in List A: " << listA.countMembers() << endl;
                break;
            }
            case 9: {
                cout << "Total members in List B: " << listB.countMembers() << endl;
                break;
            }
            case 0: {
                cout << "Exiting program..." << endl;
                return 0;
            }
            default: {
                cout << "Invalid choice! Please try again." << endl;
            }
        }
    }
}
// Output:
// Enter: 
// 1. List A 
// 2. List B 
// 3. Concatenate
// 0. Exit
// 1

// List A:
// Enter: 
// 1. Add 
// 2. Delete 
// 3. Member's Count 
// 4. Display 
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// a
// Enter PRN: 12345
// Enter Name: abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 2

// Enter:
// A. Delete President
// B. Delete Secretary
// C. Delete Member
// a

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 3
// Count: 1

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 4
// President: 12345 ΓÇö abcd -> Secretary: 12345 ΓÇö abcd -> NULL

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 12345 ΓÇö abcd

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 2

// List B:
// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 1

// Enter:
// A. Add President
// B. Add Secretary
// C. Add Member
// b
// Enter PRN: 34567
// Enter Name: defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 5
// Secretary: 34567 ΓÇö defg

// Enter:
// 1. Add
// 2. Delete
// 3. Member's Count
// 4. Display
// 5. Reverse the List
// 0. Prev Menu
// 0
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit
// 3
// President: 12345 ΓÇö abcd -> Secretary: 34567 ΓÇö defg -> NULL
// Enter:
// 1. List A
// 2. List B
// 3. Concatenate
// 0. Exit

