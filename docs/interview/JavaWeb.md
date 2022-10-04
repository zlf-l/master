# JavaWeb

## 1.session和cookie的区别

session是存储在服务器端，cookie是存储在客户端的，所以安全来讲session的安全性要比cookie高，然后我们获取session里的信息是通过存放在会话cookie里的sessionid获取的。又由于session是存放在服务器的内存中，所以session里的东西不断增加会造成服务器的负担，所以会把很重要的信息存储在session中，而把一些次要东西存储在客户端的cookie里，然后cookie确切的说分为两大类分为会话cookie和持久化cookie，会话cookie确切的说是，存放在客户端浏览器的内存中，所以说他的生命周期和浏览器是一致的，浏览器关了会话cookie也就消失了，然而持久化cookie是存放在客户端硬盘中，而持久化cookie的生命周期就是我们在设置cookie时候设置的那个保存时间，然后我们考虑一问题当浏览器关闭时session会不会丢失，从上面叙述分析session的信息是通过会话cookie的sessionid获取的，当浏览器关闭的时候会话cookie消失所以我们的sessionid也就消失了，但是session的信息还存在服务器端，这时我们只是查不到所谓的session但它并不是不存在。那么，session在什么情况下丢失，就是在服务器关闭的时候，或者是session过期(默认时间是30分钟)，再或者调用了invalidate()的或者是我们想要session中的某一条数据消失调用session.removeAttribute()方法，然后session在什么时候被创建呢，确切的说是通过调用getsession()来创建，这就是session与cookie的区别.

## 2、session和cookie联系

session是通过cookie来工作的session和cookie之间是通过$_COOKIE['PHPSESSID']来联系的，通过$_COOKIE['PHPSESSID']可以知道session的id，从而获取到其他的信息。

在购物网站中通常将用户加入购物车的商品联通session_id记录到数据库中，当用户再次访问是，通过sessionid就可以查找到用户上次加入购物车的商品。因为sessionid是唯一的，记录到数据库中就可以根据这个查找了。

## 3.servlet的生命周期

Servlet生命周期可以分成四个阶段：加载和实例化、初始化、服务、销毁。

当客户第一次请求时，首先判断是否存在Servlet对象，若不存在，则由Web容器创建对象，而后调用init()方法对其初始化，此初始化方法在整个Servlet生命周期中只调用一次。

完成Servlet对象的创建和实例化之后，Web容器会调用Servlet对象的service()方法来处理请求。

当Web容器关闭或者Servlet对象要从容器中被删除时，会自动调用destory()方法。

## 4.什么是webservice

从表面上看，WebService就是一个应用程序向外界暴露出一个能通过Web进行调用的API，也就是说能用编程的方法通过Web来调用这个应用程序。我们把调用这个WebService的应用程序叫做客户端，而把提供这个WebService的应用程序叫做服务端。从深层次看，WebService是建立可互操作的分布式应用程序的新平台，是一个平台，是一套标准。它定义了应用程序如何在Web上实现互操作性，你可以用任何你喜欢的语言，在任何你喜欢的平台上写WebService，只要我们可以通过WebService标准对这些服务进行查询和访问。

## 5.jsp和servlet的区别、共同点、各自应用的范围

JSP是Servlet技术的扩展，本质上就是Servlet的简易方式。JSP编译后是“类servlet”。Servlet和JSP最主要的不同点在于，Servlet的应用逻辑是在[Java](http：//ask.bdqn.cn/view/18470)文件中，并且完全从表示层中的HTML里分离开来。而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。JSP侧重于视图，Servlet主要用于控制逻辑。在struts框架中，JSP位于MVC设计模式的视图层，而Servlet位于控制层.

## 6.转发（forward）和重定向（redirect）的区别

**从地址栏显示来说**

forward：是服务器请求资源，服务器直接访问目标地址的URL，把那个URL的响应内容读取过来，然后把这些内容再发给浏览器.浏览器根本不知道服务器发送的内容从哪里来的，所以它的地址栏还是原来的地址。

redirect：是服务端根据逻辑，发送一个状态码，告诉浏览器重新去请求那个地址。所以地址栏显示的是新的URL.

**从数据共享来说**

forward：转发页面和转发到的页面可以共享request里面的数据.

redirect：不能共享数据.

**从运用地方来说**

forward：一般用于用户登陆的时候，根据角色转发到相应的模块.

redirect：一般用于用户注销登陆时返回主页面和跳转到其它的网站等

**从效率来说**

forward：高.

redirect：低.

## 7.request.getAttribute()和request.getParameter()有何区别

1. request.getParameter()取得是通过容器的实现来取得通过类似post，get等方式传入的数据。
2. request.setAttribute()和getAttribute()只是在web容器内部流转，仅仅是请求处理阶段。
3. getAttribute是返回对象，getParameter返回字符串
4. getAttribute()一向是和setAttribute()一起使用的，只有先用setAttribute()设置之后，才能够通过getAttribute()来获得值，它们传递的是Object类型的数据。而且必须在同一个request对象中使用才有效。，而getParameter()是接收表单的get或者post提交过来的参数

## 8.jsp静态包含和动态包含的区别

1. 两者格式不同，静态包含：<%@ include file="文件"%>，而动态包含：<jsp：include page="文件"/>。

2. 包含时间不同，静态包含是先将几个文件合并，然后再被编译，缺点就是如果含有相同的标签，会出错。动态包含是页面被请求时编译，将结果放在一个页面。

3. 生成的文件不同，静态包含会生成一个包含页面名字的servlet和class文件；而动态包含会各自生成对应的servlet和class文件

4. 传递参数不同，动态包含能够传递参数，而静态包含不能

## 9.MVC的各个部分都有哪些技术来实现如何实现

MVC是Model－View－Controller的简写。

"Model"代表的是应用的业务逻辑（通过JavaBean，EJB组件实现）；

"View"是应用的表示面（由JSP页面产生）；

"Controller"是提供应用的处理过程控制（一般是一个Servlet），通过这种设计模型把应用逻辑，处理过程和显示逻辑分成不同的组件实现。

这些组件可以进行交互和重用。

## 10.jsp有哪些内置对象作用分别是什么

JSP有9个内置对象：

request：封装客户端的请求，其中包含来自GET或POST请求的参数；

response：封装服务器对客户端的响应；

pageContext：通过该对象可以获取其他对象；

session：封装用户会话的对象；

application：封装服务器运行环境的对象；

out：输出服务器响应的输出流对象；config：Web应用的配置对象；

page：JSP页面本身（相当于Java程序中的this）；

exception：封装页面抛出异常的对象。

## 11.Http请求的get和post方法的区别。

1. Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求

2. Get是获取信息，而不是修改信息，类似数据库查询功能一样，数据不会被修改

3. Get请求的参数会跟在url后进行传递，请求的数据会附在URL之后，以分割URL和传输数据，参数之间以&相连，％XX中的XX为该符号以16进制表示的ASCII，如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密。

4. Get传输的数据有大小限制，因为GET是通过URL提交数据，那么GET可提交的数据量就跟URL的长度有直接关系了，不同的浏览器对URL的长度的限制是不同的。

5. GET请求的数据会被浏览器缓存起来，用户名和密码将明文出现在URL上，其他人可以查到历史浏览记录，数据不太安全。

   >在服务器端，用Request.QueryString来获取Get方式提交来的数据
   >
   >Post请求则作为http消息的实际内容发送给web服务器，数据放置在HTMLHeader内提交，Post没有限制提交的数据。Post比Get安全，当数据是中文或者不敏感的数据，则用get，因为使用get，参数会显示在地址，对于敏感数据和不是中文字符的数据，则用post。

6. POST表示可能修改变服务器上的资源的请求，在服务器端，用Post方式提交的数据只能用Request.Form来获取。

## 12.tomcat容器是如何创建servlet类实例用到了什么原理

当容器启动时，会读取在webapps目录下所有的web应用中的web.xml文件，然后对xml文件进行解析，并读取servlet注册信息。然后，将每个应用中注册的servlet类都进行加载，并通过反射的方式实例化。（有时候也是在第一次请求时实例化）

在servlet注册时加上<load-on-startup>1</load-on-startup>如果为正数，则在一开始就实例化，如果不写或为负数，则第一次请求实例化。

## 13.JDBC访问数据库的基本步骤是什么

第一步：Class.forName()加载数据库连接驱动；

第二步：DriverManager.getConnection()获取数据连接对象;

第三步：根据SQL获取sql会话对象，有2种方式Statement、PreparedStatement;

第四步：执行SQL，执行SQL前如果有参数值就设置参数值setXXX();

第五步：处理结果集；

第六步：关闭结果集、关闭会话、关闭连接。

## 14.为什么要使用PreparedStatement

PreparedStatement接口继承Statement，PreparedStatement实例包含已编译的SQL语句，所以其执行速度要快于Statement对象。

作为Statement的子类，PreparedStatement继承了Statement的所有功能。三种方法execute、executeQuery和executeUpdate已被更改以使之不再需要参数。

在JDBC应用中，多数情况下使用PreparedStatement，原因如下：

* 代码的可读性和可维护性。Statement需要不断地拼接，而PreparedStatement不会。

* PreparedStatement尽最大可能提高性能。DB有缓存机制，相同的预编译语句再次被调用不会再次需要编译。

* 最重要的一点是极大地提高了安全性。Statement容易被SQL注入，而PreparedStatement传入的内容不会和sql语句发生任何匹配关系。

## 15.数据库连接池的原理。为什么要使用连接池

1. 数据库连接是一件费时的操作，连接池可以使多个操作共享一个连接。

2. 数据库连接池的基本思想就是为数据库连接建立一个“缓冲池”。预先在缓冲池中放入一定数量的连接，当需要建立数据库连接时，只需从“缓冲池”中取出一个，使用完毕之后再放回去。我们可以通过设定连接池最大连接数来防止系统无尽的与数据库连接。更为重要的是我们可以通过连接池的管理机制监视数据库的连接的数量、使用情况，为系统开发，测试及性能调整提供依据。

3. 使用连接池是为了提高对数据库连接资源的管理

## 16.execute，executeQuery，executeUpdate的区别是什么

1. Statement的execute(Stringquery)方法用来执行任意的SQL查询，如果查询的结果是一个ResultSet，这个方法就返回true。如果结果不是ResultSet，比如insert或者update查询，它就会返回false。我们可以通过它的getResultSet方法来获取ResultSet，或者通过getUpdateCount()方法来获取更新的记录条数。

2. Statement的executeQuery(Stringquery)接口用来执行select查询，并且返回ResultSet。即使查询不到记录返回的ResultSet也不会为null。我们通常使用executeQuery来执行查询语句，这样的话如果传进来的是insert或者update语句的话，它会抛出错误信息为“executeQuerymethodcannotbeusedforupdate”的java.util.SQLException。

3. Statement的executeUpdate(Stringquery)方法用来执行insert或者update/delete（DML）语句，或者什么也不返回，对于DDL语句，返回值是int类型，如果是DML语句的话，它就是更新的条数，如果是DDL的话，就返回0。

   只有当你不确定是什么语句的时候才应该使用execute()方法，否则应该使用executeQuery或者executeUpdate方法。

## 17.JDBC的ResultSet是什么

在查询数据库后会返回一个ResultSet，它就像是查询结果集的一张数据表。

ResultSet对象维护了一个游标，指向当前的数据行。开始的时候这个游标指向的是第一行。如果调用了ResultSet的next()方法游标会下移一行，如果没有更多的数据了，next()方法会返回false。可以在for循环中用它来遍历数据集。

默认的ResultSet是不能更新的，游标也只能往下移。也就是说你只能从第一行到最后一行遍历一遍。不过也可以创建可以回滚或者可更新的ResultSet

当生成ResultSet的Statement对象要关闭或者重新执行或是获取下一个ResultSet的时候，ResultSet对象也会自动关闭。

可以通过ResultSet的getter方法，传入列名或者从1开始的序号来获取列数据。

## 18.什么是Servlet

Servlet是使用JavaServlet应用程序接口（API）及相关类和方法的Java程序，所有的Servlet都必须要实现的核心接口是javax.servlet.servlet。每一个servlet都必须要直接或者间接实现这个接口，或者继承javax.servlet.GenericServlet或javax.servlet.HTTPServlet。

Servlet主要用于处理客户端传来的HTTP请求，并返回一个响应。

## 19.doGet和doPost方法有什么区别

**doGet**：GET方法会把名值对追加在请求的URL后面。因为URL对字符数目有限制，进而限制了用在客户端请求的参数值的数目。并且请求中的参数值是可见的，因此，敏感信息不能用这种方式传递。

**doPOST**：POST方法通过把请求参数值放在请求体中来克服GET方法的限制，因此，可以发送的参数的数目是没有限制的。最后，通过POST请求传递的敏感信息对外部客户端是不可见的。

## 20.JSP有哪些动作分别是什么

JSP共有以下6种基本动作

jsp：include：在页面被请求的时候引入一个文件。

jsp：useBean：寻找或者实例化一个JavaBean。

jsp：setProperty：设置JavaBean的属性。

jsp：getProperty：输出某个JavaBean的属性。

jsp：forward：把请求转到一个新的页面。

jsp：plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记

## 21.JSP常用的指令

page：针对当前页面的指令。

include：包含另一个页面

taglib：定义和访问自定义标签

## 22.页面间对象传递的方法

request、session、application、cookie

## 23.JSP中动态INCLUDE与静态INCLUDE的区别

**动态include**：用于jsp：include动作实现<jsp：include page = “include.jsp” flush = “true”/>它总是会检查所含文件的变化，适用于包含动态页面，并且可以带参数。

**静态include**：用include伪码实现，不会检查所含文件的变化，适用于包含静态页面<%@ include file=“include.html”%>.

## 24.JSP的四大范围

JSP中的四种作用域包括page、request、session和application，具体来说：

page代表与一个页面相关的对象和属性。

request代表与Web客户机发出的一个请求相关的对象和属性。一个请求可能跨越多个页面，涉及多个Web组件；需要在页面显示的临时数据可以置于此作用域。

session代表与某个用户与服务器建立的一次会话相关的对象和属性。跟某个用户相关的数据应该放在用户自己的session中。

application代表与整个Web应用程序相关的对象和属性，它实质上是跨越整个Web应用程序，包括多个页面、请求和会话的一个全局作用域。

## 25.BS与CS的联系与区别

**硬件环境不同**

C/S一般建立在专用的网络上，小范围里的网络环境，局域网之间再通过专门服务器提供连接和数据交换服务.

B/S建立在广域网之上的，不必是专门的网络硬件环境，例与电话上网，租用设备.信息自己管理.有比C/S更强的适应范围，一般只要有操作系统和浏览器就行

**对安全要求不同**

C/S一般面向相对固定的用户群，对信息安全的控制能力很强.一般高度机密的信息系统采用C/S结构适宜.可以通过B/S发布部分可公开信息.

B/S建立在广域网之上，对安全的控制能力相对弱，可能面向不可知的用户。

**对程序架构不同**

C/S程序可以更加注重流程，可以对权限多层次校验，对系统运行速度可以较少考虑.

B/S对安全以及访问速度的多重的考虑，建立在需要更加优化的基础之上.比C/S有更高的要求B/S结构的程序架构是发展的趋势，从MS的.Net系列的BizTalk 2000 Exchange 2000等，全面支持网络的构件搭建的系统.SUN和IBM推的JavaBean构件技术等，使B/S更加成熟.

**软件重用不同**

C/S程序可以不可避免的整体性考虑，构件的重用性不如在B/S要求下的构件的重用性好.

B/S对的多重结构，要求构件相对独立的功能.能够相对较好的重用.就入买来的餐桌可以再利用，而不是做在墙上的石头桌子

**系统维护不同**

C/S程序由于整体性，必须整体考察，处理出现的问题以及系统升级.升级难.可能是再做一个全新的系统

B/S构件组成，方面构件个别的更换，实现系统的无缝升级.系统维护开销减到最小.用户从网上自己下载安装就可以实现升级.

**处理问题不同**

C/S程序可以处理用户面固定，并且在相同区域，安全要求高需求，与操作系统相关.应该都是相同的系统

B/S建立在广域网上，面向不同的用户群，分散地域，这是C/S无法作到的.与操作系统平台关系最小.

**用户接口不同**

C/S多是建立的Window平台上，表现方法有限，对程序员普遍要求较高

B/S建立在浏览器上，有更加丰富和生动的表现方式与用户交流.并且大部分难度减低，减低开发成本.

**信息流不同**

C/S程序一般是典型的中央集权的机械式处理，交互性相对低

B/S信息流向可变化，B-BB-CB-G等信息、流向的变化，更像交易中心。

## 26.说出Servlet的生命周期，并说出Servlet和CGI的区别

Web容器加载Servlet并将其实例化后，Servlet生命周期开始，容器运行其init方法进行Servlet的初始化，请求到达时运行其service方法，service方法自动派遣运行与请求对应的doXXX方法（doGet，doPost）等，当服务器决定将实例销毁的时候调用其destroy方法。与cgi的区别在于servlet处于服务器进程中，它通过多线程方式运行其service方法，一个实例可以服务于多个请求，并且其实例一般不会销毁，而CGI对每个请求都产生新的进程，服务完成后就销毁，所以效率上低于servlet。

## 7.如何防止表单重复提交

针对于重复提交的整体解决方案：

1. 用redirect（重定向）来解决重复提交的问题
2. 点击一次之后，按钮失效
3. 通过loading(Loading原理是在点击提交时，生成Loading样式，在提交完成之后隐藏该样式)
4. 自定义重复提交过滤器

## 28.request作用

1. 获取请求参数getParameter()
2. 获取当前Web应用的虚拟路径getContextPath
3. 转发getRequestDispatcher(路径).forward(request，response);
4. 它还是一个域对象

## 29.get请求中文乱码

**乱码的根本原因**

浏览器的编码方式UTF-8和服务器的解码方式ISO-859-1不一样

**解决方法**

1. 第一种方式使用URLEncoder和URLDecoder两个类编解码。先以iso-8895-1进行编码，然后再以utf-8进行解码

2. 第二种方式使用String类的方法进行编解码

3. 第三种方式更改server.xml配置文件。

GET请求是在URL地址栏中传递请求参数的，它会被Tomcat服务器自动解码，而Tomcat服务器默认的字符集也是ISO-8859-1，

所以我们需要修改Tomcat服务器的字符集为UTF-8。

## 30.post请求中文乱码问题

1. post请求方式乱码的原因是：因为post是以二进制流的形式发送到的服务器。服务器收到数据后。默认以iso-8859-1进行编码。
2. post请求乱码解决，只需要在获取请求参数之前调用request.setCharacterEncoding("UTF-8");方法设置字符集即可。

## 31.响应乱码

**原因**	

由服务器编码，默认使用ISO-8859-1进行编码

由浏览器解码，默认使用GBK进行解码

**解决方案**

1. 设置响应头response.setHeader("Content-Type"，"text/html;charset=utf-8");

2. 设置响应的内容类型response.setContentType("text/html;charset=utf-8");

   通过这种方式可以在响应头中告诉浏览器响应体的编码方式是UTF-8；同时服务器也会采用该字符集进行编码

> 但需要注意的是，两种方法一定要在response.getWriter()之前进行。

## 32.Cookie对象的缺陷

1. Cookie是明文的，不安全

2. 不同的浏览器对Cookie对象的数量和大小有限制

3. Cookie对象携带过多费流量

4. Cookie对象中的value值只能是字符串，不能放对象

> 网络中传递数据只能是字符串

## 33.Session的运行机制

1. 在服务器端创建Session对象，该对象有一个全球唯一的ID

2. 在创建Session对象的同时创建一个特殊的Cookie对象，该Cookie对象的名字是JSESSIONID，该Cookie对象的value值是Session对象的那个全球唯一的ID，并且会将这个特殊的Cookie对象携带发送给浏览器
3. 以后浏览器再发送请求就会携带这个特殊的Cookie对象

4. 服务器根据这个特殊的Cookie对象的value值在服务器中寻找对应的Session对象，以此来区分不同的用户

## 34.钝化和活化

1. Session与session域中的对象一起从内存中被序列化到硬盘上的过程我们称为钝化。服务器关闭时会发生钝化。
2. Session与session域中的对象一起从硬盘上反序列化到内存中的过程我们称为活化。服务器再次开启时会发生活化。
3. 要保证session域中的对象能和Session一起被钝化和活化，必须保证对象对应的类实现Serializable接口

## 35.Filter的工作原理

Filter接口中有一个doFilter方法，当我们编写好Filter，并配置对哪个web资源进行拦截后，WEB服务器每次在调用web资源的service方法之前，都会先调用一下filter的doFilter方法，因此，在该方法内编写代码可达到如下目的：

* 调用目标资源之前，让一段代码执行。
* 是否调用目标资源（即是否让用户访问web资源）。
* 调用目标资源之后，让一段代码执行。
* web服务器在调用doFilter方法时，会传递一个filterChain对象进来，filterChain对象是filter接口中最重要的一个对象，它也提供了一个doFilter方法，开发人员可以根据需求决定是否调用此方法，调用该方法，则web服务器就会调用web资源的service方法，即web资源就会被访问，否则web资源不会被访问

## 36.Filter链是什么

在一个web应用中，可以开发编写多个Filter，这些Filter组合起来称之为一个Filter链。web服务器根据Filter在web.xml文件中的注册顺序，决定先调用哪个Filter，当第一个Filter的doFilter方法被调用时，web服务器会创建一个代表Filter链的FilterChain对象传递给该方法。在doFilter方法中，开发人员如果调用了FilterChain对象的doFilter方法，则web服务器会检查FilterChain对象中是否还有filter，如果有，则调用第2个filter，如果没有，则调用目标资源。

## 37.监听器类型

按监听的对象划分：servlet2.4规范定义的事件有三种：

1. 用于监听应用程序环境对象（ServletContext）的事件监听器

2. 用于监听用户会话对象（HttpSession）的事件监听器
3. 用于监听请求消息对象（ServletRequest）的事件监听器按监听的

事件类项划分

1. 用于监听域对象自身的创建和销毁的事件监听器

2. 用于监听域对象中的属性的增加和删除的事件监听器

3. 用于监听绑定到HttpSession域中的某个对象的状态的事件监听器

> 在一个web应用程序的整个运行周期内，web容器会创建和销毁三个重要的对象，ServletContext，HttpSession，ServletRequest。

## 38.ServletFilterListener启动顺序

启动的顺序为listener->Filter->servlet.

简单记为：理(Listener)发(Filter)师(servlet).

执行的顺序不会因为三个标签在配置文件中的先后顺序而改变。
