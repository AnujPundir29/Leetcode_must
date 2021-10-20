### [380\. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Math](https://leetcode.com/tag/math/), [Design](https://leetcode.com/tag/design/), [Randomized](https://leetcode.com/tag/randomized/)


Implement the `RandomizedSet` class:

*   `RandomizedSet()` Initializes the `RandomizedSet` object.
*   `bool insert(int val)` Inserts an item `val` into the set if not present. Returns `true` if the item was not present, `false` otherwise.
*   `bool remove(int val)` Removes an item `val` from the set if present. Returns `true` if the item was present, `false` otherwise.
*   `int getRandom()` Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the **same probability** of being returned.

You must implement the functions of the class such that each function works in **average** `O(1)` time complexity.

**Example 1:**

```
Input
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
Output
[null, true, false, true, 2, true, false, 2]

Explanation
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomizedSet.remove(2); // Returns false as 2 does not exist in the set.
randomizedSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomizedSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomizedSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomizedSet.insert(2); // 2 was already in the set, so return false.
randomizedSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
```

**Constraints:**

*   `-2<sup>31</sup> <= val <= 2<sup>31</sup> - 1`
*   At most `2 * ``10<sup>5</sup>` calls will be made to `insert`, `remove`, and `getRandom`.
*   There will be **at least one** element in the data structure when `getRandom` is called.


#### Solution

Language: **C++**

```c++
class RandomizedSet {
public:
    unordered_map<int,int> s;  // stores the current value as keys and values as there position in vector
    int pos;  //position variable stores position where the current variable is stored in vector
    vector<int> vec;   //stores the current values
    RandomizedSet() {
        s.clear();
        pos=0;
        vec.clear();
    }
    
    bool insert(int val) { // according to the statement
        if(s.find(val)!=s.end())
        {
            return false;
        }
        s.insert({val,pos++});
        vec.push_back(val);
        return true;
    }
    
    bool remove(int val) {
        if(s.find(val)!=s.end()) //if found 
        {
            int p=s[val]; // get the position of variable in vector 
            int n=vec.size()-1;
            s[vec[n]]=p;    // change the position of last variable as the current value to be deleted position
            swap(vec[n],vec[p]); // swap the to be deleted variable with the last value to delete in o(1)
            vec.pop_back();
            s.erase(val);
            pos--; // dec the position
            return true;
        }
        return false;
    }
    
    int getRandom() {
        int r=rand() % vec.size();   // gives value in range of 0 to vec.size()-1
        return vec[r];
    }
};
/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
