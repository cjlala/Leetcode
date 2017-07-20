# Implement strStr()
题目：

首先给出这个函数的原型：```const char* strstr( const char* str, const char* target );
```也就是给定一个子串，查看这个子串是否在给定的字符串里面。假如存在，在这道题目里面，返回这个子串第一个字符对应在字符串里面的位置；假如不存在就返回-1。

实现思路如下：
<br>首先要明确的是当字符串是空的时候或者字符串的长度小于子串的长度时直接返回-1.还有当子串是空的时候直接返回0。这是两种特殊情况，明确出来对优化代码以及减少错误有很大帮助。
<br>找子串的过程分为以下步骤<br>
- 从0开始遍历字符串，循环结束条件为字符串的长度 ／- 子串的长度 ／+ 1。
- 在上述循环中有个内循环，每次从0开始遍历子串。将迭代的变量 j 作为两个字符串往后移位比较的变量 ```haystack[i+j] != needle[j]```采用这个判断条件判断子串是否在字符串里面。假如开始比较后，子串里面有一位和字符串对应位不相等，就break继续外循环。假如在内循环里面 j 已经等于子串的长度了，意味着子串存在与字符串里面，直接返回外循环的迭代变量的值。
- 最后假如外循环也结束还没有返回一个值，就直接返回-1。

代码如下：
```cpp
int strStr(string haystack, string needle) {
        if(needle=="") return 0;
        else if(haystack=="" || needle.size() > haystack.size()) return -1;
        for(int i = 0;i < haystack.size() - needle.size() + 1; i++) {
            for(int j = 0;j < needle.size();)
            {
              if(haystack[i+j] != needle[j]) break;
              j++;
              if(j == needle.size()) return i;
            }
        }
        return -1;
}
``` 