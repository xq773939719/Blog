---
title: LeetCode-LinkList
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
description: LeetCode链表专题。
passwords:
img:

---

给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:

输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL

``` cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        int length = 0;
        ListNode* cur = head;
        while(cur){
            length++;
            cur = cur->next;
        }
        if(length == 0) return NULL;
        cur = head;
        if(k%length == 0) return head;
        int count = length - k%length;
        ListNode * p;
        ListNode * newhead;
        ListNode * r;
        if(!cur) return NULL;
        while(cur->next){
            if(--count == 0){
                p = cur;
                newhead = p->next;
            }
            cur = cur->next;
             
    
        }
        r = cur;
        p->next = NULL;
        r->next = head;
        return newhead;
        
        
    }
};
```
执行用时: 8 ms, 在Rotate List的C++提交中击败了100.00% 的用户

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:

输入: 1->2->3->3->4->4->5
输出: 1->2->5
示例 2:

输入: 1->1->1->2->3
输出: 2->3
``` cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* p = new ListNode(0);
        p->next = head;
        head=p;
        ListNode *left,*right;
        while(p->next)
        {
            left = p->next;
            right = left;
            while(right->next && right->next->val == left->val)
                right = right->next;
            if(left == right) p = p->next;
            else p->next = right->next;
        }
        return head->next;
    }
};
```

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

输入: 1->1->2
输出: 1->2
示例 2:

输入: 1->1->2->3->3
输出: 1->2->3

``` cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        if(head==NULL)return head;
        set<int> ret;
        ListNode *p = head;
        while(p!=NULL){
            ret.insert(p->val);
            p=p->next;
        }
        auto begin = ret.begin();
        auto end = ret.end();
        ListNode * res = new ListNode(*begin);
        ListNode * tail = res;
        begin++;
        while(begin!=end){
            ListNode * p = new ListNode(*begin);
            tail->next = p;
            tail = p;
            begin++;
        }
        return res;
    }
};

```

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

示例:

输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode * headnode = new ListNode(0);
        headnode->next = head;
        ListNode * tail = headnode;
        ListNode * cur = headnode;
        ListNode * pre = cur;
        cur = cur->next;
        while(cur){
            
            if(cur->val >= x){
                pre = cur;
                cur = cur->next;
                
            }
            else{
                if(pre == tail){
                    tail = cur;
                    pre = cur;
                    cur = cur->next;
                }
                else{
                    pre->next = cur->next;
                    cur->next = tail->next;
                    tail->next = cur;
                    tail = cur;
                    cur = pre->next;
                }              
            }   
        }
        return headnode->next;
    }
};
```
执行用时: 4 ms, 在Partition List的C++提交中击败了100.00% 的用户

``` cpp
/*
 * @lc app=leetcode.cn id=92 lang=cpp
 *
 * [92] 反转链表 II
 *
 * https://leetcode-cn.com/problems/reverse-linked-list-ii/description/
 *
 * algorithms
 * Medium (40.37%)
 * Total Accepted:    5.8K
 * Total Submissions: 14.4K
 * Testcase Example:  '[1,2,3,4,5]\n2\n4'
 *
 * 反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。
 * 
 * 说明:
 * 1 ≤ m ≤ n ≤ 链表长度。
 * 
 * 示例:
 * 
 * 输入: 1->2->3->4->5->NULL, m = 2, n = 4
 * 输出: 1->4->3->2->5->NULL
 * 
 */
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        int k = 1;
        ListNode *res = new ListNode(0);
        res->next = head;
        ListNode *cur = res;
        ListNode *pre = NULL;
        for (; k <= m; ++k)
        {
            pre = cur;
            cur = cur->next;
        }
        ListNode *newhead = cur;
        ListNode *temp = NULL;
        for (; k <= n; ++k)
        {
            temp = cur->next;
            cur->next = temp->next;
            temp->next = newhead;
            newhead = temp;
            pre->next = newhead;
        }
        return res->next;
    }
};
//执行用时: 8 ms, 在Reverse Linked List II的C++提交中击败了14.95% 的用户
```

