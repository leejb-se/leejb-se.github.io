---
title : "Leetcode - 206.Reverse linked list"
date : "2020-02-23 08:23:00"
categories : Leetcode
comments : True
tags : []
---
# 206. Reverse Linked List
[문제링크](https://leetcode.com/problems/reverse-linked-list/)

> 단일 연결리스트의 head가 주어졌을 때 reverse해서 반환하라.

전에 다중할당에 대해서 보았다. 이 문제가 이를 활용하는 문제 이므로 한번 풀어 보자.


```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        reverse = None

        while(head != None):
            head , reverse , reverse.next = head.next , head , reverse
        return(reverse)
```
보면 알겠지만
reverse 를 none으로 설정하고 

head 와 reverse, reverse.next 를 각각 head.next , head, reverse로 할당해주면 된다. 

예를들어 head가   1->2->3->4->5 의 1을 참조하고있고 
reverse = None 이라 해보자.
그리고 

```python
head , reverse , reverse.next  = head.next  , head , reverse
```
을 실행한다하면

먼저 right side가 먼저 evaluate된다.

즉, head.next 는 2->3->4->5 의 2를 참조하는것이고
 head는 1->2->3->4->5의 1을 참조하는것이고
 reverse는 None 이다.
이것을 head와 reverse, reverse.next에 각각 할당하면 
head 는 2->3->4->5 의 2를 참조하고

reverse는 1->2->3->4->5의 1을 참조하고
reverse.next 는 None을 참조하니까 
실제로 reverse는 1->None의 1을 참조하게 될것이다 
즉, 한번 저 다중할당이 일어나면 head는 2->3->4->5 의 2를참조
reverse는 1->None의 1을 참조 하게 되는것이다.

그런데 만약 다중할당을 안하게된다면 어떻게 될까?

똑같은 상황에서 코드가
```python
reverse , reverse.net = head , reverse
head = head.next 
```
라고 해보자

Right side가 먼저 evaluate되므로
head 는 1->2->3->4->5의 1을참조
reverse는 None 
이것이 각각 할당되면
reverse가 1->2->3->4->5 의 1을 참조하게되고
reverse.next 는  None을 참조하게 되므로
실제로 reverse는 1->None의 1을 참조하는것인데...

여기서 무엇이 문제냐면 
reverse가 참조하는 1과 head가 참조하는1이 같았다는것이다.
즉 reverse 와 head가 같은 객체를 참조했으므로
head도 1->None이 되었다는것이다.
따라서 다중할당을 한번에 하지않으면 이런 불상사가 생기는것이다.

이것을 visualize해서 보자면

[다중할당 활용](http://pythontutor.com/visualize.html#code=class%20ListNode:%0A%20%20%20%20def%20__init__%28self,%20val=0,%20next=None%29:%0A%20%20%20%20%20%20%20%20self.val%20=%20val%0A%20%20%20%20%20%20%20%20self.next%20=%20next%0A%0Ahead%20=%20ListNode%281,ListNode%282,ListNode%283,ListNode%284,ListNode%285%29%29%29%29%29%0A%0Areverse%20=%20None%0Awhile%28head%20!=%20None%29:%0A%20%20%20%20head,%20reverse,%20reverse.next%20=%20head.next,%20head%20,%20reverse%0A%20%20%20%20%0A&cumulative=false&curInstr=0&heapPrimitives=false&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false) 
[다중할당 활용X](http://pythontutor.com/visualize.html#code=class%20ListNode:%0A%20%20%20%20def%20__init__%28self,%20val=0,%20next=None%29:%0A%20%20%20%20%20%20%20%20self.val%20=%20val%0A%20%20%20%20%20%20%20%20self.next%20=%20next%0A%0Ahead%20=%20ListNode%281,ListNode%282,ListNode%283,ListNode%284,ListNode%285%29%29%29%29%29%0A%0Areverse%20=%20None%0Awhile%28head%20!=%20None%29:%0A%20%20%20%20reverse%20,%20reverse.next%20=%20head%20,%20reverse%0A%20%20%20%20head%20=%20head.next%0A&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

여기서 확인 가능하다.
파이썬 다중할당의 강력함을 느낄 수 있을것이다.
