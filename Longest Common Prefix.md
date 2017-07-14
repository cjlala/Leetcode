# Longest Common Prefix

题目：Write a function to find the longest common prefix string amongst an array of strings.
本题就是要找到一系列字符串的最长公共前缀。

实现思路：
<br>最简单的思路就是暴力求解，但是暴力算法也有分写的简短的或者是写的复杂的。下面就是我一开始的复杂版代码。实现的思路就是使用一个字符串记录着公共前缀，在一个循环里面每一次取第一个字符串的字符存在记录的字符串内，再拿这个新加入的字符和后续的字符串的字符相比较。
<pre>class Solution {
public:
   string longestCommonPrefix(vector\<string>& strs){
    string tmp="",tmp2;
    if(strs.empty()) return tmp;
    for(int i=0;i\<strs.size();i++)
        if(strs[i]=="") return tmp;
    int i,index[strs.size()+1],flag=1;
    for(i=0;i\<strs.size();i++) index[i]=0;
    while(1){
        if(index[0]>strs[0].size()-1) break;
        tmp2 = tmp;
        tmp += strs[0][index[0]];
        for (i=1; i< strs.size(); i++) {
            if(index[i]>strs[i].size()-1){
                tmp = tmp2;
                flag = 0;
                break;
            }
            if(strs[i][index[i]] == tmp.back()) {
                index[i]++;
                continue;
            }
            else{
                tmp = tmp2;
                flag=0;
                break;
            }
        }
        if(!flag) break;
        index[0]++;
    }
    return tmp;
}
}; </pre>

下面是精简版的暴力，合理运用判断条件可以很大程度简化代码。这样的暴力算法是使用垂直比较字符串之间的字符来实现的，还有另外一种暴力是水平比较相邻的字符串，找出相邻的公共前缀，再将得到的公共前缀和下一个字符串比较一直到最后，这种方法使用java来写十分方便，但是使用c++并没有很好的函数直接调用，所以这里也不采用了。
<pre>class Solution {
public:
    string longestCommonPrefix(vector\<string>& strs) {
        string prefix = "";
        for(int idx=0; strs.size()>0; prefix+=strs[0][idx], idx++)
            for(int i=0; i<strs.size(); i++)
                if(idx >= strs[i].size() ||(i > 0 && strs[i][idx] != strs[i-1][idx]))
                    return prefix;
        return prefix;
    }
}; </pre>

下面是两种官网上给出的比较好的方法，一个是分治法，另一个是二分查找。代码量较长但是效率较高。
分治法的思想是将字符序列分成两半处理，找出分别两半的公共前缀最后再合并找公共前缀。
<pre>分治法：
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
      if(strs.empty()) return "";
      return longestCommonPrefix(strs, 0 , strs.size() - 1);
    }
    string longestCommonPrefix(vector<string>& strs,int l,int r){
      if(l == r){
        return strs[l];
      }
      else {
        int mid = (l + r)/2;
        string lcpleft = longestCommonPrefix(strs, l ,mid);
        string lcpright = longestCommonPrefix(strs, mid+1 ,r);
        return commonPrefix(lcpleft,lcpright);
      }
    }
    string commonPrefix(string left,string right){
      int min = std::min(left.size(),right.size());
      for(int i = 0; i < min; i++){
        if(left[i] != right[i])
          return left.substr(0, i);
      }
      return left.substr(0, min);
    }
};</pre>

二分查找的思路如下：
假如有需要处理的字符串如下：
<pre> strs = [
    "leetcode","leetcddd","leet"]
</pre>
我们将整个字符串数组分为左右两个部分（注意不是上下两个部分），结果如下：
<pre>
strs = [ |
    "leet|code",
    "leet|cddd",
    "leet|"]
</pre>
假设strs左半部分的最长公共前缀为LCS1，右半部分的最长公共前缀为LCS2。在这里我们分两种情况讨论：

1.如果LCS1的长度等于左半部分每一个字符串的长度（例子中的长度为4）的话，那么整个字符串数组strs的最长公共前缀就是LCS1 + LCS2，也就是说，这个最长公共前缀的右边界由LCS2决定。

2.如果LCS1的长度小于左半部分每一个字符串的长度（例子中的长度为4）的话，那么整个字符串数组strs的最长公共前缀就是LCS1，在这种情况下我们不需要再计算LCS2。

那怎么计算LCS1或者LCS2呢？把strs的左半部分再分成左右两个部分，得到子字符串数组之后再继续进行切割，一直到我们所获得的子字符串数组中每一个字符串的长度均为1为止，如下所示：

<pre>
    "l|eetcode",
    "l|eetcddd",
    "l|eet"
</pre>
在这种情况下，我们看一下每一个数组的当前位置所对应的字符是否都一样，如果一样，就返回这个字符（如例子中返回的就是l），如果不一样，返回空字符串。<br>
整个过程如下：
![avatar](https://segmentfault.com/img/bVLDl9?w=811&h=706/view.png)
实现代码如下：
<pre>
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
      if(strs.empty()) return "";
      int min = INT_MAX;
      for(int i = 0; i < strs.size(); i++)
        if(min>strs[i].length()) min = strs[i].length();
      int low = 1,high = min;
      while(low <= high){
        int mid = (low + high) / 2;
        if(isCommonPrefix(strs, mid))
          low = mid + 1;
        else 
          high = mid - 1;
      }
      return strs[0].substr(0,(low + high) / 2);
    }
    bool isCommonPrefix(vector<string>& strs,int len){
      string str1 = strs[0].substr(0,len);
      for(int i=1; i < strs.size();i++)
        if(!strs[i].rfind(str1))
          return false;
      return true;
    }
};
</pre>

