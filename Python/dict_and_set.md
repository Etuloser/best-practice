# Dict

>Python 内置了字典：dict 的支持，全程 dictionary，类似于 Java 中的键值对(key-value)，具有极快的查找速度

```python
>>> dict = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> dict['Michael']
95
```

其原理和查字典一样，当需要搜索一个元素的时候，可以逐一检索，这是在 list 中查找元素的方法，当 list 较大时，查找速度缓慢

而 dict 采用键值对存放在内存中，当需要一个 value 时，只需根据 key 所记录的位置即可得到 value 故速度极快

### 操作方式

1. 除了初始化，也可以直接通过 key 放入 value

   ```python
   >>> dict[key] = value
   ```

   需要注意的是，由于一个 key 对应一个值，所以多次对同一个 key 放入值会覆盖之前的 value

2.  可以使用 in 判断 key 是否存在

   ```python
   >>> 'Thomas' in dict
   False
   ```

3. 或者使用 get() 方法，如果 key 不存在，返回 none，或者返回自己指定的 value

   ```python
   >>> dict.get('Thomas')
   >>> dict.get('Thomas',-1)
   -1
   ```

4. 要删除一个键值对，可以使用 pop(key) 方法

   ```python
   >>> dict.pop('Bob')
   75
   >>>dict
   {'Michael':95,'Tracy':85}
   ```

5. dict 的特点

   * 查找和插入速度快，不会随着 key 的增加而变慢
   * 需要占用大量内存，内存浪费多，是用控件来换取时间的一种方法
   * dict 的 key 必须是不可变对象，key 采用哈希算法计算位置

---

# Set

> set 和 dict 类似，但不存储 value，由于 key 不能重复，所以在 set 中，没有重复的 key

```python
>>> set = set([1,2,3])
>>> set
{1,2,3}
```

### 操作方法

1. 可以通过 add(key) 方法添加元素到 set 中，可以重复添加，但不会有效果

2. 可以通过 remove(key) 方法可以删除元素

3. set 可以做数学意义上的交集、并集等操作

   ```python
   >>> set1 = set([1, 2, 3])
   >>> set2 = set([2, 3, 4])
   >>> set1 & set2
   {2, 3}
   >>> set1 | set2
   {1, 2, 3, 4}
   ```

   ​

