# URL类

URL类是java.net包中的一个类

使用URL对象可以获得URL中的资源,包含三种信息(协议,地址,资源)

## URL的构造方法

```java
public URL(String spec)throws MalformedURLException
    
try{
    URL url = new URL("http://www.google.com");
}
catch(MalformedURLException){
    System.out.println("Bad URL:"+url);
}


```

