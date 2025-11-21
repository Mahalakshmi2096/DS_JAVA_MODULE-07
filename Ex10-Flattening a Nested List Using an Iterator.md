# Flattening a Nested List Using an Iterator
## DATE: 08.09.2025
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1. Flatten a Multilevel Doubly Linked List
2. If the head is NULL, return NULL.
3. Create an empty stack.
4. Set current = head.
5. While current is not NULL:
6. If current has a child:
7. If current.next exists, push it onto the stack.
8. Link current.next to current.child and set child's prev back to current.
9. Set current.child to NULL.
10. Else if current.next is NULL and stack is not empty:
11. Pop a node from the stack and connect it as current.next.
12. Set popped node's prev to current.
13. Move current to current.next.
14. Return head of the list.  

## Program:
```
import java.util.*;
class Node {
    int val;
    Node prev;
    Node next;
    Node child;

    Node(int val) {
        this.val = val;
    }
}
class Solution {
    public Node flatten(Node head) {
        //Type your code here
         if (head == null) return null;
        flattenDFS(head);
        return head;
    }
    // Helper function: returns the tail after flattening
    private Node flattenDFS(Node node) {
        Node current = node;
        Node last = null;
        while (current != null) {
            Node next = current.next;
            // If the current node has a child, flatten it
            if (current.child != null) {
                Node childHead = current.child;
                Node childTail = flattenDFS(childHead);
                // Connect current -> childHead
                current.next = childHead;
                childHead.prev = current;
                // Connect childTail -> next
                if (next != null) {
                    childTail.next = next;
                    next.prev = childTail;
                }
                // Remove child pointer
                current.child = null;
                last = childTail;
            } else {
                last = current;
            }
            current = next;
        }
        return last;
    }
}
public class Main {
    public static Node parseInput(String input) {
        input = input.replaceAll("\\[|\\]", "").trim();
        if (input.isEmpty()) return null;
        String[] tokens = input.split(",");
        List<Node> nodes = new ArrayList<>();
        for (String token : tokens) {
            token = token.trim();
            if (token.equals("null")) {
                nodes.add(null);
            } else {
                nodes.add(new Node(Integer.parseInt(token)));
            }
        }
        Node head = null, prev = null;
        List<Node> parents = new ArrayList<>();
        int i = 0;
        while (i < nodes.size()) {
            Node curr = nodes.get(i++);
            if (curr == null) {
                if (!parents.isEmpty()) {
                    Node parent = parents.remove(0);
                    Node childHead = null, childPrev = null;
                    while (i < nodes.size() && nodes.get(i) != null) {
                        Node child = nodes.get(i++);
                        if (childHead == null) childHead = child;
                        if (childPrev != null) {
                            childPrev.next = child;
                            child.prev = childPrev;
                        }
                        childPrev = child;
                    }
                    parent.child = childHead;
                }
                continue;
            }
            if (head == null) head = curr;
            if (prev != null) {
                prev.next = curr;
                curr.prev = prev;
            }
            prev = curr;
            parents.add(curr);
        }
        return head;
    }
    public static void printFlattened(Node head) {
        List<Integer> result = new ArrayList<>();
        while (head != null) {
            result.add(head.val);
            head = head.next;
        }
        System.out.println(result);
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        Node head = parseInput(input);
        Solution solution = new Solution();
        Node flat = solution.flatten(head);
        printFlattened(flat);
    }
}
```
Developed by : Mahalakshmi B

Reg No : 212224040182
## Output:
<img width="1236" height="231" alt="image" src="https://github.com/user-attachments/assets/08bf3179-70a3-49b2-aad4-21de4422cf5d" />

## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
