# 多维数组\(ndarray\)

ndarray\(通常大小固定\) 是一个多维容器,包含相同类型和大小的成员。数组中维度和成员的数量是由其形状定义的，它是用于指定每个维度的大小的n个正整数元组。数组中的成员类型由单独的数据类型对象\(ntype\)指定，其中一个与每个ndarray相关联。

与python中的其他容器对象一样，可以通过索引和切片数组\(例如,使用n个整数\)以及通过ndarray的方法和属性来访问和修改ndarray的内容。

不同的ndarray可以共享相同的数据，因此在其中一个ndarray中所做的更改可在另一个ndarray可见。也就是说，一个ndarray可以是看另一个ndarray的视图，重新生成的数据由基础ndarray处理，也可以是python字符串所拥有的内存或实现缓冲区或数组接口的对象的视图。

### 例如：

一个2\*3的二维数组，由4字节的整数元素组成：

```text
>>> x = np.array([[1, 2, 3], [4, 5, 6]], np.int32)
>>> type(x)
<type 'numpy.ndarray'>
>>> x.shape
(2, 3)
>>> x.dtype
dtype('int32')
```

可以使用类似python容器语法索引数组：

```text
>>> # The element of x in the *second* row, *third* column, namely, 6.
>>> x[1, 2]
```

例如，切片可以生成数组的视图

```text
>>> y = x[:,1]
>>> y
array([2, 5])
>>> y[0] = 9 # this also changes the corresponding element in x
>>> y
array([9, 5])
>>> x
array([[1, 9, 3],
       [4, 5, 6]])
```

### 构建数组

可以使用数组创建例程中详述的例程以及使用低级ndarray数组构造函数来构建新数组：

     ndarray\(shape\[, dtype, buffer, offset, …\]\)数组对象表示固定大小的成员的多维同构数组。

### 索引数组

可以使用拓展的python切片语法进行数组索引，array\[selection\],类似的语法也用于访问结构化数据类型中的字段

也可以看看:[数组索引](https://numpy.org/devdocs/reference/arrays.indexing.html#arrays-indexing)

### ndarray 内部储存器布局



