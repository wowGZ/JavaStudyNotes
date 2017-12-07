---
title: JavaStudyNotes-Swing程序设计
---
## Swing概述

### Swing特点

原来的AWT组件来自java.awt包，当含有AWT组件的Java应用程序在不同的平台上执行时，每个平台的GUI组件的显示会有所不同，但是在不同平台上运行使用Swing开发的应用程序时，就可以统一GUI组件的显示风格，因为Swing组件允许编程人员在跨平台时指定统一的外观和风格。
Swing组件通常被称为“轻量级组件”，因为它完全由Java语言编写，而Java是不依赖于操作系统的语言，它可以在任何平台上运行；相反名依赖于本地平台的组件成为“重量级组件”，如AWT组件就是依赖本地平台的窗口系统来决定组件的功能、外观和风格、Swing主要有一下特点：
1. 轻量级插件
2. 可插入外观组件

### Swing包

为了有效地使用Swing组件，必须了解Swing包的层次结构和继承关系，其中比较重要的类是Component类、Container类和JComponent 类。
在Swing组件中大多数GUI组件都是Componen类的直接子类或间接子类，JComponent类是Swing组件各种特性的存放位置，这些组件的特性包括设定组件边界、GUI组件自动滚动等。
在Swing组件中最重要的父类是Comtainer类，而Comtainer类有两个最重要的子类，分别为java.awt.Window与java.awt.Frame,除了以往的AWT类组件会继承这两个类之外，现在的Swing组件也扩展了这两个类，Java关于窗口组件的编写，都与组件以及荣放弃的概念相关联。

### 常用Swing组件概述

下面给出基本Swing组件的概述，有关这些组件的内容将在后面详细讲解。下表列举了常用的Swing组件及其含义。

组  件  名  称  |  定    义
---------------|-------------
JButton        |代表SWing按钮，按钮可以带一些图片或文字
JCheckBox      |代表Swing中的复选框组件
JComBox        |代表下拉列表框，可以在下拉显示区域显示多个选项
JFrame         |代表Swing的框架类
JDialog        |代表版本的对话框
JLabel         |代表中的标签组件
JRadioButton   |代表Swing的单选按钮
JList          |代表能够在用户界面中显示一些列条目的组件
JTextField     |代表文本框
JPasswordField |代表密码框
JTextArea      |代表Swing中的文本区域
JOptionPane    |代表Swing中的一些对话框

## 常用窗体

### JFrame窗体

JFrame窗体是一个容器，它是Swing程序中各个组件的载体，可以将JFrame看作是承载这些Swing组件的容器。在开发应用程序时可以通过继承java.swing.JFrame类创建一个窗体，在这个创体中添加组件，同时为组件设置事件。由于该窗体继承了JFrame类，所以它拥有“最大化”“最小化”“关闭”等按钮。
下面将详细的讲解JFrame窗体在Java应用程序中的使用方法。
JFrame在程序中的语法格式如下：
```java
JFrame jf = new JFrame(titlt);
Container container = jf.getContentPane();
```
- jf：JFrame类的对象。
- container：Container类的对象，可以使用JFrame对象调用getContentPane()方法获取。

读者大致应该有这样一个概念，Swing组件的窗体通常与组件和容器相关，所以在JFrame对象创建完成后，需要调用getContentPane()方法将窗体转换为容器，然后在容器中添加组件或设置布局管理器。通常，这个容器用来包含和显示组件。如果需要将组件添加至容器，可以使用来自Container类的add()方法进行设置。例如：

```java
container.add(new JButton("按钮"));
```

在容器中添加组件后，也可以使用Container类的remove()方法将这些组件从容器中删除。例如：

```java
container.remove(new JButton("按钮"));
```

下面的实例中实现了JFrame对象创建一个窗体，并在其中添加一个组件。

在项目中创建Example类，该类继承JFrame类成为窗体类，在该类中创建标签组件，并添加到窗体界面中。

```java
import java.awt.*;
import javax.swing.*;
public class Example1 extends JFrame{
    public void CreatJFrame(String title){
        JFrame jFrame = new JFrame(title);
        Container container = jFrame.getContentPane();
        JLabel jLabel = new JLabel("这是一个JFrame窗体");
        //使标签文字居中上
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        container.add(jLabel);
        container.setBackground(Color.white);
        jFrame.setVisible(true);
        jFrame.setSize(200, 150);
        //设置窗体关闭方式
        jFrame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Example1().CreatJFrame("创建一个JFrame窗体");
    }
}
```

在该例中Example1类继承了JFrame类，在CreatJFrame()方法中实例化JFrame对象。JFrame类的吃那个用构造方法包括以下两种形式：

- public JFrame()
- public JFrame(String title)

JFrame类中的两种构造方法分别为无参的构造方法与有参的构造方法，第一种形式的构造方法可以创建一个初始不可见、没有标题的新窗体；第二种形式的构造方法在实例化该JFrame对象时可以创建一个不可见但具有标题的窗体。可以使用JFrame对象调用show()方法使窗体可见，但是该方法早已被新版JDK所弃用，通常使用setVisible(true)方法使窗体可见。

同时可以使用setSize(int x, int y)方法设置窗体大小，其中x与y分别代表窗体的宽和高。

创建窗体之后，需要给予窗体一个关闭方式，可以调用setDefaultCloseOperation()方法关闭窗体。Java为窗体的关闭提供了多种方式，常用的有以下四种：

1. DO_NOTHING_ON_CLOSE
2. DISPOSE_ON_CLOSE
3. HIDE_ON_CLOSE
4. EXIT_ON_CLOSE
这几种操作实质上是将一个int类型的常量封装在java.swing.WindowConstants接口中。

- 第一种窗体的退出方式代表什么都不做就将窗体关闭；
- 第二种退出方式则代表任何注册监听程序对象后会自动隐藏并释放窗体；
- 第三种方式表示隐藏窗口的默认窗口关闭；
- 第四种退出方式表示退出应用程序默认窗口关闭。

### JDialog窗体

JDialog窗体是Swing组件中的对话框，它继承了AWT组件中的java.awt.Dialog类。
JDialog窗体的功能是从一个创体中弹出另一个窗体，就想是在使用IE浏览器时弹出的确定对话框一样。JDialog窗体实际上就是另一类的窗体，它与JFrame窗体类似，在使用时也需要调用getContentPane()方法将窗体转换为容器，然后在容器中设置窗体的特性。
在应用程序中创建JDialog窗体需要实例化JDialog类，通常使用以下几个JDialog类的构造方法。

- public JDialog()：创建一个没有标题和父窗体的对话框。
- public JDialog(Frame f)：创建一个指定父窗体的对话框，但是该窗体没有标题。
- public JDialog(Frame f, boolean model)：创建一个指定类型的对话框，并指定父窗体，但该窗体没有指定标题。
- public JDialog(Frame f, String title)：创建一个指定标题和父窗体的对话框。
- public JDialog(Frame f, String title, boolean model)：创建一个指定标题、窗体和模式的对话框。

下面来看一个实例，该实例主要实现单击JFrame窗体中的按钮后，弹出一个对话框窗体。

在项目中创建MyJDialog类，该类继承JDialog窗体，并在窗口中添加按钮，当用户单击该按钮后，将弹出一个对话框窗体。代码如下：
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MyJDialog extends JDialog {                        //创建新类继承JDialog类
    public MyJDialog(MyFrame myFrame) {
        //实例化一个JDialog类对象，指定对话框的父窗体、窗体标题和类型
        super(myFrame, "第一个JDialog窗体",true);
        Container container = getContentPane();                 //创建一个容器
        container.add(new JLabel("这是一个对话框"));         //在容器中添加标签
        setBounds(120,120,100,100);        //设置对话框窗体的大小
    }
}

class MyFrame extends JFrame{                                   //创建新类
    public static void main(String[] args) {
        MyFrame myFrame = new MyFrame();                        //实例化MyDialog类对象
        new MyJDialog(myFrame);
    }
    public MyFrame(){
        Container container = getContentPane();                 //创建一个容器
        container.setLayout(null);
        JLabel jLabel = new JLabel("这是一个JFrame窗体");   //在窗体中设置标签
        //将标签的文字至于标签中间container.add(jLabel);
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        container.add(jLabel);
        JButton jButton = new JButton("弹出对话框");
        jButton.setBounds(10,10,100,21);
        jButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {        //为按钮添加鼠标单击事件
                //是MyJDialog窗体可见
                new MyJDialog(MyFrame.this).setVisible(true);
            }
        });
        container.add(jButton);                                 //将按钮添加到容器中
    }
//此处省略部分代码
}
```
