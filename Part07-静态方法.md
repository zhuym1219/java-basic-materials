# 静态方法

## 一、理论梳理

### 1. 方法的用途

使用方法，可以定义表示同一功能且重复代码块，以达到简化代码的效果。

比如我们有个需求，当我们输入1-9的数字时，可以打印乘法表，那么我们可以将打印乘法表这一功能提取出来成为一个方法

### 2. 方法的定义与调用

我们在学习方法的时候，要能清晰的区分两个概念：

**（1）方法的定义** 

方法的定义可看作是一个模版，根据转递指定的参数，而得到相对应的结果。不同方法的定义，与方法的先后顺序无关，而且可以仅设计定义方法的代码，不写调用代码。

示例代码：

```java
public static double avg(int a, int b, int c) {
   return (a + b + c) / 3.0;
 }
```

这个方法名字是avg，目的是求三个数的平均值。

**（2）方法的调用**

方法的调用的前提是方法必须先定义好。定义一次方法，可以多次调用，如果是带参数的方法，那么根据传递的参数不同，方法中会运算出不同的结果。

示例代码：

```
public static void main(String[] args) {
   double avg1 = avg(3,5,7);
   System.out.println(avg(5,2,1));
 }
```

这段代码我们调用了两次avg方法，第一次是将3，5，7的平均值赋值给avg1，第二次调用是直接输出5，2，1的平均值。

### 3. 静态方法的设计规范

在方法的定义是写在类的大括号内不，模型如下：

```
public static 方法返回值 方法名称(参数类型1 参数名1， 参数类型2，参数名2, …){
					方法体；
					return ；
}
```

**要点1:** public关键字是公有访问权限，也就是说用public修饰的方法在当前项目中都可以直接调用。

**要点2:** static关键字是静态类型，目前我们通过main方法调用的方法，都需要添加static关键字。非static方法我们在后续类与对象课程中会介绍。

**要点3:** 方法返回值，可以是基本数据类型、数组或类。表示方法执行后要返回给调用的地方什么数据。如果返回值为空，可以写void，方法体中可以不用写return，否则要写return。

下面我们分三种情况来举例介绍不同类型的方法：

- **无参数无返回值的方法**

  定义一个打印``*``的方法，这里我们可以看到返回值为void：

  ```java
  public static void printPattern(){
     for (int i = 1; i <= 3; i++) {
       for (int j = 0; j < i; j++) {
         System.out.print("*");
       }
       System.out.println();
     }
   }
  ```

  调用printPattern()方法：

  ```java
  public static void main(String[] args) {
     printPattern();
   }
  ```

   

- **有参数无返回值的方法**

  定义一个打印``*``的方法，根据传递的参数line来决定打印``*``的行数：

  ```java
  public static void printPattern(int line){
      for (int i = 0; i <= line; i++) {
          for (int j = 0; j < i; j++) {
              System.out.print("*");
          }
          System.out.println();
      }
  }
  ```

  调用printPattern(int line)方法：

  ```java
  public static void main(String[] args) {
      printPattern(5);
  }
  ```

- **有参数有返回值的方法**

  定义一个根据圆的半径求圆的面积的方法： 参数为double类型的radius，返回值为double类型，那么return 后面的数据类型必须是double

  ```java
  public static double circleArea(double radius) {
      return Math.PI * radius * radius;
  }
  ```

  调用circleArea(double radius): 输出的内容便是circleArea(3)的返回值。如果返回值为void，则不能写在System.out.println()中。

  ```java
  public static void main(String[] args) {
      System.out.println(circleArea(3));
  }
  ```

### 4. 方法的重载 （Overload）

方法的重载发生在：（1）方法名相同 （2）方法参数不同。

**为什么要使用方法重载？** 比如说我们求最大值这个需求，可以计算几个int类型的最大值，也可以计算double类型，同时也可以计算表示其他的数字类型，因此，我们可以用一个方法名max来设计，里面根据我们传递的参数类型不同，返回不同的数据类型。

**方法参数不同体现在：**

- **参数个数不同**

例如：

```java
public class Example {
   public static int findMax(int a, int b) {
     return Math.max(a, b);
   }
   public static int findMax(int a, int b, int c) {
     return Math.max(Math.max(a, b), c);
   }
 }
```

第一个方法有两个参数，第二个方法有三个参数。

- **参数类型不同**

例如：

```java
public class Example {
   public static double findMax(double a, double b, double c) {
     return Math.max(Math.max(a, b), c);
   }
 
   public static int findMax(int a, int b, int c) {
     return Math.max(Math.max(a, b), c);
   }
 }
```

第一个方法中的参数是double类型，第二个方法中的参数是int类型

- **参数顺序不同**

例如：

```java
public static void function(int a, double b){
 }

public static void function(double a, int b){
 }
```

### 5. 方法中传递数组的引用

在方法中也可以传递数组，编写规范：在方法定义中，要写清楚数组类型，在方法调用中，仅使用引用就可以了。

例如下面求矩阵转置的例子：

```java
public static int[][] transMatrix(int[][] a) {
   int[][] trans = new int[a[0].length][a.length];
   for (int i = 0; i < trans.length; i++) {
     for (int j = 0; j < trans[i].length; j++) {
       trans[i][j] = a[j][i];
     }
   }
   return trans;
 }
```

在方法的定义中，需要写清楚传递的参数类型是int[][], 返回值类型是 int[][]。

方法的调用：

```java
public static void main(String[] args) {
   int[][] matrix = {{1,2,3},{4,5,6}};
   int[][] target = transMatrix(matrix);
   for (int[] line: target) {
     System.out.println(Arrays.toString(line));
   }
 }
```

在方法调用时，传递参数仅将引用名称matrix传递进来就好，同时对于返回值，也可以返回给另一个二维数组的引用target。

**要点1 地址传递：**我们在传递引用的过程中，是传递一个地址，即方法体中获得这个地址后，可以根据地址指向的具体元素的值来进行修改。例如：

```java
public static void increaseMatrix(int[][] matrix){
   for (int i = 0; i < matrix.length; i++) {
     for (int j = 0; j < matrix[i].length; j++) {
       matrix[i][j]++;
     }
   }
 }
```

这个方法调用之后，原数组matrix中所有的元素都会自增，也就是说，数组中实际元素的值**是会改变的**。

**要点2 值传递：**相对比而言，如果方法中仅仅传递值，那么在方法体中修改这个值是代表修改了参数，原数据不会发生任何改变。例如：

```java
public static void main(String[] args) {
   int num1 = 2, num2 = 3;
   changeValue(num1, num2);
   System.out.printf("num1=%d, num2=%d", num1, num2);
 }

public static void changeValue(int a, int b) {
   int temp = a;
   a = b;
   b = temp;
 }
```

这段代码的执行结果：

```num1=2, num2=3```

这段代码的执行流程是这样：

1)   调用changeValue(num1,num2)方法，将num1，num2的值分别复制给参数a与b。

2)   交换a与b的值

3)   changeValue方法调用结束后，释放a与b的空间

4)   最后，num1与num2的值不受影响

