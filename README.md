#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

struct Product {
    int id;
    string name;
    float price;
    int quantity;
    string item;
};

typedef struct Node {
    Product data;
    Node *next;
} Node;

typedef struct List {
    Node *head;
    Node *tail;
    int size;
    List();
    Node* createNode(Product p);
    void addFirst(Product p);
    void addLast(Product p);
    void insert(Product p, int pos);
    void deleteFirst();
    void deleteLast();
    void remove(int pos);
    void print();
    void check(int id);
    void clear();
    void sortByPrice();
    void searchById(int id);
    void inputMultipleProducts(int num);
    void inputProductDetails(Product &p, int id);
    void displayProduct(const Product &p);
} List;

List::List() {
    head = tail = NULL;
    size = 0;
}

Node* List::createNode(Product p) {
    Node *newNode = new Node();
    newNode->data = p;
    newNode->next = NULL;
    return newNode;
}

void List::addFirst(Product p) {
    Node *newNode = createNode(p);
    if (head == NULL) {
        head = tail = newNode;
    } else {
        newNode->next = head;
        head = newNode;
    }
    size++;
}

void List::addLast(Product p) {
    Node *newNode = createNode(p);
    if (head == NULL) {
        head = tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }
    size++;
}

void List::insert(Product p, int pos) {
    if (pos < 1 || pos > size + 1) {
        cout << "Vi tri khong hop le\n";
        return;
    }
    
    if (pos == 1) {
        addFirst(p);
        return;
    }
    
    if (pos == size + 1) {
        addLast(p);
        return;
    }
    
    Node *newNode = createNode(p);
    Node *temp = head;
    for (int i = 1; i < pos - 1; i++) {
        temp = temp->next;
    }
    newNode->next = temp->next;
    temp->next = newNode;
    size++;
}

void List::deleteFirst() {
    if (head == NULL) {
        cout << "Danh sach trong\n";
    } else {
        head = head->next;
        size--;
    }
}
