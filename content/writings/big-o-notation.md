---
title: Big O Notation
date: 2016-10-01
---

Big-O notation illustrates how a function responds to various inputs. Simply put: How fast will my function run if I change the input from 10 elements to 1000000 elements. Big-O is all about the approximate worst-case performance of doing something. The upper bound is the mathematic limit of the worst output. 

**log** of 50 = x

10^x = 50  

To the power of what do I need to raise 10 to end up with 50. 


#### O(1)

Constant. No matter how large or how big the input is, the duration will be the same duration.

#### O(n)

Linear growth. Looping through all the values once. 

#### O(log n)

Very small increase but not linear. 

#### O(n log n)

No linear growth as we are multiplying by the log of N. But the log of N will never be big so it's goes up slowly.

#### O(n^2)

For every entry in the n long list, you need to do n calculations. N squared

#### O(2^n)

Grows tremendously fast

#### O(!n)

In mathematics, the factorial of a non-negative integer n, denoted by n!, is the product of all positive integers less than or equal to n.

* 1! = 1
* 2! = 2 x 1
* 3! = 3 x 2 x 1
* 4! = 4 x 3 x 2 x 1

This gets out of hand extremely quickly. 


[Big-o Notation cheatsheet](http://bigocheatsheet.com/img/big-o-cheat-sheet-poster.png)

[Lots of extra information and screenshots](http://bigocheatsheet.com/?goback=.gde_98713_member_241501229)

[Good explanation of Big-O](https://justin.abrah.ms/computer-science/big-o-notation-explained.html)
