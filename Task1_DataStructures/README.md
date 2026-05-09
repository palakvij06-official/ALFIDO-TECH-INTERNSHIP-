#include <iostream>
using namespace std;

// ---------- LINKED LIST ----------
class Node {
public:
    int data;
    Node* next;
};

class LinkedList {
public:
    Node* head = NULL;

    void insert(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = head;
        head = newNode;
    }

    void deleteNode(int key) {
        Node* temp = head;
        Node* prev = NULL;

        if (temp != NULL && temp->data == key) {
            head = temp->next;
            delete temp;
            return;
        }

        while (temp != NULL && temp->data != key) {
            prev = temp;
            temp = temp->next;
        }

        if (temp == NULL) return;

        prev->next = temp->next;
        delete temp;
    }

    void display() {
        Node* temp = head;
        while (temp != NULL) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL\n";
    }
};

// ---------- STACK ----------
class Stack {
    int arr[100];
    int top;

public:
    Stack() { top = -1; }

    void push(int x) {
        if (top >= 99) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
    }

    void pop() {
        if (top < 0) {
            cout << "Stack Underflow\n";
            return;
        }
        top--;
    }

    void display() {
        for (int i = top; i >= 0; i--)
            cout << arr[i] << " ";
        cout << endl;
    }
};

// ---------- MAIN ----------
int main() {
    LinkedList list;
    list.insert(10);
    list.insert(20);
    list.insert(30);
    list.display();

    list.deleteNode(20);
    list.display();

    Stack s;
    s.push(1);
    s.push(2);
    s.push(3);
    s.display();

    s.pop();
    s.display();

    return 0;
}
