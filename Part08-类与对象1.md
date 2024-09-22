# 第八部分 类与对象1

## 一、理论梳理

### 1. 什么是类与对象

**(1) 为何要引入面向对象的概念？**

我们思考一个简单的问题，如果传递一组数据该怎么办？

我们学过了数组，可以使用数组传递一组数据。然而，数组有一定的局限性，因为数组里要求每一个元素的数据类型相同。

假如我们的需求是，传递学生信息：包含学号、姓名、年龄、身份证号、性别、籍贯、专业等信息。

首先：通过传递数组的引用解决不了问题，因为这些信息的数据类型不同。 

其次：如果将这些信息分开传递，比如一个方法里的参数包含全部信息（学号、姓名、年龄、身份证号、性别、籍贯、专业），那么这个方法显然会十分复杂，同时，方法的返回值也不允许返回多条数据。

综上，我们引入了面向对象编程，即将多条信息封装成一个对象，通过传递对象的引用来管理我们的程序。也就是说，在处理系统工程问题时，面向过程编程常常无法满足我们的需求，需要面向对象编程增强代码的功能性。

**(2) 类与对象**

我们就拿学生为例，比如一个学生具有学号、姓名、年龄、性别这几个特征：

**类：**可以称之为一个模版，在模版中定义好这个类型需要有哪些特征，有哪些方法。例如学生可以称之为一个类，学生类中包含学号、姓名、年龄、性别等特征。UML图示：

<img src="./pictures/part08-class-object1.png" alt="avater" style="zoom:40%;" />

### 2. 属性

属性便是一个类中所具备的特征，常常也叫做成员变量。例如上述学生类中的姓名、学号、性别、年龄。**在代码中创建一个类并声明属性如下**：

 ```java
public class Student {
   private String name;
   private String studentNumber;
   private char gender;
   private int age;
 }
 ```

属性的作用域是当前整个类中，对于当前类，属性也可以称为全局变量。在当前类中的任意一个方法，都可以直接访问属性。

**创建对象代码：**

```java
Student student1 = new Student();
Student student2 = new Student();
```

很显然，这段代码是创建了两个Student的对象，其引用名称分别为student1， student2.这里在内存堆与栈空间分配如下：

<img src="./pictures/part08-class-object2.png" alt="avater" style="zoom:60%;" />

通过这个图，我们可以看到：

**要点1:** 创建对象后，会分别给对象的每一个属性分配一个存储空间。同时，其引用会指向这个空间。

**要点2:** 在内存堆创建的空间，都会赋予一个初始值。比如表示数字的就是0.

### 3. 访问权限

我们在这里介绍的访问权限，主要以private， public两种为主。

**private权限：**私有访问权限，仅在当前类中可以访问。优势在于利于封装，不会将数据暴露在外层类中。例如，密码如果为public，那么在外层调用中，不限权限不限情景，都可以直接访问当密码这个属性，这样的设计就会有一定的安全隐患。

**public权限:** 公有访问权限，在用一个工程项目里，任何一个类，任何地方，都可以访问带有public标识的属性与方法。

一般在设计上，public常常会标识方法，private常常标识类的属性。

### 4. 成员方法

**(1) 成员方法的基本概念**

成员方法，即由对象可以去调用的方法。一般来说，一个类里属性代表的是特征，那么方法代表的就是功能。一般成员方法写在类的大括号内部，其的格式与静态的区别就在于缺少static，格式为：

```
public 方法返回值 方法名称(参数类型1 参数名1， 参数类型2，参数名2, …){
			方法体；
			return ；
}
```

比如对于Student这个类，我们可以**定义这样两个方法**：（1）自我介绍。 （2）年龄自增。 

```java
public class Student {
    private String name;
    private String studentNumber;
    private char gender;
    private int age;

    public void introduce() {
        System.out.printf("%s Name:%s %c, %d years old", studentNumber, name, gender, age);
    }

    public int increaseAge() {
        return ++age;
    }
}
```

**要点1：**在成员方法中，可以直接使用属性。属性在当前类中是全局变量。

**要点2:** 成员方法是写在类中，没有static关键字。

如何调用成员方法：

public static void main(String[] args) {
   Student stu1 = new Student();
   stu1.increaseAge();
   stu1.introduce();
 }

**要点1:** 成员方法一定要通过对象去调用，不能通过类名.方法名去调用。

**(2)  getter 与 setter**方法

我们使用getter与setter方法，主要是为了提供一种由其他类去访问私有属性的途径。

**Getter:** 获取私有属性。

因此，该方法需要有一个返回值，返回私有属性的值已达到获取的目的。

```java
public String getName() {
   return name;
 }
```

**Setter:** 重置私有属性。

因此该方法需要传递一个参数，用来重新设置私有属性的值。

```java
public void setName(String name) {
   this.name = name;
 } 
```

**要点1:** 如果属性的访问权限都是public，是不是不需getter 与 setter方法了？

显然不可以。因为为了确保类的封装性，部分敏感数据不适合对外暴露，比如密码、银行存款等，因此getter与setter方法必须存在。我们可以在这些方法中，添加逻辑，来判断是否允许获取或重置某些私有成员变量。

比如重置age，我们知道age不能小于0，因此我没用setter方法可以添加逻辑判断：

```java
public void setAge(int age) {
   if (this.age > 0)
     this.age = age;
 }
```

可能对于其他的私有成员一开始没有这类逻辑判断，但不等于以后没有，因此一般在一开始设计类的时候，会讲getter与setter这个架构添加上。 

