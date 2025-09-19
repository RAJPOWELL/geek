# Binary Tree  to DLL

## Problem

Given a **root** of binary tree (BT), convert it to a Doubly Linked List (DLL) in place using the **same node** structure. The **left** and **right** pointers in the binary tree nodes should be used as **prev** and **next** pointers respectively in the resulting DLL .The DLL should be formed by performing an **inorder** traversal of the binary tree (i.e., Left → Root → Right).The **first node** in the inorder traversal (i.e., the leftmost node) should become the **head** of the DLL. Return the **head** of the resulting DLL.  
**Note:** h is the tree's height, and this space is used implicitly for the recursion stack.

![TreeToList](http://www.geeksforgeeks.org/wp-content/uploads/TreeToList.png)

**Examples:**

```
Input: root = [1, 2, 3]
Output: [3, 1, 2]   
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700144/Web/Other/blobid0_1723093893.png)
Explanation: DLL would be 3<=>1<=>2
```

```
Input:  root = [10, 20, 30, 40, 60]
Output: [40, 20, 60, 10, 30]   
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700144/Web/Other/blobid1_1723093972.png)  
Explanation: DLL would be 40<=>20<=>60<=>10<=>30.
```

**Constraints:**  
1 ≤ Number of nodes ≤ 105  
0 ≤ Data of a node ≤ 105

## Solution

# Convert Binary Tree to Doubly Linked List by fixing left and right pointers

Last Updated : 
23 Jul, 2025

Comments

Improve

Suggest changes

Like Article

Like



Report

[Try it on GfG Practice

![redirect icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Group-arrow.svg)](https://www.geeksforgeeks.org/problems/binary-tree-to-dll/1)

Given a ****Binary Tree****, the task is to convert it to a ****Doubly Linked List (DLL)**** in place. The ****left****and ****right****pointers in ****nodes**** will be used as ****previous****and ****next****pointers respectively in converted DLL. The order of nodes in ****DLL****must be the same as the order of the given ****Binary**** Tree. The first node of ****Inorder**** traversal (the ****leftmost**** node in Binary Tree) must be the ****head**** node of the DLL.

****Examples:****

> ****Input:****
>
> ![Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-ex-1](https://media.geeksforgeeks.org/wp-content/uploads/20240930100624/Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-ex-1.webp)
>
> ****Output:****
>
> ![Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-1](https://media.geeksforgeeks.org/wp-content/uploads/20240930102216/Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-1.webp)
>
> ****Explanation:**** **The above binary tree is converted into doubly linked list where left pointer of the binary tree node act as the previous node and right pointer of the binary tree node act as the next node.**
>
> ****Input:****
>
> ![Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-ex-2](https://media.geeksforgeeks.org/wp-content/uploads/20240930100624/Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-ex-2.webp)
>
> ****Output:****
>
> ![Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-2](https://media.geeksforgeeks.org/wp-content/uploads/20240930102216/Convert-Binary-Tree-to-Doubly-Linked-List-using-inorder-traversal-2.webp)
>
> ****Explanation:**** **The above binary tree is converted into doubly linked list where left pointer of the binary tree node act as the previous node and right pointer of the binary tree node act as the next node.**

****Approach:****

> The idea involves converting a ****Binary Tree to a Doubly Linked List (DLL)**** in place by first ****fixing**** the l****eft pointers**** during an [in-order traversal](https://www.geeksforgeeks.org/dsa/inorder-traversal-of-binary-tree/) to point to the ****previous**** node, then ****fixing the right pointers**** by traversing the modified tree in ****reverse**** using the left pointers to point to the next node in the DLL.

Step by step approach:

* Perform an ****in-order traversal**** of the tree to fix the ****left pointers****, updating each ****node’s left**** to point to the ****previously**** visited node.
* Use the ****rightmost nod****e ****(last node in DLL)**** and ****traverse back**** using left pointers to fix the right pointers for each node.
* Ensure the ****leftmost**** node ****(first in DLL****) is returned as the ****head**** of the DLL.

C++

```` ```
// C++ program for in-place
// conversion of Binary Tree to DLL
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* left;
    Node* right;
    Node (int x) {
        data = x;
        left = nullptr;
        right = nullptr;
    }
};

// function to fix left pointers
void fixPrevPtr(Node* root, Node*& prev) {
    if (!root) return;

    // Recur for left subtree
    fixPrevPtr(root->left, prev);

    // Update left pointer
    root->left = prev;

    // Update previous pointer
    prev = root;

    // Recur for right subtree
    fixPrevPtr(root->right, prev);
}

// function to fix right pointers and get the head
Node* fixNextPtr(Node* root) {
    
    // Find the rightmost node
    Node* prev = nullptr;
    while (root && root->right) root = root->right;

    // Traverse back using left 
    // pointers to fix right pointers
    while (root) {
        root->right = prev;
        prev = root;
        root = root->left;
    }

    // Return the head (leftmost node)
    return prev;
}

// The main function that converts 
// Binary Tree to DLL and returns head of DLL 
Node* bToDLL(Node* root) { 
    if (!root) return nullptr;

    Node* prev = nullptr;

    // Fix the left pointers
    fixPrevPtr(root, prev);

    // Fix the right pointers 
    // and return the head
    return fixNextPtr(root);
} 

void printList(Node* head) {
    Node* curr = head;
    
    while (curr != nullptr) {
        cout << curr->data << " ";
        curr = curr->right;
    }
    cout << endl;
}

int main() {
    
    // Create a hard coded binary tree
    //          10
    //         /  \
    //       12    15    
    //      / \    /
    //     25 30  36
    Node* root = new Node(10);
    root->left = new Node(12);
    root->right = new Node(15);
    root->left->left = new Node(25);
    root->left->right = new Node(30);
    root->right->left = new Node(36);

    Node* head = bToDLL(root);

    printList(head);

    return 0;
}
``` ````
C

```` ```
// C program for in-place
// conversion of Binary Tree to DLL
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// function to fix left pointers
void fixPrevPtr(struct Node* root, struct Node** prev) {
    if (!root) return;

    // Recur for left subtree
    fixPrevPtr(root->left, prev);

    // Update left pointer
    root->left = *prev;

    // Update previous pointer
    *prev = root;

    // Recur for right subtree
    fixPrevPtr(root->right, prev);
}

// function to fix right pointers and get the head
struct Node* fixNextPtr(struct Node* root) {
    
    // Find the rightmost node
    struct Node* prev = NULL;
    while (root && root->right) root = root->right;

    // Traverse back using left 
    // pointers to fix right pointers
    while (root) {
        root->right = prev;
        prev = root;
        root = root->left;
    }

    // Return the head (leftmost node)
    return prev;
}

// The main function that converts 
// Binary Tree to DLL and returns head of DLL 
struct Node* bToDLL(struct Node* root) { 
    if (!root) return NULL;

    struct Node* prev = NULL;

    // Fix the left pointers
    fixPrevPtr(root, &prev);

    // Fix the right pointers 
    // and return the head
    return fixNextPtr(root);
}

void printList(struct Node* head) {
    struct Node* curr = head;

    while (curr != NULL) {
        printf("%d ", curr->data);
        curr = curr->right;
    }
    printf("\n");
}

struct Node* createNode(int x) {
    struct Node* newNode = 
    (struct Node*)malloc(sizeof(struct Node));
    newNode->data = x;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

int main() {
    
    // Create a hard coded binary tree
    //          10
    //         /  \
    //       12    15    
    //      / \    /
    //     25 30  36
    struct Node* root = createNode(10);
    root->left = createNode(12);
    root->right = createNode(15);
    root->left->left = createNode(25);
    root->left->right = createNode(30);
    root->right->left = createNode(36);

    struct Node* head = bToDLL(root);

    printList(head);

    return 0;
}
``` ````
Java

```` ```
// Java program for in-place
// conversion of Binary Tree to DLL
import java.util.ArrayList;

class Node {
    int data;
    Node left;
    Node right;

    Node(int x) {
        data = x;
        left = null;
        right = null;
    }
}

class GfG {
    
    // function to fix left pointers
    static void fixPrevPtr(Node root, Node[] prev) {
        if (root == null) return;

        // Recur for left subtree
        fixPrevPtr(root.left, prev);

        // Update left pointer
        root.left = prev[0];

        // Update previous pointer
        prev[0] = root;

        // Recur for right subtree
        fixPrevPtr(root.right, prev);
    }

    // function to fix right pointers and get the head
    static Node fixNextPtr(Node root) {
        
        // Find the rightmost node
        Node prev = null;
        while (root != null && root.right != null) root = root.right;

        // Traverse back using left 
        // pointers to fix right pointers
        while (root != null) {
            root.right = prev;
            prev = root;
            root = root.left;
        }

        // Return the head (leftmost node)
        return prev;
    }

    // The main function that converts 
    // Binary Tree to DLL and returns head of DLL 
    static Node bToDLL(Node root) { 
        if (root == null) return null;

        Node[] prev = new Node[1];

        // Fix the left pointers
        fixPrevPtr(root, prev);

        // Fix the right pointers 
        // and return the head
        return fixNextPtr(root);
    }

    static void printList(Node head) {
        Node curr = head;

        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.right;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        
        // Create a hard coded binary tree
        //          10
        //         /  \
        //       12    15    
        //      / \    /
        //     25 30  36
        Node root = new Node(10);
        root.left = new Node(12);
        root.right = new Node(15);
        root.left.left = new Node(25);
        root.left.right = new Node(30);
        root.right.left = new Node(36);

        Node head = bToDLL(root);

        printList(head);
    }
}
``` ````
Python

```` ```
# Python program for in-place
# conversion of Binary Tree to DLL

class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# function to fix left pointers
def fixPrevPtr(root, prev):
    if not root:
        return

    # Recur for left subtree
    fixPrevPtr(root.left, prev)

    # Update left pointer
    root.left = prev[0]

    # Update previous pointer
    prev[0] = root

    # Recur for right subtree
    fixPrevPtr(root.right, prev)

# function to fix right pointers and get the head
def fixNextPtr(root):
    
    # Find the rightmost node
    prev = None
    while root and root.right:
        root = root.right

    # Traverse back using left 
    # pointers to fix right pointers
    while root:
        root.right = prev
        prev = root
        root = root.left

    # Return the head (leftmost node)
    return prev

# The main function that converts 
# Binary Tree to DLL and returns head of DLL
def bToDLL(root):
    if not root:
        return None

    prev = [None]

    # Fix the left pointers
    fixPrevPtr(root, prev)

    # Fix the right pointers 
    # and return the head
    return fixNextPtr(root)

def printList(head):
    curr = head
    while curr:
        print(curr.data, end=" ")
        curr = curr.right
    print()

if __name__ == "__main__":
    
    # Create a hard coded binary tree
    #          10
    #         /  \
    #       12    15    
    #      / \    /
    #     25 30  36
    root = Node(10)
    root.left = Node(12)
    root.right = Node(15)
    root.left.left = Node(25)
    root.left.right = Node(30)
    root.right.left = Node(36)

    head = bToDLL(root)

    printList(head)
``` ````
C#

```` ```
// C# program for in-place
// conversion of Binary Tree to DLL
using System;
using System.Collections.Generic;

class Node {
    public int data;
    public Node left, right;

    public Node(int x) {
        data = x;
        left = null;
        right = null;
    }
}

class GfG {
    
    // function to fix left pointers
    static void fixPrevPtr(Node root, ref Node prev) {
        if (root == null) return;

        // Recur for left subtree
        fixPrevPtr(root.left, ref prev);

        // Update left pointer
        root.left = prev;

        // Update previous pointer
        prev = root;

        // Recur for right subtree
        fixPrevPtr(root.right, ref prev);
    }

    // function to fix right pointers and get the head
    static Node fixNextPtr(Node root) {
        
        // Find the rightmost node
        Node prev = null;
        while (root != null && root.right != null) root = root.right;

        // Traverse back using left 
        // pointers to fix right pointers
        while (root != null) {
            root.right = prev;
            prev = root;
            root = root.left;
        }

        // Return the head (leftmost node)
        return prev;
    }

    // The main function that converts 
    // Binary Tree to DLL and returns head of DLL 
    static Node bToDLL(Node root) { 
        if (root == null) return null;

        Node prev = null;

        // Fix the left pointers
        fixPrevPtr(root, ref prev);

        // Fix the right pointers 
        // and return the head
        return fixNextPtr(root);
    }

    static void printList(Node head) {
        Node curr = head;

        while (curr != null) {
            Console.Write(curr.data + " ");
            curr = curr.right;
        }
        Console.WriteLine();
    }

    static void Main(string[] args) {
        
        // Create a hard coded binary tree
        //          10
        //         /  \
        //       12    15    
        //      / \    /
        //     25 30  36
        Node root = new Node(10);
        root.left = new Node(12);
        root.right = new Node(15);
        root.left.left = new Node(25);
        root.left.right = new Node(30);
        root.right.left = new Node(36);

        Node head = bToDLL(root);

        printList(head);
    }
}
``` ````
JavaScript

```` ```
// JavaScript program for in-place
// conversion of Binary Tree to DLL

class Node {
    constructor(x) {
        this.data = x;
        this.left = null;
        this.right = null;
    }
}

// function to fix left pointers
function fixPrevPtr(root, prev) {
    if (!root) return;

    // Recur for left subtree
    fixPrevPtr(root.left, prev);

    // Update left pointer
    root.left = prev.node;

    // Update previous pointer
    prev.node = root;

    // Recur for right subtree
    fixPrevPtr(root.right, prev);
}

// function to fix right pointers and get the head
function fixNextPtr(root) {

    // Find the rightmost node
    let prev = null;
    while (root && root.right) root = root.right;

    // Traverse back using left 
    // pointers to fix right pointers
    while (root) {
        root.right = prev;
        prev = root;
        root = root.left;
    }

    // Return the head (leftmost node)
    return prev;
}

// The main function that converts 
// Binary Tree to DLL and returns head of DLL 
function bToDLL(root) {
    if (!root) return null;

    let prev = { node: null };

    // Fix the left pointers
    fixPrevPtr(root, prev);

    // Fix the right pointers 
    // and return the head
    return fixNextPtr(root);
}

function printList(head) {
    let curr = head;

    while (curr) {
        console.log(curr.data + " ");
        curr = curr.right;
    }
    console.log();
}

// Create a hard coded binary tree
//          10
//         /  \
//       12    15    
//      / \    /
//     25 30  36
let root = new Node(10);
root.left = new Node(12);
root.right = new Node(15);
root.left.left = new Node(25);
root.left.right = new Node(30);
root.right.left = new Node(36);

let head = bToDLL(root);

printList(head);
``` ````

**Output**

```
25 12 30 10 36 15
```

****Time Complexity:**** O(n), where n is the number of nodes in Binary tree.  
****Auxiliary Space:**** O(n)

****Related Article:****

* [Convert Binary Tree to Doubly Linked List](https://www.geeksforgeeks.org/dsa/convert-binary-tree-to-doubly-linked-list-using-inorder-traversal/)

  

Convert a given Binary Tree to Doubly Linked List | Set 2

Comment

More info

[K](https://www.geeksforgeeks.org/user/kartik/)

[kartik](https://www.geeksforgeeks.org/user/kartik/)

Follow

Improve

Article Tags :

* [Linked List](https://www.geeksforgeeks.org/category/dsa/data-structures/linked-list/)
* [Tree](https://www.geeksforgeeks.org/category/dsa/data-structures/tree/)
* [DSA](https://www.geeksforgeeks.org/category/dsa/)
* [Microsoft](https://www.geeksforgeeks.org/tag/microsoft/)
* [Amazon](https://www.geeksforgeeks.org/tag/amazon/)
* [Goldman Sachs](https://www.geeksforgeeks.org/tag/goldman-sachs/)
* [doubly linked list](https://www.geeksforgeeks.org/tag/doubly-linked-list/)

+3 More
