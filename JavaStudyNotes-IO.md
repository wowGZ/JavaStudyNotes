---
title: JavaStudyNotes-I/O（输入/输出）
---

## 流概述

流是一组有序数列，根据操作的类型，可以分为输入流和输出流两种。I/O(Input/Output，输入/输出)流提供了一条通道程序，可以使用这条通道把源中的字节序列送到目的地。虽然I/O流通常与磁盘文件存取有关，但是程序的源和目的地也可以是键盘、鼠标、内存或显示器窗口等。
Java由数据流处理输入/输出模式，程序从指向源的输入流中读取源中的数据。源可以是文件、网络、压缩包或其他数据源。
输出流的指向是数据要到达的目的地，程序通过输出流中写入数据把信息传递到目的地。输出流的目标可以是文件、网络、压缩包、控制台和其他数据输出目标。

## 输出/输入流

### 输入流

InputStream类是字节输入流的抽象类，是所有字节输入流的父类。InputStream类的具体结构层次如图所示。
![]()
该类中所有方法遇到错误时都会引发IOException异常。下面是对该类中的一些方法的简要说明。

- read()方法：从输入流中读取数据的下一个字节。返回范围为0~255的int字节值。如果因为已经到达流末尾而没有可用的字节，则返回值为-1。
- read(byte[] b)：从输入流中读入一定长度的字节，并以整数形式返回字节数。
- mark(int readlimit)方法：在输入流的当前位置放置一个标记，readlimit参数告知此输入流在标记位置失效前允许读取字节数。
- reset()方法：将输入指针返回到当前所做的标记处。
- skip(long n)方法：跳过输入流上的n个字节并返回实际跳过的字节数。
- markSupported()方法：如果当前流支持mark()/reset()操作就返回true。
- close方法：关闭此输入流并释放与该流关联的所有系统资源。

Java中的字符是Unicode编码，是双字节的。InputStream类是用来处理字节的，并不适合处理字符文本。Java为字符文本的输入专门提供了一套单独的类Reader，但Reader类并不是InputStream类的替换者，只是在处理字符串时简化了编程。Reader类是字符输入流的抽象类，所有字符输入流的实现都是它的子类。

### 输出流

OutputStream类是字节输出流的抽象类，此抽象类是表示输出字节流的所有类的超类。

OutputStream类中的所有方法均返回void，在遇到错误时会发生IOException异常。下面对OutputStream类中的方法作简单的介绍：

- write(int b)方法：将指定字节写入此输出流。
- write(byte[] b)方法：将b个字节从指定的byte数组写入此输出流。
- write(byte[] b, int off, int len)方法：将指定byte数组中从偏移量off开始的len个字节写入此输出流。
- flush()方法：彻底完成输出并清空缓存区。
- close()方法：关闭输出流。

Writer类是字符输出流的抽象类，所有字符输出流类的实现都是它的子类。

## File类

### 文件的创建与删除

可以使用File类创建一个文件对象。通常通过以下三种构造方法来创建文件对象。

1. File(String pathname)
该构造方法通过将给定路径名字符串转换为抽象路径名来创建一个新File实例。
语法如下：
- new File(String pathname)
其中，pathname是指路径名称（包含文件名）。例如：
- File file = new File("D:\\1.txt");

2. File(String parent, String child)
该构造方法根据定义的父路径和子路径字符串（包括文件名）创建一个新File类对象。
语法如下：
- new File(String parent, String child)

3. File(File f, String child)
该构造方法根据parent抽象路径名和child路径名字符串创建一个新File实例。
语法如下：
- new File(File f, String child)


当使用File类创建一个文件对象之后，例如：
- File file = new File("word.txt");
如果当前目录中不存在名称为word的文件，File类对象可以通过createNewFile()方法创建一个吗，名为word.txt的文件；如果存在一个名为word.txt的文件，可以通过文件对象的delete()方法将其删除掉。

eg:在项目中创建类FileTest，在主方法中判断D盘的myword文件夹是否存在word.txt文件，如果该文件存在则将其删除，不存在则创建该文件。

```java
import java.io.File;
import java.io.IOException;

public class practice {
    public static void main(String[] args) {
        File file = new File("D:\\myword\\word.txt");
        if(file.exists()){
            file.delete();
            System.out.println("该文件已经删除。");
        }
        else {
            try {
                file.createNewFile();
                System.out.println("该文件已经创建。");
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### 获取文件信息

File类提供了很多方法用于获取一些文件本身的信息常用的方法如下表所示：

方法                 |返回值              |说明
---------------------|-------------------|---------------------------------
getName()            |String             |获取文件的名称
canRead()            |boolean            |判断文件是否为可读的
canWrite()           |boolean            |判断文件是否可被写入
exists()             |boolean            |判断文件是否存在
length()             |long               |获取文件的长度（以字节为单位）
getAbsolutePath()    |String             |获取文件的绝对路径
getParent()          |String             |获取文件的父路径
isFile()             |boolean            |判断文件是否存在
isDirectory()        |boolean            |判断文件是否为同一个目录
isHidden()           |boolean            |判断文件是否为隐藏文件
lastModified()       |long               |获取文件最后修改时间

eg:获取D盘myword文件夹下word.txt文件的文件名、文件长度 并判断该文件是否为隐藏文件。

```java
import java.io.File;

public class practice {
    public static void main(String[] args) {
        File file = new File("D:\\myword\\word.txt");
        if(file.exists()){
            String name = file.getName();
            long length = file.length();
            boolean hidden = file.isHidden();
            System.out.println("文件名是" + name);
            System.out.println("文件长度为" + length);
            System.out.println("文件是否为隐藏文件：" + hidden);
        }
        else {
            System.out.println("该文件不存在！");
        }
    }
}
```

## 文件输入/输出流

### FileInputStream类和FileOutputStream类

FileInputStream类和FileOutputStream类都用来操作磁盘文件。如果用户的文件读取需求比较简单，则可以使用FileInputStream类，该类继承自InputStream类。FileOutputStream类与FileInputStream类相对应，提供了基本的文件写入能力。FileOutputStream类是OutputStream类的子类。
FileInputStream类的常用构造方法如下：
- FileInputStream(String name)
- FileInputStream(File file)
第一个方法使用给定的文件名name创建一个FileInputStream对象，第二个构造方法使用File对象创建FileInputStream对象。第一个构造方法比较简单，但第二个构造方法允许在把文件连接输入流之前对文件作进一步分析。
FileOutputStream类有与FileInputStream类相同的参数构造方法，创建一个FileOutputStream类对象时，可以指定不存在的文件名，但此文件不能是一个已经被其他程序打开的文件。下面的实例就是使用FileInputStream与FileOutputStream类实现文件的读取与写入功能的。

eg:使用FileOutputStream类向文件word.txt写入信息，然后通过FileInputStream类将文件中的数据读取到控制台上。

```java
import java.io.*;

public class practice {
    public static void main(String[] args) {
        File file = new File("D:\\myword\\word.txt");
        try {
            FileOutputStream fileOutputStream = new FileOutputStream(file);
            byte[] buy = "我有一只小毛驴，我从来也不骑。".getBytes();
            fileOutputStream.write(buy);
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            FileInputStream fileInputStream = new FileInputStream(file);
            byte[] b = new byte[1024];
            int len = fileInputStream.read(b);
            System.out.println("文件中的信息是：" + new String(b, 0, len));
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
