---
title: Python3 之类型注解
top: true
cover: true
toc: true
comments: true
lang: zh-CN
summary: 本文主要介绍如何注解 Python，方便代码的审查。
tags: [typing, dataclass]
categories: Python
abbrlink: 55e01cf0
date: 2019-10-18 22:11:21
updated:
password:
---

参考资料：[typing --- 类型标注支持](https://docs.python.org/zh-cn/3.7/library/typing.html) 与 [dataclasses --- 数据类](https://docs.python.org/zh-cn/3.7/library/dataclasses.html)。

## 0 引言：定义一个线段

假设我们使用 Python 实现数学中的整点线段的概念，即 $L = [a,b]$, 且 $a,b \in Z$。使用 Python 可以这样写：

```python
class LineSegment:
    def __init__(self, start, end):
        '''
        整点线段
        =======
        start 和 end 均是整数
        '''
        assert start <= end, "线段的方向错误"
        self.start = start  # 线段的起点
        self.end = end  # 线段的终点

    def __len__(self):
        '''
        获取线段的长度
        '''
        return self.end - self.start + 1
```

类 `LineSegment` 模拟了线段的形态与长度。但是，这样的写法是不是有点繁琐？为了更加人性化，Python 提供了 `typing` 模块，让我们可以对代码进行注解。

## 1 typing 注解 Python

如果想要声明函数参数和返回值的类型，您可以这样做：

```python
def add(x:int, y:int=2) -> int:
    return x + y
```

这就是被称为 `function annotation` 的写法。使用冒号 `:` 加类型名来代表参数的类型，使用箭头 `->` 加类型表示返回值的类型。注解部分不会被 Python 解析器所解析。只是一种注解的方式，类似于：

```python {cmd=true id="izdlk700"}
def add(x, y):
    '''
    x: int
    y: int
    return int
    '''
    return x + y
```

注意：**由于 Python 是动态语言，所以注解是对函数参数和返回值的“注释”，没有强制定义的作用。**

比如，您像这样 `add(1.2, 3.0)` 传入参数，Python 解释器并不会报错。

```python {cmd=true continue="izdlk700" id="izdlkhso"}
print("print 'add(1.2, 3.0)', result is", add(1.2, 3.0))
```

输出结果并没有报错：

```js
print 'add(1.2, 3.0)', result is 4.2
```

### 1.1 使用 `inspect` 检查 python 对象的类型

如果您想要让 Python 对类型进行检查，可以借助模块 `inspect`。比如：

```python
# 1、类型检查
import inspect
inspect.isfunction(add)  # 判断add是否是函数
inspect.ismethod(add)  # 判断add是否是类的方法
inspect.isgenerator(add)  # 判断add是否是生成器对象
inspect.isclass(add)  # 判断add是否是类
```

如果对函数的参数进行检查呢？这个需要借助 `sig=inspect.signature`：

```python {cmd=true continue="izdlk700" id="izdlksso"}
from inspect import signature
# 获得函数的签名
sig = signature(add)
sig
```

输出结果：

```js
<Signature (x: int, y: int = 2) -> int>
```

接着，可以直接获取函数的信息：

```python
params = sig.parameters  # 获取函数的参数信息
params
```

输出结果：

```js
mappingproxy({'x': <Parameter "x: int">, 'y': <Parameter "y: int = 2">})
```

`Parameter` 是 `inspect` 下的一个类，可以把它看做是一个有序字典，里面存放了函数的参数和参数类型，遍历 `params.values()` 的 annotation 属性会得到参数的注解类型：

```python
for v in params.values():
    print(v, 'annotation is', v.annotation)
```

输出结果是：

```python
x: int annotation is <class 'int'>
y: int = 2 annotation is <class 'int'>
```

您可以这样定义类型检查函数：

```python
from inspect import signature


def checkParameterType(fn):
    def wrapper(*args, **kwargs):
        sig = signature(fn)
        # 获取函数的参数信息
        params = sig.parameters
        values = params.values()
        for p, v in zip(args, values):
            print(p, v)
            # 判断传入参数的类型和参数注解类型是否相符
            if not isinstance(p, v.annotation):
                print('TypeWrong')
        for k, v in kwargs.items():
            if not isinstance(v, params[k].annotation):
                print('TypeWrong')
        return fn(*args, **kwargs)
    return wrapper


@checkParameterType
def add(x: int, y: int = 2) -> int:
    return x + y
```

### 1.2 利用 python 对象的 `__annotations__` 属性检查类型

下面以定义一个商品对象：

```python
from typing import Any


def goods(name: str, price: float) -> Any:
    return goods


fish = goods('fish', 10.0)
fish.__annotations__
```

输出结果是（`Any` 代表 Python 很难表达的形式或者类型）：

```js
{'name': str, 'price': float, 'return': typing.Any}
```

可以看出，`__annotations__` 属性与 1.1 中的 `params.values()[k].annotations` 很相似。

这样，可以改写其类型检查函数为：

```python
def checkParameterType(fn):
    def wrapper(*args, **kwargs):
        annotations = fn.__annotations__
        for k, v in zip(annotations.keys(), args):
            if not isinstance(v, annotations[k]):
                 print('TypeWrong')
        for k, v in kwargs.items():
            if not isinstance(v, annotations[k]):
                print('TypeWrong')
        return fn(*args, **kwargs)
    return wrapper
```

## 2 dataclass 提供强大的类型注解机制

`dataclass` 的定义位于 [PEP-557](https://www.python.org/dev/peps/pep-0557/)，一个 dataclass 是指“一个带有默认值的可变的 [namedtuple](https://docs.python.org/3/library/collections.html?highlight=namedtuple#collections.namedtuple
)”，广义的定义就是有一个类，它的属性均可公开访问，可以带有默认值并能被修改，而且类中含有与这些属性相关的类方法，那么这个类就可以称为 `dataclass`，再通俗点讲，`dataclass` 就是一个含有数据及操作数据方法的容器。

我们先看看 `dataclass` 的参数：

key|含义
:-|:-
`init`|指定是否自动生成`__init__`，如果已经有定义同名方法则忽略这个值，也就是指定为`True`也不会自动生成
`repr`|同`init`，指定是否自动生成`__repr__`；自动生成的打印格式为`class_name(arrt1:value1, attr2:value2, ...)`
`eq`|同`init`，指定是否生成`__eq__`；自动生成的方法将按属性在类内定义时的顺序逐个比较，全部的值相同才会返回`True`
`order`|自动生成`__lt__`，`__le__`，`__gt__`，`__ge__`，比较方式与`eq`相同；如果`order`指定为`True`而`eq`指定为`False`，将引发`ValueError`；如果已经定义同名函数，将引发`TypeError`
`frozen`|设为`True`时对`field`赋值将会引发错误，对象将是不可变的，如果已经定义了`__setattr__`和`__delattr__`将会引发`TypeError`

参数 `unsafehash` 的使用比较复杂，当设置为`unsafehash=True`时将会根据类属性自动生成`__hash__`，然而这是不安全的，因为这些属性是默认可变的,这会导致`hash`的不一致，所以除非能保证对象属性不可随意改变，否则应该谨慎地设置该参数为`True`。对于 `unsafehash=False` 的情况将根据`eq`和`frozen`参数来生成`__hash__`，下面单独列出：

参数设置|含义
:-|:-
`eq=True,frozen=True`|`__hash__`将会生成
`eq=True,frozen=False`|`__hash__`将被设为`None`
`eq=False,frozen=True`|`__hash__`将使用超类（`object`）的同名属性（通常就是基于对象`id`的`hash`）

注意：最好去掉了`__init__`方法，以确保 `dataclass` 装饰器可以添加它生成的对应方法。
如果要覆盖 `__init__`，我们将失去 `dataclass` 的优势，因此，如果要处理任何附加功能可以使用新的 dunder 方法：`__post_init__`，让我们看看`__post_init__`方法对于我们的包装类来说是什么样子的。

由于 Python 支持中文作为变量名、类名、函数名等，所以，我可以这样定义一个 Python 类：

```python
from dataclasses import dataclass

@dataclass
class 清单:
    名称: str
    单价: float
    数量: int=0

    def __post_init__(self) -> float:
        self.花费成本 = self.单价 * self.数量

书籍 = 清单('书籍', 10.0, 7)

print(f'{书籍}，花费的成本{书籍.花费成本}元')
```

输出结果：

```js
清单(名称='书籍', 单价=10.0, 数量=7)，花费的成本70.0元
```

上面的代码模拟了出售商品的清单，整个代码看起来都很清爽。
