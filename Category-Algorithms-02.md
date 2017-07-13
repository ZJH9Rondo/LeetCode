# LeetCode-Category-Algorithms-02

## Title
  * Add Two Numbers

  * Descriptions
  > You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
  You may assume the two numbers do not contain any leading zero, except the number 0 itself.

  * Example
  ```
      Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

      Output: 7 -> 0 -> 8
  ```

### How can I solve the question

   > 首先，根据问题描述，目的是对两数求和，但是数据结构使用的是链表存放数据，并且如果当前从两个链表读取到的结点数据累加和大于9，那么当前两链表结点的和按0算，并给next结点的求和值加1，也就是为什么在Example中当4+6=10时，结点存放的是当前值对10取余的结果，而next结点上4+3不为7，而为8的原因，弄明白需求是什么之后，接下来的问题是我用javascript写，那么如何用javascript来写链表这个数据结构是一个问题，当这个问题解决，那就可以AC掉这道题了(当然，第二个问题是对我个人而言，不用javascript写的就不用关注了)。


### code
  * 我的实现(参考open solution)
  * Runtime: 229ms

    ```
            /**
        * Definition for singly-linked list.
        * function ListNode(val) {
        *     this.val = val;
        *     this.next = null;
        * }
        */
        /**
        * @param {ListNode} l1
        * @param {ListNode} l2
        * @return {ListNode}
        */
        var addTwoNumbers = function(l1, l2) {
            var ListNode1 = l1,
                ListNode2 = l2,
                ListNodeSum = new ListNode(-1),
                LastNode = ListNodeSum,
                CurrentNode,
                LastSum = 0;

            while((ListNode1 !== null) || (ListNode2 !== null)){
                    var CurrentSum = (ListNode1 && ListNode1.val || 0) + (ListNode2 && ListNode2.val || 0) + LastSum;
                    CurrentNode = new ListNode(CurrentSum % 10);
                    LastNode.next = CurrentNode;
                    LastNode = LastNode.next;
                    LastSum = (CurrentSum > 9)?1 : 0;
                    ListNode1 = ListNode1 && ListNode1.next || null;
                    ListNode2 = ListNode2 && ListNode2.next || null;  
            }
            if(LastSum){
                LastNode.next = new ListNode(LastSum);
            }
            return ListNodeSum.next;
        };
    ```

  * 大牛实现
  * Runtime: 185ms
    ```
            /**
        * Definition for singly-linked list.
        * function ListNode(val) {
        *     this.val = val;
        *     this.next = null;
        * }
        */
        /**
        * @param {ListNode} l1
        * @param {ListNode} l2
        * @return {ListNode}
        */
        var addTwoNumbers = function(l1, l2) {
            var carry = 0
            var p1 = l1
            var p2 = l2
            var head = new ListNode(-1)
            var p = head
            while (p1 || p2)
            {
                var v1 = 0
                var v2 = 0
                if (p1)
                {
                    v1 = p1.val
                    p1 = p1.next
                }
                if (p2)
                {    
                    v2 = p2.val
                    p2 = p2.next
                }
                var s = v1+v2+carry
                if (s>9)
                {
                    carry = 1
                    s = s % 10
                }
                else
                {
                    carry = 0
                }
                p.next = new ListNode(s)
                p = p.next
            }

            if (carry)
            {
                p.next = new ListNode(carry)
            }
            return head.next
        };
    ```
### 对比总结

#### 对比

    > 代码逻辑上区别几乎没有，Runtime之所以高是因为在程序的编写上，在运算中整和了过多的判断条件，导致Runtime变化，如果将判断作为先决条件分离出来，Runtime肯定会降低。

#### 总结
  * 代码在编写时尽可能不要在实际操作部分混入逻辑判断代码，影响其执行速率
  * 如何用javascript写各种基本的数据结构

#### 知识点
  * 如何用javascript写链表
    > 如果你熟悉链表这个数据结构的基本原理的话，那么对于javascript而言，实现其实就是利用的对象来实现链表以及表示其各个结点，但用javascript做链表，数据小的时候还能玩玩，数据大了，根本不行，你想象过嵌套1000个对象，甚至10000个对象是什么概念吗？所以，归根到底还是要用其他强类型语言来实现的，个人选择C来实现，毕竟是入门时的选择(逃)。

  * 下面是一个实例的javascript实现的增删改查的链表操作代码

    ```
            function LinkedList() {
                var Node = function (element) {　　　　　　　　//新元素构造
                    this.element = element;
                    this.next = null;
                };
                var length = 0;
                var head = null;

                this.append = function (element) {
                    var node = new Node(element);　　　　　　　　//构造新的元素节点
                    var current;
                    if (head === null) {　　　　　　　　　　　　　//头节点为空时  当前结点作为头节点
                        head = node;
                    } else {
                        current = head;　　　　　　　　　　　　　　
                        while (current.next) {　　　　　　　　　　//遍历，直到节点的next为null时停止循环，当前节点为尾节点
                            current = current.next;
                        }
                        current.next = node;　　　　　　　　　　　　//将尾节点指向新的元素，新元素作为尾节点
                    }           
                    length++;　　　　　　　　　　　　　　　　　　　　//更新链表长度
                };

                this.removeAt = function (position) {
                    if (position > -1 && position < length) {
                        var current = head;
                        var index = 0;
                        var previous;
                        if (position == 0) {
                            head = current.next;
                        } else {
                            while (index++ < position) {
                                previous = current;
                                current = current.next;
                            }
                            previous.next = current.next;
                        }
                        length--;
                        return current.element;
                    } else {
                        return null;
                    }
                };

                this.insert = function (position, element) {
                    if (position > -1 && position <= length) {　　　　　　　　//校验边界
                        var node = new Node(element);　　　　　　　　
                        current = head;
                        var index = 0;
                        var previous;
                        if (position == 0) {　　　　　　　　　　　　　　　　　　　　//作为头节点，将新节点的next指向原有的头节点。
                            node.next = current;
                            head = node;　　　　　　　　　　　　　　　　　　　　　　　　//新节点赋值给头节点
                        } else {
                            while (index++ < position) {
                                previous = current;
                                current = current.next;
                            }　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　//遍历结束得到当前position所在的current节点，和上一个节点
                            previous.next = node;　　　　　　　　　　　　　　　　　　　　//上一个节点的next指向新节点  新节点指向当前结点，可以参照上图来看
                            node.next = current;
                        }
                        length++;
                        return true;
                    } else {
                        return false;
                    }

                };

                this.toString = function () {
                    var current = head;
                    var string = '';
                    while (current) {
                        string += ',' + current.element;
                        current = current.next;
                    }
                    return string;
                };

                this.indexOf = function (element) {
                    var current = head;
                    var index = -1;
                    while (current) {
                        if (element === current.element) {　　　　　　　　　　　　//从头节点开始遍历
                            return index;
                        }
                        index++;
                        current = current.next;
                    }
                    return -1;
                };

                this.getLength = function () {
                    return length;
                }
        }
    ```
