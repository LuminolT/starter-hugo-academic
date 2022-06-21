---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "A Guide for Newbies in Cryptography"
subtitle: "密码学学习路线"
summary: "密码学学习路线"
authors: [admin]
tags: [Cryptography]
categories: []
date: 2022-06-21T18:52:53+08:00
lastmod: 2022-06-21T18:52:53+08:00
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

## 什么是密码学？

密码学是数学和计算机科学的交叉学科。在国内一般作为
信息安全专业的必修课程。密码学的开端是Shannon在1945年发表的《Communication Theory of Secrecy Systems》而在这之前，密码更像是一种技艺（Art）而非一种科学技术（Technique）。

> You can check the [Wiki Page](https://zh.wikipedia.org/wiki/%E5%AF%86%E7%A0%81%E5%AD%A6) for more information.

按照Shannon理论，密码学可分为两个阶段：

- 古典密码学：基于巧妙构造形成的Art
- 现代密码学：基于数学原理形成的Technique

## 古典密码学

一种比较有趣的，并且能在影视剧中看到的古典密码叫做滚筒密码。滚筒密码的加密原理就是双方规定好木棍的直径，写信人把腰带绑在木棍上书写，在收信人收到信之后，只需要把腰带绑到相同规格的木棍上就能还原信的内容。

![滚筒密码](https://nic.sdufe.edu.cn/__local/3/B1/28/67F57C5431D87E41BCC727F9364_90183162_2CDE.jpg)

如果用现代密码学的语言去描述，信件的内容即为明文，通过滚筒写出来的纸片就是明文，而密钥就是那根木棍。

而实质上我们可以发现，我们是在对一个字符串间隔取字符：
例如对串：`Hello-Crypto!`，我们把他写在正四棱柱形成的纸带上，就可以获得：`Hoy!e-plCtlro`，而这和隔4个字符1取的操作是一样的，我们可以给出一个形式化的代码实现：

```python
>>> def encrypt(msg: string, key: int) -> string:
...     splitted_str = ['' for _ in range(key)]
...     iter = 0
...     for ch in msg:
...         splitted_str[iter].append(ch)
...         iter += 1
...     cipher = ''
...     cipher.join(splitted_str)

>>> encrypt('Hello-Crypto!', 4)
'Hoy!e-plCtlro'
```

而事实上，这就是一个栅栏密码，你可以在[这个网站](https://www.qqxiuzi.cn/bianma/zhalanmima.php)上尝试。

> 解密过程偷懒不写啦，聪明如你一定能自己figure out!

而这就是古典密码学从最原始的的阶段，步入了近现代的阶段。从一些工具的使用，变成了算数。在此基础上形成了大量的替换密码（如Caesar密码、Vigenère密码）。

> 事实上computer最早的含义是计算员，大多都是一些熟练算术技巧的人来破译密码的，而我们熟知的Alan Turing事实上在二战时也是负责这个工作。


## 现代密码学

现代密码学的开端是Shannon的那篇文章，其中提出了一个重要的概念，完美安全性（Perfect Security）。完美安全性的形式化定义用到了概率论的知识，因此此处不展开。我们仅对其产生的原因进行一些阐述。

古典密码在当时基本全都被破解了，密码欠缺一个正式的、准确的定义去衡量证明一个密码方案是否具有严格的安全性，因此Shannon理论应运而生。

一个密码体系保证完美安全性，当其加密后的密文不会透露任何关于明文的信息。而在这种定义下，即使攻击者拥有无穷的算力，也不能被破解。

> 😮注意，是无穷的算力！

但是根据Shannon的推论，一个保证完美安全性的密码体系，其密钥空间一定大于明文空间。也就是说，我的密钥不会比明文更短。而我们可以思考，如果有一个信道，可以安全的用于传输密钥，为什么不直接拿来传输明文呢？因此目前的密码体系都**不保证**完美安全性。

而在这基础上，就催生了流密码和分块密码，他们被统称为对称密码学。总的来说，对称密码学致力于让短密钥经过一些神奇的操作，也可以发挥和长密钥相同的作用：

- 流密码：通过随机数生成器序列，生成长密钥
- 分块密码：通过对明文分块，逐一用短密钥加密

> 此处是非常不严谨的表达，仅作为理解

而与之对应的，是非对称密码学（又称为公钥密码学），该类密码体系的特点是拥有公钥和私钥两个密钥，他们往往基于数学上的难题进行规约：

- RSA：大数质因数分解难题
- ElGamal：模乘群上的离散对数问题
- ECC-ElGamal：椭圆曲线加法群上的离散对数问题

一个简单的例子是，给定两个大质数$p, q$，给你他们的乘积$N = pq$，你是很难分别求解出$p$和$q$的。

> 😈试试吧！N = 115157048927615167000080222307830600550443405087336034834570254657109854848846966155326673813367130632850579378687042597345617010423842872052308839845927421052730005967200985762648016655477422221735535543563770813175765249421783025141172284969133662823566566070113584080582203941254237438639149018559749238997

而这种数学上的难解特性就可以被利用，构造密码体系。

> 具体需要一些数论和抽象代数的知识，这里就不展开啦~

## 小结

事实上，上面两个问题都只解决了数据隐秘性的保护，不一定能够保证数据仍是完整的、未被篡改过的。而这就需要更多的知识，包括：

- 消息认证码
- 数字签名

而目前随着量子计算机的出现，Shor算法已经从理论上证明了能够在多项式时间内攻破目前常见的密码体系，于是又有了一些后量子密码学的研究：

- 格密码学
- 编码密码学

当然还有一些和其他方向的交叉，如：

- 区块链（散列和共识机制）
- 安全多方计算（联邦学习）
- 零知识证明

## 学习路线

笔者的学习路线是：密码基础-数学基础-现代密码学，比较诡异，下面整理一下比较正常的路线：

1. 数学基础：离散数学、数论、近世代数、概率论
2. 古典密码学：了解代换密码
3. 对称密码学：流密码、对称密码、PRG、PRF
4. 非对称密码学：Diffie-Hellman密钥交换、陷门函数、RSA、ElGamal、同态加密
5. 应用密码学：哈希函数、消息认证码、数字签名

推荐一些书目：
- [Introduction to Modern Cryptography](http://www.cs.umd.edu/~jkatz/imc.html#:~:text=Introduction%20to%20Modern%20Cryptography%20is%20an%20introductory-level%20treatment,without%20sacrificing%20rigor%20or%20an%20emphasis%20on%20foundations.), Jonathan Katz and Yehuda Lindell
- 初等数论, 潘承洞、潘承彪
- 抽象代数学, 姚慕生