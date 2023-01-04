---
title: 如何在python中draw samples
author: yuanbo
date: 2020-10-25
slug:  python-drawing-samples
category:   
tags: 
draft: no
---



# 如何在python中draw samples



https://stackoverflow.com/questions/10803135/weighted-choice-short-and-simple/15907274



[Youtube videos tutorial]https://www.youtube.com/watch?v=KzqSDvzOFNA&pbjreload=101&ab_channel=CoreySchafer



Since Python 3.6 there is a method [`choices`](https://docs.python.org/dev/library/random.html#random.choices) from the [`random`](https://docs.python.org/dev/library/random.html#module-random) module.

```python
import random
random.choices(population = [['a','b'], ['b','a'], ['c','b']],
               weights = [0.2, 0.2, 0.6],
               k = 10)
```

```python
import random
random.choices(['one', 'two', 'three'], [0.2, 0.3, 0.5], k=10)
```

也可以用numpy模块

```python
numpy.random.choice(items, trials, p = probs)
```

Since [numpy](https://stackoverflow.com/questions/tagged/numpy) version 1.7 you can use [`numpy.random.choice()`](http://docs.scipy.org/doc/numpy-1.7.0/reference/generated/numpy.random.choice.html):

```python
elements = ['one', 'two', 'three'] 
weights = [0.2, 0.3, 0.5]

from numpy.random import choice
print(choice(elements, p = weights))
```





通过这个语句可以按照一定的概率选取一个或几个元素，用来控制强化学习任务中的输钱和赢钱的

```python
random.choices(population = ['H', 'T'], weights = [0.3, 0.7], k = 1)
```



Note that `random.choices` will sample *with replacement*, per the [docs](https://docs.python.org/dev/library/random.html#random.choices):





https://pynative.com/python-random-choice/

Use random.choice() to Randomly select an item from a list

```python
import random
movie_list = ['The Godfather', 'The Wizard of Oz', 'Citizen Kane', 'The Shawshank Redemption', 'Pulp Fiction']

moview_item = random.choice(movie_list)
print ("Randomly selected item from list is - ", moview_item)
```



https://pynative.com/python-weighted-random-choices-with-probability/

**random.choices()**

Python 3.6 introduced a new function [choices()](https://docs.python.org/3/library/random.html#random.choices) in the [random module](https://pynative.com/python-random-module/). By using `random.choices()` we can make a weighted random choice with replacement. You can also call it a weighted [random sample](https://pynative.com/python-random-sample/) with replacement. Let’s have a look into the syntax of this function.