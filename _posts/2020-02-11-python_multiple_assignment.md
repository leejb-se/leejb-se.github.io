---
title : "Python multiple assignment (파이썬 다중 할당)"
date : "2020-02-11 11:56:00"
categories : Free
comments : True
tags : []
---

# Python multiple assignment (파이썬 다중 할당)
이번에 Leetcode문제 [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)를 풀면서 하나 알게된 테크닉이 있다. 바로 파이썬 다중 할당이라는것인데, 말 그대로의 것이다. 한번 봐보자

```python
x = 1
y = 2
x = y
y = x+y
print(x)
>>> 2
print(y)
>>> 4
```
이것은 다중할당을 하지 않은 것인데, 우리가 이미 당연히 아는 결과가 나온다.
그렇다면 다음 코드를 보자
```python
x = 1
y = 2
x , y = y , x+y 
print(x)
>>>2
print(y)
>>>3
```
단순히 값의 할당을 2줄로 하던걸 1줄로 줄였을 뿐인데 다른 결과가 나온다.  무엇 때문일까?

(사실 간단한 예시기때문에 충분히 직관적으로 이해 할 수있다.
하지만 그 이유에 대해서 살펴보자)

파이썬 docs에서 [evaluation order](https://docs.python.org/3/reference/expressions.html#evaluation-order)이라는 항목이 있다. 한번 살펴보자

> Python evaluates expressions from left to right. Notice that while evaluating an assignment, the right-hand side is evaluated before the left-hand side.

간단하게 해석해보자면 파이썬은 expressions를 evaluate할 때 left ->right로 하는데
right side는 left side보다 먼저 evaluated 된다는것이다.

즉 위에서의 
```python
x , y = y , x+y 
```
에서 오른쪽에 있는 y 와x+y가 먼저 값이 결정되고 이 값이 x와y에 할당된다는 것이다.

별거 아닌것처럼보여도 꽤나 유용한 개념이다.
예를 들자면 ,위에서 말한 206번 문제를 풀 때 사용하면 좋은 테크닉이다.

다음 포스팅에서 같이 풀어보자.  