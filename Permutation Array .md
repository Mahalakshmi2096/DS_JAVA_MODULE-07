# Ex9 Finding the Longest Length of Nested Set in a Permutation Array
## DATE: 09.09.2025
## AIM:
To write a program that finds the length of the longest set s[k] defined as s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … },where the iteration stops before a duplicate element occurs.

The task is to return the maximum size among all such sets.
## Algorithm
1. Create a visited array of size n, initialized to false.
2. Set maxSize = 0.
3. Loop through each index i in the array:
4. If i is not visited:
5. Start a counter at 0.
6. Follow the chain: go to nums[i], mark visited, increase count, repeat until you return to a visited index.
7. Update maxSize with the maximum count found.
8. After checking all indices, return maxSize.   

## Program:
```
import java.util.*;

public class ArrayNestingMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine().trim();
        input = input.replace("nums =", "").replace("[", "").replace("]", "").trim();
        String[] parts = input.split(",");
        int[] nums = new int[parts.length];

        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }
        Solution sol = new Solution();
        int result = sol.arrayNesting(nums);
        System.out.println(result);
        sc.close();
    }
}
class Solution {
    public int arrayNesting(int[] nums) {
        boolean[] visited = new boolean[nums.length];
        int maxSetSize = 0;
        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                int start = i;
                int count = 0;
                while (!visited[start]) {
                    visited[start] = true;
                    start = nums[start];
                    count++;
                }
                maxSetSize = Math.max(maxSetSize, count);
            }
        }
        return maxSetSize;
    }
}
```
Developed by: Mahalakshmi B

Reg No: 212224040182
## Output:
<img width="641" height="161" alt="image" src="https://github.com/user-attachments/assets/f7646b3c-aa7a-418d-8065-7abd9965cc74" />

## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.
