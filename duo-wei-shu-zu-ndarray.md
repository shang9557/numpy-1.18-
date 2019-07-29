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

ndarray 的实例是由计算机的连续一维段\(由数组或其他对象拥有\)组成，并将N个整数映射到块中成员的位置的索引方案相结合。索引的变化是由ndarray的形状指定的，每个成员采用多少个字节以及如何解释字节由与数组相关联的数组类型对象定义。

一段内存的本质是一个一维数组，并且有许多不同的方案用于在一维块中排列n维数组的成员。numpy是灵活的，ndarray对象可以适应任何跨步索引方案。在一个跨步方案中，多维索引\(n0,n1,...\)对应于偏移量\(以字节为单位\):

![](.gitbook/assets/image%20%281%29.png)

从与数组关联的内存块的开头。这儿Sk是指定步长的整数。列主要顺序\(例如:在Fortran语言和matlab中使用\) 和 行主要顺序\(在c中使用\) 方案只是特定种类的跨步方案，并且对应可以通过步长解决的内存:

![](.gitbook/assets/image%20%282%29.png)

其中 ![d\_j](https://numpy.org/devdocs/_images/math/5e6cfb16a1d0565098e1a35072ef6fbfef092db3.svg) _= self.shape\[j\]_.

C和Fortran 顺序都是连续的，即，单端存储器布局，其中存储器块的每个部分都可以通过索引的某种组合来访问。

而具有相应标志集合的c风格和Fortran风格的连续数组可以解决上述问题，实际步幅可能不同。这可能发生在两种情况下：

1. 如果self.shape \[k\] == 1那么对于任何合法索引索引\[k\] == 0.这意味着在偏移量n\_k = 0的公式中，因此s\_k n\_k = 0，s\_k = self.strides的值 \[k\]是任意的。
2. 如果数组没有元素（self.size == 0），则没有合法索引，并且从不使用步幅。 任何没有元素的数组都可以被认为是C风格和Fortran风格的连续数组。

