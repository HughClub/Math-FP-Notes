# 数字

## Peano 自然数公理

1. 0是自然数。用符号表示为$\exists 0 \in N$;
2. 每个自然数都有它的下一个自然数，称为它的后继。用符号表示为$\forall n \in N, \exists n' = succ(n) \in N$;
3. 0不是任何自然数的后继。用符号表示为$\forall n \in N: n' \neq 0$;
4. 不同的自然数有不同的后继数。或者说，如果两个自然数的后继数相同，那么这两个自然数相等。用符号表示为$\forall n, m \in N: n' = m' \Rightarrow n = m$;
5. 如果自然数的某个子集包含0，并且其中每个元素都有后继元素。那么这个子集就是全体自然数。用符号表示为$\forall S \subset N: (0 \in S \land \forall n \in S \Rightarrow n' \in S) \Rightarrow S = N$.


可以构建出一阶算术系统(Peano 算术系统)

## 自然数和计算机程序

```Haskell
data Nat = zero | succ Nat
```

定义加法

$$
a+0=a\\
a+b'=(a+b)'
$$

定义乘法

$$
a \cdot 0=0\\
a\cdot b'=a\cdot b+a
$$

定义重复运算的简单形式

```
n=foldn(zero,succ,n) // 自然数的简单记法
// foldn 函数实现
foldn(z,f,0)=z
foldn(z,f,n')=f(foldn(z,f,n))
```

## 自然数的结构

定义累加和阶乘

$$
sum(0)=0\\
sum(n+1)=(n+1)+sum(n)
$$


$$
fact(0)=1\\
fact(n+1)=(n+1)\cdot fact(n)
$$

统一运算形式
$$
f(0)=c\\
f(n+1)=h(f(n))
$$

使用原始递归形式 `f=foldn(c,h)`

使用 `foldn` 定义累加和阶乘

```
// 定义额外操作
1st(a,b)=a
2nd(a,b)=b

// 累加
c=(0,0)
h(m,n)=(m',m'+n)
sum=2nd(foldn(c,h))

// 阶乘
c=(0,1)
h(m,n)=(m',m'n)
fact=2nd(foldn(c,h))
```

## 自然数的同构

定义列表
```haskell
data List A= nil | cons(A,List A)
```

列表的连接运算 `++`

```
nil++y=y
cons(a,x)++y=cons(a,x++y)
```

**该形式同构于自然数加法**

## 练习

### 证明

#### 加法交换律

#### 加法结合律

当$c=0$的情况下成立
$$
(a+b)+0=a+b\\
=a+(b+0)
$$

推广形式

$$
(a+b)+c'=(a+b+c)'\\
=(a+(b+c)')\\
=a+(b+c)'\\
=a+(b+c')
$$

#### 乘法结合律

#### 乘法交换律

### 使用`foldn`定义

#### 定义平方 $()^2$

```
c=(0,1)
h(m,n)=(m+m+n,n')
square=1st . foldn(c,h)
```

#### 定义 $()^m$

#### 定义奇数和

```
c=(1,3)
h(m,n)=(m+n,n'')
odd_sum=foldn(c,h)
```