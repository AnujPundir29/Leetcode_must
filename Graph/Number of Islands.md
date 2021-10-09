### [200\. Number of Islands](https://leetcode.com/problems/number-of-islands/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Matrix](https://leetcode.com/tag/matrix/)


Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 300`
*   `grid[i][j]` is `'0'` or `'1'`.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int n=grid.size(),m=grid[0].size(),count=0;
        int dr[4]={0,0,1,-1};
        int dc[4]={1,-1,0,0};
        
        queue<pair<int,int>> q;
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(grid[i][j]=='1') // fetch the land
                {
                    grid[i][j]='0'; // make it water 
                    count++; 
                    q.push({i,j});  
                    while(!q.empty()) 
                    {
                        auto p=q.front();
                        q.pop();
                        for(int k=0;k<4;k++)  // traverse all its neibhors
                        {
                            
                            int r=p.first+dr[k],c=p.second+dc[k];
                            
                            if(r>=0 and r<n and c>=0 and c<m and grid[r][c]=='1')  // if a neibhour is land
                            {
                                q.push({r,c});      // add to the queue
                                grid[r][c]='0';     // make it water
                            }
                        }
                    }
                }
            }
        }
        return count;
    }
};
```
