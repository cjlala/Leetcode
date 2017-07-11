# Palindrome Number（回文）
题目：Determine whether an integer is a palindrome. Do this without extra space.

这道题秒A，是真的简单。
<br>值得注意的是负数在这里不是回文。

实现思路：对于题目给出的数字，将其翻转后再判断是否相等。

<pre> bool isPalindrome(int x) {
        if(x < 0) return false;
        int x1=0,x2=x;
        while(x){
            x1 = x%10 + x1*10;
            x /= 10;
        }
        if(x2 == x1) return true;
        return false;
 }</pre>
 
上面就是我的实现代码，但是其实可以更加简便。因为回文的话只需要计算数的一半和他的另一半的翻转是否相等就可以了，然后通过比较两半是否相等就可以判断回文，这样能够减少一半的运算。

<pre>bool isPalindrome(int x) {
        if(x<0|| (x!=0 &&x%10==0)) return false;
        int sum=0;
        while(x>sum)
        {
            sum = sum*10+x%10;
            x = x/10;
        }
        return (x==sum)||(x==sum/10);//这里的或对应的是<br>基数或者偶数的情况，由于是或操作，只要有一个满足即可
    } </pre>
