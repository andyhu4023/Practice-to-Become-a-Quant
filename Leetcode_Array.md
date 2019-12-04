- [1. Two Sum](#1-Two-Sum)
- [4. Median of Two Sorted Arrays](#4-Median-of-Two-Sorted-Arrays)
- [11. Container With Most Water](#11-Container-With-Most-Water)
- [31. Next Permutation](#31-Next-Permutation)
- [33. Search in Rotated Sorted Array (Hard)](#33-Search-in-Rotated-Sorted-Array-Hard)
- [39. Combination Sum](#39-Combination-Sum)
- [40. Combination Sum II](#40-Combination-Sum-II)
- [41. First Missing Positive](#41-First-Missing-Positive)


----------------------------------
### 1. Two Sum
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.
>
>You may assume that each input would have  exactly  one solution, and you may not use the  same  element twice.

**Naive Solution:** (Brute Force, $O(n^2)$ time, $O(1)$ space)

**Optimized Solution:** (Hash Table, $O(n)$ time, $O(n)$ space)

**A Noteworthy Solution:** (Two pointer, $O(nlog(n))$, $O(1)$ space) 
dfs

-------
### 4. Median of Two Sorted Arrays
>There are two sorted arrays nums1 and nums2 of size m and n respectively.
>Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
>
>You may assume nums1 and nums2 cannot be both empty.

**Induction Solution:** (Merge and Binary Search, $O(m+n)$ time, $O(m+n)$ space)

**Required Solution:** (Divide and conquere, $O(log(m+n))$ time, $O(1)$ space)
Pivot




---------------------------
### 11. Container With Most Water
>Given  n  non-negative integers  a1 ,  a2 , ...,  an , where each represents a point at coordinate ( i ,  ai ).  n  vertical lines are drawn such that the two endpoints of line  i  is at ( i ,  ai ) and ( i , 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
>
>Note: You may not slant the container and  n is at least 2.

**Naive Solution:** (Brute Force, $O(n^2)$ time, $O(1)$ space)

**Optimized Solution:** (Two pointer, $O(n)$ time, $O(1)$ space)

------------------------------
### 31. Next Permutation
> Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
>
>The replacement must be in-place and use only constant extra memory.

**Solution:** (Math)

---------------------
### 33. Search in Rotated Sorted Array (Hard)
> Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand. (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]). You are given a target value to search. If found in the array return its index, otherwise return -1.
>
> Note: You may assume no duplicate exists in the array. Your algorithm's runtime complexity must be in the order of  O (log  n ).

**Indunction Solution:** (Rotate and Binary Search)

**Required Solution:** (Direct Search)


--------------------
### 39. Combination Sum
>Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. The same repeated number may be chosen from candidates unlimited number of times.
>
>Note: All numbers (including target) will be positive integers. The solution set must not contain duplicate combinations.

------------------------
### 40. Combination Sum II
>Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. Each number in candidates may only be used once in the combination.
>
>Note: All numbers (including target) will be positive integers. The solution set must not contain duplicate combinations.

---------------------------
### 41. First Missing Positive (Hard)
>Given an unsorted integer array, find the smallest missing positive integer.
>
>Note: Your algorithm should run in $O(n)$ time and uses constant extra space.

**Required Solution:**
We can only do constant linear search and operation in place. The idea is like sorting. If we have a sorted array without negative numbers or 0. Then we can loop over the array and return the first index i plus 1 that is not equal to nums[i]. (As the index of array is 0 based, the sorted index should have `nums[0]==1` and so on.) Also notice that if a value is greater than `len[nums]`, we can omit that value as we are expecting an array from 1 to `len(nums)`. So the algorithm is to implement [count sort](#count-sort) within range value 1 to `len(nums)` inplace.

The solution code:
```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        i=0
        while i < len(nums):
            value = nums[i]
            if (value>0) and (value<= len(nums)) and (nums[value-1]!=nums[i]):
                nums[i], nums[value-1] = nums[value-1], nums[i]
            else:
                i+=1
        
        for i in range(len(nums)):
            if i+1 !=nums[i]:
                return i+1
        
        return len(nums)+1
```

-----------------------------
### 42. Trapping Rain Water

> Given  n  non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.
>![Illustration](https://camo.githubusercontent.com/0c47a8932b88a9f587d22e2100464c3f7135ec0b/68747470733a2f2f6173736574732e6c656574636f64652e636f6d2f75706c6f6164732f323031382f31302f32322f7261696e7761746572747261702e706e67)
>The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

**Simple Solution**

**Optimized solution** (Two pointers, $O(n)$ time, $O(1)$ space)

**A noteworthy solution** (Stack)
































--------------------------
## Appendix:
### Count Sort: (Wikipedia)
**Introduction:**
In computer science, counting sort is an algorithm for sorting a collection of objects according to keys that are small integers; that is, it is an integer sorting algorithm. It operates by counting the number of objects that have each distinct key value, and using arithmetic on those counts to determine the positions of each key value in the output sequence. Its running time is linear in the number of items and the difference between the maximum and minimum key values, so it is only suitable for direct use in situations where the variation in keys is not significantly greater than the number of items. However, it is often used as a subroutine in another sorting algorithm, radix sort, that can handle larger keys more efficiently.

Because counting sort uses key values as indexes into an array, it is not a comparison sort, and the Ω(n log n) lower bound for comparison sorting does not apply to it. Bucket sort may be used for many of the same tasks as counting sort, with a similar time analysis; however, compared to counting sort, bucket sort requires linked lists, dynamic arrays or a large amount of preallocated memory to hold the sets of items within each bucket, whereas counting sort instead stores a single number (the count of items) per bucket.

**The Algorithm:**
In pseudocode, the algorithm may be expressed as:
```
count = array of k+1 zeros
for x in input:
   count[key(x)] += 1

total = 0
for i in 0, 1, ... k:
   count[i], total = total, count[i] + total

output = array of the same length as input
for x in input:
   output[count[key(x)]] = x
   count[key(x)] += 1 

return output
```
Here input is the input array to be sorted, key returns the numeric key of each item in the input array, count is an auxiliary array used first to store the numbers of items with each key, and then (after the second loop) to store the positions where items with each key should be placed, k is the maximum value of the non-negative key values and output is the sorted output array.

In summary, the algorithm loops over the items in the first loop, computing a histogram of the number of times each key occurs within the input collection. After that, it then performs a prefix sum computation on count to determine, for each key, the position range where the items having that key should be placed in; i.e. items of key {\displaystyle i}i should be placed starting in position `count[i]`. This is done through the second loop. Finally, it loops over the items again in the third loop, moving each item into its sorted position in the output array. The relative order of items with equal keys is preserved here; i.e., this is a stable sort.
