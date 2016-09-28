## servlet生命周期

### servlet生命周期包含如下的几个阶段

![servlet生命周期图](https://github.com/chlsmile/blogfile/blob/master/blogfile/servlet生命周期图.png)


### servlet生命周期详细过程

#### 1.加载和实例化
Servlet容器负责加载和实例化Servlet。加载和实例化可以发生在容器启动时，或者延迟初始化直到容器决定有请求需要处理时。当Servlet 引擎启动后，servlet 容器必须定位所需要的Servlet 类。Servlet 容器使用普通的Java 类加载设施加载Servlet类。可以从本地文件系统或远程文件系统或者其他网络服务加载。加载完Servlet 类后，容器就可以实例化它并使用了

#### 2.初始化
一旦一个Servlet 对象实例化完毕，容器接下来必须在处理客户端请求之前初始化该Servlet 实例。初始化的目的是以便Servlet 能读取持久化配置数据，初始化一些代价高的资源（比如JDBC API 连接），或者执行一些一次性的动作。容器通过调用Servlet 实例的init 方法完成初始化，init方法定义在Servlet 接口中，并且提供一个唯一的ServletConfig接口实现的对象作为参数，该对象每个Servlet实例一个。
配置对象允许Servlet 访问由Web 应用配置信息提供的键-值对的初始化参数。该配置对象也提供给Servlet去访问一个ServletContext对象，ServletContext描述了Servlet的运行时环境。

#### 3.请求处理
- Servlet 完成初始化后，Servlet 容器就可以使用它处理客户端请求了。客户端请求由ServletRequest 类型的request对象表示。Servlet封装响应并返回给请求的客户端，该响应由ServletResponse类型的response对象表示。这两个对象（request 和response）是由容器通过参数传递到Servlet接口的service方法的。
- 在 HTTP 请求的场景下，容器提供的请求和响应对象具体类型分别是HttpServletRequest和HttpServletResponse。
- 需要注意的是，由Servlet 容器初始化的某个Servlet 实例在服务期间，可以在其生命周期中不处理任何请求。

#### 4.终止服务




