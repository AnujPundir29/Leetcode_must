### [937\. Reorder Data in Log Files](https://leetcode.com/problems/reorder-data-in-log-files/)

Difficulty: **Easy**  

Related Topics: [Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Sorting](https://leetcode.com/tag/sorting/)


You are given an array of `logs`. Each log is a space-delimited string of words, where the first word is the **identifier**.

There are two types of logs:

*   **Letter-logs**: All words (except the identifier) consist of lowercase English letters.
*   **Digit-logs**: All words (except the identifier) consist of digits.

Reorder these logs so that:

1.  The **letter-logs** come before all **digit-logs**.
2.  The **letter-logs** are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
3.  The **digit-logs** maintain their relative ordering.

Return _the final order of the logs_.

**Example 1:**

```
Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
Explanation:
The letter-log contents are all different, so their ordering is "art can", "art zero", "own kit dig".
The digit-logs have a relative order of "dig1 8 1 5 1", "dig2 3 6".
```

**Example 2:**

```
Input: logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
Output: ["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
```

**Constraints:**

*   `1 <= logs.length <= 100`
*   `3 <= logs[i].length <= 100`
*   All the tokens of `logs[i]` are separated by a **single** space.
*   `logs[i]` is guaranteed to have an identifier and at least one word after the identifier.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    
    // Easy version N(logN)
    
    bool myCompare(string a, string b){
    int i = a.find(' ');
    int j = b.find(' ');
    if(!isdigit(a[i + 1]) && !isdigit(b[j + 1])) {
        if (a.substr(i + 1) == b.substr(j + 1)) return a < b;
        return a.substr(i + 1) < b.substr(j + 1);
    } else if (!isdigit(a[i + 1])) return true;
    return false;
    }
    vector<string> reorderLogFiles(vector<string>& logs) {
        stable_sort(logs.begin(), logs.end(), myCompare);
        return logs;
    }
    
    // My version

    vector<string> reorderLogFiles(vector<string>& logs) {
        map<string,set<string>> mp;
        vector<string> res,digit;
        
        for(auto i:logs)        //traverse all the logs
        {
            string temp="";
            for(int j=0;j<i.size();j++)  //traverse all char of a log
            {
                if(i[j]!=' ')
                {
                    temp+=i[j];
                }
                else        // if u got a first word
                {   
                    if(isdigit(i[j+1]))     // check if the char after space is digit
                    {
                        digit.push_back(i);     //store it in a simple vector(relative order)
                    }
                    else
                    {
                        string leftOver=i.substr(j,i.size()-j);     //else store the key as word which are stored to be sorted
                        mp[leftOver].insert(temp);
                    }
                    break;
                }
            }
        }
        
        for(auto i:mp)
        {
            for(auto j:i.second)
                res.push_back(j+i.first);
        }
        for(auto i:digit)
        {
            res.push_back(i);
        }
        return res;
        
    }
};
```
