### [1192\. Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/)

Difficulty: **Hard**  

Related Topics: [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Biconnected Component](https://leetcode.com/tag/biconnected-component/)


There are `n` servers numbered from `0` to `n - 1` connected by undirected server-to-server `connections` forming a network where `connections[i] = [a<sub style="display: inline;">i</sub>, b<sub style="display: inline;">i</sub>]` represents a connection between servers `a<sub style="display: inline;">i</sub>` and `b<sub style="display: inline;">i</sub>`. Any server can reach other servers directly or indirectly through the network.

A _critical connection_ is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png)

```
Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
```

**Example 2:**

```
Input: n = 2, connections = [[0,1]]
Output: [[0,1]]
```

**Constraints:**

*   `2 <= n <= 10<sup>5</sup>`
*   `n - 1 <= connections.length <= 10<sup>5</sup>`
*   `0 <= a<sub style="display: inline;">i</sub>, b<sub style="display: inline;">i</sub> <= n - 1`
*   `a<sub style="display: inline;">i</sub> != b<sub style="display: inline;">i</sub>`
*   There are no repeated connections.


#### Solution

Language: **C++**

```c++
class Solution {
public:
    
    void dfs(int source,vector<vector<int>> &adj,vector<int> &disc,vector<int> &low,vector<vector<int>> &res,vector<int> &parent)
    {
        static int time = 0;
        
        //when discovered time is eq to parent+1 
        disc[source]=low[source]=time;
        time++;
        
        // traverse every node of that source node        
        for(auto i:adj[source])
        {
            if(disc[i]==-1)  // not visited
            {
                parent[i]=source;  //assign the parent
                dfs(i,adj,disc,low,res,parent);
                
                //assign a new lowest time if i can be reach from a another back edge
                low[source]=min(low[source],low[i]);
                
                //check if it can be a bridge
                if(low[i]>disc[source])
                {
                    res.push_back({i,source});
                }
            }
            else if(i!=parent[source])
            {
                low[source]=min(low[source],disc[i]);
            }
        }
    }
    void findBridge(vector<vector<int>> &adj,vector<vector<int>> &res,int n)
    {
        //create three list(discovered, lowest time,parent node)
        vector<int> disc(n,-1),low(n,-1),parent(n,-1);
        
        //check for every node
```
