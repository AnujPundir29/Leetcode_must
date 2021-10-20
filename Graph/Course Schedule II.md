### [210\. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

Difficulty: **Medium**  

Related Topics: [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Topological Sort](https://leetcode.com/tag/topological-sort/)


There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a<sub style="display: inline;">i</sub>, b<sub style="display: inline;">i</sub>]` indicates that you **must** take course `b<sub style="display: inline;">i</sub>` first if you want to take course `a<sub style="display: inline;">i</sub>`.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses_. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0\. So the correct course order is [0,1].
```

**Example 2:**

```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2\. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```

**Example 3:**

```
Input: numCourses = 1, prerequisites = []
Output: [0]
```

**Constraints:**

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
*   `prerequisites[i].length == 2`
*   `0 <= a<sub style="display: inline;">i</sub>, b<sub style="display: inline;">i</sub> < numCourses`
*   `a<sub style="display: inline;">i</sub> != b<sub style="display: inline;">i</sub>`
*   All the pairs `[a<sub style="display: inline;">i</sub>, b<sub style="display: inline;">i</sub>]` are **distinct**.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    vector<int> findOrder(int n, vector<vector<int>>& pre) {
        vector<int> in(n,0);
        vector<int> res;
        vector<vector<int>> g(n);
        
        for(auto i:pre)
        {
            g[i[1]].push_back(i[0]);
            in[i[0]]++;
        }
        queue<int> q;
        
        for(int i=0;i<in.size();i++)
            if(in[i]==0)
                q.push(i);
        while(!q.empty())
        {
            int cur=q.front();
            q.pop();
            
            res.push_back(cur);
            
            for(auto i:g[cur])
            {
                in[i]--;
                if(in[i]==0)
                    q.push(i);
            }
        }
        
        return res.size()!=n? vector<int>{}:res;
    }
};
​
```
