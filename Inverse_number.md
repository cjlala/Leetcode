# Inverse Number
<br>题目：Reverse digits of an integer.<br>
Example1: x = 123, return 321<br>
Example2: x = -123, return -321<br>

实现思路：
<br>这么简单的一题我都做了这么久。。。的确是老了。。
<br>思路非常简单，就是用一个long类型的变量来记录结果，因为int类型表示的结果刚好是题目所给出的溢出范围，因此假如用int来存储结果的话，就不知道什么时候会发生溢出了。
<br>最后将算得的值和int能表示的最大值或者最小值相比较，使用 ?: 这个语句来简化return语句。

<pre> int reverse(int x) {
        if(x >= pow(2,31)-1 || x <= -pow(2,31)) return 0;
        int flag = 0;
        if(x < 0) {
            flag = 1;
            x = -x;
        }
        long result=0;
        while(x != 0)
        {
            result += x%10;
            x /= 10;
            if(x != 0) result *= 10;
        }
        if(result > pow(2,31)-1) return 0;
        else return flag?-(int)result:(int)result;
    }</pre>
上面这个方法说实话有点蠢，下面这个方法是代码量比较少的。思路其实是一样的。
<pre> int reverse(int x) {
        long result = 0;
        while(x)
        {
            result = x%10 + result*10;
            x /= 10;
        }
        return (result > INT\_MAX || result < INT\_MIN) ? 0 : result;
    }</pre>
值得注意的是直接调用的INT\_MAX以及INT\_MIN，这个方法比较好。而且其实正负的x对10的取模得到的值都是一样的，无需分开讨论。
