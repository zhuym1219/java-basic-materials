# 第六部分 多维数组

## 一、理论梳理

### 1. 多维数组的声明

我们要形成一个思想，即二维数组本质上是比一维数组多一个维度，也就是说，二维数组中每一个元素，是一维数组的引用。

**(1)** **声明时确定行与列的个数**

```int[][] array1 = new int[3][4];```

这种声明方式，是声明了一个3行4列的int类型的二维数组，这种声明方式常常用于矩阵的计算。结构如下图所示：

<img src="./pictures/part06-1.png" alt="avater" style="zoom:50%;" />

**(2)** **声明时确定行与列以及所有元素**

```int[][] array2 = {{1,2},{3,4},{5,6,7}};```

这种声明方式，是声明好了有3行，以及每一行的长度与具体元素的值。通过这个例子我们可以发现，在java中的二维数组每一行里的元素个数是可以不同的。结构如下图所示：

<img src="./pictures/part06-2.png" alt="avater" style="zoom:70%;" />

**(3)** **声明时只确定行数**

```int[][] array3 = new int[2][];```

这种声明方式，是指声明了二维数组有2行。此时，二维数组中的元素是一维数组的引用，此时都为null。如下图所示：

<img src="./pictures/part06-3.png" alt="avater" style="zoom:50%;" />

当我们再执行下面两条语句后，便可以给二维数组中每一个元素，即一维数组的引用指向一个具体的空间。

```java
array3[0] = new int[2];
array3[1] = new int[]{1,2,3};
```

如下图所示：

<img src="./pictures/part06-4.png" alt="avater" style="zoom:50%;" />

### 2. 二维数组的遍历

遍历二维数组，可以使用for循环，也可以使用foreach循环。例如，对于下面的二维数组：

```int[][] array2 = {{1,2},{3,4},{5,6,7}};```

我们用for循环遍历每一个元素：

```java
for (int i = 0; i < array2.length; i++) {
   for (int j = 0; j < array2[i].length; j++) {
     System.out.print(array2[i][j]+" ");
   }
   System.out.println();
 }
```

**要点1:** ```array2.length``` 代表的是二维数组的行数，或者说是二维数组元素的个数，即一维数组的引用。

**要点2:** ```array2[i].length``` 代表的是每一行的一维数组的长度。这里必须用```array2[i].length ```而不能使用```array2[0].length```，因为每一行一维数组的长度是不同的。

**要点3:** ```array2[i][j] ```代表二维数组中，具体的元素值。

 

我们也可以用foreach来遍历二维数组中每一个元素：

```java
for (int[] row : array2) {
   for (int e : row) {
     System.out.print(e + " ");
   }
   System.out.println();
 }
```

这段代码的输出结果与前面用for循环遍历的结果一致。

**要点1:** ```for(int[] row : array2)```: 代表每一轮循环将array2中的每一个元素的地址赋值给row，我们知道二维数组中每一个元素是一维数组的地址，因此row的数据类型也是int[]类型。

**要点2:** ```for(int e : row)```： 代表每一轮循环将一维数组row中的每一个元素的值赋值给e，因此e便是二维数组中具体的元素。

从中我们可以验证，二维数组其实只比一维数组高一个纬度。 可以推演出：n维数组中的每一个元素都是n-1维数组的引用。