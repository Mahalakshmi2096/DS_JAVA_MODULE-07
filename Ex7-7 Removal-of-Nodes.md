# Ex7 Removal of Nodes with a Specific Value from a Linked List
## DATE: 08.09.2025
## AIM:
To write a java  program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm
1. Create a dummy node pointing to the head of the list.
2. Set a pointer current to the dummy node.
3. While current.next is not null:
4. If current.next.val equals the target value, skip the node by linking current.next to current.next.next.
5. Otherwise, move current to current.next.
6. Return dummy.next (new head of the updated list). 

## Program:
```
import java.util.*;
public class RemoveElementsDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();
        
        String[] input = sc.nextLine().split("\\s+");
        int[] nums = new int[input.length];

        for (int i = 0; i < input.length; i++) {
            nums[i] = Integer.parseInt(input[i]);
        }
        int val = sc.nextInt();

        ListNode head = sol.buildList(nums);
        ListNode result = sol.removeElements(head, val);
        sol.printListAsArray(result);

        sc.close();
    }
}

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

class Solution {
    // Function to remove all occurrences of val
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode current = dummy;

        while (current.next != null) {
            if (current.next.val == val) {
                current.next = current.next.next; // skip node
            } else {
                current = current.next;
            }
        }
        return dummy.next;
    }
    // Helper: build linked list from array
    public ListNode buildList(int[] nums) {
        if (nums.length == 0) return null;
        ListNode head = new ListNode(nums[0]);
        ListNode current = head;
        for (int i = 1; i < nums.length; i++) {
            current.next = new ListNode(nums[i]);
            current = current.next;
        }
        return head;
    }
    // Helper: print linked list as array format
    public void printListAsArray(ListNode head) {
        List<Integer> list = new ArrayList<>();
        while (head != null) {
            list.add(head.val);
            head = head.next;
        }
        System.out.println(list);
    }
}
```
Developed by: Mahalakshmi B

Reg No: 212224040182
## Output:
<img width="569" height="247" alt="image" src="https://github.com/user-attachments/assets/b1c1a509-5401-4c64-bbc1-55a111d71778" />

## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.
