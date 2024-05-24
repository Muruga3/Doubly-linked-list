# Doubly-linked-list
include<stdio.h>
#include<stdlib.h>

struct Node {
    int data;
    struct Node* next;
    struct Node* prev;
};

typedef struct Node node;
node* head = NULL;

void insert(int d) { // d = 30
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    newNode->prev = NULL;
    
    if(head==NULL) {
        head = newNode;
    }
    else {
        node* temp = head;
        while(temp->next!=NULL) {
            temp = temp->next;
        }
        temp->next = newNode;
        newNode->prev = temp;
    }
}
void insertbeg(int d) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = head;
    newNode->prev = NULL;
    if(head!=NULL) {
        head->prev = newNode;
    }
    head = newNode;
}
void insertafter(int x, int d) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    newNode->prev = NULL;
    
    if(head == NULL) {
        printf("\nList is Empty");
        return;
    }
    node* temp = head;
    while(temp->data!=x) {
        temp = temp->next;
    }
    newNode->next = temp->next;
    temp->next->prev = newNode;
    temp->next = newNode;
    newNode->prev = temp;
}
void insertbefore(int x, int d) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    newNode->prev = NULL;
    
    if(head==NULL) {
        printf("\nList is Empty");
    }
    else {
        node* temp = head;
        node* prev = NULL;
        
        while(temp->data!=x) {
            prev = temp;
            temp = temp->next;
        }
        
        newNode->next = temp;
        prev->next = newNode;
        newNode->prev = prev;
        temp->prev = newNode;
    }
}
void insertPosition(int Position, int d) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    newNode->prev = NULL;
    int CurrentPosition = 0;
    if(head==NULL) {
        printf("\nList is Empty");
    }
    else {
        node* temp = head;
        node* prev = NULL;
        
        if(Position == 0) {
            insertbeg(d);
            return;
        }
        
        while(temp!=NULL && CurrentPosition != Position) {
            prev = temp;
            temp = temp->next;
            CurrentPosition++;
        }
        
        newNode->prev = prev;
        newNode->next = temp;
        temp->prev = newNode;
        prev->next = newNode;
    }
}
void display() {
    node* temp = head;
    while(temp!=NULL) {
        printf("\nNode = %d", temp->data);
        temp = temp->next;
    }
}
int main() {
    insert(10);
    insert(20);
    insert(30);
    insertbeg(40);
    insertafter(20, 50);
    insertbefore(20, 60);
    insertPosition(2, 70);
    display();
    return 0;
}
