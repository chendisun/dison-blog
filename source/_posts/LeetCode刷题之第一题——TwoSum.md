title: LeetCode刷题之第一题——TwoSum
date: 2015-09-01 16:02:05
categories:
- 学习
tags:
- leetcodt
- java
---
## 原题目
> Given an array of integers, find two numbers such that they add up to a specific target number.

> The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

> You may assume that each input would have exactly one solution.

> Input: numbers={2, 7, 11, 15}, target=9
> Output: index1=1, index2=2

<!--more-->
--------------
## 原题网上翻译：
> 给定一个整数数组，找出其中两个数满足相加等于你指定的目标数字。
> 要求：这个函数twoSum必须要返回能够相加等于目标数字的两个数的索引，且index1必须要小于index2。请注意一点，你返回的结果（包括index1和index2）都不是基于0开始的。
> 你可以假设每一个输入肯定只有一个结果。

> 举例：
> 输入：numbers={2, 7, 11, 15}, target = 9
> 输出：index1 = 1, index2 = 2(不是基于0开始的)

## 解法
 这个解法是尝试多次相对较好的解法，显然还有更加好的解法。所以只供参考
```bash
import java.util.Hashtable;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
	Hashtable<Integer, Integer> ht = new Hashtable<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            Integer n = ht.get(nums[i]);
            if (n == null)
        	ht.put(nums[i], i);
            n = ht.get(target - nums[i]);
        	
            if (n != null && n < i) {
                result[0] = n + 1;
                result[1] = i + 1;
                
                return result;
            }
        }
        
        return result;
    }
}
```
