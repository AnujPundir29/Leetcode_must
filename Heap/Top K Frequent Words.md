### [692\. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)

Difficulty: **Medium**  

Related Topics: [Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Trie](https://leetcode.com/tag/trie/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Bucket Sort](https://leetcode.com/tag/bucket-sort/), [Counting](https://leetcode.com/tag/counting/)


Given an array of strings `words` and an integer `k`, return _the_ `k` _most frequent strings_.

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.

**Example 1:**

```
Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2:**

```
Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Constraints:**

*   `1 <= words.length <= 500`
*   `1 <= words[i] <= 10`
*   `words[i]` consists of lowercase English letters.
*   `k` is in the range `[1, The number of **unique** words[i]]`

**Follow-up:** Could you solve it in `O(n log(k))` time and `O(n)` extra space?


#### Solution

Language: **C++**

```c++
class Solution {
public:
    struct comp{
    bool operator()(const pair<int,string> &a,const pair<int,string> &b)
    {
        // sort acc to the freq(high to low) if same then on lexicographical order
        return a.first==b.first? (a.second>b.second):(a.first<b.first);
    }
    };
    vector<string> topKFrequent(vector<string>& words, int k) {
        
        unordered_map<string,int> mp;
        for(auto i:words)
            mp[i]++;
        
        priority_queue<pair<int,string> ,vector< pair<int,string> >,comp>pq;
        
        for(auto i:mp)
        {
            pq.push({i.second,i.first});
        }
        vector<string> res;
        while(!pq.empty() and k--)
        {
            res.push_back(pq.top().second);
            pq.pop();
        }
        
        return res;
            
    }
};
```
