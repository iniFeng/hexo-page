---
title: 使用JavaScript实现各种排序算法
date: 2020-10-03 22:36:19
tags: [算法]
---

用惯了语言自带的 sort，还没有自己系统归纳各种排序，硬要写排序的话估计只能想出个冒泡......

趁现在赶紧补一补.。

既然想入前端的坑，就用  JS 来试着写写各种排序吧！

》》[在LeetCode中尝试](https://leetcode-cn.com/problems/sort-an-array/ ) 《《

## 冒泡排序

冒泡排序只在相邻元素大小不符合要求时才调换他们位置，不会改变相同元素之间的相对顺序，所以它是稳定的排序算法。

1. 一般解法

```javascript
var sortArray = function(nums) {
    for(let i = 0; i<nums.length; i++) {
		for(let j = i; j<nums.length; j++) {
            if (nums[i] > nums[j]) { // 升序
                let tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
            }
        }
    }
    return nums;
}
```

2. JS的解构赋值

```javascript
var sortArray =function(nums) {
	for(let i = 0; i<nums.length; i++) {
		for(let j = i; j<nums.length; j++) {
			[nums[i], nums[j]] = [nums[j], nums[i]];
		}
	}
	return nums;
}
```

| 平均时间复杂度 | 最好情况 | 最坏情况 | 空间复杂度 |
| -------------- | -------- | -------- | ---------- |
| O(n²)          | O(n)     | O(n²)    | O(1)       |



## 选择排序

选择排序也是两层循环，内层循环每次执行一遍，挑出本次待排序的元素中最小/大的一个，存放在数组的排序后位置。

选择排序每次交换的元素都有可能不是相邻的，因此它可能改变了相同值元素的相对位置。因此选择排序不稳定。


```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortArray = function(nums) {
    for(let i = 0; i<nums.length-1; i++) {
        let sel=nums[i];  //选中的最小值
        let n = i;		  //最小值的索引
        for(let j=i+1; j<nums.length; j++) {
            if (nums[j] < sel) {
                sel = nums[j];
                n = j;
            }
        }
        nums[n] = nums[i];
        nums[i] = sel;
    }
    return nums;
};	
```
| 平均时间复杂度 | 最好情况 | 最坏情况 | 空间复杂度 |
| -------------- | -------- | -------- | ---------- |
| O(n²)          | O(n²)    | O(n²)    | O(1)       |



## 插入排序

插入排序将数组分成两个部分，前半部分为排序部分，后半部分为待插入的元素部分。插入排序不会影响相同值元素的相对位置，所以是稳定的排序。

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortArray = function(nums) {
    for(let i = 1; i<nums.length; i++) {
       let temp = nums[i];
       let j = i-1;
       for(j; j>=0; j--) {
           if(nums[j]<=temp) break; // 找到插入的位置时break;
           nums[j+1] = nums[j];		// 将值比temp大的元素后移一位
       }
       nums[j+1] = temp;			// 完成插入操作
    }
    return nums;
};
```

| 平均时间复杂度 | 最好情况 | 最坏情况 | 空间复杂度 |
| -------------- | -------- | -------- | ---------- |
| O(n²)          | O(n²)    | O(n²)    | O(1)       |



## 希尔排序

希尔排序可以看作是一个冒泡排序或者插入排序的变形。希尔排序在每次排序的时候都把数组拆分成若干个序列，一个序列的相邻的元素索引相隔固定的距离 gap, 每一轮对这些序列进行冒泡或者插入排序，然后再缩小 gap 得到新的序列，一一排序，直到 gap 为1。



## 快速排序

快速排序借用了分治的思想，并基于冒泡排序做了改进，它由C.A.R. Hoare在1962年提出。它将数组拆分为两个子数组，其中一个子数组的所有元素都比另一个子数组的元素小，然后对这两个子数组再重复进行上述操作，直到数组不可拆分，排序完成。

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortArray = function(nums) {
    if(nums.length < 2) return nums;
    quickSort(nums,0,nums.length-1);
    return nums;
};
// 递归
function quickSort(nums, left, right) {
    if(left>=right) return;
    let partitionIndex = partition(nums,left, right);
    quickSort(nums,partitionIndex+1, right);
    quickSort(nums,left, partitionIndex-1);
    return nums;
}
// 分区
function partition(nums, left, right) {	
    let pivot = right; 		//规定pivot为序列最右值
    let leftIndex = left;	
    for(let i = left; i<=right; i++) {
        if(nums[i] < nums[pivot]) {
            // 遍历，将小于pivot的的元素与当前leftindex的元素交换，leftindex自增
            [nums[i],nums[leftIndex]] = [nums[leftIndex], nums[i]];
            leftIndex++;
        }
    }
    // 将pivot所在的元素与自增后的leftindex所指元素交换，即可分好区
    [nums[pivot],nums[leftIndex]] = [nums[leftIndex], nums[pivot]];
    // 返回交换完的pivot所在位置
    return leftIndex;
}
```



| 平均时间复杂度 | 最好情况  | 最坏情况 | 空间复杂度 |
| :------------: | :-------: | :------: | :--------: |
|   O(nlog₂n)    | O(nlog₂n) |  O(n²)   | O(nlog₂n)  |