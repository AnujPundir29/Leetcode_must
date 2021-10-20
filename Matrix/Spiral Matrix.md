### [54\. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Matrix](https://leetcode.com/tag/matrix/), [Simulation](https://leetcode.com/tag/simulation/)


Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 10`
*   `-100 <= matrix[i][j] <= 100`


#### Solution

Language: **C++**

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n=matrix.size(),m=matrix[0].size(),t=0,d= -1,l=0,r=m-1;
        int dir=0;
        vector<int> res;
        while(t<=d and l<=r)
        {
            if(dir==0)
            {
                for(int i=l;i<=r;i++)
                {
                    res.push_back(matrix[t][i]);
                }
                t++;
                dir=1;
            }
            else if(dir==1)
            {
                for(int i=t;i<=d;i++)
                {
                    res.push_back(matrix[i][r]);
                }
                r--;
                dir=2;
            }
            else if(dir==2)
            {
                for(int i=r;i>=l;i--)
                {
                    res.push_back(matrix[d][i]);
                }
                d--;
                dir=3;
            }
            else if(dir==3)
            {
                for(int i=d;i>=t;i--)
                {
                    res.push_back(matrix[i][l]);
                }
                l++;
                dir=0;
            }
        }
        return res;
    }
};
```
