---
Date: 2025-08-07
tags:
  - csGrammar
  - pythonProject
  - Python
---
### 生词

##### Built-in Types
>内置数据类型
>>特点:最基础、最常用的数据类型
>>直接使用，不需导入任何模块

##### substring
>子字符串



### Method

##### str.replace(old, new[, count])
>**返回一个 str**
>基础用法：
>将str中的 substring old 替换为 substring new
>进阶用法：
>若加上count，则只将前 count 个 substring old 替换为 substring new
>>eg. `txt="orange apple apple"`
>>`txt.replace("orange","apple")
>>`#txt现在为"apple apple apple"`

##### str.split(sep=None, maxsplit=-1)
>**返回一个list, 里面的element为许多substring**
>基础用法：
>将 sep 作为delimiter string 分割原字符串
>进阶用法：
>1. 若传入maxsplit，则取前 maxsplit 个delimiter进行分割，最终list中会有 maxsplit+1 个elements
>2. 若maxsplit 没有传入或等于-1，则在所有delimiter处进行分割
>> eg.`txt="1,2,3"
>> `txt.split(',', maxsplit=1)
>> `#返回['1','2,3']`
>特殊情况：
>1.若
>