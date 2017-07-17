# Merge Two Sorted Lists
题目：Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
<br>实际上就是将两个有序的链表合并成一个新的有序的链表。

实现思路：自定义一个新的链表，然后有一个指针记录着新链表的尾部。下面直接贴出代码。

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
      ListNode new_list(0);
      ListNode *tail = &(new_list);

      while(l1 && l2){
        if(l1->val < l2->val) {
          tail->next = l1;
          l1 = l1->next;
        }
        else {
          tail->next = l2;
          l2 = l2->next;
        }
        tail = tail->next;
      } 
      tail->next = l1 ? l1:l2;
      return new_list.next;
    }
```
值得注意的是头部定义的是一个值为0的节点，所以从它的next开始记录有用的信息。而记录指针tail就是指针类型用于迭代的了。<br>
在迭代的过程中比较l1和l2对应的元素，进行增加节点的操作。<br>
倒数第二句的```tail->next = l1 ? l1:l2;```处理的是l1和l2不等长的情况下，最后肯定就直接将剩余的部分直接放进新链表的尾部，由于while循环的跳出条件是l1和l2都是非空，那么当l1和l2其中有一个空而另一个非空的话就是直接将非空的那个直接放进新的链表里面了。<br>所以这里利用三元条件语句，当l1非空就直接粘l1，反之粘l2，值得注意的是l1和l2在迭代过程中是一直更新的。
最后由于我们是从```tail->next```开始存新的链表的，所以返回的是```new_list.next```
