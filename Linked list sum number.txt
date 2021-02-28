### [2\. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

Difficulty: **Medium**  

Related Topics: [Linked List](https://leetcode.com/tag/linked-list/), [Math](https://leetcode.com/tag/math/), [Recursion](https://leetcode.com/tag/recursion/)


You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:**

*   The number of nodes in each linked list is in the range `[1, 100]`.
*   `0 <= Node.val <= 9`
*   It is guaranteed that the list represents a number that does not have leading zeros.


#### Solution

Language: **C++**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry=0;
        ListNode *l3=new ListNode(),*cur=l3;
        
        while(l1 or l2)
        {
            if(l1 and l2){
            int sum=l1->val+l2->val;
            cur->next=new ListNode((sum+carry)%10);
            carry=(sum+carry)/10;
            l1=l1->next;
            l2=l2->next;
            }
            else if(l1)
            {
               cur->next=new ListNode((carry+l1->val)%10);
                carry=(carry+l1->val)/10;
                l1=l1->next;
            }
            else{
                cur->next=new ListNode((carry+l2->val)%10);
                carry=(carry+l2->val)/10;
                        l2=l2->next;}
​
                        cur=cur->next;
        }
        if(carry)
            cur->next=new ListNode(carry);
        return l3->next;
    }
};
```