### [146\. LRU Cache](https://leetcode.com/problems/lru-cache/)

Difficulty: **Medium**  

Related Topics: [Hash Table](https://leetcode.com/tag/hash-table/), [Linked List](https://leetcode.com/tag/linked-list/), [Design](https://leetcode.com/tag/design/), [Doubly-Linked List](https://leetcode.com/tag/doubly-linked-list/)


Design a data structure that follows the constraints of a .

Implement the `LRUCache` class:

*   `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
*   `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
*   `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

**Constraints:**

*   `1 <= capacity <= 3000`
*   `0 <= key <= 10<sup>4</sup>`
*   `0 <= value <= 10<sup>5</sup>`
*   At most 2` * 10<sup>5</sup>` calls will be made to `get` and `put`.


#### Solution

Language: **C++**

```c++
class LRUCache
{
    /*
    In this question we have to keep track of the most least recently used item in the cache. I have designed the cache using           list and map in C++.
    We do it by following the steps below :-
    When we access an item in the cache it moves to the front of the list as it is the most recently used item.
    When we want to remove an item we remove it from the last of the list as it is the least recently used item in the cache.
    When we insert an item we insert it into the front of the list as it is the most recently used item.
    The idea is to store the keys in the map and its corrosponding values into the list...
    Note : splice() function here takes the element at the m[key] and places it at the beginning of the list...
    */
    public:
        list<pair<int,int>> l;
        unordered_map<int,list<pair<int, int>>::iterator> m;  // 1 : {1,2}
        int size;
        LRUCache(int capacity)
        {
            size=capacity;
        }
        int get(int key)
        {
            if(m.find(key)==m.end())  //if not found return -1
                return -1;
            l.splice(l.begin(),l,m[key]);  // move the called key to front
            return m[key]->second;          // return the value to the particular key
        }
        void put(int key, int value)
        {
            // if already present then put the list iteretor to first place 
            if(m.find(key)!=m.end())
            {
                l.splice(l.begin(),l,m[key]);
                m[key]->second=value;
                return;
            }
            // if size if filled then remove last element as least freq and remove from map also
            if(l.size()==size)
            {
                auto d_key=l.back().first;
                l.pop_back();
                m.erase(d_key);
            }
            // push it into front as new/most freq
            l.push_front({key,value});
            // insert the iterator to map also
            m[key]=l.begin();
        }
        
};
​
```
