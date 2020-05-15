---
title: Data Structure & Algo - Binary Search
date: 2020-05-15 00:15:00
excerpt: Binary search algorithm is an efficient way to find an item from a sorted array. It has O(log n) time complexity and O(1) space complexity. This algorithm works on the principle of divide and conquer, using half-interval search to compare the location of the target value and the middle element of the array. 
type: post
blog: true
---

Binary search is an effective algorithm for searching a target element in a **sorted** array. It does so by always dividing the list of items into half and compare the position of the target value with the middle element. Elements need to be sorted first if it is not in order. The implementation of this search algorithm can be made in the iterative method or the recursive method.

```js
int binarySearch(int arr[],int left,int right, target) {
    int n = arr.length;
    int left = 0;
    int right = n-1;
    while(left<=right) {
        int mid = (left + (right-left))/2;//prevent integer overflow
        if(arr[mid]==target) return target;
        elseif(arr[mid]<target) {
            left = mid + 1; //search between the mid to right
        } else {
            right = mid - 1; //search between left to mid
        }

    }
    return -1; // can't find target

}
```

## Demo of Binary Search 
#### Time Complexity: O(log n)
#### Space Complexity: O(1)
Given a sorted array [ 0, 1, 2, 3, 5, 7, 9] and our target element is 7, we first find the middle element by diving the array into two. Identifying 3 as the middle element, we have the left interval [0, 1, 2] and the right interval [5, 7, 9]. The sorted array (in ascending order) ensures elements in left interval are all smaller than the middle element while the elements in the right interval are all bigger than the middle element.

<img src="/binary_search_0.png" width="800rem" height="280rem">

Next, we compare the target element 7 with the middle element 3. Since 7 is larger than 3, we can discard the left interval entirely and search the target value in the right interval. Then we repeat the process after updating the lower bound (middle element) of the right interval by one index.

<img src="/binary_search_1.png" width="700rem" height="280rem">

This leads to the search in interval [5, 7, 9] and we return the mid element 7 as it is equal to the target value.

<img src="/binary_search_2.png" width="650rem" height="290rem">



### Leetcode 33. Search in Rotated Sorted Array (no duplicates)

An array given was originally sorted in ascending order. However, it has been pivoted at an element, generating a new array that is partially sorted in two parts. Our goal is to find the target element in the new pivoted array in O(log n) time. If the target value is not found, return -1. Without pivoting, this is a typical question that can be solved with binary search algorithm. 

The brute force solution ignoring the time constraint will simply be iterating each elements in the array size of n with time complexity of O(n). However, let's stick to the rules of the game and solved it in the time required. 

```js
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if(nums.size() == 0 ) return -1;
        int low = 0;
        int high = nums.size()-1;
        //modified binary search to find the pivot
        while(low<high) {
            int mid = (low+high)/2;
            //can change to (low + (high-low))/2 to prevent integer overflow
            if(nums[mid]>nums[high]) {
                low = mid+1;
            } else {
                high = mid;
            }
        }
        int begin = low;
        low = 0;
        high = nums.size()-1;
        
        if(target>=nums[begin]&&target<=nums[high]){
            low = begin;
        } else {
            high = begin;
        }
        
        // original binary search 
        while(low<=high){
            int mid = (low + high)/2;
            if(nums[mid]==target){
                return mid;
            } else if(nums[mid]<target){
                low = mid+1;
            } else {
                high = mid - 1;
            }
        }
        return -1;
    }
};
```

First, we can locate the smallest element in the array. Since the smallest element is the pivot point, we know that both left and right side of the smallest element will be arraged in ascending order. With this in mind, the first while loop is set to find the smallest element. Observed that the smallest element is always named as the left bounded variable.

<img src="/binary_search_3.png" width="780rem" height="650rem">

Once the smallest element in the array is found, a variable `int begin = left ` is created to indicate the starting index of smallest element. Next, left and right boundary are reset again with the new variable `begin` in the array. Two sorted arrays can be seen from left to begin and from begin to right. Now, original binary search can be conducted after we compare target value to the value in the `begin` index. If target value is bigeer than the nums[begin] and smaller than nums[right], we shift left boundary to begin and binary search on the right side. Else, we shift the right boundary to begin and search on the left side. As such, the target value will be returned in O(log n) time.

<img src="/binary_search_4.png" width="680rem" height="650rem">

### Notes
This is my first time dissecting a leetcode problem and solution step by step to ensure that I know exactly what each line of codes is doing. I hope this post can help someone to understand the solution better by the visualization. It was indeed a challenging task to thoroughly comprehend the solution even though the solution is short. Sometimes when we watch or read a tutorial on coding question, there is a tendency to think that we understand the solution. I admit I often fall into this rabbit hole and so this is a good start to improve my coding.








