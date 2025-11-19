# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE: 08.09.2025
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1. Start
2. Input number of nodes n.
3. Initialize head = null, tail = null.
4. Repeat for i = 1 to n:
5. Read a data value.
6. Create a new node.
7. If list is empty:
8. Set head = tail = newNode.
9. Else: Link tail.next = newNode.
10. Update tail = newNode.
11. Input loop position pos.
12. If pos > 0:
13. Move a pointer from head to reach the pos-th node.
14. Set tail.next to that node (creates a loop).
15. Loop Detection (Floyd’s Cycle Detection)
16. If head is null or has only one node → no loop.
17. Set:  slow = head, fast = head.next
18. Repeat while slow != fast:
19. If fast is null or fast.next is null: No loop, stop.
20. Move slow one step forward.
21. Move fast two steps forward.
22. If slow == fast, then loop detected.
## Program:
```
import java.util.Scanner;
public class DetectLoopFloyd {
    public static boolean hasLoop(Node head) {
       //Type your code here
       if(head==null || head.next==null){
           return false;
       }
       Node slow = head;
       Node fast=head.next;
       while(slow!=fast){
           if(fast==null ||  fast.next==null){
               return false;
           }
           slow=slow.next;
           fast=fast.next.next;
       }
       return true;
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
        int pos = scanner.nextInt();
        if (pos > 0) {
            Node loopNode = head;
            for (int i = 1; i < pos && loopNode != null; i++) {
                loopNode = loopNode.next;
            }
            if (loopNode != null) {
                tail.next = loopNode;
            }
        }
        if (hasLoop(head)) {
            System.out.println("Loop detected in the LinkedList.");
        } else {
            System.out.println("No loop detected in the LinkedList.");
        }
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
<img width="922" height="203" alt="image" src="https://github.com/user-attachments/assets/d61f01c8-71a1-4c59-b561-56a2d47729fe" />

## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.
