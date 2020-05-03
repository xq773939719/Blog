---
title: LeetCode-String
categories: [算法]
tags: [算法,C++,数据结构]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2019-01-11 20:56:54
updated: 2019-01-11 20:56:54
keywords:
description: LeetCode字符串专题。
passwords:
img:
---

### ·整数反转

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例 1:

输入: 123
输出: 321
示例 2:

输入: -123
输出: -321
示例 3:

输入: 120
输出: 21
注意:

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231, 231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

------

```cpp
class Solution {
public:
    int reverse(int x) {
        queue<int> q;
        while(x != 0){
            q.push(x % 10);
            x /= 10;
        }
        int res = 0;
        while(!q.empty()){
            if((long)res * 10 + q.front() < -pow(2,31) || (long)res * 10 + q.front() > pow(2,31) -1) return 0;
            res = res * 10 + q.front();
            q.pop();
            
        }
        return res;
        
    }
};
```

---

### ·字母大小写全排列

给定一个字符串S，通过将字符串S中的每个字母转变大小写，我们可以获得一个新的字符串。返回所有可能得到的字符串集合。

示例:
输入: S = "a1b2"
输出: ["a1b2", "a1B2", "A1b2", "A1B2"]

输入: S = "3z4"
输出: ["3z4", "3Z4"]

输入: S = "12345"
输出: ["12345"]
注意：

S 的长度不超过12。
S 仅由数字和字母组成。


分析

回溯算法，遍历字符串，判断是数字，大写字母，小写字母，做相应的处理。

数字的时候直接添加到字符串temp后面然后递归，如果是字母，需要把字母本身添加到temp字符串后面，递归完之后还要把字母本身从temp后面去掉，然后将其变身（大写变小写，小写变大写）放到temp字符串后面再递归调用。

``` cpp
class Solution {
public:
    vector<string> letterCasePermutation(string S) {
        vector<string> v;
        bt(v,S,0);
        return v;
    }
    void bt(vector<string>& v,string s,int i){
        if(i==s.length()){
            v.push_back(s);
            return;
        }
        if(s[i]>='a'&&s[i]<='z'){
            bt(v,s,i+1);
            s[i] = s[i]-'a'+'A';
            bt(v,s,i+1);
        }
        else if(s[i]>='A'&&s[i]<='Z'){
            bt(v,s,i+1);
            s[i] = s[i]-'A'+'a';
            bt(v,s,i+1);
        }
        else
            bt(v,s,i+1);
    }
};
```

### ·隐藏个人信息

给你一条个人信息 string `S`，它可能是一个邮箱地址，也可能是一个电话号码。

我们将隐藏它的隐私信息，通过如下规则:

\1. 电子邮箱

定义名称 <name> 的长度大于2，并且只包含小写字母 a-z 和大写字母 A-Z。

电子邮箱地址由名称 <name> 开头，紧接着是符号 ['@'](mailto:'@')，后面接着一个名称 <name>，再接着一个点号 '.'，然后是一个名称 <name>。

电子邮箱地址确定为有效的，并且格式是"[name1@name2.name3](mailto:name1@name2.name3)"。

为了隐藏电子邮箱，所有的名称 <name> 必须被转换成小写的，并且第一个名称 <name> 的第一个字母和最后一个字母的中间的所有字母由 5 个 '*' 代替。

\2. 电话号码

电话号码是一串包括数组 0-9，以及 {'+', '-', '(', ')', ' '} 这几个字符的字符串。你可以假设电话号码包含 10 到 13 个数字。

电话号码的最后 10 个数字组成本地号码，在这之前的数字组成国际号码。注意，国际号码是可选的。我们只暴露最后 4 个数字并隐藏所有其他数字。

本地号码是有格式的，并且如 "***-***-1111" 这样显示，这里的 1 表示暴露的数字。

为了隐藏有国际号码的电话号码，像 "+111 111 111 1111"，我们以 "+***-***-***-1111" 的格式来显示。在本地号码前面的 '+' 号和第一个 '-' 号仅当电话号码中包含国际号码时存在。例如，一个 12 位的电话号码应当以 "+**-" 开头进行显示。

注意：像 "("，")"，" " 这样的不相干的字符以及不符合上述格式的额外的减号或者加号都应当被删除。

 

最后，将提供的信息正确隐藏后返回。

 

**示例 1：**

```
输入: "LeetCode@LeetCode.com"
输出: "l*****e@leetcode.com"
解释： 
所有的名称转换成小写, 第一个名称的第一个字符和最后一个字符中间由 5 个星号代替。
因此，"leetcode" -> "l*****e"。
```

**示例 2：**

```
输入: "AB@qq.com"
输出: "a*****b@qq.com"
解释: 
第一个名称"ab"的第一个字符和最后一个字符的中间必须有 5 个星号
因此，"ab" -> "a*****b"。
```

**示例 3：**

```
输入: "1(234)567-890"
输出: "***-***-7890"
解释: 
10 个数字的电话号码，那意味着所有的数字都是本地号码。
```

**示例 4：**

```
输入: "86-(10)12345678"
输出: "+**-***-***-5678"
解释: 
12 位数字，2 个数字是国际号码另外 10 个数字是本地号码 。
```

**注意:**

1. `S.length <= 40`。
2. 邮箱的长度至少是 8。
3. 电话号码的长度至少是 10。

``` cpp
class Solution {
public:
    string maskPII(string S) {
        if(isEmail(S)){
            return email(S);
        }
        else{
            return phone(S);     
        }
        return NULL;
    }//主调用 
    bool isEmail(string _s){
        if(_s.size()<8)return false;
        int i = 0;
        int flag = 0;
        while(i<_s.size()){
            if(_s[i]=='.'||_s[i]=='@'){
                flag ++;
            }
            i++;
        }
        if(flag == 2){
            return true;
        }
        return false;
    }//判断格式  
    string email(string _s){
        string s = _s;
        if(s.size()==0) return NULL;
        int i = 0;
        int at = -1;
        
        while(i<s.size()){
            if(s[i] == '@') {
                at = i;
                break;
                
            }
            else ++i;
    
        }//找到正确的邮件格式,@所在位置
        for(int k = 0; k < s.size(); k++){
            if(k == at) continue;
            s[k] += (s[k]>='A'&&s[k]<='Z') ? (32) :0;
            //变成小写
        }
        s.erase(s.begin()+1,s.begin()+at-1);
        for(int k = 0; k < 5; k++){
            s.insert(s.begin()+1,'*');
        }//隐藏要求的信息

        return s;
    }
    string phone(string _s){
        string s = _s;
        int sum = 0;
        for(int i = 0; i < s.size(); i++){
            if(s[i] >='0' && s[i] <= '9'){
                sum++;
            }
            
        }//计算号码的位数
        if(sum < 10) return NULL;
        /*添加特定格式*/
        string res;
        if(sum == 10)   res += "***-***-";
        if(sum == 11)   res += "+*-***-***-";
        if(sum == 12)   res += "+**-***-***-";
        if(sum == 13)   res += "+***-***-***-";
        
        /*用于显示后四位数字*/
        string temp;
        int index = 0;
        int k = 0;
        while(k < sum - 4){
            if(s[index] >= '0' && s[index] <= '9'){
                k++;
            }
            index ++;  
        }
        for(int i = index; i < s.size(); i++){
            if(s[i] >= '0' && s[i] <= '9'){
                res.push_back(s[i]);
            }
        }
        return res;
    }
    
};
```

