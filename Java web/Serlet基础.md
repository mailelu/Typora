# Servlet体系结构

Servlet包含两个软件包:

* java.servlet包:包含支持所有协议的通用的Web组件接口和类
* java.servlet.http包:包含支持HTTP协议的接口和类



1. Servlet接口

Javax.servlet.Servlet接口源码:主要包含了

* `init() `: 初始化
* `service()`: 用户请求回复方法
* `destroy`: 服务销毁方法
* `getServletConfig() `: 获得serlvetconfig对象
* `getServletInfo()`: 返回一个String对象,包含Servlet信息,例如开发者,创建日期和描述信息等



2.HttpServlet类

* 实现HTTP
* `srevice()`
* `doGet()`: 用来处理一个HTTP GET请求
* `doPost()`:用来处理一个HTTP POST请求



Http的缺省的请求方式是:GET



# Servlet生命周期

Servlet程序本身不直接在Java虚拟机上运行,而是由Servlet容器负责管理其整个生命周期

分为7个状态:创建,初始化,服务可用,服务不可用,处理请求,终止服务,销毁

分为4个阶段:加载和实例化,初始化,处理请求,销毁



# 重定向与请求转发

1. 重定向

重定向是指由原请求地址重新定位到某个新地址,原有的请求失效,客户端看到的是新的请求返回的响应结果,客户端浏览器地址栏变为新请求地址

* 是由`sendRedirect()`方法实现的

2. 请求转发

请求转发是指将请求再转发到其他的地址,转发过程中使用的是用一个请求,转发后浏览器地址栏内容不变.

* `forward()`:将请求转发给其他资源
* `include()`:将其他资源并入到当前请求中



# Servlet核心接口

* ServletConfig接口:用于获取Servlet初始化参数和SevletContext对象
* ServletContext接口:代表当前Servlet运行环境,可以使用这个接口访问Servlet容器中的资源
* HttpServletRequest接口:用于封装HTTP请求信息
* HttpServletResponse接口:用于封装HTTP响应信息



## ServletConfig接口

容器在初始化一个Servlet时,将为该Servlet创建一个唯一的ServletConfig对象,并将这个ServletConfig对象通过init()方法传递并保存在此Servlet对象中

* `getInitParameter()`: 根据给定的初始化参数名称,返回参数值
* `getInitParamenter()`: 返回一个Enumeration对象,包含所有初始化参数名称
* `getServletContext()`: 返回当前ServletContext()对象
* `getServletName()`: 返回当前Servlet名字



## ServletContext接口

也成为Servlet上下文,代表当前Servlet环境,是Servlet与Servlet容器之间直接通信的接口.

Servlet容器在启动一个Web应用时,会为该应用创建一个唯一的ServletContext对象供应用中的所有Servlet对象共享

* `getInitParameter()`返回一个web应用范围内指定的初始化参数值
* `setAttribute()`: 把一个对象和一个属性名关联
* `getAttribute()`: 根据属性名,返回一个Object类型的对象
* `getContextPath()`:返回当前Web应用的根路径



## HttpServletRequest接口

用于封装请求信息,每次请求Servlet时,创建并传入Servlet的service()方法中

在HttpServlet类的service()中,传入的ServletRequest对象被强制转换为HttpServletRequest对象来进行HTTP请求信息的处理



## HttpServletResponse接口

ServletResponse接口被定义为用于创建响应消息,每次用户请求servlet时都会创建并传入Servlet的service()方法中



HTTP码常见的响应代码:

* 200 : 请求成功
* 302 : 资源暂时转移到其他URL
* 404 : 请求的资源不存在
* 500 : 服务器内部错误











