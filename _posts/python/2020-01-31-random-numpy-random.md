---
layout:     post
title:      python
subtitle:   比较random和numpy.random
date:       2020-01-31
author:     赵梓杉
header-img: img/blog/desk_blue.jpg
catalog: true
tags:
    - python

---

在Python中，使用Random方法有random.rand(), random.random(), random.randn()等几种用法，这篇文章整理下他们的区别：

**Random.rand(x,y)** 
在[0,1)平均分布中，随机生成x行y列的数组 
```
import numpy as np
a = np.random.rand(3,4)
a
#返回结果：
array([[0.21910559, 0.05793295, 0.7849145 , 0.05153582],
       [0.30389682, 0.6197685 , 0.15432231, 0.28394065],
       [0.02324611, 0.57761753, 0.32870006, 0.23687286]])
#返回结果中，所有元素都是在[0,1)范围内
```
**Random.random((x,y))** 
在[0,1)连续均匀分布中，随机生成x行y列的数组，表达时，括号中需要是元素(x,y)

```
import numpy as np
b = np.random.random((3,4))
b
#返回结果：
array([[0.78222625, 0.33768558, 0.71446672, 0.87338934],
       [0.05477066, 0.93346398, 0.96674004, 0.09631826],
       [0.55809982, 0.79443892, 0.52232507, 0.50771992]])
#返回结果中，所有元素都是在[0,1)范围内
```



**Random.randn(x,y)** 
#n代表normal distribution正态分布，所以randn是在正态分布中随机取值，随机生成x行y列的数组

```
import numpy as np
c = np.random.randn(3,4)
c
#返回结果：
array([[-1.11484323, -0.65341823,  0.65742213,  0.75972666],
       [ 1.61186733,  1.10022426,  0.47649539, -0.48034237],
       [ 0.22707267, -0.92035598,  0.42941085,  1.3884699 ]])
#返回结果中，取出了标准正态分布的随机数，有正数有负数。
```
我们可以留意到，上面的情况是符合Standard Normal Distribution标准正态分布的，如果是Normal Distribution，平均值和方差不为0的时候应该怎么写代码呢？

当满足N(μ,σ^2)的正态分布，其中μ表示平均值mean,σ2  表示方差variance。随机取值时，可以使用语句 σ * np.random.randn(x,y) + μ 

```
import  numpy as np 
import math 
d = math.sqrt(5) * np.random.randn(2,3) + 10 
d
#返回结果：
array([[ 9.22747308, 10.66586555,  9.5086992 ],
       [ 8.97535766, 14.55856398, 12.89246362]])
#返回结果中，取出了均值为10，方差为5的正太分布N(10, 5)的2行3列的随机数
```
总结：
1. np.random.rand()以及np.random.random()返回的结果都在[0,1)范围内，功能基本一致，区别在于表达时，random括号中需要体现元素()。
2. np.random.randn()跟上面两个存在很大区别，取值时侧重于在正态分布的范围内，书写时，添加的内容也会更多。

