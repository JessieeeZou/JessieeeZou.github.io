---
title: Recursion I
author: Xiaoxu Zou
date: 2022-02-03
category: Algorithm
layout: post
---
# Recursion I (Binary Tree)
##Part 1: Recursion
<font color=red size=4>Recursion rules:</font>
<font size=2.5>
1. 表面上：Function calls itself
2. 实质上：Boil down a big problem to smaller ones(size n depends on size n-1, or n-2 or …n/2)
3. Implementation上：
a) Base case: smallest problem to solve
b) Recursive rule. How to mask the problem smaller (if we can resolve the same problem but with a smaller size, then what is left to do for the current problem size n)

### Examples
<b>1. 斐波那契数列</b>
>Fibonacci sequence:
>>Base case: F(0)=0; F(1)=1;
>>Recursive rule: F(n) = F(n-1) + F(n-2);

**Java实现：**
```java
class Solution{
    public int fibo(int n){
        //base case
        if(n == 0){
            return 0;
        }else if(n == 1){
            return 1;
        }
        //Recursive rule
        return fibo(n - 1) + fibo(n - 2);
    }
}

public class Fibonacci{
    public static void main(String[] args){
        Solution f = new Solution();
        int result = f.fibo(4);
        System.out.println(result);
    }
}
```

<font color=red>Time =1 + 2 + 4 + 8 + 2^(n-1) = O(2^n)</font>
<table><tr><td bgcolor=#F5F5F><b>Trick:</b> For binary tree, the number of all leaf nodes in the binary tree is larger than the rest nodes in the binary tree. Thus, we only care about the nodes in the leaf level.</td></tr></table>

<b>2. 求a的b次幂</b>
>Calculate a^b (where a and b are integers, we do not care the about the corner case where a = 0 or b < 0 for now)

**Java实现：**
Solution 1 时间复杂度高
Solution 2 revised 时间复杂度更低
```java
//Recursion方法1
//时间复杂度较高
//Solution 1
class Solution1{
    public int power(int a, int b){
        //Base case
        if (b == 0){
            return 1;
        }
        return a * power(a, b-1);
    }
}

//Solution 2
class Solution2{
    public int power(int a, int b){
        //Base case
        if (b == 0) {
            return 1;
        }
        //b为奇数和偶数recursive rule不一样
        //b为奇数时
        if (b % 2 != 0){
            return a * power(a, b/2) * power(a, b/2);
        }
        //b为偶数时
        else{
            return power(a, b/2) * power(a, b/2);
        }
    }
}


public class APowerB{
    public static void main(String[] args){
        Solution1 p1 = new Solution1();
        Solution2 p2 = new Solution2();
        int result1 = p1.power(3,5);
        int result2 = p2.power(3,5);
        System.out.println(result1 + " " + result2);
    }
}
//结果：243 243
```
</font>

##Part 2: Binary Search
<font size=2.5>
<b>1. 一维二分查找</b>

**Java实现：**
```java
class Solution{
    public int search(int[] arr, int target){
        int left = 0;
        int right = arr.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(arr[mid] == target){
                return mid; 
            }else if(arr[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return -1;
    }
}

public class BinarySearch{
    public static void main(String[] args){
        int[] array = {1,2,3,4,5,6,7,8};
        int target = 5;
        Solution bs = new Solution();
        int result = bs.search(array, target);
        System.out.println(result);
    }
}
```

<b>2. 二维二分查找</b>

**Java实现：**
```java
class Solution{
    public int search(int[][] matrix, int target){
        if(matrix.length == 0 || matrix[0].length == 0){
            return -1;
        }
        int row = matrix.length;
        int col = matrix[0].length;
        int i = 0;
        int j = row * col - 1;
        while(i <= j){
            int mid = i + (j - i) / 2;
            //将摊平的一维数组查找还原为二维
            int r = mid / col;
            int c = mid % col;
            if (matrix[r][c] == target){
                return mid;
            }else if (matrix[r][c] < target){
                i = mid + 1;
            }else {
                j = mid - 1;
            }
        }
    return -1;
    }
}
```

### Examples
<b>1. 找到数组中离目标值最近的数字</b>
>how to find an element in the array that is closest to the target number?

**Java实现：**

```java
import java.lang.Math.*;

class Solution{
    public int closest(int[] arr, int target){
        if(arr.length == 0){
            return -1;
        }
        int left = 0;
        int right = arr.length - 1;
        while(left < right - 1){
            int mid = left + (right - left) / 2;
            if (arr[mid] == target){
                return mid;
            }else if(arr[mid] < target){
                left = mid;
            }else{
                right = mid;
            }
        }
        if(Math.abs(arr[left] - target) <= Math.abs(arr[right] - target)){
            return left;
        }
        else{
            return right;
        }
    }
}

public class ClosestPoint{
    public static void main(String[] args){
        int[] array = {1,3,5,6,9,13,16,23};
        int target = 10;
        Solution c = new Solution();
        int result = c.closest(array, target);
        System.out.println("The closest point is: " + result);
    }
}
```
<b>2. 返回数组中数字第一次出现的下标</b>
>Return the index of the first occurrence of an element.

**Java实现：**

```java
class Solution{
    public int occur(int[] arr, int target){
        if (arr.length == 0){
            return -1;
        }
        int left = 0;
        int right = arr.length - 1;
        while(left < right - 1){
            int mid = left + (right - left) / 2;
            if (arr[mid] == target){
                right = mid;
            }else if(arr[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        if (arr[left] == target){
            return left;
        }else if(arr[right] == target){
            return right;
        }
        else{
            return -1;
        }

    }
}

public class FirstOccur{
    public static void main(String[] args){
        int[] array = {4,5,5,5,5,7,7,8,8,9,11,11,11};
        int target = 7;
        Solution f = new Solution();
        int i = f.occur(array, target);
        System.out.println("The first occurance of " + target + " has the index of " + i);
    }
}
```
<b>3. 在排序数组中查找元素的第一个和最后一个位置</b>
>Find First and Last Position of Element in Sorted Array

**Java实现：**

```java
//我的方法
class Solution {
    public int[] searchRange(int[] arr, int target) {
        int[] array = new int[2];
        if (arr.length == 0){
            array[0] = -1;
            array[1] = -1;
            return array;
        }
        int left1 = 0;
        int left2 = 0;
        int right1 = arr.length - 1;
        int right2 = arr.length - 1;
        while(left1 < right1 - 1){
            int mid = left1 + (right1 - left1) / 2;
            if (arr[mid] == target){
                right1 = mid;
            }else if(arr[mid] < target){
                left1 = mid + 1;
            }else{
                right1 = mid - 1;
            }
        }
        if (arr[left1] == target){
            array[0] = left1;
        }else if(arr[right1] == target){
            array[0] = right1;
        }
        else{
            array[0] = -1;
        }
        while(left2 < right2 - 1){
            int mid = left2 + (right2 - left2) / 2;
            if (arr[mid] == target){
                left2 = mid;
            }else if(arr[mid] < target){
                left2 = mid + 1;
            }else{
                right2 = mid - 1;
            }
        }
        if (arr[right2] == target){
            array[1] = right2;
        }else if(arr[left2] == target){
            array[1] = left2;
        }
        else{
            array[1] = -1;
        }
        return array;
    }
}
```

```java
//力扣官方视频解法
//比我的方法多了两个函数
//reference: https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/zai-pai-xu-shu-zu-zhong-cha-zhao-yuan-su-de-di-3-4/
public class Solution{
    public int[] searchRange(int[] nums, int target) {
        int len = nums.length;
        if (len == 0) {
            return new int[]{-1, -1};
        }

        int firstPosition = findFirstPosition(nums, target);
        if (firstPosition == -1) {
            return new int[] {-1, -1};
        }

        int lastPosition = findLastPosition(nums, target);
        return new int[] {firstPosition, lastPosition};
    }

    private int findLastPosition(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        while(left < right) {
            int mid = (left + right + 1) >>> 1;
            if (nums[mid] < target){
                // 下一轮的搜索区间是 [mid + 1, right]
                left = mid + 1;
            } else if (nums[mid] == target){
                // 下一轮的搜索区间是 [mid, right]
                left = mid;
            } else {
                // nums[mid] > target
                // 下一轮的搜索区间是 [left, mid - 1]
                right = mid - 1;
            }
        }
        return left;
    }

    private int findFirstPosition(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        while(left < right) {
            int mid = (left + right) >>> 1;
            if (nums[mid] < target){
                // 下一轮的搜索区间是 [mid + 1, right]
                left = mid + 1;
            } else if (nums[mid] == target){
                // 下一轮的搜索区间是 [left, mid]
                right = mid;
            } else {
                // nums[mid] > target
                // 下一轮的搜索区间是 [left, mid - 1]
                right = mid - 1;
            }
        }
        if (nums[left] == target) {
            return left;
        }
        return -1;
    }
}
```
<table><tr><td bgcolor=#F5F5F><b>技巧：</b>二分用这个模板就不会出错了。满足条件的都写l = mid或者r = mid，mid首先写成l + r >> 1，如果满足条件选择的是l = mid，那么mid那里就加个1，写成l + r + 1 >> 1。然后就是else对应的写法l = mid对应r = mid - 1，r = mid对应l = mid + 1。</td></tr></table>

