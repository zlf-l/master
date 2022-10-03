# JavaIO

## 1.IO里面的常见类，字节流、字符流、接口、实现类、方法阻塞

输入流：就是从外部文件输入到内存

输出流：主要是从内存输出到文件

IO里面常见的类，第一印象就只知道IO流中有很多类，IO流主要分为字符流和字节流。字符流中有抽象类InputStream和OutputStream，它们的子类FileInputStream，FileOutputStream，BufferedOutputStream等。字符流BufferedReader和Writer等。都实现了Closeable，Flushable，Appendable这些接口。程序中的输入输出都是以流的形式保存的，流中保存的实际上全都是字节文件。

java中的阻塞式方法是指在程序调用改方法时，必须等待输入数据可用或者检测到输入结束或者抛出异常，否则程序会一直停留在该语句上，不会执行下面的语句。比如read()和readLine()方法。

## 2.谈谈对NIO的认知

对于NIO，它是非阻塞式，核心类：

1. Buffer为所有的原始类型提供(Buffer)缓存支持。

2. Charset字符集编码解码解决方案

3. Channel一个新的原始I/O抽象，用于读写Buffer类型，通道可以认为是一种连接，可以是到特定设备，程序或者是网络的连接。

## 3.字节流和字符流的区别

字符流和字节流的使用非常相似，但是实际上字节流的操作不会经过缓冲区（内存）而是直接操作文本本身的，而字符流的操作会先经过缓冲区（内存）然后通过缓冲区再操作文件

以字节为单位输入输出数据，字节流按照8位传输

以字符为单位输入输出数据，字符流按照16位传输

## 4.NIO和传统的IO有什么区别

传统IO一般是一个线程等待连接，连接过来之后分配给processor线程，processor线程与通道连接后如果通道没有数据过来就会阻塞（线程被动挂起）不能做别的事情。NIO则不同，首先，在selector线程轮询的过程中就已经过滤掉了不感兴趣的事件，其次，在processor处理感兴趣事件的read和write都是非阻塞操作即直接返回的，线程没有被挂起。

传统io的管道是单向的，nio的管道是双向的。

两者都是同步的，也就是java程序亲力亲为的去读写数据，不管传统io还是nio都需要read和write方法，这些都是java程序调用的而不是系统帮我们调用的，nio2.0里这点得到了改观，即使用异步非阻塞AsynchronousXXX四个类来处理。

## 5.BIO和NIO和AIO的区别以及应用场景

**同步**：java自己去处理IO。

**异步**：java将IO交给操作系统去处理，告诉缓存区大小，处理完成回调。阻塞：使用阻塞IO时，Java调用会一直阻塞到读写完成才返回。

**非阻塞**：使用非阻塞IO时，如果不能立马读写，Java调用会马上返回，当IO事件分发器通知可读写时在进行读写，不断循环直到读写完成。

**BIO**：同步并阻塞，服务器的实现模式是一个连接一个线程，这样的模式很明显的一个缺陷是：由于客户端连接数与服务器线程数成正比关系，可能造成不必要的线程开销，严重的还将导致服务器内存溢出。当然，这种情况可以通过线程池机制改善，但并不能从本质上消除这个弊端。

**NIO**：在JDK1.4以前，Java的IO模型一直是BIO，但从JDK1.4开始，JDK引入的新的IO模型NIO，它是同步非阻塞的。而服务器的实现模式是多个请求一个线程，即请求会注册到多路复用器Selector上，多路复用器轮询到连接有IO请求时才启动一个线程处理。

**AIO**：JDK1.7发布了NIO2.0，这就是真正意义上的异步非阻塞，服务器的实现模式为多个有效请求一个线程，客户端的IO请求都是由OS先完成再通知服务器应用去启动线程处理（回调）。

> 应用场景：并发连接数不多时采用BIO，因为它编程和调试都非常简单，但如果涉及到高并发的情况，应选择NIO或AIO，更好的建议是采用成熟的网络通信框架Netty。

## 6.什么是Java序列化，如何实现Java序列化

序列化就是一种用来处理对象流的机制，将对象的内容进行流化。可以对流化后的对象进行读写操作，可以将流化后的对象传输于网络之间。序列化是为了解决在对象流读写操作时所引发的问题

序列化的实现：将需要被序列化的类实现Serialize接口，没有需要实现的方法，此接口只是为了标注对象可被序列化的，然后使用一个输出流（如：FileOutputStream）来构造一个ObjectOutputStream(对象流)对象，再使用ObjectOutputStream对象的write(Object obj)方法就可以将参数obj的对象写出

## 7.PrintStream、BufferedWriter、PrintWriter的比较

* PrintStream类的输出功能非常强大，通常如果需要输出文本内容，都应该将输出流包装成PrintStream后进行输出。它还提供其他两项功能。与其他输出流不同，PrintStream永远不会抛出IOException；而是，异常情况仅设置可通过checkError方法测试的内部标志。另外，为了自动刷新，可以创建一个PrintStream

* BufferedWriter：将文本写入字符输出流，缓冲各个字符从而提供单个字符，数组和字符串的高效写入。通过write()方法可以将获取到的字符输出，然后通过newLine()进行换行操作。

  BufferedWriter中的字符流必须通过调用flush方法才能将其刷出去。并且BufferedWriter只能对字符流进行操作。如果要对字节流操作，则使用BufferedInputStream

* PrintWriter的println方法自动添加换行，不会抛异常，若关心异常，需要调用checkError方法看是否有异常发生，PrintWriter构造方法可指定参数，实现自动刷新缓存（autoflush）

## 8.什么是节点流，什么是处理流，各有什么好处，处理流的创建有什么特征

节点流：直接与数据源相连，用于输入或者输出

处理流：在节点流的基础上对之进行加工，进行一些功能的扩展

处理流的构造器必须要传入节点流的子类

## 9.什么是IO流

它是一种数据的流从源头流到目的地。比如文件拷贝，输入流和输出流都包括了。输入流从文件中读取数据存储到进程(process)中，输出流从进程中读取数据然后写入到目标文件。

## 10.有哪些可用的Filter流

在java.io包中主要由4个可用的filter Stream。两个字节filter Stream，两个字符filter Stream.分别是FilterInputStream，FilterOutputStream，FilterReader and FilterWriter，这些类是抽象类，不能被实例化的。

## 11.Java中有几种类型的流

**按照流的方向**：输入流（inputStream）和输出流（outputStream）

**按照实现功能分**：节点流（可以从或向一个特定的地方（节点）读写数据。如FileReader）和处理流（是对一个已存在的流的连接和封装，通过所封装的流的功能调用实现数据读写。如BufferedReader。处理流的构造方法总是要带一个其他的流对象做参数。一个流对象经过其他流的多次包装，称为流的链接。）

**按照处理数据的单位**：字节流和字符流。字节流继承于InputStream和OutputStream，字符流继承于InputStreamReader和OutputStreamWriter。

## 12.如何实现对象克隆

有两种方式：

* 实现Cloneable接口并重写Object类中的clone()方法；
* 实现Serializable接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆

## 13.什么是缓冲区、有什么作用

缓冲区就是一段特殊的内存区域，很多情况下当程序需要频繁地操作一个资源（如文件或数据库）则性能会很低，所以为了提升性能就可以将一部分数据暂时读写到缓存区，以后直接从此区域中读写数据即可，这样就可以显著的提升性能。

对于Java字符流的操作都是在缓冲区操作的，所以如果我们想在字符流操作中主动将缓冲区刷新到文件则可以使用flush()方法操作。

## 14.什么是阻塞IO什么是非阻塞IO

IO操作包括：对硬盘的读写、对socket的读写以及外设的读写。

当用户线程发起一个IO请求操作（本文以读请求操作为例），内核会去查看要读取的数据是否就绪，对于阻塞IO来说，如果数据没有就绪，则会一直在那等待，直到数据就绪；对于非阻塞IO来说，如果数据没有就绪，则会返回一个标志信息告知用户线程当前要读的数据没有就绪。当数据就绪之后，便将数据拷贝到用户线程，这样才完成了一个完整的IO读请求操作，也就是说一个完整的IO读请求操作包括两个阶段：

1. 查看数据是否就绪；

2. 进行数据拷贝（内核将数据拷贝到用户线程）。

那么阻塞（blockingIO）和非阻塞（non-blockingIO）的区别就在于第一个阶段，如果数据没有就绪，在查看数据是否就绪的过程中是一直等待，还是直接返回一个标志信息。Java中传统的IO都是阻塞IO，比如通过socket来读数据，调用read()方法之后，如果数据没有就绪，当前线程就会一直阻塞在read方法调用那里，直到有数据才返回；而如果是非阻塞IO的话，当数据没有就绪，read()方法应该返回一个标志信息，告知当前线程数据没有就绪，而不是一直在那里等待。