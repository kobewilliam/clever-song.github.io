---
title:      LeetCode中Backtrack例题
subtitle:   Backtrack在python中的应用(dict)
date:       2020-04-10
author:     William Song
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Algorithm(medium)
---

# LeetCode No 17 Question :Letter Combinations of a Phone Number

### Description
![题目](img/backtrack-phone.png)

### Analysis
此题目中，给我们一个串数字，一个数字代表着3或4个字母，我们需要从第一个数字中代表的第一个字母开始往后去和后一个数字代表的每个字母两两结合。因为一个数字代表着几个字母，所以我们很容易想到在python用dict去存储这些。如：

                 digital_map = {'2':['a','b','c'],
                                '3':['d','e','f'],
                                '4':['g','h','i'],
                                '5':['j','k','l'],
                                '6':['m','n','o'],
                                '7':['p','q','r','s'],
                                '8':['t','u','v'],
                                '9':['w','x','y','z']}
因为当我们第一个数字对应所有字母匹配完后，我们将会用第二个数字对应的所有字母去对应后面的。最简单的方法就是写三个循环，知道对应到最后一个，但是这种方法他的时间空间复杂度太大，不符合我们的应用。所以我们可以采用backtrack的方法。当我们用一个函数找完第一个数字对应所有字母与后面数字对应所有字母的匹配之后，我们可以再次调用这个函数，并把下一个数字对应的字母当成开头，去匹配接下来的组合。

### Code
```python
    class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        
        digital_map = {'2':['a','b','c'],
                       '3':['d','e','f'],
                       '4':['g','h','i'],
                       '5':['j','k','l'],
                       '6':['m','n','o'],
                       '7':['p','q','r','s'],
                       '8':['t','u','v'],
                       '9':['w','x','y','z']}
        def backtrack(combination, next_digital):
            if len(next_digital) == 0:
                   out.append(combination) 
            else:
                   for letter in digital_map[next_digital[0]]:
                            backtrack(combination+letter, next_digital[1:])                          
         out = []        
         if digitals:       
            backtrack("", digitals)      
         return out
                   
```

                             
                          
