# Valid_Parentheses

题目：Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
<br>
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

这道题目考验的其实就是对栈的使用是否熟练，对于这种对称匹配的模型最好的就是使用栈来实现。通过题意我们知道当有一个最右边的*左边符号*比如 ( , { , [ 这种那么其下一个对应的*右边符号*一定要是其对应的，不然就直接```return false```

再说明的话比如```(){}[]```这样，从左开始看，首先最右边的*左边符号*是 ```( ```那么其下一个出现的最左边的*右边符号*就应该是 ```) ```，之后的同理。

而对于```([)]```这样的，最右边的*左边符号*是 [ 而对应的最左边的*右边符号*是 ) ,这样就不符合规定了。

原理已经说的很清楚了。那么使用栈来实现的思路就是:
<br> 
- 一遇到左边符号就扔进栈内
- 一遇到右边符号就判断当前的栈是否为空活着栈顶是否为对应左边符号
  + 为空说明之前没有的符号已经匹配完或者没有对应的左边符号
  + 如果栈顶不是的话说明匹配发生错误
  + 反之就弹出栈头，说明匹配成功
- 最后当遇到不是括号的字符直接跳过不压栈就行啦。

下面是代码<br>
```cpp
class Solution {
public:
    bool isValid(string s){
    stack<char> T;
    for(char &c:s)
    {
        switch (c) {
            case '{':
            case '[':
            case '(': T.push(c);break;
            case '}': if(T.empty() || T.top()!='{') return false; else T.pop(); break;
            case ']': if(T.empty() || T.top()!='[') return false; else T.pop(); break;
            case ')': if(T.empty() || T.top()!='(') return false; else T.pop(); break;
            default:break;
        }
    }
    return T.empty();
}
};
```