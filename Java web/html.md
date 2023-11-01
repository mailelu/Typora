# html

示例:

```html
<html>
  <body>
    <p>Hello World</p>
  </body>
</html>
最简单的html
```

## 中文乱码

设置浏览器编码方式为GB2312



## 标签

HTML是由一套标记标签 （markup tag）组成，通常就叫标签

```html
<h1>
    大标题
</h1>
//将1 换成 2 , 3 将得到大小递减的标签
```

## 元素

元素指的是从开始标签到结束标签之间所有的代码
比如**<p>HelloWord</p>**



##属性

属性用来修饰标签的
比如要设置一个标题居中

```html
<h1 align="center">居中标题</h1>
```

# html的基本元素

* 标题:使用\<h1> \</h1>来表示网页标题
* 段落:使用\<p> \</p>来表示段落
* 预格式:使用\<pre>\</pre>来突出展示一段代码
* 删除效果:\<del>\</del>
* 下划线:\<ins>\</ins>
* 设置图片:\< img width = " " height =" " src="图片位置,或者一个网页链接" > width和height设置了长度和宽度
* 超链接: \<  a href = "跳转到的页面地址" >超链接文本\</a>
* 字体: \<font color = "字体颜色">内容\</font>
* 内联框架:\<iframe src = " " width = " " height = "">\</iframe>



# 表单元素

* 下拉列表: <select size = "表示大小,即显式的行数"> <option>表示列表内容</option></select>
* 普通按钮: <input type = " button" valude = "按钮名字">
* 提交按钮:\<input type = "submit " value = " 按钮名字"></input>
* 重置按钮:将type改为reset即可重置
* button按钮: \<button> </button>使用该按钮可以设置更丰富的标签,设置type="submit",IE下button的type的默认值为button不具备提交功能,其他浏览器type的默认值是submit
