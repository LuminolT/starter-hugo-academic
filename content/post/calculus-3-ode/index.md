---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Calculus(3) ODE Part"
subtitle: "微积分(3)常微分方程部分整理"
summary: "微积分(3)常微分方程部分整理"
authors: [admin]
tags: [Calculus]
categories: [Mathsmatics]
date: 2021-06-05T00:59:04+08:00
lastmod: 2021-06-05T00:59:04+08:00
featured: false
draft: false
math: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# 0 前言

1.  我烂了

2.  非数学专业书写，仅供微积分3考试参考，具体的拓展概念可能有错，欢迎交流讨论指正

# 1 什么是常微分方程 (Ordinary Differential Equation)?

​	在微积分课程中，我们学到的最后一个章节“微分方程”是被用来解决力学、天文学、物理学等，科学学科的实际问题的. 其中未知函数是一元函数的微分方程称作常微分方程 (Ordinary differential equation)，未知函数是多元函数的微分方程称作偏微分方程 (Partial differential equation).

​	其中，我们学习的部分为常微分方程（以下简称ODE），可以被1.1式定义：
$$
F(x,\frac{\mathrm{d} y}{\mathrm{d} x} ,\frac{\mathrm{d}^2 y}{\mathrm{d} x^2} ,\frac{\mathrm{d}^3 y}{\mathrm{d} x^3} ,\cdots,\frac{\mathrm{d}^n y}{\mathrm{d} x^n} )=0\tag{1.1}
$$
​	其中，$n$称为ODE的阶数 (Order)，是一个很重要的概念.

## 1.1 什么是ODE的通解 (General Solution)?

​	ODE通解(General Solution)的维数应等同于方程阶数，也就是说对于一个二阶ODE，其通解应该有两个自由度 ($C_1$,$C_2$). 与其对应的是特解 (Particular Solution)

​	需要注意的是，通解不一定指所有解，例如对下微分方程：
$$
e^x\mathrm{d}y=y\mathrm{d}x
$$
​	该方程属于1.2节中最典型的可分离变量的ODE，经过变量分离，微分方程表示为以下形式
$$
\frac{\mathrm{d}x}{e^x}=\frac{\mathrm{d}y}{y}
$$
​	两边积分得通解：$-e^{-x}=\ln{\left|y\right|}+C$

​	值得注意的是，在计算过程中我们默认了$y≠0$，但当$y=0$时，可得特解$y^*=C$，但该特解并不包含在上述通解内，此时方程的所有解并不是我们求出的通解.

​	该特解被称为奇点的解，但我们在计算通解时不需要考虑.

## 1.2 可分离变量的ODE (Separable variables ODE)

​	形如1.2式的ODE称为可分离变量的ODE：
$$
f(x)\mathrm{d}y=g(y)\mathrm{d}x\tag{1.2}
$$
​	可以通过变量分离，两遍积分求解：
$$
\int{\frac{\mathrm{d}x}{f(x)}}=\int{\frac{\mathrm{d}y}{g(y)}}+C
$$

# 2 齐次方程 (Homogeneous ODE)

## 2.1 齐次性

​	齐次性描述的是一个函数符合以下性质，我们称这样的函数齐$k$次：
$$
f(ax)=a^kf(x)\tag{2.1}
$$
​	例如：$f(x)=x^2+xy+y^2$，有$f(ax)=a^2(fx)$，为齐二次函数.

## 2.2 齐次方程的形式

​	形如2.2式的ODE称为齐次ODE：
$$
\frac{\mathrm{d} y}{\mathrm{d} x}=g(\frac{y}{x})
$$

## 2.3 齐次方程的解法

​	Step1. 化为一阶可分离变量方程

​	Step2. 设$u=x/y$（比较坏的有$u=y/x$），则有：
$$
\frac{\mathrm{d}y}{\mathrm{d}x}=u+x\frac{\mathrm{d}u}{\mathrm{d}x}\tag{2.3}
$$

# 3 线性方程 (Linear ODE)

## 3.1 线性

​	线性描述的是一个函数符合以下性质：
$$
f(ax)=af(x)\tag{3.1}
$$

$$
f(x+y)=f(x)+f(y)\tag{3.2}
$$

>   ​	具体见线性代数，有定义线性空间的8个基本性质

​	**Rmk:** 线性操作是ODE中很关键的环节，微分算子$\frac{\mathrm{d}-}{\mathrm{d}x}$、欧拉算子$D-$都是符合线性的

## 3.2 一阶线性方程

### 3.2.1 一阶线性方程的形式

​	形如3.3式的ODE称为一阶线性ODE：
$$
\frac{\mathrm{d}y}{\mathrm{d}x}+P(x)y=Q(x)\tag{3.3}
$$
​	其中，若$Q(x)\equiv 0$，则称该方程为**齐次**线性ODE，否则称之为**非齐次**线性ODE.

### 3.2.2 一阶齐次线性方程的解法

​	属于可分离变量的ODE，可以直接记以下公式：
$$
y=Ce^{-\int{P(x)\mathrm{d}x}}\tag{3.4}
$$

### 3.2.3 一阶非齐次线性方程的解法

​	很关键的运用了**常数变易法**，即先猜测方程的解，带入验证，考试时还是直接记公式：
$$
y=e^{-\int{P(x)\mathrm{d}x}}(\int{Q(x)e^{\int{P(x)\mathrm{d}x}}\mathrm{d}x+C})\tag{3.5}
$$

## 3.3 伯努利方程 (Bernoulli ODE)

### 3.3.1伯努利方程的形式

​	形如3.6式的ODE称为伯努利方程：
$$
\frac{\mathrm{d}y}{\mathrm{d}x}+P(x)y=Q(x)y^n\tag{3.6}
$$

### 3.3.2 伯努利方程的解法

​	Step1. 线性化
$$
y^{-n}\frac{\mathrm{d}y}{\mathrm{d}x}+y^{1-n}P(x)=Q(x)
$$
​	Step2. 凑微分
$$
\frac{1}{1-n}\frac{\mathrm{d}y^{1-n}}{\mathrm{d}x}+y^{1-n}P(x)=Q(x)
$$
​	Step3. 换元整理
$$
\frac{\mathrm{d}z}{\mathrm{d}x}+z(1-n)P(x)=(1-n)Q(x)
$$
​	Step4. 当做一阶非齐次线性方程求解

​	Step5. 还元

## 3.4 可降阶的高阶微分方程

​	害这不就是大学物理吗.

## 3.5 高阶线性微分方程解的结构

​	害这不就是线性代数吗.

## 3.6 常系数微分方程

### 3.6.1 常系数微分方程的形式

​	以二次常系数线性微分方程为例，其他也是一样的：
$$
\frac{\mathrm{d}^2y}{\mathrm{d}x^2}+p\frac{\mathrm{d}y}{\mathrm{d}x}+qy=f(x)\tag{3.7}
$$
​	其中，若$f(x)\equiv 0$，则称该方程为**齐次**的，反之为**非齐次**的.

### 3.6.2 常系数齐次微分方程的解法

​	Step.1 写出对应方程的特征方程，以式3.7中方程为例，则为3.8式：
$$
r^2+pr+q=0\tag{3.8}
$$
​	Step.2 根据解的情况，其通解形式也不同：

| 特征方程根的情况                            | 齐次微分方程的通解                                     |
| ------------------------------------------- | ------------------------------------------------------ |
| $\Delta>0$，不等实根 $r1,r2$                | $y=C_1e^{r_1x}+C_2e^{r_2x}$                            |
| $\Delta=0$，二重实根 $r$                    | $y=(C_1+C_2x)e^{rx}$                                   |
| $\Delta<0$，共轭虚根 $\lambda \pm \omega i$ | $y=e^{\lambda x}(C_1\cos{\omega x}+C_2\sin{\omega x})$ |

### 3.6.3 常系数非齐次微分方程的解法

​	首先，解出对应齐次方程的通解$y_g$，再用常数变易法求特解

​	其中，我们能够解决的只对应两种情况，即为3.7式中$f(x)=P_n(x)e^{\alpha x}$ 或 $f(x)=P_n(x)e^{(\lambda+\omega i) x}$，

​	公式理解比较麻烦，建议直接看例题.

## 3.7 欧拉方程(Euler Equation)

​	以二阶为例，形如3.9式的方程称为欧拉方程：
$$
x^2\frac{\mathrm{d}^2y}{\mathrm{d}x^2}+xp\frac{\mathrm{d}y}{\mathrm{d}x}+qy=f(x)\tag{3.8}
$$
​	设$x=e^t$，并引入欧拉算子$\mathrm{D}=\frac{\mathrm{d}}{\mathrm{d}t}=x\frac{\mathrm{d}}{\mathrm{d}x}$

​	则原方程可化为：
$$
\mathrm{D}^2y+p\mathrm{D}y+qy=g(t)
$$
​	然后按照3.6.3继续求解即可

# 4 全微分方程(Totol Differential Equation)

## 4.1 全微分方程的条件

​	对方程$P(x,y)\mathrm{d}x+Q(x,y)\mathrm{d}y=0$，若满足$\frac{\partial Q}{\partial x} =\frac{\partial P}{\partial y}$，则称该方程为全微分方程.

## 4.2 全微分方程的解法

### 4.2.1 公式法

​	公式如4.1式，注意$(x_0,y_0)$的选取，一定在函数的定义域内：
$$
u(x,y)=\int_{x_0}^{x}{P(x,y)\mathrm{d}x}+\int_{y_0}^{y}{Q(x_0,y)\mathrm{d}y}\tag{4.1}
$$

### 4.2.2 偏积分法

​	和常数变易法类似，用不太到，算咯.

### 4.2.3 烧香拜佛法

​	随缘凑微分，没什么好讲的.

## 4.3 积分因子

​	取一个神秘的$\mu(x,y)$使得$\mu(x,y)P(x,y)\mathrm{d}x+\mu(x,y)Q(x,y)\mathrm{d}y=0$变成全微分方程.

​	随缘凑微分，没什么好讲的.
