# lab-Evaluation
** TO FIND MIDDLE ELEMENT OF SINGLY LL WITHOUT USING LENGHTH OF LINKED LIST

#include <stdio.h>
#include <stdlib.h>


struct Node {
    int data;
    struct Node* next;
};

struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}


void findMiddle(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }

    struct Node* slow = head;
    struct Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    printf("Middle element: %d\n", slow->data);
}


void insertEnd(struct Node** head, int data) {
    struct Node* newNode = createNode(data);
    if (*head == NULL) {
        *head = newNode;
        return;
    }

    struct Node* temp = *head;
    while (temp->next != NULL)
        temp = temp->next;

    temp->next = newNode;
}


int main() {
    struct Node* head = NULL;

    
    insertEnd(&head, 1);
    insertEnd(&head, 2);
    insertEnd(&head, 3);
    insertEnd(&head, 4);
    insertEnd(&head, 5);

    findMiddle(head); 

    return 0;
}



**DELETE A NODE FROM SINGLY LL WHERE ONLY SINGLE POINTER OF THAT NODE IS GIVEN

#include <stdio.h>
#include <stdlib.h>


struct Node {
    int data;
    struct Node* next;
};



void deleteNode(struct Node* node) {
    if (node == NULL || node->next == NULL) {
        printf("Cannot delete the last node using this method.\n");
        return;
    }

    struct Node* temp = node->next;
    node->data = temp->data;
    node->next = temp->next;

    free(temp);
}


void printList(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}


struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}


int main() {
    
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);
    head->next->next->next = createNode(4);
    head->next->next->next->next = createNode(5);

    printf("Original list:\n");
    printList(head);

  
    printf("\nDeleting node with value 3 (only pointer to it is given)...\n");
    deleteNode(head->next->next); 

    printf("\nUpdated list:\n");
    printList(head);

    return 0;
}


**REVERSE CONTENT OF STACK USING RECURSSION WITHOUT USING EXTRA ARRAY 

#include <stdio.h>
#include <stdlib.h>

#define MAX 100


struct Stack {
    int arr[MAX];
    int top;
};


void initStack(struct Stack* stack) {
    stack->top = -1;
}


int isEmpty(struct Stack* stack) {
    return stack->top == -1;
}


void push(struct Stack* stack, int value) {
    if (stack->top >= MAX - 1) {
        printf("Stack Overflow\n");
        return;
    }
    stack->arr[++stack->top] = value;
}


int pop(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack Underflow\n");
        return -1;
    }
    return stack->arr[stack->top--];
}


void printStack(struct Stack* stack) {
    for (int i = 0; i <= stack->top; i++) {
        printf("%d ", stack->arr[i]);
    }
    printf("\n");
}


void insertAtBottom(struct Stack* stack, int value) {
    if (isEmpty(stack)) {
        push(stack, value);
        return;
    }

    int temp = pop(stack);
    insertAtBottom(stack, value);
    push(stack, temp);
}


void reverseStack(struct Stack* stack) {
    if (isEmpty(stack))
        return;

    int temp = pop(stack);
    reverseStack(stack);
    insertAtBottom(stack, temp);
}


int main() {
    struct Stack stack;
    initStack(&stack);

    
    push(&stack, 1);
    push(&stack, 2);
    push(&stack, 3);
    push(&stack, 4);
    push(&stack, 5);

    printf("Original Stack:\n");
    printStack(&stack);

    reverseStack(&stack);

    printf("Reversed Stack:\n");
    printStack(&stack);

    return 0;
}
