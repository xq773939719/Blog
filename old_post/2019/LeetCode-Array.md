---
title: LeetCode-Array
categories: [算法]
tags: [算法,C++,数据结构]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2018-12-28 23:56:44
updated: 2018-12-28 23:56:44
keywords:
description: LeetCode数组专题。
passwords:
img:
---

‌·加一

给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
示例 2:

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。

------

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> ret;
        for(int i = 0; i < digits.size(); i++){
            ret.push_back(digits[i]);
        }
        ret[ret.size()-1]++;
        int i = ret.size()-1;
        for(; ret[i]<10; i --){
        }
        for(int j = i; j >= 1; j --){
            
            if(ret[j]==10){
                ret[j]=0;
                ret[j-1]++;
            }
        }
        if(ret[0]==10){
            ret[0] = 0;
            ret.insert(ret.begin(),1); 
        }
        return ret;    
    }
   
};
```

### ·从排序数组中删除重复项

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:

给定数组 nums = [1,1,2],

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。

你不需要考虑数组中超出新长度后面的元素。
示例 2:

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
print(nums[i]);
}

------

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int i = 0;
        if(nums.size()==0) return 0;
        while(i<nums.size()-1){
            if(nums[i+1]==nums[i]) {
                nums.erase(nums.begin()+i+1);
            }
            else {
                i++;
            }
        }
        return nums.size();
    }
};
```



### ·买卖股票的最佳时机 II

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:

输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
示例 2:

输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

------

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size()==0) return 0;
        int total = 0;
        for (int i=0; i< prices.size()-1; i++) {
            if (prices[i+1]>prices[i]) total += prices[i+1]-prices[i];
        }   

    return total;
    }
};
```



### ·旋转数组

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
示例 2:

输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释:
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
说明:

尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
要求使用空间复杂度为 O(1) 的原地算法。

------

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if(k==0) return;
        int temp = nums[nums.size()-1];
        auto it_begin = nums.begin();
        auto it_end = nums.end();
        nums.erase(it_end-1);
        nums.insert(it_begin,temp);
        rotate(nums,k-1);
        
    }
};
```

### ·存在重复

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例 1:

输入: [1,2,3,1]
输出: true
示例 2:

输入: [1,2,3,4]
输出: false
示例 3:

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true

------

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> res;
        auto it = res.end();
        for(int i = 0; i < nums.size(); i++){
            res.insert(nums[i]);       
        }
        if(res.size()==nums.size()) return false;
        else return true;
    }
};
```



### ·移动零

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

------

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        
        for (auto it = nums.end() - 1; it >= nums.begin(); it--) {
            if (*it == 0) {
                nums.erase(it);
                nums.push_back(0);
            }
        }
    }
};
```



### ·两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

\--

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        vector<int> res;
        for (int i = 0; i < nums.size(); ++i) {
            m[nums[i]] = i;
        }
        for (int i = 0; i < nums.size(); ++i) {
            int t = target - nums[i];
            if (m.count(t) && m[t] != i) {
                res.push_back(i);
                res.push_back(m[t]);
                break;
            }
        }
        return res;
    }
};
```

### ·有效的数独

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 '.' 表示。

示例 1:

输入:
[
["5","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]
]
输出: true
示例 2:

输入:
[
["8","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]
]
输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。
说明:

一个有效的数独（部分已被填充）不一定是可解的。
只需要根据以上规则，验证已经填入的数字是否有效即可。
给定数独序列只包含数字 1-9 和字符 '.' 。
给定数独永远是 9x9 形式的。

------

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        for(int i = 0; i < 9; i ++){
            for(int j = 0; j < 9; j++){
                if(board[i][j]>='0'&&board[i][j]<='9'){                
                    for(int k = 0; k < 9 ; k ++){
                        if(k != j && board[i][k] == board[i][j]){
                            return false;
                        }
                    }
                    for(int k = 0; k < 9 ; k ++){                     
                        if(k != i && board[k][j] == board[i][j]){
                            return false;
                        }                 
                    }
                    for(int m = i/3*3; m < i/3*3+3; m ++){
                        for(int n = j/3*3; n < j/3*3+3; n++){
                            if(m != i && n != j && board[m][n] == board[i][j]){
                                return false;
                            }            
                        }
                    }
                }     
                else{
                    continue;
                }
            }
        }
        return true;
    }
};
```

### ·旋转图像

给定一个 n × n 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

说明：

你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

示例 1:

给定 matrix =
[
[1,2,3],
[4,5,6],
[7,8,9]
],

原地旋转输入矩阵，使其变为:
[
[7,4,1],
[8,5,2],
[9,6,3]
]
示例 2:

给定 matrix =
[
[ 5, 1, 9,11],
[ 2, 4, 8,10],
[13, 3, 6, 7],
[15,14,12,16]
],

原地旋转输入矩阵，使其变为:
[
[15,13, 2, 5],
[14, 3, 4, 1],
[12, 6, 8, 9],
[16, 7,10,11]
]

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        //方法1
        int length = matrix.size();
        //i代表正方形的起始位置，i=0即（0，0），i=1即（1，1）
        for(int i = 0 ; i < length/2 ; i++){
            //j代表当前正方形上的一条边上的一个点。
            for(int j = i ; j<length-i-1 ; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[length-j-1][i];
                matrix[length-j-1][i] = matrix[length-i-1][length-j-1];
                matrix[length-i-1][length-j-1] = matrix[j][length-i-1];
                matrix[j][length-i-1] = temp;
            }
        }
        //方法2
        int length = matrix.size();
        // 调换对角元素
        for (int i = 0; i < length; i++) {
            for (int j = 0; j < length - i; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[length - j - 1][length - i - 1];
                matrix[length - j - 1][length - i - 1] = tmp;
            }
        }
        // 调换列元素
        for (int i = 0; i < length; i++) {
            for (int j = 0; j < length / 2; j++) {
                int tmp = matrix[j][i];
                matrix[j][i] = matrix[length - j - 1][i];
                matrix[length - j - 1][i] = tmp;
            }
        }
    }
};
```

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。 求在该柱状图中，能够勾勒出来的矩形的最大面积。
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png) 
以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。 
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png) 
图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。
``` cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        
        int length = heights.size();
        if (length == 0) return 0;
        vector<vector<int>> res;
        int max = INT_MIN;
        for(int i = 0; i < length; i++){
            vector<int> temp;
            for(int j = 0; j < length - i; j++){
                int min = INT_MAX;
                int height = INT_MAX;
                for(int k = j; k < j + i + 1; k++){
                    height = height > heights[k] ? heights[k] : height;     
                }
                min = (i+1)*height;
                temp.push_back(min);
            }
            res.push_back(temp);
        }
        int indexi;
        int indexj;
        for(int i = 0; i < length; i++){
            for(int j = 0; j < length - i; j++){
                if(max < res[i][j]){
                    max = res[i][j];
                    indexi = i;
                    indexj = j;
                }
            } 
            
        }
        return max;
        
    }
};

```
94 / 96 个通过测试用例 状态：超出时间限制 

给出一个区间的集合，请合并所有重叠的区间。

示例 1:

输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
示例 2:

输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。

```cpp
/*直观的解法*/
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> merge(vector<Interval>& intervals) {
        if(intervals.size()<=1) return intervals;
        sort(intervals.begin(), intervals.end(), [](Interval a, Interval b) {
            return a.start < b.start;
        });
        for(int i = 0; i < intervals.size() - 1; ){
            if(intervals[i].start > intervals[i+1].end || intervals[i+1].start > intervals[i].end){
                i++;
            }
            else{
                int a = intervals[i+1].start > intervals[i].start ? intervals[i].start : intervals[i+1].start;
                int b = intervals[i+1].end > intervals[i].end ? intervals[i+1].end : intervals[i].end;
                intervals[i].start = a;
                intervals[i].end = b;
                intervals.erase(intervals.begin()+i+1);
                i = 0;
            }
        }
        return intervals;
    }
};
执行用时: 68 ms, 在Merge Intervals的C++提交中击败了13.18% 的用户

/*贪心解法*/
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> merge(vector<Interval>& intervals) {
        if(intervals.size()<=1) return intervals;
        sort(intervals.begin(), intervals.end(), [](Interval a, Interval b) {
            return a.start < b.start;
        });
        vector<Interval> res;
        res.push_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++){
            if(res.back().end < intervals[i].start){
                res.push_back(intervals[i]);
            }
            else{
                if(intervals[i].end > res.back().end){
                    res.back().end = intervals[i].end;
                }
            }
        }
        return res;
    }
};
执行用时: 12 ms, 在Merge Intervals的C++提交中击败了88.25% 的用户
```

给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

示例 1:

输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
输出: [[1,5],[6,9]]
示例 2:

输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出: [[1,2],[3,10],[12,16]]
解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。

```cpp
/*参考上一题贪心直观的解法*/
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
        intervals.push_back(newInterval);
        sort(intervals.begin(),intervals.end(),[](Interval a, Interval b){
            return a.start < b.start;
        });
        vector<Interval> res;
        res.push_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++){
            if(res.back().end < intervals[i].start){
                res.push_back(intervals[i]);
            }
            else{
                res.back().end = intervals[i].end > res.back().end ? intervals[i].end : res.back().end;    
            }           
        }
        return res;   
    }
};
```
执行用时: 20 ms, 在Insert Interval的C++提交中击败了29.92% 的用户

``` cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
        vector<Interval> res;
        if(intervals.size() == 0)
        {
            res.push_back(newInterval);
            return res;
        }
        auto it = intervals.begin(); 
        for(;it!=intervals.end();it++){
            if(it->end < newInterval.start){
                res.push_back(*it);
            }else if(it->start > newInterval.end){
                res.push_back(newInterval);
                res.insert(res.end(),it,intervals.end());
                return res;
            }else{
                newInterval.start = min(newInterval.start, it->start);
                newInterval.end   = max(newInterval.end, it->end);
            }
        }
        res.push_back(newInterval);
        return res;
    }

};
```
执行用时: 12 ms, 在Insert Interval的C++提交中击败了97.31% 的用户

``` cpp
/*8ms解法*/
class Solution {
public:
    vector<Interval> insert(vector<Interval> &intervals, Interval newInterval) {
        int i = 0;
        int size = intervals.size();
        vector<Interval> ans;
        while (i < size && intervals[i].end < newInterval.start) {
            ans.push_back(intervals[i]);
            ++i;
        }
        while (i < size && intervals[i].start <= newInterval.end) {
            newInterval.start = min(newInterval.start, intervals[i].start);
            newInterval.end = max(intervals[i].end, newInterval.end);
            ++i;
        }
        ans.push_back(newInterval);
        while (i < size) {
            ans.push_back(intervals[i]);
            ++i;
        }
        return ans;
    }
};
```

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1:

输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
示例 2:

输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1

``` cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        if(nums.size() == 0) return -1;
        if(nums[l] <= nums[r]) return func(l, r, nums, target);
        while(l < r){
            int mid = l + (r - l)/2;
            if(nums[mid] > nums[r]){
                if(target <= nums[mid] && target >= nums[l]){
                    return func(l, mid, nums, target);
                }else{
                    l = mid + 1;
                }
            }else{
                if(target <= nums[r] && target >= nums[mid]){
                    return func(mid, r, nums, target);
                }else{
                    r = mid - 1;
                }
            }
        }
        if(nums[r] == target) return r;
        if(nums[l] == target) return l;
        return -1;
    }
    
    int func(int l, int r, vector<int>& nums, int target){
        int idx = -1;
        while(l <= r){
            int mid = l + (r-l)/2;
            if(nums[mid] == target){
                idx = mid;
                break;
            }else if(nums[mid] < target){
                l = mid + 1;
            }else{
                r = mid - 1;
            }
        }
        if(nums[r] == target) return r;
        if(nums[l] == target) return l;
        return idx;
    }
};
```
执行用时: 4 ms, 在Search in Rotated Sorted Array的C++提交中击败了99.89% 的用户

``` cpp
0ms
这又是什么妖魔鬼怪
static const auto io_speed_up = []()
    {
        std::ios::sync_with_stdio(false);
        cin.tie(nullptr);
        return 0;
    }();
class Solution {
public:
    int search(vector<int>& nums, int target) {
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]==target) return i;
        }
        return -1;
    }
};
```

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        /* 
            将所有正数为置为相反数。那么，出现正数的位置，即没出现过的数字。比如，[4,3,2,7,8,2,3,1]
            重置后将为[-4,-3,-2,-7,8,2,-3,-1]
            [8,2] 分别对应的index为[5,6]
        */
        for (int i = 0; i < nums.size(); ++i){
            nums[abs(nums[i])-1] = -abs(nums[abs(nums[i])-1]);
        }
        vector<int> ans;
        for (int i = 0; i < nums.size(); ++i){
            if (nums[i] > 0){
                ans.push_back(i+1);
            }
        }
        return ans;
    
    }
};
```
执行用时: 104 ms, 在Find All Numbers Disappeared in an Array的C++提交中击败了93.32% 的用户