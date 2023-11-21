# 过滤器

过滤器也成为拦截器,可以在用户访问某个Web资源之前,对访问的请求和响应进行拦截,从而实现一些特殊功能

以下是一个过滤器运行过程的步骤:

1. 匹配过滤器
2. 发送给目标资源(过滤器修改内容后)
3. 响应返回给过滤器
4. 过滤器发送给用户(可以修改内容)



# 过滤核心接口

* javax.servlet.Filter 接口
* javax.servlet.FilterConfig接口
* javax.servlet.FilterChain接口



## Filter接口

开发Filter需要实现Filter接口

* `init()`: 初始化方法
* `doFilter()`: 过滤器的功能实现方法
* `destory()`: 在过滤器生命周期结束前由Web容器调用,释放资源



## 过滤器的生命周期

分为四个阶段

1. 加载和实例化
2. 初始化
3. doFilter()方法的执行
4. 销毁



## FilterConfig接口

FilterConfig接口由容器实现,容器将其实例作为参数传入过滤器的初始化方法中

* `getFilterName()`: 获取过滤器名字
* `getFilterParameter()`: 获取指定名字的初始化参数值
* `getServletContext()`: 获取Servlet上下文对象



## FilterChain接口

由容器实现,将其实例作为参数传入过滤器的 doFilter() 方法中,过滤器对象使用FilterChain对象调用过滤器链中的下一个过滤器,如果这是最后一个过滤器,就调用目标资源

* 只有一个方法`doFliter(request, response)`: 将使过滤器链中的下一个过滤器被调用



# 监听器

使用监听器监测用户活动以实现与用户的交互



## 与Servlet上下文相关的监听器

* `ServletContentListener`: 用于监听Context 的创建和销毁
* `ServletContentAttributeListener`: 用于监听范围内属性的改变



## 与会话相关的监听器

* `HttpSessionListener`: 用于监听会话对象的创建和销毁
* `HttpSessionAttributeListener`: 用于监听会话域内属性的改变(增删改)



## 与请求相关的监听器

* `ServletRequestListener`:用于监听用户请求的产生和结束
* `ServletRequsetAttributeListener`:用于监听Request内属性的改变







