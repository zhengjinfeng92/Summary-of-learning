## 理解Servlet

### 什么是Servlet

**servlet就是一个Java接口**

servlet接口定义的是一套处理网络请求的规范，所有实现servlet的类，都需要实现它那五个方法，其中最主要的是两个生命周期方法 init()和destroy()，还有一个处理请求的service()，也就是说，所有实现servlet接口的类，或者说，所有想要处理网络请求的类，都需要回答这三个问题：

- 你初始化时要做什么
- 你销毁时要做什么
- 你接受到请求时要做什么

这是Java给的一种规范！就像阿西莫夫的机器人三大定律、行尸走肉里Rick的那三个问题一样，规范！

### Servlet的前世今生

Servlet是**Ser**ver App**let**（运行在服务端的小程序）

Tomcat其实是Web服务器和Servlet容器的结合体

#### 什么是Web服务器？

作用：将某个主机上的资源映射为一个URL供外界访问

#### 什么是Servlet容器？

Servlet容器，顾名思义里面存放着Servlet对象

通过Web服务器映射的URL访问资源的3个过程

- 接收请求
- 处理请求
- 响应请求

接收和响应两个步骤抽取成Web服务器，但**处理请求的逻辑**是不同的。没关系，**抽取出来做成Servlet**。

![preview](.\v2-ce6e39bb02e3c6a2f4eb1e5afaa6e4e6_r.jpg)

#### 接口方法

![preview](.\v2-cbb35ec0c92292ea599108e643fd5183_r.jpg)

![img](.\v2-1a911529c489ebdcb2a17a8e19d87290_720w.jpg)

##### ServletConfig

servletConfig对象封装了servlet的一些参数信息

![img](.\v2-3dd656100783b3e9e62621ad8e2e9b04_720w.jpg)

##### **Request/Response**

![preview](.\v2-7405fb1912570c73de8dd76da725b17c_r.jpg)

如果使用servlet处理请求：

![preview](.\v2-94e6aac29c7bb1353020d2df7f422d58_r.jpg)

简单点的就使用GenericServlet

![preview](.\v2-b9f65e77009de2832d721cb28d5ae6f1_r.jpg)

再简单点  HttpServlet

![img](.\v2-73b703e690ce018ffe88280376a67dc0_720w.jpg)

最后我们只要覆盖HttpServlet中的doGet，doPost 这些方法就好了

![img](.\v2-ab9504d35eab343a522926bf18c3167b_720w.jpg)

![img](.\v2-b33c2c238803958be0bfa70d0f40c211_720w.jpg)

