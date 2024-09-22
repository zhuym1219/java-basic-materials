# 第十五部分 文件读写

## 一、理论梳理

### 1. 字节流与字符流

#### (1) 字节流与字符流

存储在硬盘中的单位是字节，存储在JVM内存中的单位是字符。如果将硬盘中的数据读入到JVM中用java代码去处理，就需要将字节流(也称比特流)转化成字符流。同理，写文件操作是将字符流转化成字节流，并存储在硬盘中的过程。

#### (2) 在文件读写中对应的库方法

**1)**获取文件

```FileInputStream```: 根据硬盘中具体的文件路径，获取该文件中的比特流。

```FileOutputStream```: 根据硬盘中具体的文件路径，用于写文件的输出流。要写入的文件是否需要提前创建好，根据不同系统的要求而定。 

**2)**  字节流与字符流相互转换

```InputStreamReader```: 是一种输入流，字节流向字符流转化的桥梁，可以读入字节流通过指定的字符集将其解码成字符流。

```OutputStreamWriter```: 是一种输出流，字符流向字节流转化的桥梁，可以将字符流编码成字节流。

**3)  **1)与2)的结合体

```FileReader```: 是InputStreamReader的子类，其构造方法中，直接创建了FileInputStream的实例，可以将其当作 FileInputStream与InputStreamReader的结合体。

```FileWriter```: 是OutputStreamWrither的子类，其构造方法中，直接创建了FileOutputStream的实例，可以将其当作FileOutputStream与OutputStreamWriter的结合体。

**4)**  缓冲区加速

```BufferedReader```:可以将访问硬盘获取的比特流转化成的字符流存储在缓冲区中，后续的解析可以从缓冲区中通过```read()```, ```readLine()```等方法读取,而非频繁访问硬盘，已达到加速效果。

```BufferedWriter```: 在写入硬盘前，将字符码存储到缓冲区中，当输出流结束后，一次性写入到硬盘，已到达减少访问硬盘次数提高效率的效果。

### 2. 文件读写样例

#### (1) 读文件

将上述介绍的类连接起来，根据指定的类名，找到获取文件、字节流与字符流转换、缓冲区加速的过程。读文件操作如下：

```java
try {
       FileInputStream fileInputStream = new FileInputStream("file.txt");
       InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream);
       BufferedReader reader = new BufferedReader(inputStreamReader);
       String line;
       while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
} catch (IOException e) {
       throw new RuntimeException(e);
}
```

或

```java
try {
    FileReader fileReader = new FileReader("file.txt");
    BufferedReader reader = new BufferedReader(fileReader);
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

#### (2) 写文件

将上述介绍的类连接起来，根据指定的类名，找到获取文件、字节流与字符流转换、缓冲区加速的过程。写文件操作如下：

```java
try {
    FileOutputStream fileOutputStream = new FileOutputStream("newFile.txt");
    OutputStreamWriter outputStreamWriter = new OutputStreamWriter(fileOutputStream);
    BufferedWriter writer = new BufferedWriter(outputStreamWriter);
    writer.write("hello");
    writer.write(System.lineSeparator());
    writer.write("world");
    writer.close();
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

**要点1:** System.lineSeparator() 代表的是系统换行符

或

```java
try {
    FileWriter fileWriter = new FileWriter("newFile.txt");
    BufferedWriter writer = new BufferedWriter(fileWriter);
    writer.write("hello");
    writer.write(System.lineSeparator());
    writer.write("world");
    writer.close();
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

### 3. Files 库方法

JDK11以上，为了减少文件读写的代码复杂度文件读写操作，引入了Files类。

#### (1) 读文件

上述操作的读文件简化为：

```java
try {
    List<String> lines = Files.readAllLines(Path.of("file.txt"));
    for (String line: lines) {
        System.out.println(line);
    }
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

#### (2) 写文件

上述操作的写文件简化为：

```java
try {
    List<String> lines = new ArrayList<>();
    lines.add("hello");
    lines.add("world");
    Files.write(Path.of("newFile.txt"), lines);
} catch (IOException e) {
    throw new RuntimeException(e);
}
```



