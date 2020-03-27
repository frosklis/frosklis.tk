---
draft: false
date: 2016-07-28
title: Distance between two random points in a square
---

I don't remember where I read this problem. What is the average distance of two points chosen randomly in a square?

This simple python script gives an approximation.

```python
import random
import math
n = 100000
s = 0
for i in range(n):
    p = [random.random() for i in range(4)]
    s += math.sqrt((p[0]-p[2])**2 + (p[1]-p[3])**2)
print(s / n)
```

Turns out it is around 0.52 (I got 0.5217335102356029 from my simulation). This is a hard one to solve analytically, but we don't need to.
