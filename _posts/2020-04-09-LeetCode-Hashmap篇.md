---
title:      LeetCode中HashMap例题
subtitle:   hashmap在python中的应用(dict)
date:       2020-04-09
author:     William Song
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Algorithm
---

# LeetCode No 15 Question：3Sum

The question is from  LeetCode No 15 Question：3Sum

### Desrciption

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

### Analysis

题目中需要找出三个数 a,b,c 并满足 a+b+c = 0.那么可以先循环找出 a,b 接下来c便可以用 0 - a - b 来表示。 为了减少时间复杂度，可以先将数组排序，接下来通过两个pointer一个从左，一个从右开始遍历数组。 在遍历的时候，当我们第一次得到正数的时候，这个正数后面2个数必然为正数（数组以及排序），那么我们可以直接break，因为无论怎样这三个数或者再往后都无法相加等于0。

### Code
 

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        
        used = set()  # 避免重复使用
        
        nums.sort()
        n = len(nums)
        solution = []
        for i in range(n-2): 
            if nums[i] > 0:     # 如果遇见大于0的可以直接跳过，因为后面都会大于0 
            
                break	
            if nums[i] in used: # 防止重复
            
                continue	
            used.add(nums[i])
            prev = i+1   #左pointer 

            last = n-1   #右pointer
             
            while prev!=last :
                c = nums[i] + nums[prev] +nums[last]
                if c<0:  prev+=1 # 如果c<0证明左边太小，右pointer往右移动
                    
                elif c>0: last-=1# 如果c>0证明右边太大，右pointer向左移动
                    
                else:     # c=0符合条件
                
                    answer = [nums[i],nums[prev],nums[last]]
                    if not solution:
                        solution.append(answer)  
                    elif solution[-1]!=answer:  solution.append(answer) #防止结果重复
                        
                    prev+=1
        return solution
```
### Another Version 3Sum Closest
Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

### Analysis for 3Sum Closest
题目中给出一个目标值，在数组找出三个整数相加与目标值最接近，此题与上一个题非常相似，有一个小不同就是此题可以使用重复元素因此我们不需要加used这一个list去判定是否重复出现。那为了找出最接近的值，我们首先可以想到数值之间的距离那当然就是绝对值了。于是我们可以用差的绝对值算出距离最终找到离目标值最近的数。

### Code for 3Sum Closest
```python
    class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        
        closest = nums[0]+nums[1]+nums[2]
       
        nums.sort()
        
        n = len(nums)
  
 
        for i in range(n-2):
           
                prev = i + 1
                
                last = n -1
                
                while prev < last:
                
                    c = nums[prev] + nums[last] + nums[i]
                    
                    if abs(c - target) < abs(closest-target):
                    
                        closest = c
                    
                    if c < target:
                    
                        prev += 1
                        
                    elif c>target:
                    
                        last -= 1
                        
                    else:
                    
                        return closest
                        
        return closest
```
