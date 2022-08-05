# Object与Objects的区别

## Object类

* `java.lang.Object`类是Java语言中的根类，即所有类的父类。它中描述的所有方法子类都可以使用。在对象实例化的时候，最终找的父类就是`Object`。如果一个类没有特别指定父类， 那么默认则继承自`Object`类。

* 根据`JDK`源代码及`Object`类的`API`文档，`Object`类当中包含的方法有11个：

  > 经常用到：
  >
  > `equals()，toString()`都是直接使用或者重写的`Object`里面的这些方法；
  > `final native`修饰的方法：反射需要用到的`getClass()`，线程操作需要的`notify()，notifyAll()，wait(long timeout)`；
  > `native`修饰的方法：`hashCode()`和`clone()`
  >
  > native本地方法
  >
  > * 在Object类的源码中定义了 native 修饰的方法， native 修饰的方法称为本地方法。
  >
  > * 本地方法的作用： 就是Java调用非Java代码的接口。方法的实现由非Java语言实现，比如C或 C++。
  > * 被native修饰的本地方法我们无法查看源码。

| 返回值           | 方法名                        | 作用                                                         |
| ---------------- | ----------------------------- | ------------------------------------------------------------ |
| protected Object | clone()                       | 创建并返回此对象的副本                                       |
| boolean          | equals(Object obj)            | 判断一些其他对象是否等于此                                   |
| protected void   | finalize()                    | 当垃圾收集确定不再有对该对象的引用时，垃圾收集器在对象上调用该对象 |
| Class<?>         | getClass()                    | 返回此Object的运行时类                                       |
| int              | hashCode()                    | 返回对象的哈希码值                                           |
| void             | notify()                      | 唤醒正在等待对象监视器的单个线程                             |
| void             | notifyAll()                   | 唤醒正在等待对象监视器的所有线程                             |
| String           | toString()                    | 返回对象的字符串表示形式                                     |
| void             | wait()                        | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法 |
| void             | wait(long timeout)            | 导致当前线程等待，直到另一个线程调用 notify()方法或该对象的 notifyAll()方法，或者指定的时间已过 |
| void             | wait(long timeout, int nanos) | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法，或者某些其他线程中断当前线程，或一定量的实时时间 |

> toString方法可以将对象转成字符串。
>
> equals方法可以判断两个对象是否相同，如果要定义自己的比较规则，需要进行重写。

## Objects类

* 该类由`static`用于对对象进行`static`实用方法组成。这些实用程序包括用于计算对象的哈希码的`null` -safe或`null`方法，为对象返回一个字符串，并比较两个对象。

* Objects类是final修饰的类，不可继承，内部方法都是static方法，从jdk1.7开始才引入了Objects类 。

| 返回值         | 方法名                                          | 作用                                                         |
| -------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| static int     | compare(T a, T b, Comparator<? super T> c)      | 如果参数a,b相同则返回0，否则返回c.compare(a, b)的结果        |
| static boolean | deepEquals(Object a, Object b)                  | 对比a,b参数是否深层次相等，假定a,b为数组，对比数组的每个参数 |
| static boolean | equals(Object a, Object b)                      | 对比a,b参数是否相等                                          |
| static int     | hash(Object… values)                            | 为输入值序列生成哈希码                                       |
| static int     | hashCode(Object o)                              | 返回哈希码。如果o为null则返回0                               |
| static boolean | isNull(Object obj)                              | 如果obj参数为null返回true                                    |
| static boolean | nonNull(Object obj)                             | 如果obj参数不为null返回true                                  |
| static T       | requireNonNull(T obj)                           | 检查指定的对象引用不是 null，为null报空指针错误              |
| static T       | requireNonNull(T obj, String message)           | 检查指定的对象引用不是null并抛出自定义的NullPointerException（如果是） |
| static T       | requireNonNull(T obj, Supplier messageSupplier) | 检查指定的对象引用不是null并抛出一个自定                     |
| static String  | toString(Object o)                              | 返回对象的字符串表示形式                                     |
| static String  | toString(Object o, String nullDefault)          | 如果第一个参数不是 null ，则返回第一个参数调用 toString的结果，否则直接将第二个参数nullDefault返回 |

