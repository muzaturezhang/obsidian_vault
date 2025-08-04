---
Date: 2025-08-04
aliases:
  - function‘s arguments in Python
tags:
  - csGrammar
  - Python
---

## 宏观分类Python中的参数类型

### 按使用位置分，分为形参(定义函数时)和实参(调用函数时)
**这是大分类，形参和实参下有各自一套不同的命名方法**

#### 形参

**形参的5种类型**
1. 限定位置形参
2. 普通形参
3. 特殊形参args*
4. 限定关键字形参
5. 特殊形参kwargs**

函数定义时 形参列表的顺序也按照上述顺序
即： `def func1(a,b,c,/,m,n,*,args*,kw1,kw2,**kwargs)`


> **限定位置形参**
> 
