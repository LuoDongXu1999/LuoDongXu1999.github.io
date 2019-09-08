# **JavaScript 简史**

 ## **1.1 JavaScript的简介**

- JavaScript 是脚本语言。
- JavaScript 是一种轻量级的编程语言。
- JavaScript 是可插入 HTML 页面的编程代码。
- JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。
- JavaScript 很容易学习。

## **1.2 DOM**

DOM是一套对文档内容进行抽象和概念化的方法。

因为JavaScript预先定义了“images”和“forms”等术语，我们才能像下面这样在JavaScript脚本里引用“文档中的第三个图像”或“文档中名为‘details’的表单”：
```
document.images[2]
document.froms['details']
```

通常把这种试验性质的初级DOM称为“第0级DOM”（DOM Level 0）。在还没未形成统一标准的初级阶段，“第0级DOM”的常见用途是翻转图片和验证表单数据。

## **1.3 浏览器之争**

### **1.3.1 DHTML**
 
DHTML是“Dynamic HTML”（动态HTML）的简称。DHTML并不是一项新技术，而是描述HTML、CSSHE和JavaScript技术组合的术语。DHTML的含义是：

- 利用HTML把网页标记为各种元素；
- 利用CSS设置元素样式和它们的显示位置；
- 利用JavaScript实时地操控页面和改变样式。

例如，用HTML标记一个页面元素：
```
<div id="myelement">This is my element</div>
```

然后用CSS为这个页面元素定义如下位置样式：
```
#myelement{
    postition: absolute;
    left: 50px;
    top: 100px;
}
```

接下来，利用JavaScript改变myelement元素的left和top样式，就可以随意移动，这是理论。

### **1.3.2 浏览器之间的冲突**

Netscape公司的DOM的专有元素是层（layer）。层有唯一的ID，需要这样引用：
```
document.layers['myelement']
```

微软公司的DOM中的这个元素是这样引用：
```
document.all['myelement']
```

假设你想找出myelement元素的left位置并赋值给变量xpos，在Netscape Navigator4浏览器这样做：
```
var xpos =  document.layers['myelement'].left;
```

在IE4浏览器得这样做：
```
var xpos = document.all['myelement'].leftpos;
```

所以人们对DHTML的评价变成了“宣称噱头”和“难以实现”。

## **1.4 指定标准**

Netscape、微软和其他浏览器制造商与W3C，在1998年10月完成了“第1级DOM”（DOM Level1）。

我们已经用<div>标签定义了一个ID为myelement的页面元素，现在需要找出它的left位置并把值保存到变量xpos中。以下是新标准化语法：
```
var xpos = document.getElementById('myelement').style.left
```

标准化DOM可以让任何一种程序设计语言对使用任何一种标记语言编写出来的任何一份文档进行操控。

DOM是一种API（应用编程接口）。

“DOM脚本程序设计”，表示使用W3C DOM来处理文档和样式表，涵盖了任何一种支持DOM API的程序设计语言去处理任何一种标记文档的情况。

# **JavaScript 语法**

## **2.1 准备工作**

JavaScript编写的代码必须通过HTML/XHTML文档才能执行。
第一种方式是将JavaScript代码放到文档<head>标签中的<script>标签之间：
```
<!DOCTYPE html>
<html lang = "en">
<head>
    <meta charset="utf-8"/>
    <title>Example</title>
    <script>
        JavaScript goes here...
    </script>
</head>
<body>
    Mark-up goes here...
</body>
</html>
```

一种更好的方式是把JavaScript代码存为一个扩展名为.js的独立文件。典型的作法是在文档的</head>部分放一个<script>标签，并把它的src属性指向该文件：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <title>Example</title>
    <script src="file.js"></script>
</head>
<body>
        Mark-up goes here...
</body>
</html>
```

最好的做法是把<script>标签放到HTML文档的最后，在</body>标签之前：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <title>Example</title>
</head>
<body>
    Mark-up goes here...
    <script src="file.js"></script>
</body>
</html>
```
这样能使浏览器更快地加载页面。

实践：创建名为test.html的文件并包含<script>标签，将标签的src属性设置为创建的第二个文件的名字，比如example.js。你的test.html文件应该包含以下内容：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <title>Example</title>
</head>
<body>
    <script src="example.js"></script>
</body>
</html>
```

程序设计语言分为解释型和编译型两大类。

Java或C++等语言需要编译器，把源代码翻译为直接在计算机上执行的文件。代码有错编译阶段就能发现。

解释型程序设计语言仅需要解释器，直接读入源代码并执行。代码有错解释器执行到相关代码才能发现。

## **2.2 语法**

### **2.2.1 语句**

放在不同行上：

```
first statement
second ststement
```

放在同一行上：

```
first statment; second statment;
```

建议分行并加上分号：

```
first statment;
second statment;
```

### **2.2.2 注释**

//单行注释

/*多
行
注
释 */

### **2.2.3 变量**

把值存入变量称为赋值：

```
mood = "happy";
age = 33;
```
把两个变量的值显示在一个弹出式警告窗口：

```
alert(mood);
alert(age);
```

声明变量：

```
var mood;
var age;
```

也可以一次声明多个变量：

```
var mood, age;
```

声明变量同时赋值：

```
var mood = "happy";
var age = 33;
```

还可以这样：

```
var mood = "happy", age = 33;
```

在JavaScript语言中，变量和其他语法元素的名字区分字母大小写。以下是对两个不同变量的赋值：

```
var mood = "happy";
MOOD = "sad";
```

不建议使用下划线，不可以空格。以下是首选格式：

```
var myMood = "happy";
```

“var”是关键字，myMood是变量名。

### **2.2.4 数据类型**

在JavaScript中不同的数据类型声明和赋值的语法完全相同，在其他语言中声明变量的同时还必须声明变量的数据类型，这称为类型声明。

必须明确类型声明的语言称为强类型语言，不需要类型声明的是弱类型语言。意味着程序员在可以在任何阶段改变变量的数据类型。

##### **1.字符串**

字符串有零个或多个字符构成。必须包在引号里，单双引号都可以。下面两条语句含义完全相同：

```
var mood = 'happy';
var mood = "happy";
```

如果字符串包含双引号，就把整个字符串放在单引号里；如果字符串包含单引号，反之：

```
var mood = "don't sak";
```

在JavaScript中用反斜扛对字符进行转义：

```
var mood = 'don\'t ask';
```

如果想用双引号包住本身就包含双引号的字符串，必须用反斜杠进行转义；

```
var height = "about 5'10\" tall";
```

可以将下段代码添加到之前创建的example.js文件中，然后重新加载。test.html文件：

```
var height = "about 5'10\" tall";
alert(height);
```

#### **2. 数值**

在JavaScript中允许带小数点的数值，并且允许任意位小数，称为浮点数：

```
var age = 33.25;
```

也可以用负数，在数值前加上一个减号即可：

```
var temperature = -20;
```

同样支持负浮点数：

```
var temperature = -20.33333333;
```

#### **3. 布尔值**

布尔数据只有两个可选值-----true或flase：

```
var sleeping = true;
var sleeping = false;
```

布尔值不是字符串，布尔值flase和字符串''flase"是两码事：

将变量married设置为布尔值true：

```
var married = true;
```

将变量married设置为字符串"true"：

```
var married = "true";
```

### **2.2.5 数组**

数组是指用一个变量表示一个值的集合，集合中的每个值都是这个数组的一个元素。

在JavaScript中，数组用关键字Array声明。还可以指定数组初始元素个数，也是数组的长度：

```
var beatles = Array();
```
填充数组时，需要给出新元素的值，还要给出新元素在数组中存放的位置，就是下标。下标用[]括起来：

```
array[index] = eleement;
```

下面是声明和填充beatles数组的过程：

```
var beatles = Arraay(4);
beatles[0] = "John";
beatles[1] = "Paul";
beatles[2] = "George";
beatles[3] = "Ringo";
```

数组下标从0开始

也可以这样：

```
var beatles = Array("John", "Paul", "George", "Ringo");
```

还可以这样：

```
var beatles = ["John", "Paul", "George", "Ringo"];
```

数组元素不必非得是字符串：

```
var years = [1900, 1901, 1902, 1903];
```

甚至可以放不同的数据类型：

```
var lennon = ["John", 1900, false];
```

数组元素还可以是变量：

```
var name = "John";
beatles[0] = name;
```

数组元素还可以是另一个数组的元素：

```
var lennon = ["Ringo",  "John",  "George", "Paul"];
beatles[1] = names[3];
```

数组还可以包含其他的数组：

```
var lennon = ["John", 1940, false];
var beatles = [];
beatles[0] = lennon;
```

#### 关联数组

在填充数组时为每个新元素明确地给出下标来改变这种默认的行为，在为新元素给出下标时，不必局限于使用整数数字。可以用字符串：

```
var lennon = Array();
lennon["name"] = "John";
lennon["years"] = 1940;
lennon["living"] = false;
```

### **2.2.6 对象**

对象是使用一个名字表示一组值。对象的每个值都是对象的一个属性。

例如：

```
var lennon = Object();
lennon.name = "John";
lennon.year = 1940;
lennon.living = false;
```

创建对象使用Object关键字，使用点号获取属性。

还有一种更简洁的语法，花括号语法：

```
{propertyName:value, propertyName:value};
```

lennon对象也可以写成下面这样：

```
var lennon = {name:"John", year:1940, living:false};
```

创建一个新的beatles数组，并用刚才创建的lennon对象来填充它的第一个元素：

```
var beatles = Array();
beatles[0] = lennon;
```

作为下标去访问数组里的元素：

```
var beatles = {};
beatles.vocalist = lennon;
```

## **2.3 操作**

#### **算术操作符**

- 赋值操作符是(=);
- 加法操作符是(+);
- 减法操作符是(-);
- 除法操作符是(/);
- 乘法操作符是(*);

## **2.4 条件语句**

if语句的基本语法：

```
if(condition){
    statements;
}
```

### **2.4.1 比较运算符**

- 大于操作符(>)
- 小于操作符(<)
- 大于或等于操作符(>=)
- 小于或等于操作符(<=)
- 比较操作符(==)

### **2.4.2 逻辑运算符**

- “逻辑与”操作符(&&)
- “逻辑或”操作符(||)
- “逻辑非”操作符(!)

## **2.5 循环语句**

### **2.5.1 while循环**

给定的值是true就会一直循环下去

```
while(condition){
    statements;
}
```

包含在循环语句内部的代码至少执行一次，就得使用do循环：

```
do{
    statements;
}while(condition);
```

### **2.5.2 for循环**

上一节while循环的例子：

```
initialize;
while(condition){
    statements;
    increment;
}
```

for循环的语法格式：

```
for(initial condition; test condition; alter condition){
    statements;
}
```

## **2.6 函数**

函数就是一组允许在代码里随时调用的语句，多次使用同一段代码，可以进行封装成函数。

一个例子：

```
function shout(){
    var beatles = Array("John", "Paul", "George", "Ringo");
    for(var count = 0; count < beatles.length; count++){
    alert(beatles[count]);
}
}
```

可以随时使用如下的语句来调用函数：

```
shout();
```

定义一个函数的语法：

```
function name(argument){
    statements;
}

#### **变量的作用域**

- 全局变量可以在脚本中的任何位置引用
- 局部变量只存在于声明它的函数的内部

## **2.7 对象**

对象是包含的数据集合，包含在对象里的数据可以通过两种形式访问----属性和方法：

- 属性是隶属于某个特定对象的变量。
- 方法是由属性和方法组合在一起构成的数据尸体。

在JavaScript里，属性和方法使用“点”语法访问：

```
Object.prpoerty
Object.method()
```
为给定对象创建一个新实例需要使用new关键字：

```
var jeremy = new person;
```






