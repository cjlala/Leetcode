# Search Insert Position

题目：Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
<br>You may assume no duplicates in the array.

就是要我们在一个给定的升序并且没有重复数字的数组中找到给定的target数，如果没有的话返回按照target的大小插到数组中的位置。

##### 实现思路：
一个O(n)的实现方法就是第一次遍历整个数组看看有没有这个target数，假如有就直接返回index；假如没有就进行第二次遍历找到插入的位置。代码如下：
```cpp
 int searchInsert(vector<int>& nums, int target) {
        if(nums.empty()) return 0;
        for(int i = 0; i < nums.size(); i++) {
           if(nums[i] == target){
             return i;
           }
        }
        if(target < nums[0]) return 0;
        else if(target > nums[nums.size()-1]) return nums.size();
        for(int i = 0; i < nums.size()-1; i++) {
           if(target > nums[i] && target < nums[i+1]) return i+1;
        }
    }
};
```
另一个O(logn)的方法就是二分查找，给定low和high两个动态下标，根据target和low及high之间的mid对应的数比较。如果target大于mid的数，说明target的位置应该靠右，那么直接将low更新为mid+1；否则high更新为mid-1.
代码如下：
```cpp
int searchInsert(vector<int>& nums, int target) {
        if(target > nums[nums.size()-1]) return nums.size();
        int low = 0, high = nums.size()-1;
        while(low <= high){
            int mid = (high + low)/2;
            if(target > nums[mid]) low = mid+1;
            else high = mid-1;
        }
        return low;
    }
```
我们知道所求的下标在`[low,high+1]`中，所以有`low<=high+1` .而循环中最后得到的结果是`low>=high+1`.综合以上两点有最后循环结束以后动态下标停在了`[low,low]`中，所以最后返回low就是要求的结果。
