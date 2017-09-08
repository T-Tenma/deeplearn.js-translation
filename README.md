# 非机器学习专家指南 Guide for non-ML experts


## NDArrays, Tensors, and numbers

### 数学张量 Mathematical tensors

Mathematically, a “tensor” is the most basic object of linear algebra, a generalization of numbers, vectors, and matrices. A vector can be thought of as a 1-dimensional list of numbers; a matrix as a 2-dimensional list of numbers. A tensor simply generalizes that concept to n-dimensional lists of numbers. It is any arrangement of component numbers (or even strings or other data types) arranged in any multi-dimensional rectangular array.

从数学角度来说，“张量”就是线性代数最基础的对象， 对于数字，向量，和矩阵的概括。向量可以被认为是一维的数字列表；矩阵可以认为是一个二维的数字列表。简单的概括张量的概念为n维的数字列表。他是由组件数字（或者甚至字符串或者其他数据类型）任意排列成任意多维矩形阵列？

A tensor has several properties:

- It has a **type**, which describes the types of each of its components, for instance `integer`, `float`, etc. **deeplearn.js** only supports float32 for now.
- It has a **shape**, a list of integers which describes the shape of the rectangular array of components. When you say a matrix is “4 by 4”, you are describing the shape of the matrix.
- It has a **rank**, which is the length of its shape; the dimension of the array of components. A vector has rank 1; a matrix has rank 2.

行量拥有几个属性:

- **类型**，它描述每个组件的类型，例如`integer`，`float`等等。 **deeplearn.js** 目前只支持float32。
- **形状**，一个整型列，它描述了组件矩形阵列的形状。当你说一个矩阵是 4x4 时，你就在描述这个矩阵的形状。
- **阶**，代表了形状的长度；组件阵列的维度。 向量的阶是1；矩阵的阶是2。


| Example tensor | Type | Shape| Rank|
|--------|--------|--------|--------|--------|
| Scalar: 3.0 | float | [] | 0 |
| Vector: (1, 5, -2)| int | [3] | 1 |
| 2x2 Matrix | int | [2, 2] | 2|

| 张量示例 | 类型 | 形状 | 阶|
|--------|--------|--------|--------|--------|
| 标量 3.0 | floagt | [] | 0 |
| 向量：(1, 5, -2) | int | [3] | 1 |
| 2x2 矩阵 | int | [2,2] | 2 |

### number[], NDArray, Tensor: Three data types for mathematical tensors

### numer[], NDArray, Tensor: 数学张量的三种数据类型

This same object a mathematician would call a “tensor” is represented in three different ways in **deeplearn.js**. The above discussion (ranks, shapes, and types), applies to all of them, but they are different and it is important to keep them straight:

- **`number[]`** is the underlying javascript type corresponding to an array of `numbers`. Really it is number for a 0-rank tensor, `number[] `for a 1-rank tensor, `number[][]` for 2-rank, etc. You won’t use it much within **deeplearn.js**, but it is the way you will get things in and out of **deeplearn.js**.
- **`NDArray`** is **deeplearn.js**’s more powerful implementation. Calculations involving NDArrays can be performed on the client’s GPU, which is the fundamental advantage of **deeplearn.js**. This is the format most actual tensor data will be in when the calculations ultimately happen. When you call `Session.eval`, for instance, this is what you get back (and what the `FeedEntry` inputs should be). You can convert between `NDArray` and `number[]` using `NDArray.new(number[])` and `NDArray.get([indices])`
- **`Tensor`** is an empty bag; it has no actual data inside. It is a placeholder used when a Graph is constructed, which records the shape and type of the data that will ultimately fit inside it. It contains no actual values in its components. Just by knowing the shape and type, however, it can do important error-catching at Graph-construction time; if you want to multiply a 2x3 matrix by a 10x10 matrix, the graph can yell at you when you create the node, before you ever give it input data. It does not make sense to convert directly between a `Tensor` and an `NDArray` or `number[]`; if you find you are trying to do that, one of the following is probably true:
 - You have a static `NDArray` that you want to use in a graph; use graph.constant() to create a constant `Tensor` node.
 - You have an `NDArray` that you want to feed in as an input to the Graph. Create a Placeholder with `graph.placeholder` in the graph, and then send your input to the graph in the `FeedEntry`.
 - You have an output tensor and you want the session to evaluate and return its value. Call `Session.eval(tensor)`.

数学家称之为“张量”的相同对象在 **deeplearn.js** 中以三种不同的方式表示。上述讨论（阶，形状和类型）适用于它们全部，但它们是有区别的，另外保持它们的straight？是非常重要的：

-  **`number[]`** 是 javascript 对应一组`数字`的底层类型。一个数字为0阶张量，`number[]`为1阶张量，`number[][]`为2阶，等等。在使用 **deeplearn.js** 时不会太多的使用到`number[]`，但是这是一种在 **deeplearn.js** 中获取things输入和输出的方式。
- **`NDArray`** 是 **deeplearn.js** 更强大的实现。涉及到 NDArrays 的计算可以在客服端的 GPU  上执行，这是 **deeplearn.js** 的根本优势。NDArray 是大多数真实张量在最终计算发生时的格式。当你调用`Session.eval`时，NDArray就是你得到的返回值(输入应该是`FeedEntry`)。你可以使用`NDArray.new(number[])`和`NDArray.get([indices])`在`NDArray`和`number[]`之间做转换。
- **`Tensor`** 是一个空容器；它里面没有真实的数据。

