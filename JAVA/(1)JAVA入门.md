# 简单的JAVA程序

如果源文件有多个类,那么有一个类是public类

如果一个类是public类,那么源文件必须和名字相同

如果没有public类,源文件只要和其中一个类名字相同



main()方法是java应用的入口方法,**必须**是 public static void 类型的

1. public main()方法是Java虚拟机 调用的
2. void 和 static      虚拟机调用main()时,不产生任何对象



类可以用 

>public    //类只能被同一个源程序文件或包中的其他类应用
>
>abstract  //定义的类代表了一个抽象的概念 不能实例化一个对象
>
>final        //不能有子类 即不能被继承,可以提高系统的安全性

来定义

## JDK的安装目录

* bin   JDK的各种工具命令,javac和java在这个目录
* conf      JDK的配置文件
* include   平台特定的头文件
* jmods  JDK的各种模块
* legal  JDk模块授权文档
* lib  JDK补充JAR包





# 编译

使用cmd编译java语言

1. 保存Java语言的编码时ANSI

​                   直接使用javac编译java文件

2. 保存的Java语言的编码不是ANSI,以UTF-8举例

​                   使用**-encoding**给出编译的编码

```java
C:\wenjianjia>  javac -encoding utf-8 Hello.java
```



反编译java:javap



编译cmd中   javac+文件名.java  -->生成  .class  文件

运行cmd中  java + 文件名  -->运行  .class文件



使用javac *.java编译所有源文件

