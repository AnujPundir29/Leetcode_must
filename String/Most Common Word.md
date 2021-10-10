### [819\. Most Common Word](https://leetcode.com/problems/most-common-word/)

Difficulty: **Easy**  

Related Topics: [Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/)


Given a string `paragraph` and a string array of the banned words `banned`, return _the most frequent word that is not banned_. It is **guaranteed** there is **at least one word** that is not banned, and that the answer is **unique**.

The words in `paragraph` are **case-insensitive** and the answer should be returned in **lowercase**.

**Example 1:**

```
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```

**Example 2:**

```
Input: paragraph = "a.", banned = []
Output: "a"
```

**Constraints:**

*   `1 <= paragraph.length <= 1000`
*   paragraph consists of English letters, space `' '`, or one of the symbols: `"!?',;."`.
*   `0 <= banned.length <= 100`
*   `1 <= banned[i].length <= 10`
*   `banned[i]` consists of only lowercase English letters.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
        string res;
        unordered_map<string, int> count;
        
        // Step 1: remove punctuations and change to lower case;
        for(auto &c : paragraph)
            c =  isalpha(c)? tolower(c) : ' '; 
        
        // Step 2: count the frequency of every word
        istringstream iss(paragraph);
        string lower_word;
        while(iss >> lower_word)
            ++count[lower_word];  
    
        // Step 3: set the frequency of banned word to zero
        for(auto b : banned) count[b] = 0; 
        
        // Step 4: get the word with highest frequency
        int max_count = 0;
        for(auto c : count){
            if(c.second > max_count){
                max_count = c.second;
                res = c.first;   
            }
        }
​
        return res;
        
        
    }
};
```
