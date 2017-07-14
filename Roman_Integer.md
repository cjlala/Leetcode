# Roman to Interger

题目：Given a roman numeral, convert it to an integer.
<br>(眨眼初看题目并没有发现题目到底要我们求的是什么，不知道罗马数字和我们的阿拉伯数字的转换规则到底是怎么样的，于是有了如下这张表）
<br>![avatar](http://osz064agz.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-07-12%20%E4%B8%8B%E5%8D%883.08.00.png)
以上这张表就是对应的转换规则，我们可以看到有几个特殊的字符代表的某个整数，分别是1，5，10，50，100，500，1000.因为题目只要求表示到3999，所以用到1000就足够了。
<br>实现思路：由于涉及到字符还有数字的对应关系，应该想到使用map最好。可以发现做这些题需要经常使用到map，所以掌握好map的相关语法非常重要。
<br>另外我们需要注意到里面的某些规则，比如4是IV而不是IIII，9又是IX，14是XIV等等这一类的存在前一个字符比后一个字符小的情况。其实这样的情况也只会出现在表示带有4，9这样的情况。所以我们的思路就是从后往前遍历这个字符串，并且对相邻的字符进行判断，假如靠左的字符比靠右的字符要小，那么就减去靠左的字符代表的数字的值，反之就加上该值。

<pre> int romanToInt(string s) {
    map<char,int> T = {
        {'I',1},{'V',5},{'X',10},{'L',50},{'C',100},{'D',500},{'M',1000}
    };
    int sum = T[s.back()];
    for (int i = s.length()-2; i >=0 ; i--) {
        if(T[s[i]] < T[s[i+1]]){
            sum -= T[s[i]];
        }
        else{
            sum += T[s[i]];
        }
    }
    return sum;
}</pre>
