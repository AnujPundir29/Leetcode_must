### [994\. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)


You are given an `m x n` `grid` where each cell can have one of three values:

*   `0` representing an empty cell,
*   `1` representing a fresh orange, or
*   `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return _the minimum number of minutes that must elapse until no cell has a fresh orange_. If _this is impossible, return_ `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

**Example 2:**

```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
```

**Example 3:**

```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.
```

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 10`
*   `grid[i][j]` is `0`, `1`, or `2`.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        vector<int> d={0,1,0,-1,0};    // direction vector
        int days=0,tot=0,cur=0;
        queue<pair<int,int>> q;
        
        for(int i=0;i<grid.size();i++)
        {
            for(int j=0;j<grid[0].size();j++)
            {
                if(grid[i][j]!=0)   // total fresh and non fresh orange
                    tot++;
                
                if(grid[i][j]==2)
                {
                    q.push({i,j});   // get all rotten orange into queue
                }
            }
        }
        
        while(!q.empty())
        {
            int s=q.size();    
            cur+=s;             // calculate the count of rotten oranges
            while(s--)
            {
                auto p=q.front();
                q.pop();
                for(int i=0;i<4;i++)   // traverse through all neighbhour
                {
                    int r=p.first+d[i],c=p.second+d[i+1];
                    
                    if(r>=0 and r<grid.size() and c>=0 and c<grid[0].size() and grid[r][c]==1)
                    {
                        grid[r][c]=2;   // make a fresh orange rotten 
                        q.push({r,c});      // add it to queue
                    }
                }
            }
            if(!q.empty()) days++;      // calculate days required
        }   
        return tot==cur? days:-1;   //check if all oranges become rotten or not
            
    }
};
```
