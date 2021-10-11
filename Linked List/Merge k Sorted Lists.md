### [23\. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

Difficulty: **Hard**  

Related Topics: [Linked List](https://leetcode.com/tag/linked-list/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Merge Sort](https://leetcode.com/tag/merge-sort/)


You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

**Example 2:**

```
Input: lists = []
Output: []
```

**Example 3:**

```
Input: lists = [[]]
Output: []
```

**Constraints:**

*   `k == lists.length`
*   `0 <= k <= 10^4`
*   `0 <= lists[i].length <= 500`
*   `-10^4 <= lists[i][j] <= 10^4`
*   `lists[i]` is sorted in **ascending order**.
*   The sum of `lists[i].length` won't exceed `10^4`.


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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<pair<int,ListNode*>,vector<pair<int,ListNode*>>,greater<pair<int,ListNode*>> > pq;
        ListNode *head=NULL,*cur;
​
        for(int i=0;i<lists.size();i++)
        {
            if(lists[i])
                pq.push({lists[i]->val,lists[i]});  // put the first element and the ref to the node in a priority queue
        }
        if (pq.empty()) {
            return NULL;
        }
​
​
        while(!pq.empty())
        {
​
            int value=pq.top().first;   // get the value at first node which is smallest
            ListNode *ref=pq.top().second;  // get the reference 
​
            pq.pop();
            if(head==NULL)  // first node
            {
                head=ref;
                cur=head;
            }
            else        // store the cur.next
            {
                cur->next=ref;
                cur=cur->next;
            }
            if(ref->next)
                pq.push({ref->next->val,ref->next});    // only store when next is not null
        }
        cur->next=NULL;
​
        return head;
        
    }
```
