### [5\. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Difficulty: **Medium**  

Related Topics: [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)


Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```
Input: s = "a"
Output: "a"
```

**Example 4:**

```
Input: s = "ac"
Output: "a"
```

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    
    /*
        B   A   B   A   D   
    B   1   0   1   0   0   
    A   x   1   0   1   0   
    B   x   x   1   0   0   
    A   x   x   x   1   0   
    D   x   x   x   x   1   
​
    */
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<int>> dp(n,vector<int> (n,0)); // make a 2d dp array
​
    for (int g = 0; g < n; g++) { // traverse diagonally
        for (int i = 0, j = i + g; j < n; i++, j++) {
            if (i == j)     //  same character at same position
                dp[i][j] = 1;
​
            else if (i > j)         // in reverse continue
                continue;
​
            else if (i + 1 == j)            // only two character (bb)
                dp[i][j] = s[i] == s[j];
​
            else
                dp[i][j] = s[i] == s[j] and dp[i + 1][j - 1];  // more than two (bab) check adjacent and check for middle
        }
    }
    
    int st=0,maxi=1;
​
        
    // go on each row and check for max dist between two 1 and that is longest palindromic substring
    for (int i = 0; i < n; i++) {
        int pos = -1;
        for (int j = i; j < n; j++) {
            if (dp[i][j]) {
                if (pos == -1)
                    pos = j;
                else
                 {
                     if(maxi<(j-pos+1))
                     {
                         maxi=j-pos+1;
                         st=pos;
                     }
                 }
            }
        }
    }
        string res(s.begin()+st,s.begin()+st+maxi);  //return the final string
        return res;
    }
};
```
