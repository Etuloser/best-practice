# List

> Python 的一种内置数据类型，是一种有序的集合，可以随时增加和删除其中的元素

例如：

```py
>>> classmates = ['test1','test2','test3']
>>> classmates
['test1','test2','test3']
```

#### len\(\) 函数

> 获取 list 元素的个数

```py
>>> len(classmate)
3
```

#### 索引访问

> 1. 访问语法：列表名\[索引\]
> 2. 索引从 0 开始
> 3. -1 索引表示最后一个元素

```py
>>> classmates[0]
'test1'
>>> classmates[1]
'test2'
>>> classmates[-1]
'test3'
```

#### list 操作

##### append\(\) 方法

> list 是一个可变的有序表，可以追加元素到末尾

```py
>>> classmates.append('test4')
>>> classmetes
['test1','test2','test3','test4']
```

##### insert\(\) 方法

> 往指定的索引插入元素

```py
>>> classmates.insert(4,'test5')
>>> classmates
['test1','test2','test3','test4','test5']
```

##### pop\(\) 方法

> 删除 list 末尾的元素
>
> 也可删除指定索引位置的元素

```py
>>> classmates.pop(4)
'test5'
>>> classmates
['test1','test2','test3','test4']
```

##### 其他

1. 要把某个位置的元素替换成别的元素，可以直接对指定位置索引赋值
2. list 中的元素也可以是 list 类型

---

# tuple

> 另一种有序列表叫元祖：tuple
>
> tuple 和 list 非常类似，区别在于 tuple 一旦初始化后就不能修改

##### tuple 的陷阱

如果要定义一个空的 tuple，可以写成 ：

```py
>>> t = ()
>>> t
()
```

但是，要定义一个只有 1 的元素的 tuple，必须加一个都好来消除歧义

```py
>>> t = (1,)
>>> t
(1,)
```



