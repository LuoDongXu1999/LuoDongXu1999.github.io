# **DOM**

## **3.1 文档：DOM中的“D”**

把你编写的网页文档转换成一个文档对象。

## **3.2 对象：DOM中的“O”**

与某个对象相关联的变量称为这个对象的属性；通过某个特定对象去调用的函数称为这个对象的方法。

JavaScript语言中的对象分三种：

- 用户定义对象：由程序员自行创建的对象
- 内建对象： 内建在JavaScript语言的对象，如Array、Math和Date等
- 宿主对象：由浏览器提供的对象

## **3.3 模型：DOM中的“M”**

DOM把一份文档表示为一棵家谱树，也就是一个模型。

家谱树模型很适合用来表示一份用（X）HTML语言编写出来的文档。

如下实例：

```
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title>Shopping list</title>
    </head>
    <body>
        <h1>What to buy</h1>
        <p title="a gentle reminder">Don't forget to buy this stuff.</p>
        <ul id="purchases">
            <li>A tin of beans</li>
            <li class="sale">Cheese</li>
            <li class="sale important">Milk</li>
        </ul>
    </body>
</html>
```

与“家谱树”相比，把文档称为“节点树”更准确。

## **3.4 节点**

表示网络中的一个连接点。一个网络是由一些节点构成的集合。其中的三种：元素节点、文本节点、属性节点。

### **3.4.1 元素节点**

DOM的原子是元素节点。

标签的名字就是元素的名字。文本段落元素的名字是“p”,无序清单元素的名字是“ul”，列表项元素的名字是“li”。所有的列表项元素都包含在一个无序清单元素内部。<html>元素是节点树的根元素，唯一的没有被包含在其他元素。

### **3.4.2 文本节点**

如果一份文档完全由一些空白元素构成，它将有一个结构，但这份文档本身不会包含什么内容。

<p>元素包含着文本“Don't forget to buy this stuff”。这是一个文本节点。

在XHTML文档中，文本节点总是被包含在元素节点内。但不是所有元素节点都包含文本节点。例如，<ul>元素没有直接包含任何文本节点，它包含着其他元素节点（<ul>元素），后者包含文本节点。

### **3.4.3 属性节点**

属性节点用来对元素作出更具体的描述。几乎所有元素都有一个title属性。

在DOM中，title="a gentle remider"是一个属性节点，属性总是被放在起始标签里，所以属性节点总是被包含在元素节点中。不是所有元素都包含属性，但是属性都被元素包含着。

例如，无序清单元素（<ul>）有id属性，有些清单元素（<li>）有class属性。

### **3.4.4 CSS**

DOM并不是与网页结构打交道的唯一技术。还可以通过CSS（层叠样式表）告诉浏览器如何让显示一份文档。

CSS声明元素样式的语法与JavaScript函数的定义语法相似：

```
selector{
    property: value;
}
```

样式声明中，还可以定义浏览器显示元素使用的颜色、字体和字号。

```
p{
    color: yellow;
    font-family: "arial", sans-serif;
    font-size: 1.2em;
}
```

继承是CSS技术中的强大功能。节点树的各个元素将继承父类的样式属性。

假如，为body元素定义了一些颜色或字体，包含在body元素里的所有元素都将自动获得样式：

```
body{
    color: white;
    backround-color: black;
}
```

#### **1. class属性**

可以在所有元素上任意应用class属性：

```
<p class="special">This paragraph has the special class</p>
<h2 class="special">So does this headline</h2>
```

在样式表里，可以为class属性值相同的所有元素定义同一种样式：

```
.special{
    font-style: italic;
}
```

还可以为class属性为一种特定类型d的元素定义一种特定的样式：

```
h2.special{
    text-transform: uppercase;
}
```

#### **2. id属性**

id属性的用途是给网页里的某个元素加上一个独一的标识符，如下：

```
<ul id="purchases">
```

在样式表里，可以为特定id属性值的元素定义一种独享的样式：

```
#purchases{
    border: 1px solid white;
    background-color: #333;
    color: #ccc;
    padding: 1em;
}
```

尽管id本身只能使用一次，样式表还可以利用id属性为包含在该特定元素里的其他元素定义样式：

```
#purchases li{
    font-weight: bold;
}
```

id属性就像挂钩，一头连着文档的某个元素，另一头连着CSS样式表里的某个样式。

### **3.4.5 获取元素**

有3中DOM方法可获取元素节点，分别是通过元素ID、通过标签名字和通过类名字来获取。

#### **1. getElementById**

这个方法将返回一个与那个有着给定id属性值的元素节点对应的对象。

它是document对象特有的函数。在脚本代码里，函数名的后面必须跟有一对圆括号，里面包含着函数的参数。想获得元素的id属性的值，必须放在单双引号中。

```
document.getElementById(id)
```

下面是一个例子：

```
document.getElementById("purchases")
```

这个调用将返回一个对象，对应着document对象独一的元素，元素的HTML id属性值是purchases。可以使用typeof操作符验证，会告诉我们操作数是什么。

将下面这段代码嵌入文档，方便测试，放在</body>结束标签之前：

```
<script>
    alert(typeof document.getElementById("purchases"));
</script>
```

会告诉你是一个对象，文档的每个元素都是对象，不用都定义独一的id  值。

#### **2. getElementsByTagName**

这个方法返回一个对象数组，每个对象分别对应着文档里有着给定标签的一个元素。也只有一个参数的函数，就是标签名：

```
element.getElementsByTagName(tag)
```
下面是一个例子：

```
document.getElementsByTagName("li")
```

这个调用返回一个对象数组，每个对象分别对应着coeument对象中的一个列表项元素。可以利用length属性查出数组的元素个数。

getElementsByTagName允许把一个通配符作为参数（星号字符“*”）必须放在引号里，可以查看文档中有多少个元素节点：

```
alert(document.getElementsByTagName("*").length);
```

如果想知道id属性是purhase的元素包含这多少个列表项，可以结合起来：

```
var shopping = document.getElementById("purchases");
var items = shopping.getElementsByTagName("*");
```
items数组长度刚好等于文档列表项元素的总数：

```
alert(items.length);
```

#### **3. getElementsByClassName**

这个方法可以通过class属性中的类名来访问元素。也只接受一个参数，就是类名：

```
getElementsByClassName(class)
```

返回的是一个具有相同类名的元素的数组。

下面实例：

```
document.getElementsByClassName("sale")
```

如果向知道id为"purchases"的元素中有多少类包含"sale"列表项，可以先找到特定的对象，再调用getElementsByClassName：

```
document.getElementById("purchases");
var sales = shopping.getElementsByClassName("sale");
```

sales数组中包含两项：

```
alert(sales.length);
```

### **3.4.6 盘点知识点**

- 一份文档就是一颗节点树。
- 节点分为不同的类型：元素、文本和属性节点。
- getElementById 将放回一个对象，该对象对应着文档里的一个特定的元素节点。
- getElementsByTagName 和 getElementsByClassName 将返回一个对象数组，分别对应着文档里的一组特定的元素节点。
- 每个节点都是一个对象。

## **获取和设置属性**

获取特定元素的方法：
getElementByIdget，ElementsByTagName 和 getElementsByClassName。

获取特定元素的属性：getAttribute
设置特定元素的属性：setAttribute

### **3.5.1 getAttribute**

getAttribute是一个函数。只有一个参数--打算查询的属性的名字：

```
object.getAttribute(attribute)
```

只能通过元素节点对象调用。例如，可以和 getElementsByTagName 方法合用，获取每个<p>元素的title属性：

```
var pars = document.getElementsByTagName("p");
for (var i=0; i< paras.length; i++) {
    var title_text = paras[i].getAttriBute("title");
    if (title_text != null) {
        alert(title_text);
    }
}
```

### **3.5.2 setAttribute**

这个方法允许对属性节点的值做出修改，与getAttribute一样，仅限于元素节点：

```
object.setAttribute(attribute,value);
```

下面例子，第一条语句得到id是purchase的元素，第二条语句把 这个元素的titile属性值设置为a list of goods;

```
var shopping = document.getElementById("purchases");
shopping.setAttribute("title", "a list of goods");
```
