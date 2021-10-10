### [240\. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

Difficulty: **Medium**  

Related Topics: [Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Matrix](https://leetcode.com/tag/matrix/)


Write an efficient algorithm that searches for a `target` value in an `m x n` integer `matrix`. The `matrix` has the following properties:

*   Integers in each row are sorted in ascending from left to right.
*   Integers in each column are sorted in ascending from top to bottom.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false
```

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= n, m <= 300`
*   `-10<sup>9</sup> <= matrix[i][j] <= 10<sup>9</sup>`
*   All the integers in each row are **sorted** in ascending order.
*   All the integers in each column are **sorted** in ascending order.
*   `-10<sup>9</sup> <= target <= 10<sup>9</sup>`


#### Solution

Language: **C++**

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& arr, int target) {
        int n=arr.size(),m=arr[0].size(),p1=0,p2=m-1;
        
        //move from top right corner
        while(p1<n and p2>=0)
        {
            if(arr[p1][p2]==target) return true;
            
            if(arr[p1][p2]>target)   // if cur number is more than target then go left
            {
                p2--;
            }
            else        //else go down
                 p1++;
        }
        return false;
    }
};
```
