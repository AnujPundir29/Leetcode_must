### [21\. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

Difficulty: **Easy**  

Related Topics: [Linked List](https://leetcode.com/tag/linked-list/), [Recursion](https://leetcode.com/tag/recursion/)


Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

**Example 2:**

```
Input: l1 = [], l2 = []
Output: []
```

**Example 3:**

```
Input: l1 = [], l2 = [0]
Output: [0]
```

**Constraints:**

*   The number of nodes in both lists is in the range `[0, 50]`.
*   `-100 <= Node.val <= 100`
*   Both `l1` and `l2` are sorted in **non-decreasing** order.


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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *newHead;
        if(!l1)
        {return l2;}
        if(!l2) return l1;
        if(l1->val<l2->val) newHead=l1,l1=l1->next; //assign a new head with sortest value
        else newHead=l2,l2=l2->next;
        
        ListNode* cur=newHead;
        
        while(l1 and l2)
        {
            if(l1->val<l2->val)
            {
                cur->next=l1;
                cur=cur->next;
                l1=l1->next;
            }
            else
            {
                cur->next=l2;
                cur=cur->next;
                l2=l2->next;
            }
        }
        
        cur->next=(l1)? l1:l2;
        
        return newHead;
        
        
    }
};
```
