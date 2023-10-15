# This is CS50x

```c
#include <Stdio.h>
int main(){
    printf("hello world!");
}
```

* **Hello World**



# Visual studio

> 编译器,用于编译你的code

我们如何评判你的code?

* 正确性
* 结构
* 风格



语法高亮将让你更清晰的查看你的代码

____

Terminal终端

它可以完成大多数的功能,如果有错误,会返回错误信息

完成一个完整的代码编写调试过程

1. code <filename.c> 创建一个文件
2. make <filename> 编译你的代码
3. ./<filename>   运行



___

## printf

* 格式化输出
* 使用`" "`为字符串
* 使用`;`结束语句
* `/n`为转义字符,用来创建新的行
* 需要引入头文件库



____

cs50为学生提供了许多能从标准输入中获得字符的方法

get_char("要输出的内容");

get_int ...

...

____

## 返回值

基本所有的函数都有返回值以帮助程序员判断运行情况



___

##使用转义词%

%s表示定义到一个string的变量



如果我想要输出100%呢?

```c
printf("I got 100%%");
输出 I got 100%
```

___

## c语言中的数据类型

* int
* char
* bool
* double
* float

等等

###溢出问题

涉及到不同数据类型在c语言以及操作系统下的储存位数

###强制类型转换问题



## 条件判断语句

* if(条件判断)

```c
if(){
    
}else{
    
}
```



* for循环

```c
for(只执行一次的代码;判断语句; ){
    
}
```



* while循环

```c
while(){

}
```



___

## const

使用const修饰一个变量使之成为**常量**



___

## 函数体

当你编译自己的方法时,如果你编译的代码放在main函数后,请在开头声明你定义的函数,否则会报错:

```c
int get_n();
int print_grid();
```

