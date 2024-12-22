# LinkedList Based Questions

## 1. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

### Problem

- Given `head`, the head of a linked list, determine if the linked list has a cycle in it. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.

- Example 1:

![alt text](image.png)

```
Input: head = [3,2,0,-4]
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

- Example 2:

![alt text](image-1.png)

```
Input: head = [1,2]
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```

### Constraints

- The number of the nodes in the list is in the range [0, 10<sup>4</sup>].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>

### Solution

#### 1. Replacing Node Values

- In this solution, we will be replacing node value by an infinity value, higher+1(10<sup>5</sup>+1) or lower-1 (-10<sup>5</sup>-1) value. While iterating over each node, we will be replacing the node value by one of above values, if the `LinkedList` is cyclic we may encounter with the replaced value.
- Python

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        while(head):
            if(head.val==10**5+1):
                return True
            head.val=10**5+1
            head=head.next
        return False
```

- Java

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null){
            return false;
        }
        while(head.next!=null){
            if(head.val==(Math.pow(10, 5)+1)){
                return true;
            }
            head.val=(int)Math.pow(10,5)+1;
            head=head.next;
        }
        return false;
    }
}
```

#### 2. Tortoise and Hare algorithm OR Floyd’s cycle finding algorithm (Two Pointer Approach)

- The idea is to start with the two pointers slow and fast, both starting at the head of the linked list.
- While traversing the List:
    - slow pointer will move one step at a time.
    - fast pointer moves two steps at a time.
    - If there’s a cycle, the fast pointer will eventually catch up with the slow pointer within the cycle because it’s moving faster.
    - If there’s no cycle, the fast pointer will reach the end of the list (i.e., it will become NULL).
- When the slow and fast pointers meet, a cycle or loop exists.
- Here, basically consider two pointer, one moves at a slowest pace (tortoise) and one moves at a fastest pace (hare). So in a circular track, when tortoise and hare starts their race, they gonna get align at one point of time.

<video controls src="Images\LinkedList\2024-1.mp4" title="title"> </video>

- Same concepts works to find out whether a linked list is cyclic or not. We will be having two pointers, the slowest pointer will iterate node by node, and the faster pointer will jump to alternates nodes. Thus when the fastest and the slowest pointer points the same node, we conclude the linked list is circular.
- Python

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True

        return False
```

- Java

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) {
            return false;
        } 
        ListNode fastest = head.next;
        ListNode slowest = head;
        while (fastest != null) {
            if (fastest == slowest) {
                return true;
            }
            if (fastest.next == null) {
                return false;
            }
            fastest = fastest.next.next;
            slowest = slowest.next;
        }
        return false;
    }
}
```

## 2. [Happy Number](https://leetcode.com/problems/happy-number/description/)

### Problem

- Write an algorithm to determine if a number `n` is happy. A happy number is a number defined by the following process:
    - Starting with any positive integer, replace the number by the sum of the squares of its digits.
    - Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
    - Those numbers for which this process ends in 1 are happy.
    - Return `true` if `n` is a happy number, and `false` if not.
- Example 1:

```
Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

- Example 2:

```
Input: n = 2
Output: false
```

### Constraints

- 1 <= `n` <= 2<sup>31</sup> - 1

### Solution

#### 1. Tortoise and Hare algorithm OR Floyd’s cycle finding algorithm (Two Pointer Approach)

- The idea is to start with the two pointers slow and fast, both starting at the head of the linked list.
- While traversing the List:
    - slow pointer will move one step at a time.
    - fast pointer moves two steps at a time.
    - If there’s a cycle, the fast pointer will eventually catch up with the slow pointer within the cycle because it’s moving faster.
    - If there’s no cycle, the fast pointer will reach the end of the list (i.e., it will become NULL).
- When the slow and fast pointers meet, a cycle or loop exists.
- Here, basically consider two pointer, one moves at a slowest pace (tortoise) and one moves at a fastest pace (hare). So in a circular track, when tortoise and hare starts their race, they gonna get align at one point of time.

<video controls src="Images\LinkedList\2024-1.mp4" title="title"> </video>

- Same concepts works to find out whether a the number is happy or not. When a number is not happy, the sum of squares of digit will always land up to the initial number it was or one of its following generated value, consider below example of unhappy number

```
4→16→37→58→89→145→42→20→4 (a cyclic loop)
```

- So here, we will have two pointers, the slowest pointer will normally compute sum of square of digit in each of it iterations, whereas the fastest pointer will compute sum of square of digit, one step ahead of the slowest pointer
- Example

```
Slowest Pointer
4→16→37→58→89→145→42→20→4

Fastest Pointer
4→37→89→42→4
```

- At one point of them, if the number is unhappy (cyclic detection), it will coincide with the same number of one of the generated number.
- Python

```
class Solution(object):
    def getSumOfSquaresOfDigit(self,n):
        s=0
        while(n):
            d=n%10
            s+=d*d
            n=n//10
        return s

    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        slow=fast=n
        while(True):
            slow=self.getSumOfSquaresOfDigit(slow)
            fast=self.getSumOfSquaresOfDigit(self.getSumOfSquaresOfDigit(fast))
            if(slow==1 or fast==1):
                return True
            if(slow==fast):
                return False
```

- Java

```
class Solution {
    public double getSumOfSquaresOfDigit(double n){
        double s=0;
        double d=0;
        while(n>0){
            d=n%10;
            s+=(d*d);
            n=(int)n/10;
        }
        return s;
    }

    public boolean isHappy(int n) {
        double slow=n;
        double fast=n;
        while(true){
            slow=getSumOfSquaresOfDigit(slow);
            fast=getSumOfSquaresOfDigit(getSumOfSquaresOfDigit(fast));
            if(slow==1 || fast==1){
                return true;
            }
            if(slow==fast){
                return false;
            }
        }
    }
}
```