# DOM

DOM是Document Object Model(文档对象模型)的缩写

DOM是吧html里面的各种数据当作对象进行操作的一种思路



## 示例

DOM把所有的html都转换为节点

* 整个文档,元素,属性,内容,注释都是节点



```html
<html>
<body>
<div id="d1">hello HTML DOM</div>
  
</body>
  
<script>
function p(s){
    document.write(s);
    document.write("<br>");
}
var  div1 = document.getElementById("d1");
p("文档节点"+document);   //获取d1对应的文档节点
p("元素"+div1);		//获取d1的元素节点
p("属性节点"+div1.attributes[0]);		//获取d1的属性节点
p("内容节点"+div1.childNodes[0]);		//获取d1的内容节点
</script>
  
</html>
```



## 获取节点

设计html的时候,html中的每个节点的id应该是对应且唯一的

故,可以通过对应的id来获取对应的元素节点(或数组)

| document.getElementById | 通过id获取元素节点             |
| ----------------------- | ------------------------------ |
| getElementsByTagName    | 通过标签名称获取元素节点       |
| getElementsByClassName  | 通过类名获取元素节点           |
| getElementsByName       | 通过表单元素的name获取元素节点 |
| null                    | 为什么会获取不到?              |
| attributes              | 获取属性节点                   |
| childNodes              | 获取内容节点                   |



* NULL:因为javascript是解释语言,是顺序执行的,所以当一个元素还没有被加载的时候,无法获取这个元素



## 节点名称

nodename表示一个节点的名字

document.nodeName文档的节点名,是固定的 #document

div1.attributes[0].nodeName元素的节点名,是 对应的标签名 div

div1.childNodes[0].nodeName 内容的节点名,是固定的#text



```html
<html>
  
<div id="d1">hello HTML DOM</div>
<script>
function p(s){
    document.write(s);
    document.write("<br>");
}
var  div1 = document.getElementById("d1");
p("document的节点名称:"+document.nodeName);
p("div元素节点的节点名称:"+div1.nodeName);
p("div下属性节点的节点名称:"+div1.attributes[0].nodeName);
p("div下内容节点的节点名称:"+div1.childNodes[0].nodeName);
</script>
</html>
```



## 修改元素的文本内容(两种方式)

```html
<html>
    
<div id="d1">hello HTML DOM</div>
<script>
 
function changeDiv1(){
  document.getElementById("d1").childNodes[0].nodeValue= "通过childNode[0].value改变内容";
}
function changeDiv2(){
  document.getElementById("d1").innerHTML= "通过innerHTML改变内容";
}
</script>
 
<button onclick="changeDiv1()">通过内容节点方式改变div的内容</button>
<button onclick="changeDiv2()">通过innerHTML改变div的内容</button>
 
</html>
```



## DOM样式

可以通过改变style的内容来改变样式

1. `style.display`   "none"表示隐藏  "block"表示显示
2. `style.background` 表示颜色



## DOM事件

| 关键字                                       | 简介           |
| :------------------------------------------- | :------------- |
| onfocus onblur                               | 焦点事件       |
| onmousedown onmouseup onmousemove onmouseout | 鼠标事件       |
| onkeydown onkeypress onkeyup                 | 键盘事件       |
| onclick ondblclick                           | 点击事件       |
| onchange                                     | 变化事件       |
| onsubmit                                     | 提交事件       |
| onload                                       | 加载事件       |
| this                                         | 当前组件       |
| return false                                 | 阻止事件的发生 |



举例说明

### 焦点事件 (关键词 onfocus和onblur)

```html
<input type="text" onfocus="f()" onblur="b()" id="input1" placeHolder="输入框1" >
<br>
<br>
<input type="text" id="input2" placeHolder="输入框2">
<br>
<br>
<div id="message"></div>
 
<script>
function f(){
 document.getElementById("message").innerHTML="输入框1获取了焦点";
}
 
function b(){
 document.getElementById("message").innerHTML="输入框1丢失了焦点";
}
 
</script>
```



## 节点关系

* 父节点关系

![节点关系图](./img/1186.png)

```html
<div id="parentDiv">
 <div id="d1">第一个div</div>
 <div id="d2">第二个div</div>
 <div id="d3">第三个div</div>
</div>
```

其中DIV[id=parentDiv] -> body->html->document

document是根节点



* 同胞节点

```html
<script>
 
function showPre(){
    var d2 = document.getElementById("d2");
    alert(d2.previousSibling.innerHTML);
}
 
function showNext(){
    var d2 = document.getElementById("d2");
    alert(d2.nextSibling.nodeName);
}
</script>
  
<div id="parentDiv">
   父Div的内容
 <div id="d1">第一个div</div><div id="d2">第二个div</div>
<div id="d3">第三个div</div></div>
  
<button onclick="showPre()">获取d2的前一个同胞</button>
 
<button onclick="showNext()">获取d2的后一个同胞</button>
```

* 通过previousSibling获取前一个节点d1.
  **注意** d1和d2标签是**紧挨着**的，所以d2前一个节点是d1。
  通过nextSibling 获取后一个节点#text.
  **注意** d2和d3**不是紧挨着** 标签之间有任何**字符、空白、换行**都会产生文本元素。 所以获取到的节点是#text.



* 子节点关系





