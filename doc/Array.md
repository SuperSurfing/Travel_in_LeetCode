#### Absract   

&emsp;&emsp;本文主要介绍 **Array - Tag** 相关的 LeetCode 问题的解题方法。

- [Maximum Subarray](#maximum_subarray)
- 


### Maximum_Subarray

#### Thinking
&emsp;&emsp;很明显，这个问题的题目中已经包含了“**Subarray**”这类“**问题与子问题**”的词汇，我们首先想到的应该是用 **递归算法**（Recursive Algorithm）去试试。  
&emsp;&emsp;递归算法最重要的是找到“**问题与子问题**”的递归关系（Recursive Relation），而本题的递归关系很不明显，它依赖于“如何定义**子问题**”。  
&emsp;&emsp;思路一：将子问题定义为数组中任意子数组（子区间）的和，即 SumOfSubarray(int [] A, int low, int high)或 f(i,j)，然后再找出其中的最大者。这是最容易想到的一种划分方法，而且 f(i, j) 的定义比较简单，就是求对应区间元素的和。但是，它的缺点有两个：一是子问题的数量很多，它是任意两个下标的组合。二是子问题的划分不是线性的，子区间交织在一起。  
&emsp;&emsp;思路二：将子问题定义为以第i个元素结尾的子数组的最大和（**求每个子区间的最优**），maxSumOfSubarray(int [] A, int high) 或 f(i)。这样划分，主要是避免子区间交织在一起，使得子问题与父问题相似而规模缩小。换句话说，这个思路就是“**线性划分子区间，求出每个子区间的最优，最后再优中取优**”。

#### Solution
&emsp;&emsp;根据思路二，我们可以很容易得到如下的递归公式（参考《剑指offer》）

```math
f(i)=\left\{\begin{matrix}
A[i] & i =0  \;or\; f(i-1) \leq 0\\ 
 f(i-1) + A[i]& f(i-1) > 0
\end{matrix}\right.
```

&emsp;&emsp;如上面的公式，问题被划分为一个规模更小的问题和一个平凡的问题，递归函数的代码如下：


```
class Solution {
public:
    int maxSumOfSubarray(vector<int>& nums, int i) {
        if (i == 0)
            return nums[i];
        
        int prev = maxSumOfSubarray(nums, i -1);     
        return  prev > 0 ? prev + nums[i] : nums[i];
    }
    
    int maxSubArray(vector<int>& nums) {
        if (nums.empty())
            throw "input array is empty";
            
        int n = nums.size();
        int max = nums[0];
        for (int i = 1; i < n; ++i) {
            int sum = maxSumOfSubarray(nums, i);
            if ( sum > max)
                max = sum;
        }
        
        return max;
    }
};
```

&emsp;&emsp;分析这个递归算法，它包含了很多重复的**递归实例**，极大地消耗了算法的性能，我们可以把它改为迭代算法，此外，就是优中取优，找出所有子问题中的最优者，这就是**动态规划**（Dynamic Programming）。  

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if (nums.empty())
            throw "input array is empty";
        
        int n = nums.size();
        int nCurrSum = nums[0];
        int max = nCurrSum;
        
        for (int i = 1; i < n; ++i) {
            nCurrSum = nCurrSum > 0 ? nCurrSum + nums[i] : nums[i];
            
            if (nCurrSum > max)
                max = nCurrSum;
        }
        
        return max;
    }
};
```
