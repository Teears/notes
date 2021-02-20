# 目录
* [HTML中的JavaScript](#HTML中的JavaScript)  
* [基本概念](#基本概念)  
    * 数据类型  
    * 操作符  
    * 语句  
    * 函数  
* [变量和作用域及内存](#变量和作用域及内存)  
* [引用类型](#引用类型)  
    * [Object](#Object类型)  
    * Array  
    * Date  
    * RegExp  
    * [Function](#Function类型)  
    * 基本包装类型（Boolean、Number、String）
    * 单体内置对象（Global、Math）
* [面向对象](#面向对象的程序设计)  
    * 创建对象  
    * 继承
* [函数表达式](#函数表达式)  
    * 闭包  
------------
------------
# HTML中的JavaScript  
HTML中常用的<script>属性 **scr**、**type**、defer（延迟脚本）、async（异步脚本）；一般情况，只要不出现defer和async浏览器会按<script>出现的顺序依次解析；<script>元素可以放在```<head>```中也可以放在```<body>```中。  
  :point_right: 使用<script>嵌入JS代码的两种方法:  
  * 内嵌:只需为<script>指定type属性
  ```javascript
  <script type="text/javascript">
    function sayHi(){
      alert("Hi,<\/script>");
    }
  </script>
  ```  
  * 外部包含:指定src属性
  ```javascript
    <script type="text/javascript" src="example.js"></script>//<script></script>之间不能包含额外的JavaScrript代码
  ```
     
------------  
# 基本概念  
:point_right:***数据类型***：JavaScript遵循ECMAScript规范。ECMAScript的变量是松散的，可以用来保存任何类型的数据。ECMAScript包含5种基本数据类型 **Undefined**、 **Null**、**Boolean**、**Number**、**String**和一种复杂数据类型**Object**，typeof操作符可以确定值是哪一个基本类型。:heavy_exclamation_mark:还有几个重要的方法valueOf()返回指定对象的原始值、toString()转换为字符串、toLocalString()数组转换为字符串。 
```javascript
var message="some string";
alert(typeof(massage));//"string"
```
|类型|值|意义|转型（函数或方法）|  
|:---:|:---:|:---:|:---:|
|Undefined|undefined|使用var声明但未初始化时这个变量就是undefined|-----|  
|Null|null|空对象|-----|  
|Boolean|true/false|布尔类型|Boolean()|  
|Number|整数（55、0xA）、浮点数（0.1/3.12e7）、NaN（非数值）、infinity（无穷大）|-----|Number()（可用于任何数据类型）、parseInt()、parseFloat()（专用于将字符串转为数值）|
|String|字符串（"）、（'）都可以|-----|.toString()|  
|Object|```var o=new Object();```|-----|-----|  

***操作符***：相比C，增加了全等和不全等符号```("55"===55)//false```、```("55"!==55)//true```、```("55"==55)//true```  
***语句***：相比C（for、do-while、while、if、break、continue、switch、case），增加了**for-in**（一种迭代语句，可用来枚举对象属性）、label（在代码中添加标签）、with（不推荐使用）  
**for-in**  
```javascript
for(var propName in window){
  document.write(propName);//输出无序
}
```
:point_down:**switch-case**  
与其他语言不同的是，JavaScript中的switch语句中可以使用任何数据类型，无论是字符串还是对象，其次，每个case的值也不一定是常量，可以是变量甚至表达式。:heavy_exclamation_mark:switch语句在比较值时使用的是全等操作符。

***函数***：ECMAScript中的函数在定义时不必指定是否返回值，任何函数在任何时候都可以通过return实现返回值。eg:
```javascript
function sayHi(){
  alert("Hello "+"friend");
}
```  
:heavy_exclamation_mark:ECMAScript不规定传入多少个参数以及传入参数的数据类型，ES中的参数在内部是用一个数组表示的，我们可以通过arguments对象对其进行访问（arguments[]可以像数组一样获取传入参数值，arguments.length可以获取传入参数的个数）。eg:  
```javascript
  function doAdd(){
    if(arguments.length==1){
      alert(arguments[0]+10);
    }
    else if(arguments.length==2){
      alert(arguments[0]+arguments[1]);
    }  
  }
  doAdd(10);//20
  doAdd(10,20)//30
```  
arguemts对象可以和命名参数一起使用。需要注意的是①arguments的值永远和与之对应的命名参数的值相同，但这并不意味着他们拥有相同的储存空间。②没有传递值的命名参数或者arguments对象将自动被赋值为undefined。③ES中的所有参数传递都是值传递，不可能通过引用传递.  
***没有重载***：通过检查输入参数的个数和类型可以模仿重载。如果定义了两个同名函数，名字只属于后定义的函数。  

------------
# 变量和作用域及内存  
:point_right:***变量***：[基本类型](#基本概念)值是按值传递的，可以操作保存在变量中的实际值；引用类型的值是按引用访问的，实际上操作的是对象的引用而不是实际的对象。对引用类型我们可以为其添加属性和方法，也可以改变属性和方法，如果对象不被删除或属性不被销毁，这个属性将一直存在。一个变量向另一个变量复制引用类型值，实际上是两个变量引用同一对象。eg:  
```javascript
var person=new Object;//创建对象并保存在person中
person.age=18;//为对象添加属性
var myfriend=person;
alert(myfriend.age);//18
```
函数的引用类型参数传递也是同样机制，eg:  
```javascript
function setAge(obj){//person传入后，obj和person是同一对象的引用，不要错误的认为person是新建对象的引用，而obj是person的引用
   obj.age=18;
}
var person=new Object();
setAge(person);
alert(person.age);//18
```
:heavy_exclamation_mark:先前我们介绍了[typeof操作符](#基本概念)```alert(typeof(person));//如果person是对象返回Object```，现在有另外一个instanceof操作符```alert(person instanceof Object);```如果变量person是对象就返回true  ；```alert(person instanceofo Array);```如果变量是Array就返回true。
***作用域***：最内层环境可以依次向外层访问，以下例子能很好的帮助理解  
```javascript
var color="blue";
function changeColor(){
   var anotherColor="red";
   function swapColoor(){
      var tempColor=anotherColor;
      anotherColor=color;
      color=tempColor;
      //这里可以访问tempColor、anotherColor、color
   }
   swapColor();//这里考可以访问anotherColor、color
}
changeColor();//这里可以访问color
alert(color);//red
```  
:heavy_exclamation_mark:JavaScript**没有块级作用域**,其他类C语言中，由花括号封闭的代码都有自己的作用域，比如  
```JavaScript
if(true){
   var color="red";
}
alert(color);//red
```
在C、C++或Java中if执行完毕后color会被销毁。但在JavaScript中，if中声明的变量会被添加到与if同级的执行环境中，在使用for语句中应尤其注意。:heavy_exclamation_mark:使用var声明的变量会被直接添加到最近的环境中，在函数内部声明，最接近的是函数的局部环境，在with中，最接近的是函数环境。如果初始化变量时没有用var声明，则添加到全局环境（但不建议这样做）。另外JavaScript具有垃圾回收机制，开发人员一般不必操心内存管理问题，但必要的解除引用操作（置null）还是要有的。

-------------
# 引用类型  
ECMAScript不支持传统的类和类接口结构，引用类型和类相似但并不是类。:heavy_exclamation_mark:```var person=new Object();```这段代码创建了Object引用类型的新实例，使用的构造函数是Object。
## Object类型  
:heavy_exclamation_mark:创建Object实例的两种方式①new②对象字面量表示法,字面量表示法很适合需要向函数传递大量可选参数的情形（传入一个实例可以带多个属性）  
```JavaScript
var person=new Object();
person.name="Tom";
person.age=5;
```
```JavaScript
var person={
   name:"Tom",//属性名也可使用字符串"name":"Tom"
   age:5
}
```
```javascript
var person={};
person.age=5;
```
对象属性的访问有两种：
```javascript
alert(person.name);
alert(person["name"]);//方括号可以通过变量来访问属性，属性名含有非法表达时也可以用方括号访问
```
## Array类型  
创建数组的方法举例：  
```JavaScript
var colors=new Array();//new可以省略
var colors=Array(3);//创建length值为3，注意length属性是可以由用户自由设置的
var colors=("red","green","blue");
//字面量表示法
var colors=["red","green","blue"];
var colors=[];//创建空数组
var values=[1,2,];//不正确
//var options=[,,,,,];不正确
colors[colors.length]="black";//可以通过length属性方便的在数组末尾添加值
```
|名称|方法|举例|  
|:---:|:---:|:---:|  
|检测数组|Array.isArray()|```alert(Array.isArray(value));//确定某个值是不是数组```|  
|转换方法|toString()、valueOf()、toLocaleString()、join()|```colors.toString();//返回逗号拼接成的字符串,实际上是调用了数组每一项的toString方法```  ```colors.valueOf();//返回数组本身```  ```colors.join("~");//返回波浪号分隔的字符串，如果不传参数默认逗号分隔```|  
|栈方法|push()、pop()|```var Len=colors.push("red");//入栈并返回数组长度``` ```var item=colors.pop();//出栈并返回出栈的值```|  
|队列方法|push()、shift()、unshift()|```var item=shift();//出队列并返回数组第一项``` ```var Len=colors.unshift("black","red");//在数组前段添加两项并返回额新数组长度```|  
|重排序|reverse()、sort()|```var values=[5,10,15];alert(values.reverse());//15,10,5反转``` ```values.sort();//10,15,5转为字符串进行排序,sort()方法一般需要传入比较函数``` ```function compare(v1,v2){return v1-v2} values.sort(compare);//5,10,15```|  
|操作方法|contact()、slice()、splice()|```var colors1=colors.conatct("yellow",["black","brown"]);``` ```var color2=colors.slice(1,4);//截取colors[1]到colors[3]``` ```var colors=["red","green","blue"]; var removed=colors.splice(1,1,"black","purple");//"red","black","purple","blue"表示从第color[1]开始删除1项再从colors[1]开始插入两项,splice()至少传入两个参数，返回值是被删除的值```|  
|位置方法|indexOf()从前往后查找、lastIndexOf()从后往前查找|两种方法都返回要查找的项的下标，没找到返回-1|  
|迭代方法|every()、some()、filter()返回调用函数返回true的项组成的数组、forEach()没有返回值、map()返回每次函数调用结果组成的数组|每个方法可以接收两个参数：**要在每一项运行的函数**，（可选）运行该函数的作用域对象。传入的函数会接收三个参数（数组项的值item、该项在数组中的位置index、数组对象本身array）|  
|归并方法|reduce()、reduceRight()|分别是从前往后和从后往前遍历，可以传入两个参数：要在每一项运行的函数，（可选）归并的初始值，传入的函数有四个参数（前一个值prev，当前值cur，项的索引index，数组对象array）|  

下面补充迭代方法和归并方法的举例：  
```javascript
var numbers=[1,2,3,4,5,4,3,2,1];
var everyResult=numbers.every(
   function(item,index,array){
      return (item>2);  
   }
);//传入要在每一项上运行的函数作为参数
alert(everyResult);//false
```
```javascript
var values=[1,2,3,4,5];
var sum=values.reduce(
   function(prev,cur,index,array){
      return prev+cur;
   }
);
alert(sum);//归并实现了数组求和
```
## date类型  
```javascript
var now=new Date();//默认获取当前时间
var someDate=new Date(Date.parse("May 25,2004"));//使用parse方法返回1970年1月1日到2004年5月25日的毫秒数
var allFives=new Date(Date.UTC)(2005,4,5,17,55,55));//返回2005年5月5日下午5:55:55的毫秒数，前两项是必须的，如果省略其他参数则自动设置为0
var someDate=new Date("May 25,2004");
var allFives=new Date(2005,4,5,17,55,55);//这样也是正确的，，只不过是基于本地时区创建的
var start=Date.now();//可以方便的获取调用这个方法时的毫秒数
```
Date类型包含众多方法，有类型转换方法，toLocakeString()以与浏览器设置地区相适应的格式返回日期和时间；toString()返回带时区信息的时间，valueOf()返回毫秒数。此外还有日期格式化方法，toUTCString()实现格式完整的UTC日期，等。但这些字符串格式的输出都因浏览器而异。**P102**列有Date类型方法表。  
## RegExp类型
```var expression=/pattern/flags```  
**flags**:g（全局模式）、i（不区分大小写）、m（多行模式）。在模式中使用元字符{}\[\]()\\^.$|?\*+需要转义 ,构造函数的模式下需要双重转义。正则表达式字面量始终会共享同一个RegExp实例，但使用构造函数创建的每一个新RegExp实例都是一个新实例。  
**RegExp实例属性**：global（是否设置了g标志）、ignoreCase（是否设置了i标志）、multiline（是否设置了m标志）、lastIndex（表示开始搜索下一个匹配项的字符位置，从0算起）、source（字面量形式的模式）  
**RegExp实例方法**：①exec()专门为**捕获组设计**，返回包含第一个匹配项信息的数组,该数组有index和input两个实例②test()，用于判断某字符串是否与某个模式匹配返回布尔类型。③RegExp实例继承的toLocaleString()、toString()方法都返回正则表达式的字面量。  
**RegExp构造函数属性**：input、leftContext、rightContext、lastMatch、lastParen、$1、$2...
```javascript
var pattern1=/[bc]at/i;//字面量创建RegExp实例，匹配第一个"bat"或"cat",不区分大小写
var pattern2=new RegExp("[bc]at","i");//构造函数创建
alert(pattern1.global);//true

var text="cat,bat,sat,fat";
var pattern2=/.at/g;
var matches=pattern2.exec(text);
alert(matches.index);      //0
alert(matches.input);      //cat,bat,sat,fat
alert(matches[0]);         //cat
alert(pattern2.lastIndex); //3

var text="this has been a short summer";
var pattern=/(..)or(.)/g;//创建了一个包含两个捕获组的模式
if(pattern.test(text)){
   alert(RegExp.$1);    //sh
   alert(RegExp.$2);    //t
}
```  
## Function类型  
每个函数都是Function类型的实例，因此函数名实际上是一个指向函数对象的指针，不会与某个函数绑定，因此函数也没有重载（这是我们在前面提到过的）。  
**函数声明和函数表达式**：  
```javascript 
var sum = function sum(num);//声明
```
```javascript
function sum(num){
   return num+1;
}//表达式
```
在代码执行之前，解析器能读取并将函数声明添加到执行环境中，JavaScript引擎能把函数声明自动提升到顶部。但是函数声明和函数表达式混用却会导致错误：
```javascript
alert(sum(10));
var sum=function sum(num){
   return num+1;
};//错误示例
```
:heavy_exclamation_mark:**函数名本身是指针，因此可以作为值来使用**：那么一个函数可以作为另一个函数的参数及返回值（这是个很有用的技术）。  
**函数内部属性**：函数内部有两个特殊的对象arguments和this。    
arguments对象:在前面介绍过，它是个类数组对象，包含了所有传入函数的参数。还有一个callee属性（在严格模式下需要采用命名函数表达式来达成），它是一个指针，指向拥有这个arguments对象的函数，它可以解决紧密耦合问题，以下是一个阶乘函数。:point_down:
```javascript
function factorial(num){
   if(num<=1){
      return 1;
   }else{
      return num*arguments.callee(num-1);//num*factorial(num)
   }
}
```
this对象:引用的是函数执行的对象对象（当在网页的全局作用域中调用函数时，this对象引用的就是window）。
```javascript
window.color="red";
var o={color:"blue"};//声明一个对象o并添加了一个color属性，将该属性初始化为"blue"
function sayColor(){
   alert(this.color);
}
sayColor();//"red"
o.sayColor=sayColor;
o.sayColor();//"blue"
```
caller函数对象的属性:这个属性中保存着调用当前函数的函数的引用，如是在全局作用域中调用当前函数，它的值为null。以下代码警告框内会显示outer()函数的源代码。
```javascript
   function outer(){
      inner();
   }
   function inner(){
      alert(inner.caller);//alert(arguments.callee.caller)
   }
   outer();//outer()调用了inner()，inner.caller又指向outer()
```
**既然函数是对象，就有属性和方法**：每个函数都包含两个属性length和prototype，两个非继承而来的方法apply()和call()。  
length属性：表示函数希望接收的命名参数的个数。
prototype属性：保存实例方法（[链接后面](#面向对象的程序设计)）。
apply()、call()方法：apply()和call()两个方法的用途都是在特定的作用域（由传入的第一个参数设置）中调用函数。apply()要传入两个参数this和参数数组。call()需要传入第一个参数也是this但是其余参数必须这个例举出来，而不能像apply()一样传数组。
```javascript
function sum(num1,mun2){
   return num1+num2;
}
function callSum1(num1,num2){
   return sum.apply(this,[num1,num2]);//return sum.apply(this,arguments)
}
function callSum2(num1,num2){
   return sum.call(this,num1,num2);
}
alert(callSum1(10,10));//20
alert(callsum2(10,20));//30
```
apply()和call()真正强大的地方在于能够扩充函数赖以运行的作用域，只需要将第一个参数设置为特定的作用域即可。
```javascript
window.color="red";
var o={color:"blue"};
function sayColor(){
   alert(this.color);
}
sayColor();//red直接调用，作用域是window
sayColor.call(this);//red,作用域设置为this,而this的值就是window
sayColor.call(window);//red,作用域设置为window
sayColor.call(o);//blue
```
bind方法：bind()方法也可以实现作用域扩充，this值被绑定到bind()的参数值。
```javascript
window.color="red";
var o={color:"blue"};
function sayColor(){
   alert(this.color);
}
var objectSayColor=sayColor.bind(o);
objectSayColor();//blue
```
## 基本包装类型  
基本包装类型（属于基本数据类型）：Boolean、Number、String。基本类型值不是对象，本不应该有方法和属性，但后台经过一系列处理使基本类型变得跟对象一样。引用类型和基本包装类型的不同之处在于，不能在运行时为基本包装类型添加值添加属性和方法。:heavy_exclamation_mark:对基本包装类型调用typeof会返回"object"。[Object](#Object类型)构造函数可作为基本包装类型的构造函数，会根据传入的类型返回相应基本包装类型的实例。
```javascript
var obj=new object("some text");
alert(obj instanceof String);//true
```
注意：使用new调用基本包装类型的构造函数，与使用同名转型函数是不一样的。
```javascript
var value = "25";
var number=Number(value);//转型函数
alert(typeof number);//"number"
var obj=new Number(value);//构造函数
alert(typeof obj);
```
Boolean类型：要创建Boolean类型，调用Boolean构造函数并传入true或false,```var booleanObject=new Boolean(true);```但不建议使用Boolean类型。  
Number类型：依然重写了valueOf()、toString()、toLocalString()方法。此外，还有①toFixed()返回指定小数位数的字符串，传入的参数表示小数位数。②toExponential()返回e表示法的字符串形式。③toPrecision()返回合适格式字符串，参数表示保留几位有效数字。  
String类型：String类型有很多方法，可以实现对字符串提取单个字符，拼接，截取，查找，删除前缀和后缀空格，大小写转换，模式匹配（本质和调用RegExp()方法相同），比较，将字符编码转换为字符串等多种功能，以及HTML方法（不建议使用）。:heavy_exclamation_mark:P123  
## 单体内置对象
前面已经介绍了大多数内置对象，如Object、Array和String。此外，还有两个单体内置对象Global和Math。
Globle对象：①URI编码方法encodeURI()和encodeURIComponent()可以对同一资源定位符进行编码，方便发送给浏览器。②eval()方法相当于一个完整的ECMAScript解析器，接收执行的代码字符串，eval()的执行最终会被替换为实际执行的代码。③我们将全局对象作为window对象的一部分。  
Math对象：①Math对象包含的属性大都是数学数学计算中可能会用到一些特殊值②min()和max()方法③舍入方法：Math.ceil()进一，Math.floor()舍去，Math.round()四舍五入④random()方法可以生成大于等于0小于1的随机数。因此产生随机数的公式是Math.floor(Math.random() \* 可能值的总数 + 第一个可能的值)⑤selectFrom(a,b)产生大于等于a小于等于b的随机数。⑥其他方法有求绝对值，对数，平方根，次幂等。  

----------
# 面向对象的程序设计
**数据属性**\[\[Configurable\]\]、\[\[Enumberable\]\]、\[\[Writable\]\]、\[\[Value\]\]。
```javascript
   var person={
      name:"Tom",
      age:29,
      sayName:function(){
         alert(this.name);
      }
   };
```
person对象的属性前三个默认为true,\[\[Value\]\]被设定为特定值。我们可以使用Object.defineProperty()方法来更改属性默认的特性。  
**访问器属性**\[\[Configurable\]\]、\[\[Enumberable\]\]、\[\[Get\]\]、\[\[Set\]\]，访问器属性也可以通过Object.defineProperty()方法来定义。  
我们可以通过Object.defineProperties()方法同时定义数据属性和访问器属性，Object.getOwnPropertyDescriptor()方法可以读取对象属性的特性。  
**用工厂模式创建对象**
```javascript
   function createPerson(name,age){
      var o=new Object();
      o.name=name;
      o.age=age;
      o.saName(){
         alert(this.name);
      };
      return o;
   }
   var person1=createPerson("Tom",10);
```
**构造函数模式创建对象**构造函数通过new操作符来调用时，体现出了它与与普通函数的不同。构造函数创建对象存在一些缺点。
```javascript
   function Person(name,age){
      this.name=name;
      this.age=age;
      this.sayName(){
         alert(this.name);
      };
   }
   var person1=new Person("Tom",10);
```
**原型模式创建对象**我们创建的每一个函数都有prototype（原型）属性。所有原型对象都会自动获取一个constructor属性，Person.prototype.constructor又指回Person。
```javascript
   function Person(){}
   Person.prototype.name="Tom";
   Person.prototype.age=10;
   Person.prototype.sayName=function(){
      alert(this.name);
   };
   var person1=new Person();
   alert(person1.name);//"Tom" 
   //为对象实例赋新值可以屏蔽原型但却不能改变原型,调用person1.name时，解析器会现在实例中搜索name属性，如果没搜到会继续搜索原型
```
当调用原型的构造函数创建一个新实例时，该实例内部包含一个指针，指向原型对象。我们可以用isPrototrpeOf()和Object.getPrototypeOf()进行测试。
原型与in操作符，通过对象能过访问给定属性时返回true，比如上面例子```alert("name" in person1);//true```。  
hasOwnPrototype()方法在属性存在于实例中时返回true```alert(person1.hasOwnPrototype("name"));//true```。  
hasPrototypeProperty()属性存在于原型中则返回true```alert(hasPrototypeProperty(person1,"name"));//true```  
获取对象上的所有实例属性可以用Object.keys()方法和Object.getOwnPropertyNames()方法```var keys=Object.keys(Person.Prototype);//keys值为"name,age,sayName"```  
字面量表示原型对象，只是这种表示会使constructor属性不再指向Person，而指向Object，当然我们可以在字面量将其设置回适当值。
```javascript
   function Person(){}
   Person.prototype={
      name:"Tom",
      age:10,
      sayName:function(){
         alert(this.name);
      }
   };
```
我们可以随时为原型添加属性和方法，并且修改可以立即在所有实例中反映出来，但是不能重写整个原型对象，这样会使所有实例依然引用最初的原型。很多的原生引用类型（Object、Array、String）都是采用原型模式创建的，因此我们可以对原生引用类型定义新的方法。原型中的属性被很多实例共享，大多数时候这样是很合适的，但是当原型中包含引用类型值的时候就会出现一些问题。P158  
:heavy_exclamation_mark:目前使用最广泛的是构造函数和原型的混合模式。此外还有，动态原型模式，它把所有信息封装在构造函数中，而在构造函数中初始化原型。寄生构造函数模式，是除了使用new以外其他都和工厂模式相同的一种创建方式。稳妥构造函数模式，稳妥构造函数遵循和寄生构造函数相同的模式，不同之处在于，新创建的实例方法不引用this，不使用new操作符。  
## 继承  
**原型链**是实现继承的主要方法，让原型对象等于另一类型的实例，就可以实现原型链。
```javascript
   function SuperType(){
      this.property=true;
   }
   SuperType.prototype.getSuperValue(){
      return this.property;
   };
   function SubType(){
      this.subproperty=false;
   }
   SubType.prototype=new SuperType();//SubType继承了SuperType
```
**借用构造函数实现继承**利用apply()和call()在子类型构造函数内部调用超类型构造函数,但是它无法避免构造函数模式存在的问题，因此很少单独使用。
```javascript
   function SubType(){
      SuperType.call(this);//继承了SuperType
   }
```
**组合继承**结合了原型链和借用构造函数，思路是使用原型链实现对原型属性和方法的继承，通过借用构造函数实现实例属性的继承。这是较为常用的一种继承模式。
```javascript
   function SuperType(name){
      this.name=name;
      tihs.colors=["red","blue"];
   }//通过借用构造函数
   SuperType.prototype.sayName=function(){
      alert(this.name);
   };//通过原型链继承
   function SubType(name,age){
      SuperType.call(this,name);//继承属性
      this.age=age;
   }
   SubType.prototype=new SuperType();//继承方法
   SubType.prototype.constructor=SubType;
   SubType.prototype.sayAge=function(){
      alert(this.age);
   }; 
```
**原型式继承**通过object()函数和Object.create()方法，在已有一个对象的情况下，创建一个类似的对象。object()接收已知对象，Object.create()接收两个参数，分别是已知对象和一个为新对象定义额外属性的对象（可选）。
**寄生式继承**与寄生构造函数和工厂模式类似
```javascript
   function createAnother(original){
      var clone=object(original);
      clone.sayHi=function(){
         alert("Hi");
         return clone;
      }
   }
```
**寄生组合式继承**通过借用构造函数来继承属性，通过原型链的混成模式来继承方法（inheritPrototype()方法接收两个参数：子类型构造函数和超类型构造函数）
```javascript
   function SuperType(name){
      this.name=name;
      tihs.colors=["red","blue"];
   }
   SuperType.prototype.sayName=function(){
      alert(this.name);
   };
   function SubType(name,age){
      SuperType.call(this,name);
      this.age=age;
   }
   inheritPrototype(SubType,SuperType);
   SubType.prototype.sayAge=function(){
      alert(this.age);
   }; 
```
# 函数表达式  
注意理解函数提升及函数声明和函数表达式的区别（链接[Function类型](#Function类型)）。  
## 闭包
闭包是指有权限访问另一个函数作用域中的变量的函数（通常是一个匿名函数），内层的闭包可以访问从全局到自己的所有变量对象，常见的创建闭包的方式是，在一个函数内部创建另一个函数。在JS中每当调用一个函数，就会创建一个包含局部活动对象的执行环境，当函数执行完毕后，该局部作用域和局部活动对象就会被销毁。但是如果这个函数还有一个内部函数（闭包），那么即使外部函数执行完毕，其活动对象也不会被销毁，直到内部函数也被销毁。关于闭包有几点注意：  
* 由于闭包保存的是整个变量对象，而不是某个特殊的变量，因此闭包只能取得包含函数中任何变量的最后一个值。要解决这个问题，我们可以给闭包传入外部变量作为参数。
* 
