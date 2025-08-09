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

##### mapping
>一种键值对 key-value 的数据结构，最常见的为dictionary字典


##### docstring
>文档字符串
>用来标注说明**模块、函数、方法、类**的字符串，写在函数定义的下面
### Method

##### str.replace(old, new[, count])
>**返回一个 str(注意是返回一个新的str，而不是直接对原str的内容进行修改(因为str是immutable的)，要想让原identifier变量名指向新str，则应重新赋值：txt=txt.replace()，但此时txt指向的地址就变了)**
>基础用法：
>将str中的 substring old 替换为 substring new
>进阶用法：
>若加上count，则只将前 count 个 substring old 替换为 substring new
>>eg. `txt="orange apple apple"`
>>`txt=txt.replace("orange","apple")
>>`#txt现在为"apple apple apple"`

##### str.split(sep=None, maxsplit=-1)
>**返回一个list, 里面的element为许多substring**
>基础用法：
>将 sep 作为delimiter string 分割原字符串
>
>进阶用法：
>1. 若传入maxsplit，则取前 maxsplit 个delimiter进行分割，最终list中会有 maxsplit+1 个elements
>2. 若maxsplit 没有传入或等于-1，则在所有delimiter处进行分割
>> eg.`txt="1,2,3"
>> `txt.split(',', maxsplit=1)
>> `#返回['1','2,3']`
>
>特殊情况：
>1.若有两个consecutive的delimiter，则并不会把这两个delimiter当作一个delimiter，而是会把这两个delimiter视为分隔了一个空白字符串
>>eg.`txt="1,2,,3"`
>>`list1=txt.split(',')`
>>`#则此时list1为['1','2','','3']`
> 2.若sep在开头或末尾heading or trailing，则会在开头或结尾分割出一个空白字符串
>> eg.`txt=",1,2,3,"
>> `txt.split(',')
>> `#则此时返回['','1','2','3','']`
> 3.若sep传入None或sep什么也不传入，则此时程序会把任意个连续whitespace当作一个sep进行分割，且若开头或结尾heading or  trailing出现whitespace，程序会直接忽略它们，而不是分割出一个空白字符串(对比2)
>>eg. `txt="  1 2  3"
>>`txt.split()`
>>`#则此时返回['1','2','3'],而不是['','','1','2','','3']`
>但如果我们将' '作为delimiter(sep)显示传入，则此时依旧按照特殊规则进行分割
>>eg. `txt="  1 2 3"
>>`txt.split(' ')`
>>`#则此时返回['','','1','2','3'](之所以前面分割出了两个空白字符串，是因为原txt前面有两个consecutive whitespace(见特殊情况1))`
> 4.若空白字符串或由whitespace组成的字符串在没有传参或传入 sep=None 的情况下被delimit，则返回的列表为空；若空白字符串被指定非空白字符串delimit，则返回的列表里有一个空白字符串
>> eg. `txt1=''
>> `txt2='  '
>> `txt1.split()  #返回[]
>> `txt2.split()  #返回[]
> 原因：由于没有传参时，默认将连续的whitespace作为delimiter，且忽略heading and trailing whitespace，则此时被分割的空白字符串或whitespace 字符串整体被忽略无效，则返回空列表
>> eg. `txt=''
>> `txt.split(',')   #返回['']
> 原因：传参时，若在被分割字符串中没有找到delimiter，则相当于没被分割，则返回列表中有一个空字符串


##### dict.get(key, default=None, /)
>**返回key值对应的value；若找不到key值，则返回default值**
>注意：最后的'/'表明前面两个参数都为限定位置参数，则传入的实参必须为位置参数
>
>作用:
>1. 给定key，找到dictionary中key对应的value
>2. 若找不到key，则会返回None或传入的default值(比如0)，这样就不会throw an keyError exception了
>> eg. `a1={'good':3, 'well':5}`
>> `a1.get('good',0)  #返回3`
>> `a1.get('bad',0)  #返回0`
>>但`a1['bad'] #这会throw 一个 keyError exception`







### Grammar
##### Python中str外面什么时候用''(单引号)，什么时候用""(双引号)，什么时候用''' '''(三引号)
>**理论上，这三者没有区别，可以随意使用**
>但一般来说
>1. 短字符串用 单 或 双
>2. 若短字符串本身中出现 单(双)引号，则外面最好使用 双(单) 引号，不然就要用转义字符避免歧义了
>eg.`txt="I'm happy." #正确，使用双引号避免与str里的'm引起歧义`
>`txt='I'm happy.' #错误，中间的'应该使用转义字符`
>3. 长字符串、跨行字符串用三引号(只有三引号能引跨行字符串)
>eg. `txt='''People use digital tools every day. Digital tools help people share information.With technology, people can access information quickly. However, too much use of digitaltechnology can lead to problems. People need to use technology wisely and think criticallyabout the information they receive.'''`
>4. 文档字符串docstring一般用三引号

##### KeyError Exception
>**当传入的key在key set中没有找到时，就会抛出一个KeyError Exception**

