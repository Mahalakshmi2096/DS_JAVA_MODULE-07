# Ex6 Right Rotation LinkedList
## DATE: 06.09.2025
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Start
2. Input the linked list
3. Read n (number of nodes).
4. Read n values and create a singly linked list.
5. Rotate the list
6. If the list is empty, has one node, or k = 0, return the head.
7. Traverse the list to find its length and the last node.
8. Connect the last node to the head → forms a circular list.
9. Compute effective rotation: k = k % length.
10. Find the new tail at position length - k.
11. Set the node after new tail as the new head.
12. Break the circular link by setting newTail.next = null.
13. Traverse from the new head and print all node values.  

## Program:
```
import java.util.Scanner;
public class RotateLinkedList {
    public static Node rotate(Node head, int k) {
       //Type your code here
       if(head==null || head.next==null || k==0)
           return head;
       Node temp=head;
       int length=1;
       while(temp.next!=null){
           temp=temp.next;
           length++;
       }
       temp.next=head;
       k=k%length;
       int stepsToNewHead= length-k;
       Node newTail=head;
       for(int i=1;i<stepsToNewHead;i++){
           newTail=newTail.next;
       }
       Node newHead=newTail.next;
       newTail.next=null;
       return newHead;
    }
    public static void display(Node head) {
        Node current = head;
        System.out.print("LinkedList: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Node head = null, tail = null;
        int n = scanner.nextInt();
        for (int i = 0; i < n; i++) {
            Node newNode = new Node(scanner.nextInt());
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        int k = scanner.nextInt();
        head = rotate(head, k);
        display(head);
        scanner.close();
    }
}
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```
Developed by: B. Mahalakshmi 

Reg No: 212224040182
## Output:
<img width="836" height="216" alt="image" src="https://github.com/user-attachments/assets/64649cc4-fe76-479b-84bd-3238923de0a3" />

## Result:
Thus, the Java program to perfom right rotation on linked list is implemented successfully.
