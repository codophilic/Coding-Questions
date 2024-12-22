# LinkedList Based Questions

## 1. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

### Problem

- Given `head`, the head of a linked list, determine if the linked list has a cycle in it. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.

- Example 1

![alt text](image.png)

```
Input: head = [3,2,0,-4]
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

- Example 2

![alt text](image-1.png)

```
Input: head = [1,2]
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```

### Constraints

- The number of the nodes in the list is in the range [0, 10^4].
- -10^5 <= Node.val <= 10 ^5^

### Solution

#### 1. Replacing Node Values

- In this solution, we can replace the node values by 