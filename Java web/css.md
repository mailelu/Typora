# CSS

使用css,就可以避免一些重复的东西,将公式化的内容使用一条语句装载

##css举例

```html
<style>
td{
  background-color:gray;
}
</style>

<table border="1">
  <tr >
      <td>1</td>
      <td>2</td>
  </tr>
 
  <tr>
      <td>3</td>
      <td>4</td>
  </tr>
 
  <tr>
      <td>a</td>
      <td>b</td>
  </tr>
 
</table>
```

设置单元格中的背景颜色



##css的语法

```css
select {property: value}
//即 选择器{属性:值}
```

## 选择器

选择器主要有3种: 元素选择器,id选择器,类选择器

id选择器:

```css
<style>
p{
  color:red; //设置p为红色
}
#p1{
  color:blue;  //设置p1为蓝色
}
#p2{
  color:green;  //设置p2为绿色
}
</style>

<p>没有id的p</p>
<p id="p1">id=p1的p</p>
<p id="p2">id=p2的p</p>
```

类选择器:选择多个进行更改

```css
<style>
.pre{
  color:blue;
}
.after{
  color:green;
}
</style>

<p class="pre">前3个</p>
<p class="pre">前3个</p>
<p class="pre">前3个</p>

<p class="after">后3个</p>
<p class="after">后3个</p>
<p class="after">后3个</p>
```

## 文本

```css
<style type="text/css">
h1 {text-decoration: overline}
h2 {text-decoration: line-through}
h3 {text-decoration: underline}
h4 {text-decoration:blink}
.a {text-decoration: none}
</style>

<h1>上划线</h1>
<h2>删除效果</h2>
<h3>下划线</h3>
<h4>闪烁效果，大部分浏览器已经取消该效果</h4>
<a href="https://how2j.cn/">默认的超链</a>
<a class="a" href="https://how2j.cn/">去掉了下划线的超链</a>

```

## css优先级

```css
<link rel="stylesheet" type="text/css" href="https://how2j.cn/study/style.css" />
//在html文件中使用css文件

<style>
.p1{
  color:green;
}
</style>

<p class="p1">p1 颜色是绿色，优先使用靠的最后出现的</p>
```

style中增加 !important表示最高优先级 > 属性中优先级 > style中优先级 > css文件中优先级



