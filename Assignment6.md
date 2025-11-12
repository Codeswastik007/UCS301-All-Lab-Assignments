###Question1
```cpp
#include <iostream>
using namespace std;
class DNode {
public:
    int data;
    DNode* next;
    DNode* prev;
    DNode(int val) {
        data = val;
        next = prev = NULL;
    }
};
class DoublyLinkedList {
    DNode* head;
public:
    DoublyLinkedList() {
        head = NULL;
    }
    void insertAtBeginning(int val) {
        DNode* newNode = new DNode(val);
        if (head != NULL) head->prev = newNode;
        newNode->next = head;
        head = newNode;
    }

    void insertAtEnd(int val) {
        DNode* newNode = new DNode(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        DNode* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
        newNode->prev = temp;
    }
    void insertAfter(int key, int val) {
        DNode* temp = head;
        while (temp != NULL && temp->data != key)
            temp = temp->next;
        if (temp == NULL) {
            cout << "Node " << key << " not found!\n";
            return;
        }
        DNode* newNode = new DNode(val);
        newNode->next = temp->next;
        newNode->prev = temp;
        if (temp->next != NULL)
            temp->next->prev = newNode;
        temp->next = newNode;
    }
    void insertBefore(int key, int val) {
        if (head == NULL) {
            cout << "List is empty!\n";
            return;
        }
        if (head->data == key) {
            insertAtBeginning(val);
            return;
        }
        DNode* temp = head;
        while (temp != NULL && temp->data != key)
            temp = temp->next;
        if (temp == NULL) {
            cout << "Node " << key << " not found!\n";
            return;
        }
        DNode* newNode = new DNode(val);
        newNode->prev = temp->prev;
        newNode->next = temp;
        temp->prev->next = newNode;
        temp->prev = newNode;
    }

    void deleteNode(int key) {
        if (head == NULL) {
            cout << "List is empty!\n";
            return;
        }
        DNode* temp = head;

        if (head->data == key) {
            head = head->next;
            if (head != NULL) head->prev = NULL;
            delete temp;
            return;
        }
        while (temp != NULL && temp->data != key)
            temp = temp->next;
        if (temp == NULL) {
            cout << "Node " << key << " not found!\n";
            return;
        }
        if (temp->next != NULL)
            temp->next->prev = temp->prev;
        if (temp->prev != NULL)
            temp->prev->next = temp->next;

        delete temp;
    }
    void search(int key) {
        int pos = 1;
        DNode* temp = head;
        while (temp != NULL) {
            if (temp->data == key) {
                cout << "Node " << key << " found at position " << pos << endl;
                return;
            }
            pos++;
            temp = temp->next;
        }
        cout << "Node not found!\n";
    }
    void display() {
        if (head == NULL) {
            cout << "List is empty!\n";
            return;
        }
        DNode* temp = head;
        cout << "Doubly Linked List: ";
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next) cout << " <-> ";
            temp = temp->next;
        }
        cout << endl;
    }
};

class CNode {
public:
    int data;
    CNode* next;
    CNode(int val) {
        data = val;
        next = NULL;
    }
};
class CircularLinkedList {
    CNode* last;
public:
    CircularLinkedList() {
        last = NULL;
    }
    void insertAtBeginning(int val) {
        CNode* newNode = new CNode(val);
        if (last == NULL) {
            last = newNode;
            last->next = last;
            return;
        }
        newNode->next = last->next;
        last->next = newNode;
    }
    void insertAtEnd(int val) {
        CNode* newNode = new CNode(val);
        if (last == NULL) {
            last = newNode;
            last->next = last;
            return;
        }
        newNode->next = last->next;
        last->next = newNode;
        last = newNode;
    }
    void insertAfter(int key, int val) {
        if (last == NULL) {
            cout << "List is empty!\n";
            return;
        }
        CNode* temp = last->next;
        do {
            if (temp->data == key) {
                CNode* newNode = new CNode(val);
                newNode->next = temp->next;
                temp->next = newNode;
                if (temp == last) last = newNode;
                return;
            }
            temp = temp->next;
        } while (temp != last->next);
        cout << "Node " << key << " not found!\n";
    }
    void deleteNode(int key) {
        if (last == NULL) {
            cout << "List is empty!\n";
            return;
        }
        CNode* curr = last->next;
        CNode* prev = last;

        if (curr == last && curr->data == key) {
            delete curr;
            last = NULL;
            return;
        }
        do {
            if (curr->data == key) {
                prev->next = curr->next;
                if (curr == last) last = prev;
                if (curr == last->next) last->next = curr->next;
                delete curr;
                return;
            }
            prev = curr;
            curr = curr->next;
        } while (curr != last->next);
        cout << "Node " << key << " not found!\n";
    }
    void search(int key) {
        if (last == NULL) {
            cout << "List is empty!\n";
            return;
        }
        int pos = 1;
        CNode* temp = last->next;
        do {
            if (temp->data == key) {
                cout << "Node " << key << " found at position " << pos << endl;
                return;
            }
            pos++;
            temp = temp->next;
        } while (temp != last->next);
        cout << "Node not found!\n";
    }

    void display() {
        if (last == NULL) {
            cout << "List is empty!\n";
            return;
        }
        CNode* temp = last->next;
        cout << "Circular Linked List: ";
        do {
            cout << temp->data;
            if (temp->next != last->next) cout << " -> ";
            temp = temp->next;
        } while (temp != last->next);
        cout << endl;
    }
};
int main() {
    DoublyLinkedList dlist;
    CircularLinkedList clist;
    int choice, type, val, key;
    cout << "Choose List Type:\n1. Doubly Linked List\n2. Circular Linked List\nEnter choice: ";
    cin >> type;
    do {
        cout << "\n=== Menu ===\n";
        cout << "1. Insert at Beginning\n2. Insert at End\n3. Insert Before Value (Doubly only)\n";
        cout << "4. Insert After Value\n5. Delete Node\n6. Search Node\n7. Display\n8. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        switch (choice) {
        case 1:
            cout << "Enter value: ";
            cin >> val;
            if (type == 1) dlist.insertAtBeginning(val);
            else clist.insertAtBeginning(val);
            break;
        case 2:
            cout << "Enter value: ";
            cin >> val;
            if (type == 1) dlist.insertAtEnd(val);
            else clist.insertAtEnd(val);
            break;
        case 3:
            if (type == 1) {
                cout << "Enter key and new value: ";
                cin >> key >> val;
                dlist.insertBefore(key, val);
            } else cout << "Not applicable for Circular List.\n";
            break;
        case 4:
            cout << "Enter key and new value: ";
            cin >> key >> val;
            if (type == 1) dlist.insertAfter(key, val);
            else clist.insertAfter(key, val);
            break;
        case 5:
            cout << "Enter value to delete: ";
            cin >> key;
            if (type == 1) dlist.deleteNode(key);
            else clist.deleteNode(key);
            break;
        case 6:
            cout << "Enter value to search: ";
            cin >> key;
            if (type == 1) dlist.search(key);
            else clist.search(key);
            break;
        case 7:
            if (type == 1) dlist.display();
            else clist.display();
            break;
        case 8:
            cout << "Exiting program...\n";
            break;
        default:
            cout << "Invalid choice!\n";
        }
```

###Question2
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

class CircularLinkedList {
    Node* last;

public:
    CircularLinkedList() {
        last = NULL;
    }

    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (last == NULL) {
            last = newNode;
            last->next = last;
            return;
        }
        newNode->next = last->next;
        last->next = newNode;
        last = newNode;
    }

    void display() {
        if (last == NULL) {
            cout << "List is empty!" << endl;
            return;
        }
        Node* temp = last->next; 
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != last->next);
        cout << last->next->data << endl; 
    }
};

int main() {
    CircularLinkedList list;
    int n, val;

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        list.insertAtEnd(val);
    }

    cout << "Output: ";
    list.display();

    return 0;
}
```

###Question3
```cpp
#include <iostream>
using namespace std;

class DNode {
public:
    int data;
    DNode* prev;
    DNode* next;
    DNode(int val) {
        data = val;
        prev = NULL;
        next = NULL;
    }
};

class DoublyLinkedList {
    DNode* head;
public:
    DoublyLinkedList() { head = NULL; }

    void insertAtEnd(int val) {
        DNode* newNode = new DNode(val);
        if (head == NULL) {
            head = newNode;
            return;
        }
        DNode* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newNode;
        newNode->prev = temp;
    }

    int getSize() {
        int count = 0;
        DNode* temp = head;
        while (temp != NULL) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    void display() {
        DNode* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

class CNode {
public:
    int data;
    CNode* next;
    CNode(int val) {
        data = val;
        next = NULL;
    }
};

class CircularLinkedList {
    CNode* last;
public:
    CircularLinkedList() { last = NULL; }

    void insertAtEnd(int val) {
        CNode* newNode = new CNode(val);
        if (last == NULL) {
            last = newNode;
            last->next = last;
            return;
        }
        newNode->next = last->next;
        last->next = newNode;
        last = newNode;
    }

    int getSize() {
        if (last == NULL)
            return 0;
        int count = 0;
        CNode* temp = last->next;
        do {
            count++;
            temp = temp->next;
        } while (temp != last->next);
        return count;
    }

    void display() {
        if (last == NULL) {
            cout << "List is empty" << endl;
            return;
        }
        CNode* temp = last->next;
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != last->next);
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;
    CircularLinkedList cll;
    int n, val;

    cout << "Enter number of elements for Doubly Linked List: ";
    cin >> n;
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        dll.insertAtEnd(val);
    }
    cout << "Doubly Linked List: ";
    dll.display();
    cout << "Size of Doubly Linked List = " << dll.getSize() << endl;

    cout << "\nEnter number of elements for Circular Linked List: ";
    cin >> n;
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        cin >> val;
        cll.insertAtEnd(val);
    }
    cout << "Circular Linked List: ";
    cll.display();
    cout << "Size of Circular Linked List = " << cll.getSize() << endl;

    return 0;
}
```

###Question4
```cpp
#include <iostream>
using namespace std;

class Node {
public:
    char data;
    Node* prev;
    Node* next;

    Node(char val) {
        data = val;
        prev = NULL;
        next = NULL;
    }
};

class DoublyLinkedList {
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() {
        head = NULL;
        tail = NULL;
    }

    void insertAtEnd(char val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = tail = newNode;
            return;
        }
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode;
    }

    void display() {
        Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    bool isPalindrome() {
        if (head == NULL)
            return true;

        Node* left = head;
        Node* right = tail;

        while (left != right && right->next != left) {
            if (left->data != right->data)
                return false;
            left = left->next;
            right = right->prev;
        }
        return true;
    }
};

int main() {
    DoublyLinkedList dll;
    int n;
    char ch;

    cout << "Enter number of characters: ";
    cin >> n;

    cout << "Enter characters: ";
    for (int i = 0; i < n; i++) {
        cin >> ch;
        dll.insertAtEnd(ch);
    }

    cout << "Doubly Linked List: ";
    dll.display();

    if (dll.isPalindrome())
        cout << "The linked list is a palindrome." << endl;
    else
        cout << "The linked list is NOT a palindrome." << endl;

    return 0;
}


```
###Question5
```cpp
#include<iostream>
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

bool isCircular(Node* head) {
    if (head == NULL) 
        return false;

    Node* temp = head->next;
    while (temp != NULL && temp != head) {
        temp = temp->next;
    }

    return (temp == head);
}

int main() {
   
    Node* head = new Node(1);
    Node* second = new Node(2);
    Node* third = new Node(3);

    head->next = second;
    second->next = third;
    third->next = head; 

    if (isCircular(head))
        cout << "The linked list is Circular." << endl;
    else
        cout << "The linked list is NOT Circular." << endl;

    return 0;
}
```



