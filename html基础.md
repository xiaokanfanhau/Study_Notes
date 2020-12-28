* input组件属性
	- autocomplete：自动完成默认on会有提示上次输入的内容。
	- autofocus：自动获取焦点
	- request：必须填写
* z-index
	- 位置static和relative设置无效
	- 默认为0，大于0则浮动
	- 小于0则为浮于下方0
* relative位置
	- 使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。
	- 因此，移动元素会导致它覆盖其它框。
* position：absolute位置
	- 父节点是body大标签
* BFC规则(待补充)
![](html基础_files/1.jpg)
![](html基础_files/3.jpg)
* box-sizing: border-box
	- 设置宽之后，padding，margin，border，都不会超出设置的宽高
* transition和animation的区别
	- transition 需要去触发比如：点击事件、鼠标移入事件；而 animation 可以配合 @keyframe 可以不触发事件就触发这个动画
	- transition 触发一次播放一次；而 animation 则是可以设置很多的属性，比如循环次数，动画结束的状态等等；
	- transition关注的是样式属性的变化，属性值和时间的关系是一个三次贝塞尔曲线；而animation作用于元素本身而不是样式属性，可以使用关键帧的概念，可以实现更自由的动画效果；
	- 在性能方面：浏览器有一个主线程和排版线程；主线程一般是对 js 运行的、页面布局、生成位图等等，然后把生成好的位图传递给排版线程，而排版线程会通过 GPU 将位图绘制到页面上，也会向主线程请求位图等等；我们在用使用 aniamtion 的时候这样就可以改变很多属性，像我们改变了 width、height、postion 等等这些改变文档流的属性的时候就会引起，页面的回流和重绘，对性能影响就比较大，但是我们用 transition 的时候一般会结合 tansfrom 来进行旋转和缩放等不会生成新的位图，当然也就不会引起页面的重排了。
	- transition: property duration timing-function delay;
	- ![](html基础_files/2.jpg)
	- transition: all 0 ease 0;
	- ![](html基础_files/4.jpg)
	- moz-transition: all 0 ease 0; /* Firefox 4 */
	- webkit-transition: all 0 ease 0; /* Safari 和 Chrome */
	- o-transition: all 0 ease 0; /* Opera */
	- animation:mymove 5s infinite;
	- webkit-animation:mymove 5s infinite; /* Safari 和 Chrome */
	- animation: name duration timing-function delay iteration-count direction;
	- ![](html基础_files/5.jpg)
	- animation-direction: normal|alternate;
	- ![](html基础_files/6.jpg)
* 响应式布局
	- 实现在不同分辨率的终端上浏览网页的不同展示方式
	- 和自适应的区别：响应式只需要开发一套代码，检测分辨率。
	- ![](html基础_files/8.jpg)
	- ![](html基础_files/9.jpg)
	- ![](html基础_files/10.jpg)
* 函数的书写方法，IIFE自动运行函数
* 对象的引用方法，中括号和普通调用obj.name的区别
	- obj.name和obj["name"]
	- obj[name]中括号里面可以写入变量
* str.indexof和str.search的区别
	- indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置，如果没有找到返回-1。
	- indexOf()对大小写敏感，indexOf(字符串,开始位置)
	- search()里面主要放的是正则表达式，相比于indexOf()更加占用资源
* 使用ajax如何获取json文件
	- 使用jQuery
 ```javascript
 $(document).ready(function(){
            $.ajax({
                type: "get",//请求类型
                datatype: "json",//数据类型
                url: "./demo.json",//向哪里请求
                success: function(data){//请求成功后执行该函数
                    console.log(data.person.name)//tom
                }
            })
        })
```

* 构造对象（工厂模式）和构造函数（创建一个类）的区别
	- 工厂模式：
```javascript
function createObj(name, age) {
      var obj = new Object();
      obj.name = name;
      obj.age = age;
      obj.sayHi = function () {
        console.log("你好");
      }
      return obj;
    }
var obj = createObj('小明','18')
```
	- 自定义模式:
```javascript
function Person(name, age) {
      this.name = name;
      this.age = age;
      this.sayHi = function () {
        console.log("你好");
      }
    }
var obj = new Person('xiaoming',18)
```
	- 1.都可以创建对象
	- 2.都有参数
	- 3.都是函数
	- 不同点：自定义函数首字母要大写
	- 调用时需要new
	- this指向当前对象

* typeof()和instanceof()的用法
	- typeof()返回运算数的类型
	- 返回number,string,booler,function,undefined,object
	- 对于array,null则返回OBJECT
	- 可用于判断变量是否存在，typeof(string) == defined
	- instanceof用于判断一个变量是否某个对象的实例
	- a instanceof Array //true 判断是否是数组
	- array包含在object中

* encodeURLComponent()和decodeURLComponent()用法

* console.log()和console.info(),console.dir()区别
	- log语句打印的是结果，直接显示信息
	- dir语句打印的是内容，对显示对象的所有属性和方法

* json和xml类型，都是一种结构化的数据表示方式，json语法支持三种类型的值：
	- 简单值：字符串，数值，布尔值，null
	- 对象：需要加上双引号，不存在赋值运算和分号
	- 数组
``` javascript
	初始：
	var str = {"name":"菜鸟教程", "site":"http://www.runoob.com"}
	
	过程：stringify(数组，保留数组/函数，缩进字符)
	str_pretty2 = JSON.stringify(str, function(key,value){
		switch(key){
			case 'name':
				return 'Mr.'+value;
			default:
				return value;
		}
		}, 4) //使用四个空格缩进
	document.write("<pre>" + str_pretty2 + "</pre>" ); // pre 用于格式化输出
	
	结果：
	{
	    "name": "Mr.菜鸟教程",
	    "site": "http://www.runoob.com"
	}
```
* DOM获取节点：获取到的都是节点数组
	- getElementByld(通过ID获取节点)
	- getElementsByTagName(通过标签名获取节点)
	- getElementsByName(通过标签的name值获取节点)
	- getElementsByClassName(通过class值来获取节点)
	- querySelect("选择器")(根据选择器返回找到结果集中的第一个)
	- querySelectAll('选择器')(通过选择器返回找到的结果集，是个节点数组)
* childNodes和children区别
```javascript
<body>
	<div>
		<botton>你好</botton>
	</div>
</body>
<script type="text/javascript">
	var div = document.getElementsByTagName("div")[];
	console.log(div.childNodes)//返回是子节点的集合button text button
	console.log(div.children)//返回的是元素节点的集合button
</script>
```
* 创建节点
	- document.createElement("标签名") //创建一个元素节点
	- document.createTextNode("文本内容")
* 插入节点
	- 父节点.appendChild(创建的节点)
	- 父节点.insertBefore(创建的节点,已知的子节点)
* 替换节点
	- 父节点.replaceChild(新节点,老节点)
* 克隆节点
	- 需要被复制的节点.cloneNode(true/false);
	- true:复制当前节点以及所有子节点
	- false:进复制当前节点
* 删除节点
	- 父节点.removeChild(子节点)
	- 实例:
```
<body>
	<div class='box'></div>
</body>
<script type="text/javascript">
	var box = document.getElementsByClassName("box")[0]
	var body = document.getElementsByTagName("body")[0]
	body.removeChild(box)
</script>
```
	
* 获取属性
	- data-自定义属性="" //自定义属性
	- 节点.getAttribute("属性名") //所有属性都可以获取
	- 节点.属性名 //只能获取已经包含的属性，不能获取自定义属性
* 设置属性
	- 节点.属性名 = 属性名;(方法一)
	- 节点.setAttribute("属性名",属性值);(方法二)
* 删除属性
	- 节点.属性名 = "";(属性名对应的属性值设为空)
	- 节点.removeAttribute("属性名");(删除属性)
* 获取文本
	- 节点.innerHTM //获取节点下的所有内容包含标签
	- 节点.innerText //获取节点下的文本内容,不包含标签
	- 节点.value //获取input输入框等表单控件的内容
	- 节点.getAttribute("value") //value是表单输入框的属性
* 设置文本
	- 节点.innerHTM = "文本内容" //会翻译html标签
	- 节点.innerText = "文本内容" //不会翻译html标签
	- 节点.value = 值
	- 节点.setAttribute("value",值) //因为value是属性
	- 会覆盖原先的值
* 删除文本
	- 节点.innerHTM = ""
	- 节点.innerText = ""
	- 节点.value = ""
	- 节点.removeAttribute("value")
	- 会覆盖原先的值
* 操作样式class获取和设置
	- 节点.className
	- 节点.getAttribute("class") //获取节点的所有class
	- 节点.className = 值
	- 节点.setAttribute("class",值)
	- HTML5提供了一个新的属性：classList来实现对元素样式表的增删改查
	- 节点.classList.add(value); //微元素添加指定的类
	- 节点.classList.contains(value); //判断元素是否含有指定的类，如果存在返回true
	- 节点.classList.remove; //删除指定的类
	- 节点.classList.toggle(value); //有就删除，没有就添加指定类
* 获取内联样式
	- 节点.style.样式属性名 //获取某个具体的内联样式box.style.backgroundColor需要使用驼峰命名法
	- 节点.style.cssText //获取某个节点的所有内联样式，返回字符串
	- obj.style只能获得内嵌样式（inline Style）就是写在Tag里面的，他访问不到那些链接的外部css和在head中用style声明的style。
```
obj.currentStyle和obj.style和getComputedStyle(obj,null)[attr]区别
getComputedStyle(obj,null)[attr],第一个是传入的节点，第二个传入:hover,:blur,:before,:after等
```
* 节点事件
	- 节点.onclick = function(){}可以设置为点击事件
	- 节点.onDblClick = function(){}双击事件
	- 节点.onMouseDown = function(){}鼠标按下事件
	- 节点.onMouseUp  = function(){}鼠标按下后，松开时事件
	- 节点.onMouseOver = function(){}鼠标移动到这个节点，相当于:hover事件
	- 节点.onMouseMove = function(){}鼠标在这个节点移动时事件
	- 节点.onMouseOut = function(){}鼠标在这个节点移出时事件
* slice()、splice()、substr()、substring()的区别
	- arrayObject.slice(start,end) 返回一个新的数组,不删除原数组
	- arrayObject.splice(index,howmany,item1,.....,itemX)
```javascript
var arr = [1, 2, 3, 4, 5]; //splice(start,end)
var arrNew = arr.splice(1, 3, 9); //从下表1开始取三个数并替换为9
console.log(arr); // [1, 9, 5]
console.log(arrNew); // [2, 3, 4]
```
```javascript
实例：
var str = "abcde";	//substr(start,lenth) 可为负数
var strNew = str.substr(1, 3); //获取从下表1开始取三个数
console.log(str); // "abcde"
console.log(strNew); // "bcd"
```
```
实例：
var str = "abcde";
var strNew = str.substring(1, 3); //substring(start,end)表示取下表为1,2的值,不能为负数
var strEmpty = str.substring();
console.log(str); // "abcde"
console.log(strNew); // "bc"
console.log(strEmpty); // ""
```
* JQuery是js库，是JavaScript的一些封装，提供大量的api
	- 集JS、CSS、DOM、Ajax于一体的强大的框架系统
	- 控制页面样式
	- 访问和操作DOMM
	- 事件处理
	- 提供了大量的插件
	- Ajax技术的封装
	- 提供大量的动画处理
* 如果JQ代码卸载body前，必须将代码写在ready事件中，表示所有DOM加载完成之后才执行
```javascript
	$(document).ready(function(){
	console.log($('.box'))
```
	- 简化写法：
```$(function(){
	console.log($('.box'))
})
```
* 基本选择器
	- #id
	- element
	- .class
	- *
	- selector1，selectorN
	- $(function(){
			$("#id,element,.class,*").css("display:flex")
		})
* 层次选择器
	- (.wrap p)选择class为wrap下的所有p标签
	- (.wrap > p)选择class为wrap下的所有子元素中的p标签
	- (.wrap + p)选择class为wrap下的和它相邻的p标签只有一个
	- (.wrap ~ p)选择class为wrap下的所有兄弟p标签
* 简单过滤器
	- first()或:first //获取第一个元素，如$("li:first").addClass("GetFocus") 或 $("li").first().addClass("GetFocus")
	- last()或:last //获取最后一个元素
	- :not(selector) //获取出给定选择器外的所有元素
	- :even //获取索引值为偶数的元素
	- :odd //获取索引值为奇数的元素
	- :eq(index) //获取指定索引值的元素
	- :gt(index) //获取大于给定索引值的元素
	- :lt(index) //获取小于给定索引值的元素
	- :header //获取所有标题类型的元素,如h1,h2...
* 内容过滤选择器
	- 根据元素中的文字内容或所包含的子元素特征获取元素，其文字内容可以模糊或绝对匹配进行元素定位
	- :contains(text) //获取包含给定文本的元素
	- :empty //获取所有不包含子元素或者文本的空元素
	- :has(selector) //获取含有选择器所匹配的元素
	- :parent //获取含有子元素或者文本的元素
* 可见性过滤选择器
	- :hidden //获取所有不可见元素，或者type为hidden的元素，display:none
	- :visible //选择display:block的元素
