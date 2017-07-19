# Remove Elements
题目：Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example**:

Given input array *nums* = ```[3,2,2,3]```, *val* = ```3```

Your function should return length = 2, with the first two elements of nums being 2.

实现思路：这一题和之前的*Remove Duplicates from Sorted Array*这一题非常相像，这一题要求的是给定一个数，在数组里面找到这一个数并且删掉。

还是一样使用迭代器来解决这个问题，遍历整个数组，找到给定数以后使用```erase(it)```语句删除这个数。

代码：
```cpp
int removeElement(vector<int>& nums, int val) {
        if(nums.size() == 0) return 0;
        vector<int> ::iterator it;
        for(it = nums.begin(); it != nums.end();) {
          if(*it == val) nums.erase(it);
          else it++;
        }    
        return nums.size();
    }
```  
