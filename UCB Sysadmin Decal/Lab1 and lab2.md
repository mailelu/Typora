  >介绍shell
  >
  >what is shell
  >
  >Free  and open Source software



终端:shell是一个对用户友好的终端,有不同类型的shell

shell的基本语法类似 [command] [flags] [arguments]



# Editor

+ Nano
+ Vim
+ Emacs



Unix类似windows

# 解压缩某个gzip文件

```shell
tar 文件名.gzip
```



# 命令行中的删除,创建文件

```vim
rm <文件名>  //删除文件
ls <文件名>
mkdir <文件夹名> //创建一个文件夹
touch <文件名.后缀>  //创建一个文件

```



unix  is all of files

which 应用 //显示文件路径



## 给文件赋予权限

```shell
chmod +/=r/w/x 文件名
```



# 使用ls

```shell
ls -a//列出所有文件
ls -l//列出所有信息
ls -t//按照文件修改时间由新到旧列出文件
```





# 使用head显示文件的前几行

```shell
head -n 显式的行数 文件名
```



#>>与>的区别
第一个表示的是追加

第二个表示的是覆盖



#使用grep查找文本内容

```shell
grep -n "查找内容" ./文件名 //查找并显示行号
```



# 使用sed更改文件内容 (直接更改)

```shell
sed  -i "s/<old>/<new>/g" ./文件名 //替换
sed  -i "/<old>/d" ./文件名 //删除整行
```





# 区分bash中的传参

对terminal中的$1 $2....

其中 传递给脚本的第一个(若为方法名则为方法名)默认为$1,一次类推

对于脚本方法中的$1,对应着命令行中脚本方法名后的参数

```shell
例如:
./phonebook new aa bb
其中new $1 $2
在文件末尾进行了输入的判断
case $1:
     "new":new $2 $3
这里case中的$1对应输入的new,进行判断后的new中的 $2 $3对应aa和bb
而方法new中的$1 $2只是局部变量,在case中的new相当于运行了这个方法,把命令行中的aa bb传给了$1 和$2
```



下面给出lab中的题目

- `./phonebook new <name> <number>` adds an entry to the phonebook. Don’t worry about duplicates (always add a new entry, even if the name is the same).
- `./phonebook list` displays every entry in the phonebook (in no particular order). If the phonebook has no entries, display `phonebook is empty`
- `./phonebook remove <name>` deletes all entries associated with that name. Do nothing if that name is not in the phonebook.
- `./phonebook clear` deletes the entire phonebook.
- `./phonebook lookup <name>` displays all phone number(s) associated with that name. You can assume all phone numbers are in the form `ddd-ddd-dddd` where `d` is a digit from 0-9.



以下是测试代码

```shell
$ ./phonebook new "Linus Torvalds" 101-110-0111
$ ./phonebook list
Linus Torvalds 101-110-1010
$ ./phonebook new "Tux Penguin" 555-666-7777
$ ./phonebook new "Linus Torvalds" 222-222-2222
$ ./phonebook list
Linus Torvalds 101-110-1010
Tux Penguin 555-666-7777
Linus Torvalds 222-222-2222
# OPTIONAL BEHAVIOR
$ ./phonebook lookup "Linus Torvalds" 
101-110-1010
222-222-2222
# ALTERNATIVE BEHAVIOR
$ ./phonebook lookup "Linus Torvalds"
Linus Torvalds 101-110-1010
Linus Torvalds 222-222-2222
$ ./phonebook remove "Linus Torvalds"
$ ./phonebook list
Tux Penguin 555-666-7777
$ ./phonebook clear
$ ./phonebook list
phonebook is empty
```



我给出的答案:

```shell
#!/bin/bash
# contents of phonebook

new(){
	echo "$1 $2" >> phonebook.txt   //区分>与>>
}
list(){
	if [  -s ./phonebook.txt ]; then  //这里区分if 的[]
		cat phonebook.txt
	else 
		echo "phonebook is empty"
	fi
}

remove(){
	if grep -q "$1" ./phonebook.txt ; then  //这里-q使用了grep的返回代码
		sed -i "/$1/d"  phonebook.txt
	fi
}

lookup(){
	grep -n "$1" ./phonebook.txt 
}

my_clear(){
	> ./phonebook.txt     //直接重定向另文件为空
}

case "$1" in
	"new")
 		new "$2" "$3"
		;;
	"list")
		list
		;;
	"remove")
		remove "$2"
		;;
	"clear")
		my_clear
		;;
	"lookup")
		lookup "$2"
		;;
	*)
		echo "unknown:$1"
		;;
esac
```

