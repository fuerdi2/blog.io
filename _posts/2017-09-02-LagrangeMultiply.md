---
layout: post
title: 拉格朗日乘数法几何意义推导
date: 2017-09-02
categories: blog
tags: [数学]
description: 
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

## 拉格朗日乘数法简介
　　在数学最优问题中，拉格朗日乘数法（以数学家约瑟夫·路易斯·拉格朗日命名）是一种寻找变量受一个或多个条件所限制的多元函数的极值的方法。假设目标函数形式为\\(f(x,y)\\),其中x,y满足的约束条件为\\(\\phi (x,y)=0\\)。当x,y为何值时，目标函数f的值会最小呢？为了解决这个问题，我们可以构造拉格朗日函数\\(L(x,y,\lambda)=f(x,y)+\\lambda \\phi (x,y)\\),求解方程组\\((Eq.1)\\)

$$
\frac{\partial L}{\partial x} = 0,\\
\frac{\partial L}{\partial y} = 0,\\
\phi (x,y)=0,\\
(Eq.1)
$$

就能够得到使得函数\\(f(x,y)\\)最小的\\(x,y\\)值。
## 几何意义
　　看到这里我们不禁要问，为什么通过构造拉格朗日函数，并求解该方程组就可以得到使得函数\\(f(x,y)\\)最小的x,y值呢？让我们回想在大学里学到过的知识：函数\\(f(x,y)\\)在空间坐标系中的表现形式是一张曲面，如图1所示。
<center>
<img src="https://fuerdi2.github.io/img/Lagarange_1.png" width = "50%">
图1：f(x,y)的空间表现形式
</center>
作曲面的等值线并投影至平面\\((x,y)\\)坐标系，见图2。
<center>
<img src="https://fuerdi2.github.io/img/Lagrange_3.png" width = "50%">
图2：f(x,y)等值线
</center>
从图中我们可以看到，同一条等值线上\\(f(x,y)\\)相同。等值线圈向外扩大，\\(f(x,y)\\)的值也就增大；等值线圈向内收缩，\\(f(x,y)\\)的值也就越小。但是，由于约束条件\\(\\phi (x,y)=0\\)使得等值线圈不可能无限向外扩大或者是向外缩小，函数\\(f(x,y)\\)的等值线与\\(\\phi (x,y)=0\\)相切点，即为\\(f(x,y)\\)的极大值或者极小值点，见图3。
<center>
<img src="https://fuerdi2.github.io/img/Lagrange_2.png" width = "50%">
图3：切点示意图
</center>
点\\((x^{\star},y^{\star})\\)为切点的充分必要条件是

$$
(\frac{\partial f}{\partial x^{\star}},\frac{\partial f}{\partial y^{\star}})= \gamma (\frac{\partial \phi}{\partial x^{\star}},\frac{\partial \phi}{\partial y^{\star}}),\\
\phi (x^{\star},y^{\star}) = 0,\\
\gamma = Constant,\\
(Eq.2)
$$

将\\((Eq.2)\\)展开得到

$$
\frac{\partial f}{\partial x^{\star}} = \gamma \frac{\partial \phi}{\partial x^{\star}},\\
\frac{\partial f}{\partial y^{\star}} = \gamma \frac{\partial \phi}{\partial y^{\star}},\\
\phi (x,y)=0,\\
\gamma = Constant,\\
(Eq.3)
$$

　　一看到这里，是不是觉得非常熟悉，不就是类似于拉格朗日乘数法求解的展开式吗\\((Eq.4)\\)？

$$
\frac{\partial L}{\partial x} = \frac{\partial f}{\partial x^{\star}}+\lambda \frac{\partial \phi}{\partial x^{\star}}=0,\\
\frac{\partial L}{\partial y} = \frac{\partial f}{\partial y^{\star}}+\lambda \frac{\partial \phi}{\partial y^{\star}}=0,\\
\phi (x,y)=0,\\
(Eq.4)
$$

使\\(\lambda = - \gamma\\)，\\((Eq.4)\\)就成了\\((Eq.3)\\)。