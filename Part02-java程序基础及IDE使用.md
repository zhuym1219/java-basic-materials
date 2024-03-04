# 第二部分 java程序基础及IDE使用

## 一、理论梳理

### 1. 什么是IDE：

集成开发环境，一般指程序开发时将编辑器、编译器、调试器及运行等工具以图形界面的形式集合成一款软件共开发者使用。Java语言常用IDE包含：Intellij IDEA, Eclipse, Vscode 等。

### 2. 基本数据类型

| 归类   | 类型    | 字节 | 占位 | 解释                                |
| ------ | ------- | ---- | ---- | ----------------------------------- |
| 整型   | byte    | 1    | 8    | -128  ~  +127                       |
|        | short   | 2    | 16   | -32768  ~  +32767                   |
|        | int     | 4    | 32   | $-2^{15}-1$ ~ $+2^{15}$             |
|        | long    | 8    | 64   | $-2^{31}-1$ ~ $+2^{31}$             |
| 浮点型 | float   | 4    | 32   | $-3.4* 10^{38}$ ~ $+3.4* 10^{38}$   |
|        | double  | 8    | 64   | $-1.7* 10^{308}$ ~ $+1.7* 10^{308}$ |
| 字符型 | char    | 2    | 16   | 对应ASCII编码                       |
| 布尔型 | boolean | 1    | 8    | 仅有true与false两种取值             |

### 3. 数据转换

数据类型的级别由低至高的顺序：

```
byte -> short -> int -> long -> float -> double
```

自动转换：低级别向高级别赋值，可以自动转换。

强制转换：高级别向低级别赋值，需要在低级别数据前加括号里面标识高级别数据类型。

自动转换举例：

```java
int number1 = 30;
double number2 = number1; 
```

强制转换举例：

```java
double number1 = 25.5;
int number2 = (int)number1;
```

强制转换后，可能会导致部分数据丢失。

### **4. **输出语句： **print, println, printf**

**print** **与println**的区别为：**print**输出引号里的内容不换行，而**println**是输出引号里的内容再换行。

```java
System.out.print(“hello world!”);
System.out.println(“hello world!”);
System.out.println(“hello world!”);
```

以上语句的输出结果为：

```
hello world!hello world!
Hello world!

```

print 与println的括号中，可以添加字符串拼接：

```java
int num1 = 5;
int num2 = 3;
System.out.println(“5+3=”+(num1+num2));
```

输出结果为：

```
5+3=8

```

**printf** **是按照指定格式输出**。

一般printf后面的括号包含两部分，每个部分用逗号间隔：

第一部分：通常为双引号区域，里面表示要输出的内容，部分内容会用占位符表示。

第二部分：参数，表示部分占位符指代的具体参数，每个参数用逗号间隔。

例如：

```java
int num1 = 5;
int num2 = 3;
System.out.printf(“%d+%d=%d\n”,num1,num2,num1+num2);
```

输出结果为：

```
5+3=8

```

| 占位符 | 表示内容                                       |
| ------ | ---------------------------------------------- |
| %s     | 通常表示字符串                                 |
| %d     | 只能标准整型数据，包含：byte, short, int, long |
| %f     | 只能表示浮点型数据,包含：float, double         |
| %c     | 表示字符型，即 char类型                        |
| \n     | 表示换行                                       |
| \t     | 表示表格跳格，通常java中4个占位符为一个表格    |

