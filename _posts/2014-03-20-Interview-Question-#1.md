---
layout: post
title: Interview Question &#35;1 Single Number
---

I'm still in the process of developing my blog. It looks sketchy now. But I think it's better for me to start my official posts along with the construction. Cheers!

-----

##Question: Single Number

After some "serious" consideration, I'm going to start with some pretty simple questions. So this one actually comes from <a href="http://oj.leetcode.com/">LeetCode OJ </a>, which is a programmer community with interview questions database and online judger. Currently suppport languages including C++, Java and Python (all OOP, interesting). So today's question, is likely the simplist question on LeetCode. It has AC (accept) rates over 44%. 

Oops, Enough background. Let's get started. 

<!-- more -->

>Given an array of integers, every element appears twice *except* for one. Find that single one.

>**Note:** 
>Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory? <a href="http://oj.leetcode.com/problems/single-number/">(link)</a>

(My most familiar programming language is C++, since I use it for most of my Computer Science courses.)


##First Approach
At the first sight, the problem itself is super easy to solve. The logic is pretty obivious. If every element appears twice except one, traverse the whole array and keep recording the times every element appears, the one integer which end up appears once will be the one we want.

##Second Thought
<u>However</u>, with the extra restriction, we need a linear runtime complexity. This looks fine for us, since we only traverse the array once (and the recording array once). This is based on the fact that we record the results in a smart way, e.g. using the integer element as the results array index to record the times that element appears; or better, using the integer element as the key of the results hashmap etc. But all of these ideas takes extra memory to store the results, especially using the array.

##Interesting Part
Here comes the interesting part, how can we do this without extra memory and still keep the linear comlexity? No extra memory means we should do all the operations on the original array to reuse the memory. So the first idea is, sort the array and then find the non-repeated element. But this is too time consuming although the space limit is preserved. We don't really need them to be sorted, the only thing we need is to find the orphan element, which has no duplicate in the array. So why don't we take each element and check if there's another one in the array? What bugged me when I try to solve this question is, I don't know if there's a linear method that could find the duplicate from an array. But there surely is one.

{% highlight C++ linenos=table %}
class Solution {
public:
    int singleNumber(int A[], int n) {
        int num=0;
        for(int x=0; x<n; x++) num ^= A[x];
        return num;
    }
};
{% endhighlight %}

##Explanation
This all happened because of the magic operation: **^=**.
This is the bitewise xor assignment operator. The usage of the operator is like:

{% highlight C++ linenos=table %}
x ^= y;
=> x = x ^ y; //if x = 2, y = 10
=> x = 0010
       1010 = 1000 = 8
{% endhighlight %}

The approach above using this bitwise feature to get rid of the duplicate ints in the array. Whenever a number appears the second time, xor will eliminate the first occurrence along with this one. Then the last remaining integer will be the one who only appears once in the array.