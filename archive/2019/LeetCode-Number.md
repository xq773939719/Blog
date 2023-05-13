---
title: LeetCode-Number
categories: [算法]
tags: [算法,C++,数据结构]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2019-02-01 20:56:54
updated: 2019-02-01 20:56:54
keywords:
description: LeetCode数学专题。
passwords:
img:


---

给定一个正整数，输出它的补数。补数是对该数的二进制表示取反。

注意:

给定的整数保证在32位带符号整数的范围内。
你可以假定二进制数不包含前导零位。
示例 1:

输入: 5
输出: 2
解释: 5的二进制表示为101（没有前导零位），其补数为010。所以你需要输出2。
示例 2:

输入: 1
输出: 0
解释: 1的二进制表示为1（没有前导零位），其补数为0。所以你需要输出0。
``` cpp
class Solution {
public:
    int findComplement(int num) {
        stack<int> s;
        while(num){
           s.push(num%2);
            num /= 2;
        }
        int res = 0;
        while(!s.empty()){
            res += s.top() == 1 ? 0 : 1;
            s.pop();
            if(!s.empty())res *= 2;
        }
        return res;
    }
};
```
执行用时: 4 ms, 在Number Complement的C++提交中击败了92.08% 的用户