### [973\. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Math](https://leetcode.com/tag/math/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Geometry](https://leetcode.com/tag/geometry/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Quickselect](https://leetcode.com/tag/quickselect/)


Given an array of `points` where `points[i] = [x<sub style="display: inline;">i</sub>, y<sub style="display: inline;">i</sub>]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x<sub style="display: inline;">1</sub> - x<sub style="display: inline;">2</sub>)<sup>2</sup> + (y<sub style="display: inline;">1</sub> - y<sub style="display: inline;">2</sub>)<sup>2</sup>`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation:
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```

**Example 2:**

```
Input: points = [[3,3],[5,-1],[-2,4]], k = 2
Output: [[3,3],[-2,4]]
Explanation: The answer [[-2,4],[3,3]] would also be accepted.
```

**Constraints:**

*   `1 <= k <= points.length <= 10<sup>4</sup>`
*   `-10<sup>4</sup> < x<sub style="display: inline;">i</sub>, y<sub style="display: inline;">i</sub> < 10<sup>4</sup>`


#### Solution

Language: **C++**

```c++
class Solution {
public:
    static bool comp(vector<int> &a,vector<int> &b)
    {
        int first=a[0]*a[0]+a[1]*a[1];
        int second=b[0]*b[0]+b[1]*b[1];
        
        return first<second;
    }
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        vector<vector<int>> res;
        sort(points.begin(),points.end(),comp);
        for(auto i:points)
        {
            if(k==0)    return res;
            k--;
            res.push_back(i);
        }
        return res;
    }
};
```
