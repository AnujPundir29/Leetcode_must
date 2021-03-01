### [42\. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

Difficulty: **Hard** 

### [Video](https://www.youtube.com/watch?v=m18Hntz4go8)

Related Topics: [Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Stack](https://leetcode.com/tag/stack/)


Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

**Constraints:**

*   `n == height.length`
*   `0 <= n <= 3 * 10<sup>4</sup>`
*   `0 <= height[i] <= 10<sup>5</sup>`


#### Solution

Language: **C++**

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int l=0,r=height.size()-1,res=0,lmax=0,rmax=0;
        
        while(l<r)
        {
            if(height[l]<=height[r])
            {
                if(height[l]<lmax)
                {
                    res+=lmax-height[l];
                }
                else
                {
                    lmax=height[l];
                }
                l++;
            }
            else
            {
                if(height[r]<rmax)
                {
                    res+=rmax-height[r];
                }
                else
                {
                    rmax=height[r];
                }
                r--;
            }
        }
        
        return res;
    }
};
```