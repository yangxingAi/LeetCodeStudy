#	合并链表
##	题目描述
>	输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。
示例1：
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
##	思路：
###	遍历判断：
1.	创建一个伪头结点node，创建一个cur指向头结点。循环遍历结束条件为两个链表其中有一个为空。
2.	遍历l1,l2，将其数值小的节点接到cur的后面，将合并的当前链表下移一个节点，
3.	将cur = cur.next
4.	当遍历结束的时候，必有一个链表为空，把不为空的链表全部拼接到cur的后面就完成了。

```java
 public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode node = new ListNode(0);
        ListNode cur = node;
        while(l1 != null && l2 != null){
            if (l1.val < l2.val){
                cur.next = l1;
                l1 = l1.next;
            }else {
                cur.next= l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }

        cur.next = l1 ==null? l2: l1;
        return node.next;
    }
```
###	递归方法:
1.	如果l2为空返回l1， 如果l1为空返回l2
2.	创建一个新节点保存合并节点
3.	新链表的尾部指向下一个比较后的节点，如果是l1的节点则l1往后移动，如果是l2的节点则l2往后移动

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1==null)
        return l2;
        if(l2==null)
        return l1;
        if(l1.val<=l2.val){
            l1.next = mergeTwoLists(l1.next,l2);
            return l1;
        }else{
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }
    }
```
