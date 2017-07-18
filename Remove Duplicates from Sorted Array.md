# Remove Duplicates from Sorted Array

题目：Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

这一题就是要将一个给定的有序数组里面重复的字符删除掉，只留下一个。只能在原来的数组空间里面进行操作，不能够另开空间处理。值得注意的是在最后得到的新的只有单一数字的长度外的数字我们可以不处理，也就是说对于```1 1 1 2 2 3 4 4```我们最后可以处理的到这样的结果```1 2 3 4 4```只需要判断前4个是否是正确的，第五个甚至第六个对结果没有影响。

实现思路：使用迭代器遍历数组，当相邻的数字相同时就删除前一个数字，由于迭代器删除了前一个数字后会自动指向下一个数字，所以此时不用增加迭代器；当相邻数字不同的时候就增加迭代器就好啦。

代码如下：
```cpp
int removeDuplicates(vector<int>& nums) {
    if(nums.size() == 0) return 0;
    vector<int>:: iterator it;
    for(it = nums.begin(); it!=nums.end()-1;) {
      if(*it==*(it+1)) {
          nums.erase(it);
      }
      else it++;
    }  
    return nums.size();
    }
```