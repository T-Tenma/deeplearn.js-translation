# 非机器学习专家指南 Guide for non-ML experts


## NDArrays, Tensors, and numbers

### 数学张量 Mathematical tensors

Mathematically, a “tensor” is the most basic object of linear algebra, a generalization of numbers, vectors, and matrices. A vector can be thought of as a 1-dimensional list of numbers; a matrix as a 2-dimensional list of numbers. A tensor simply generalizes that concept to n-dimensional lists of numbers. It is any arrangement of component numbers (or even strings or other data types) arranged in any multi-dimensional rectangular array.

从数学角度来说，“张量”就是线性代数最基础的对象， 对于数字，向量，和矩阵的概括。向量可以被认为是一维的数字列表；矩阵可以认为是一个二维的数字列表。简单的概括张量的概念为n维的数字列表。他是由组件数字（或者甚至字符串或者其他数据类型）任意排列成任意多维矩形阵列？

A tensor has several properties:

- It has a type, which describes the types of each of its components, for instance integer, float, etc. deeplearn.js only supports float32 for now.
- It has a shape, a list of integers which describes the shape of the rectangular array of components. When you say a matrix is “4 by 4”, you are describing the shape of the matrix.
- It has a rank, which is the length of its shape; the dimension of the array of components. A vector has rank 1; a matrix has rank 2.

行量拥有几个属性:

- **类型**，它描述每个组件的类型，例如`integer`，`float`等等。**deeplearn.js**目前只支持float32。
- **形状**，一个整型列，它描述了组件矩形阵列的形状。当你说一个矩阵是4x4时，你就在描述这个矩阵的形状。
- **排名**



