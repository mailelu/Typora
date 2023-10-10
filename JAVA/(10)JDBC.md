# 下载连接器



# 加载驱动

```java
try {Class.forName("com.mysql.cj.jdbc.Driver");
    }
catch(Exception e){}
```



# 连接数据库

使用con对象 处理链接数据库

```java
Connection con;
String uri =
"jdbc:mysql://localhost:3306/数据库名称?useSSL=false&serverTimezone=UTC"
String user = "";
String password="";
try{
    con = DriverManager.getConnection(uri,user,password);
}
catch(SQLException e){
    System.out.println(e);
}
```

**对DriverManager**

是用来链接数据库的

# 查询操作

## 1.声明SQL语句对象(sql)  然后用链接对象(con)调用方法

```java
Statement sql = con().createStatement;
executeQuery()用来执行sql语句
    
PreparedStatement 使用参数设置，可读性好，不易犯错
String sql = "insert into hero values(null,?,?,?)";
然后使用setString(?(1,2,3),xxx)来设置?里的内容
```



## 2.处理查询结果

查询结果放在ResultSet类声明的对象中

**按列**组织的数据行构成

````java
ResultSet rs = sql.executeQuery("select * from xxx");
````

由于一次只能看到一个数据行

所以需要使用**next()**来获得下一个数据行

索引给到getxxx(索引)



```java
whlie(re.next()){
    String number = rs.getString(1); //用来获取列
}
//re.next()是为了获取下一个数据(行)
```



# 关于优化sql语句的执行速度

预编译底层数据,减轻sql解释器的负担

prepareStatement(String sql)



```java
con.prepareStatement(sqlStr)
```



# 使用?代表通配符

```java
String str = "select * from mess where height < ? and me = ?";
PreparedStatement sql = con.prepareStatement(Str);
```



## 设置?

```java
sql.setFloat(1,1.76f);  //设置第一个?
sql.setString(2,"xxx");  //设置第二个?
```



# 通用查询

```java
ResultSetMetData metaData = rs.getMetData();
//返回集的元数据对象
int getColumnCount();//返回结果中列的数目
String getColumnName(i);//返回结果集中第i列的名字
```



# 事物处理

关闭自动提交模式(即刻生效): setAutoCommit(false); 

**再获取Statement对象**



直到con使用commit()方法  sql语句才会生效

注意:如果出现异常,使用*rollback()*恢复数据





