---
title: JavaStudyNotes-集合&&泛型
---
# 集合框架

## 了解集合框架

## List（ArrayList和LinkedList）

### List接口

List接口继承了Collection接口，因此包含Collection中的所有方法。此外，List接口还定义了以下两个非常重要的方法。

get(int index):获得指定索引位置的元素。
set(int index, Object obj):将集合中指定索引位置的对象修改为指定的对象。

### List接口的实现类

List接口的常用实现类有ArrayList与LinkedList。

- ArrayList类实现了可变的数组，允许保存所有元素，包括null，并可以根据索引位置对集合进行快速的随机访问；缺点是向指定的索引位置插入对象或者删除对象的速度较慢。
- LinedList类才用链表的结构保存对象。这种结构的有点是便于向集合中插入和删除对象，需要向集合中插入、删除对象时，使用LinkedList类实现的List集合的效率较高；但是对于随机访问集合中的对象，使用LinkedList类实现List集合的效率较低。

使用List集合时通畅声明为List类型，可通过不同的实现类来实现实例化集合

分别通过ArrayList和LinkedList类实例化List集合
eg:

```java
List<E> list = new ArrayList<>();
List<E> list2 = new LinkedList<>();
```

在以上代码中，E可以是合法的Java数据类型。例如，如果集合中的元素为字符串类型，那么E可以修改为String。

在项目中创建类Gather，在主方法中创建集合对象，通过Math类的random（）方法随机获取集合中的某个元素，然后移除数组中索引位置是“2”的元素，最后遍历数组。
eg:

```java
public class Gather{
  public static void main(String[] args){
    List<E> list = new ArrayList<>();
    list.add("a");
    list.add("b");
    list.add("c");
    int i = (int)(Math.random() * list.size());
    System.out.println("随机获取数组中的元素：" + list.get(i));
    list.remove(2);
    System.out.println("将索引位置为2的元素从数组中移除后，数组中的元素是：");
    for(int j = 0;j < list.size();j++){
      System.out.println(list.get(j));
    }
  }
}
```

## Set（HashSet）

Set集合中的对象不按照特定的方式排序，只是简单的把对象加入到集合中，但Set集合中不能包含重复的对象。Set集合由Set接口和Set接口的实现类组成。Set接口继承了Collection接口，因此包含了Collection接口的所有方法。

Set接口常用的实现类有HashSet类和TreeSet类。

- HashSet类实现Set接口，由哈希表（实际上是一个HashMap的实例）支持。它不保证Set的迭代顺序，特别是它不保证该顺序恒久不变。此类允许使用null元素。
- TreeSet类不仅实现了Set接口，还实现了java.util.SortedSet接口，因此，TreeSet类实现的Set集合在遍历集合时按照自然顺序递增排序，也可以按照指定比较器递增排序，即可以通过比较器对用TreeSet类实现的Set集合中的对象进行排序。TreeSet类新增的方法如下所示。


方法                                  |功能描述
-------------------------------------|-------------------------------------------------
first()                              |返回此Set中当前第一个（最低）元素
last()                               |返回此Set中当前最后一个（最高）元素
comparator()                         |返回对此Set中的元素进行排序的比较器。如果此Set使用自然顺序，则返回null
headSet(E toElement)                 |返回一个新的Set集合，新集合是toElement（不包含）之前的所有元素
tailSet(E fromElement)               |返回一个新的Set集合，新集合包含对象fromElement（包含）之后的所有对象
subSet(E fromElement ,E fromElement) |返回一个新的Set集合，是fromElement（包含）对象与fromElement（不包含）对象之间的所有对象

在项目中创建类UpdateStu，实现Comparable接口，重写该接口中的compareTo()方法。在主方法中创建UpdateStu对象，创建集合，并将UpdateStu对象添加到集合中。遍历该集合中的全部元素，以及通过headSet()、subSet()方法获得的部分集合。
eg:
```java
import java.util.Iterator;
import java.util.TreeSet;

public class UpdateStu implements Comparable<object>{
  String name;
  long id;

  public UpdateStu(String name, long id){
    this.name = name;
    this.id = id;
  }

  public int compareTo(Object o){
    UpdateStu upstu = (UpdateStu) o;
    int result = id > upstu.id ? 1 : (id == upstu.id ? 0 : -1);
    return result;
  }

  public String getName(){
    return name;
  }

  public void setName(String name){
    this.name = name;
  }

  public long getId(){
    return id;
  }

  public void setId(long id){
    this.id = id;
  }

  public static void main(String[] args){

    UpdateStu stu1 = new UpdateStu("李同学", 01011);
    UpdateStu stu2 = new UpdateStu("陈同学", 01021);
    UpdateStu stu3 = new UpdateStu("王同学", 01051);
    UpdateStu stu4 = new UpdateStu("马同学", 01012);

    TreeSet<UpdateStu> tree = new TreeSet<>();
    tree.add(stu1);
    tree.add(stu2);
    tree.add(stu3);
    tree.add(stu4);

    Iterator<UpdateStu> it = tree.iterator();
    System.out.println("Set集合中的所有元素：");
    while(it.hasNext()){
      UpdateStu stu = (UpdateStu)it.next();
      System.out.println(stu.getId() + " " + stu.getName());
    }
    it = tree.headSet(stu2).iterator();
    System.out.println("截取前面部分的集合：");
    while(it.hasNext()){
      UpdateStu stu = (UpdateStu)it.next;
      System.out.println(stu.getId() + " " + stu.getName());
    }
    it = tree.subSet(stu2, stu3).iterator();
    System.out.println("截取中间部分的集合：");
    while(it.hasNext()){
      UpdateStu stu = (UpdateStu)it.next;
      System.out.println(stu.getId() + " " + stu.getName());
    }
  }
}
```

代码说明：存入TreeSet类实现的Set集合必须实现Comparable接口，该接口中的compareTo(Object o)方法比较此对象与指定对象的顺序。如果该对象小于、等于、或大于指定对象则分别返回负整数、0、或正整数。


## Map（HashMap）

Map集合没有继承Collection接口，其提供的是key到value的映射。Map中不能包含相同的key，每个key只能映射一个value。key还决定了存储对象在映射中的存储位置，但不是由key对象本身决定的，而是通过一种“散列技术”进行处理，产生一个散列码的正数值。散列码通常用做一个偏移量，该偏移量对应分配给映射的内存区域的起始位置，从而确定存储对象在映射中的存储位置。Map集合包括Map接口以及Map接口的所有实现类

### Map接口

Map接口提供了将key映射到值的对象。一个映射不能包含重复的key，每个key最多只能映射到一个值。Map接口中同样提供了集合的常用方法，除此之外还包括如下表所示的常用方法。

方法                         |功能描述
----------------------------|-----------------------------------------------
put(K key, V value)         |向集合中添加指定的key与value的映射关系
containsKey(Object key)     |如果此映射中包含指定key的映射关系，则返回true
containsValue(Object value) |如果此映射将一个或多个key映射到指定值，则返回true
get(Object key)             |如果存在指定key对象，则返回该对象对应的值，否则返回null
keySet()                    |返回该集合中的所有key对象形成的Set集合
values()                     |返回该集合中所有值对象形成的Set集合

在项目中创建类UpdateStu，在主方法中创建Map集合，并获取Map集合中所有key对象的集合和所有values值的集合，最后遍历集合。
eg：

```java
public class UpdateStu{
  public static void main(String[] args){
    Map<String,String> map = new HashMap<>();
    map.put("01","李同学");
    map.put("02","魏同学");
    Set<String> set = map.keySet();
    Iterator<Stirng> it = set.iterator();
    System.out.println("key集合中的元素：");
    while(it.hasNext()){
      System.out.println(it.next());
    }
    Collection<String> coll = map.values();
    it = coll.iterator();
    System.out.println("valus集合中的元素：");
    while(it.hasNext()){
      System.out.println(it.next());
    }
  }
}
```

### Map接口的实现类

Map接口常用的实现类有HashMap和TreeMap。建议使用HashMap类实现Map集合，因为由HashMap类实现的Map集合添加和删除映射关系效率更高。HashMap是基于哈希表的Map接口的实现，HashMap通过哈希码对其内部的映射关系进行快速的查找；而TreeMap中的映射关系存在一定的顺序，如果希望Map集合中的对象也存在一定的顺序，应该使用TreeMap类实现Map集合。

- HashMap类是基于哈希表的Map接口的实现，此实现提供所有可选的映射操作，并允许使用null值和null键，但必须保证键的唯一性。HashMap通过哈希表对其内部的映射关系进行快速查找。此类不保证映射的顺序，特别是它不保证该顺序恒久不变。
- TreeMap类不仅实现了Map接口，还实现了java.util.SortedMap接口，因此，集合中的映射关系具有一定的顺序。但在添加、删除和定位映射关系的时候，TreeMap类比HashMap类性能稍差。由于TreeMap类实现的Map集合中的映射关系是根据键对象按照一定顺序排列的，因此不允许键对象是null。可以通过HashMap类创建Map集合，当需要顺序输出是，在创建一个完成相同映射关系的TreeMap类实例。

通过HashMap类实例化Map集合，并遍历该Map集合，然后创建TreeMap实例实现将集合中的元素顺序输出。
1. 首先创建Emp类
```java
public class Emp{
  private String e_id;
  private String e_name;
  public Emp(String e_id, String e_name){
    this.e_id = e_id;
    this.e_name = e_name;
  }
  //此处省略属性的get和set方法，请自行实现
}
```
2. 创建一个用于测试的主类。首先新建一个Map集合，并添加集合对象。分别遍历由HashMap类与TreeMap类实现的Map集合，观察两者的不同观点。关键代码如下：
```java
public class MapTest{
  public static void main(String[] args) {
    Map<String, String> map = new HashMap<>();

    Emp emp1 = new Emp("1","张三");
    Emp emp2 = new Emp("2","黄七");
    Emp emp3 = new Emp("3","赵六");
    Emp emp4 = new Emp("4","王五");
    Emp emp5 = new Emp("5","李四");

    map.put(emp4.getE_id(),emp4.getE_name());
    map.put(emp5.getE_id(),emp5.getE_name());
    map.put(emp1.getE_id(),emp1.getE_name());
    map.put(emp2.getE_id(),emp2.getE_name());
    map.put(emp3.getE_id(),emp3.getE_name());

    Set<String> set = map.keySet();
    Iterator<String> it = set.iterator();
    System.out.println("HashMap类实现的Map集合，无序：");
    while(it.hasNext()){
      String str = (String)it.next();
      String name = (String)map.get(str);
      System.out.println(str + " " + name);
    }

    TreeMap<String, String> treemap = new TreeMap<>();
    treemap.putAll(map);
    Iterator<String> iter = treemap.keySet().iterator();
    System.out.println("Treemap类实现的Map集合，键对象升序：");
    while(iter.hasNext()){
      Strign str = (String)iter.next();
      String name = (String)treemap.get(str);
      System.out.println(str + " " + name);
    }
  }
}
```
# 泛型

泛型实际上就是使程序员定义安全的类型。在没有出现泛型之前，Java也提供了对Object的引用“任意化”操作，这种“任意化”操作就是对Object引用进行向下转型和向上转型操作，但是某些强制类型转换的错误也许不会被编译器捕捉，而在运行后出现异常，可见强制类型转换存在安全隐患，所以在此提供了泛型机制。

## 定义泛型类

Object类为最上层的父类，很多程序员为了使程序更为通用，设计程序时通常使传入的值与返回的值卫衣Object类型为主。当需要使用这些实例时，必须正确的将该实例转换为原来的类型，否则在运行时将会发生ClassCastException异常。
泛型的语法如下：
- 类名<T>
其中，T代表一个类型的名称。
在项目中定义了OverClass类，该类的定义如下：
```java
public class OverCLass{
  private T over;
  public getOver(){
    return over;
  }
  public setOver(T over){
    this.over = over;
  }
  public static void public static void main(String[] args) {
    //实例化一个Boolean型的对象
    OverCLass<Boolean> over1 = new OverCLass<Boolean>();
    //实例化一个Float型的对象
    OverCLass<Float> over2 = new OverCLass<Float>();
    over1.setOver(true);
    over2.setOver(12.4f);
    Boolean b = over1.getOver();
    Float f = over2.getOver();
    System.out.println(b);
    System.out.println(f);
  }
}
```

在本例中定义类时，在类名后面添加了一个<T>语句，这里便使用了泛型机制。可以将OverClass类称为泛型类，同时返回和接受的参数使用T这个类型。最后在主方法中可以使用Over<Boolean>形式返回一个Boolean型的对象，使用OverClass<Float>形式返回一个Float类型的对象，使这两个对象分别调用setOver()方法不需要进行显式向上转型操作，setOver()方法直接接受相应类型的参数，而调用getOver()方法时，不需要进行向下转型操作，直接将getOver()方法返回的值赋予相应的变量即可。

从该例中可以看出，使用泛型定义的类在声明该类对象时可以根据不同的需求指定<T>真正的类型，而在使用类中的方法传递或返回数据类型时将不再需要进行类型转换操作，而是使用在声明泛型类对象时“<>”中设置的类型。

使用泛型这种形式将不会发生ClassCastException异常，因为在编译器中就可以检查类型匹配是否正确

- 在定义泛型类时，一般类型名称使用T来表达，而容器的元素使用E来表达，具体的设置大家可以参看JDK5.0以上版本的API。

## 泛型的常规用法

- 定义泛型类时声明多个类型
在定义泛型类时，可以声明多个类型。语法如下：
```java
MutiOverClass<T1, T2>
MutiOverClass:泛型类名称
```
其中，T1和T2为可能被定义的类型。
这样在实例化指定类型的对象时就可以指定多个类型。例如：
```java
MutiOverClass<Boolean, Float> = new MutiOverClass<Boolean, Float>();
```

- 定义泛型类时声明数组
定义泛型类时也可以声明数组，下面的实例中定义泛型时便声明了数组类型。

在项目中创建ArrayClass类，在该类中定义泛型类声明数组类型。
```java
public class ArrayClass <T>{
  private T[] array;
  public void setT(T[] array){
    this.arary = array;
  }
  public T[] getT(){
    return array;
  }
  public static void main(String[] args) {
    ArrayClass<String> a = new ArrayClass<String>();
    String[] array = {"member 1","member 2","member 3","member 4","member 5"};
    a.setT(array);
    for(int i = 0; i < a.getT().length; i++){
      System.out.println(a.getT()[i]);
    }
  }
}
```
本实例在定义泛型类的时候声明了一个成员数组，数组的类型为泛型，然后在泛型类中相应设置set和get方法。可见，可以在使用泛型机制时声明一个数组，但是不可以使用泛型来建立数组实例。

- 集合类声明容器的元素
可以使用K和V两个字符代表容器中的键值和与键值对应的具体值。

集  合  类 | 泛  型  定  义
---------- |---------------
ArrayList  |ArrayList<E>
HashMap    |HashMap<K,V>
HashSet    |HashSet<E>
Vector     |Vector<E>

## 泛型的高级用法

- 限制泛型可用类型
默认可以使用任何类型来实例化一个泛型对象，但Java中也对泛型类实例的类型作了限制。语法如下：

class 类名称<T extends anyClass>

其中，anyClass指某个接口或类。
使用泛型限制后，泛型类的类型必须实现或继承了anyClass这个接口或类。无论anyClass是接口还是类，在进行泛型限制时都必须使用extends关键字。

在项目中创建LimitClass类，在该类中限制泛型类型。
```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
public class LimitClass <T extends List>{
  public static void main(String[] args) {
    //可以实例化已经实现List接口的类
    LimitClass<ArrayList> l1 = new LimitClass<ArrayList>();
    LimitClass<LinkedList> l2 = new LimitClass<LinkedList>();
    //以下这句是错误的，因为HashMap没有实现List接口
    //LimitClass<HashMap> l3 = new LimitClass<HashMap>();
  }
}
```

在该例中，将泛型作了限制，设置泛型类型必须实现List接口。例如，ArrayList和LinkedList都实现了List接口，而HashMap没有实现List接口，所以在这里不能实例化泛型类对象。

- 使用类型通配符
在泛型机制中，提供了类型通配符，其主要作用是在创建一个泛型类对象时限制这个泛型类的类型实现或继承某个接口或类的子类。要声明这样一个对象可以使用“？”通配符来表示，同时使用extends关键字来对泛型加以限制。
使用泛型类型通配符的语法如下：

泛型类名称<? extends List> a = null;
其中，<? extends List>表示类型未知，当需要使用该类型对象时，可以单独实例化。

在项目中创建一个类文件，在该类中限制泛型类型。
```java
A<? extends List> a = null;
a = new A<ArrayList>();
a = new A<LinkedList>();
```

如果实例化没有实现List接口的泛型对象，编译器会报错。例如，实例化HashMap对象时，编译器将会报错，因为HashMap类没有实现List接口，
除了可以实例化一个限制泛型类型的实例之外，还可以将该实例放置在方法的参数中。

在项目中创建一个类文件，在该类中的方法参数中使用匹配字符串。
```java
public void daSomething(A<T extends List>a){

}
```
在上述代码中，定义方式有效的限制了传入doSomething()方法的参数类型。
如果使用A<?>这种形式实例化泛型类对象，则默认表示可以将A指定为实例化Object及以下的子类类型。

- 继承泛型类与实现泛型接口
定义为泛型的类和接口也可以被继承与实现。
在项目中创建一个类文件，在该类中继承泛型类。
```java
public class ExtendClass<T1>{

}
class SubClass<T1, T2, T3> extends ExtendClass<T1>{

}
```
如果在SubClass类继承ExtendClass类时保留父类的泛型类型，需要在继承时指明，如果没有指明，直接使用extends ExtendClass语句进行继承操作，则SubClass类中的T1、T2和T3都会自动变为Object，所以在一般情况一下都将父类的泛型类型保留。
定义的泛型接口也可以被实现。
```java
interface <T1>{

}
class SubClass2<T1, T2, T3> implements i<T1>{

}
```
