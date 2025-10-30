### Question 1
```cpp
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = NULL;
    }
};
class LinkedList {
    Node* head;

public:
    LinkedList() {
        head = NULL;
    }
    void insertAtBeginning(int val) {
        Node* newNode = new Node(val);
        newNode->next = head;
        head = newNode;
    }
    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
    }
    void insertAfterValue(int value, int newVal) {
        Node* temp = head;
        while (temp != NULL && temp->data != value)
            temp = temp->next;
        if (temp == NULL) {
            cout << "Node " << value << " not found!" << endl;
            return;
        }
        Node* newNode = new Node(newVal);
        newNode->next = temp->next;
        temp->next = newNode;
    }
    void insertBeforeValue(int value, int newVal) {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        if (head->data == value) {
            insertAtBeginning(newVal);
            return;
        }
        Node* temp = head;
        while (temp->next != NULL && temp->next->data != value)
            temp = temp->next;
        if (temp->next == NULL) {
            cout << "Node " << value << " not found!" << endl;
            return;
        }
        Node* newNode = new Node(newVal);
        newNode->next = temp->next;
        temp->next = newNode;
    }
    void deleteAtBeginning() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;
    }
    void deleteAtEnd() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        if (head->next == NULL) {
            delete head;
            head = NULL;
            return;
        }
        Node* temp = head;
        while (temp->next->next != NULL)
            temp = temp->next;
        delete temp->next;
        temp->next = NULL;
    }
    void deleteSpecific(int value) {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        if (head->data == value) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }
        Node* temp = head;
        while (temp->next != NULL && temp->next->data != value)
            temp = temp->next;
        if (temp->next == NULL) {
            cout << "Node " << value << " not found!" << endl;
            return;
        }
        Node* del = temp->next;
        temp->next = temp->next->next;
        delete del;
    }
    void search(int value) {
        Node* temp = head;
        int pos = 1;
        while (temp != NULL) {
            if (temp->data == value) {
                cout << "Node " << value << " found at position " << pos << endl;
                return;
            }
            temp = temp->next;
            pos++;
        }
        cout << "Node not found!" << endl;
    }

    void display() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = head;
        cout << "Linked List: ";
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next) cout << " -> ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    LinkedList list;
    int choice, val, val2;

    do {
        cout << "\n=== Singly Linked List Menu ===\n";
        cout << "1. Insert at Beginning\n";
        cout << "2. Insert at End\n";
        cout << "3. Insert Before Value\n";
        cout << "4. Insert After Value\n";
        cout << "5. Delete from Beginning\n";
        cout << "6. Delete from End\n";
        cout << "7. Delete Specific Node\n";
        cout << "8. Search Node\n";
        cout << "9. Display List\n";
        cout << "10. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter value: ";
            cin >> val;
            list.insertAtBeginning(val);
            break;
        case 2:
            cout << "Enter value: ";
            cin >> val;
            list.insertAtEnd(val);
            break;
        case 3:
            cout << "Enter value to insert before: ";
            cin >> val;
            cout << "Enter new value: ";
            cin >> val2;
            list.insertBeforeValue(val, val2);
            break;
        case 4:
            cout << "Enter value to insert after: ";
            cin >> val;
            cout << "Enter new value: ";
            cin >> val2;
            list.insertAfterValue(val, val2);
            break;
        case 5:
            list.deleteAtBeginning();
            break;
        case 6:
            list.deleteAtEnd();
            break;
        case 7:
            cout << "Enter value to delete: ";
            cin >> val;
            list.deleteSpecific(val);
            break;
        case 8:
            cout << "Enter value to search: ";
            cin >> val;
            list.search(val);
            break;
        case 9:
            list.display();
            break;
        case 10:
            cout << "Exiting program" << endl;
            break;
        default:
            cout << "Invalid choice" << endl;
        }
    } while (choice != 10);

    return 0;
}
```
### Question 2
```cpp

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = NULL;
    }
};

class LinkedList {
    Node* head;

public:
    LinkedList() {
        head = NULL;
    }

    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
    }

    int countAndDeleteKey(int key) {
        int count = 0;
        // Delete key at the beginning if present
        while (head != NULL && head->data == key) {
            Node* temp = head;
            head = head->next;
            delete temp;
            count++;
        }
        // Delete other occurrences
        Node* curr = head;
        while (curr != NULL && curr->next != NULL) {
            if (curr->next->data == key) {
                Node* del = curr->next;
                curr->next = curr->next->next;
                delete del;
                count++;
            } else {
                curr = curr->next;
            }
        }
        return count;
    }

    void display() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = head;
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next) cout << " -> ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    LinkedList list;
    int n, val, key;

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        list.insertAtEnd(val);
    }

    cout << "Enter key to delete: ";
    cin >> key;

    cout << "Original Linked List: ";
    list.display();

    int count = list.countAndDeleteKey(key);

    cout << "Count of " << key << ": " << count << endl;
    cout << "Updated Linked List: ";
    list.display();

    return 0;
}

```

### Question 3

```cpp

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = NULL;
    }
};
class LinkedList {
    Node* head;
public:
    LinkedList() {
        head = NULL;
    }
    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
    }
    void findMiddle() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* slow = head;
        Node* fast = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }
        cout << "Middle element: " << slow->data << endl;
    }
    void display() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = head;
        cout << "Linked List: ";
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next) cout << " -> ";
            temp = temp->next;
        }
        cout << endl;
    }
};
int main() {
    LinkedList list;
    int n, val;
    cout << "Enter number of elements: ";
    cin >> n;
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        list.insertAtEnd(val);
    }
    list.display();
    list.findMiddle();
    return 0;
}
```

### Question 4

```cpp

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = NULL;
    }
};

class LinkedList {
    Node* head;

public:
    LinkedList() {
        head = NULL;
    }

    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
    }

    void reverse() {
        Node* prev = NULL;
        Node* curr = head;
        Node* next = NULL;

        while (curr != NULL) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }

        head = prev;
    }

    void display() {
        if (head == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = head;
        cout << "Linked List: ";
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next) cout << " -> ";
            temp = temp->next;
        }
        cout << " -> NULL" << endl;
    }
};

int main() {
    LinkedList list;
    int n, val;

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        list.insertAtEnd(val);
    }

    cout << "\nOriginal ";
    list.display();

    list.reverse();

    cout << "Reversed ";
    list.display();

    return 0;
}

```
