* Object.freeze()阻止修改现有的property
```javascript
var obj = {
	foo:bar
}
Object.freeze(obj)
new Vue({
	el:'#app',
	data:obj
})
<div id="app">
	<p>{{ foo }}</p>
	// 这里的'foo'不会更新！
	<button v-on:click="foo = 'baz'">change it</button>
</div>
```
* v-on:事件名指令：监听事件名，可以简写为 @事件名，@click
* 使用$用来区别用户定义的property
* 使用vm.$watch('a',function(newValue,oldValue){}) 这个回调将在'vm.a改变后调用'

``` javascript
var data = { a:1 }
var vm = new Vue{
	el: '#exanple',
	data: data
}
vm.$data === data //true
vm.$el === document.getElementById('example') //true
// $watch是一个实例方法
vm.$watch('a',function(newValue,oldValue){
	// 这个回调将在'vm.a改变后调用'
})
``` 

* 实例生命周期钩子
	- created:在一个实例被创建之后执行代码
``` javascript
new Vue({
	data:{
		a:1
	},
	created:function(){
		// 'this'指向vm实例
		console.log('a is:'+this.a)
	}
})
```
	- beforeCreate:在一个实例被创建之前执行代码
	- destroyed:
	- beforeDestroy:
	- updated:
	- beforeUpdate:
	- mounted:
	- beforeMounted:
* v-once指令：执行一次性的插值，当数据改变时，插值出的内容不会更新
* v-html指令：输出真正的html内容
* v-bind指令：v-bind:class='ShowRed',控制class属性名称;v-bind:href='url'控制跳转链接
* 新增动态参数，v-bind:[attribute]='name',可以动态控制参数名称
* 缩写：:key='',:[event]='doSomething'
* v-if实例：(v-for比v-if有更高的优先级)
```javascript
<div v-if="type === 'A'">A</div>
<div v-else-if="type === 'B'">B</div>
<div v-else-if="type === 'C'">C</div>
<div v-else>D</div>
```
* 计算属性computed,会增加缓存，但效率更快
```javascript
	var vm = Vue({
	el:'#example',
	data:{
		message:'Hello'
	},
	computed:{
		reversedMessage:function(){
			// 'this'指向vm实例
			return this.message.split('').reverse().join('')
		}
	}
	
})
```
* 监听属性watch
```javascript
var vm = new Vue({
	el:'#demo',
	data:{
		firstName:'Foo',
		lastName:'Bar',
		fullName:'Foo Bar'
	},
	watch:{
		firstName:function(val){  //当firstName值发生变化时，则变化的值为val，触发watch事件
			this.fullName = val + ' ' +this.lastName
		},
		lastName:function(val){  //当lastName值发生变化时，则变化的值为val，触发watch事件
			this.fullName = this.firstName + ' ' +val
		}
	}
})
```
* class和style绑定
```javascript
<div v-bind:class="{ active: isActive }"></div> //isActive存在，则class为active
<div v-bind:class="{ active: isActive, 'text-dager':hasError }"
data:{
	isActive:true,
	hasError:false
}
<div v-bind:class="classObject"></div>
data:{
	classObject:{
		active:true,
		'text-dager':false
	}
}
<div v-bind:class="classObject"></div> //绑定到计算属性中
data:{
	isActive:true,
	error:null
},
computed:{
	classObject:function(){
		return{
			active:this.isActive && !this.error,
			'text-dager':this.error && this.error.type === 'fatal'
		}
	}
}
<div v-bind:class="[activeClass,errorClass]"></div>
data:{
	activeClass:'active',
	errorClass:'text-danger'
}
<div v-bind:class="[isActive?activeClass:'',errorClass]"></div>
<div v-bind:class="[{active:isActive},errorClass]"></div>
```
* 绑定内联样式:property名可以用驼峰式或者短横线分割(加引号)
```javascript
<div v-bind:style="{color:activeColor,fontSize:fontSize + 'px}"></div>
data:{
	activeColor:'red',
	fontSize:13
}
<div v-bind:style="styleObject"></div>
data:{
	styleObject:{
		color:'red',
		fontSize:'13px'
	}
}
<div v-bind:style="[styleObject,baseStyles]"></div>
```
* v-show:简单切换元素的CSS property中display属性
	- 不支持<template></template>元素和v-else
* v-if和v-show区别：
	- v-if是真正的条件渲染，会确保再切换过程中条件块内的事件监听器和子组件适当的被销毁和重建
	- v-if也是惰性的：如果在初始渲染时条件为假，则什么也不做--直到条件第一次变为真时，才会开始渲染条件块
	- v-show不管初始条件是什么，元素总会被渲染，并且只是简单的基于CSS进行切换
	- v-if有更高的切换开销，v-show有更高的初始渲染开销
	- 如果需要非常频繁的切换，使用v-show较好；如果运行时条件很少改变，则使用v-if较好
* 在v-for下适用对象
```javascript
<ul id="v-for-object" class='demo'>
	<li v-for='value in object'>
		{{ value }}
	</li>
</ul>
new Vue({
	el:'#v-for-object',
	data:{
		object:{
			title:'How to do lists in Vue',
			author:'Jane Doe',
			publishedAt:'2016-04-10'
		}
	}
})
//结果：
	- How to do lists in Vue
	- Jane Doe
	- 2016-04-10
//也可以提供第二个参数为property名称(键名)
<ul id="v-for-object" class='demo'>
	<li v-for='(value,name) in object'>
		{{ name }}:{{ value }}
	</li>
</ul>
new Vue({
	el:'#v-for-object',
	data:{
		object:{
			title:'How to do lists in Vue',
			author:'Jane Doe',
			publishedAt:'2016-04-10'
		}
	}
})
//结果：
	- title:How to do lists in Vue
	- author:Jane Doe
	- publishedAt:2016-04-10
//还可以提供第三个参数作为索引
<ul id="v-for-object" class='demo'>
	<li v-for='(value,name,index) in object'>
		{{index}}.{{ name }}:{{ value }}
	</li>
</ul>
new Vue({
	el:'#v-for-object',
	data:{
		object:{
			title:'How to do lists in Vue',
			author:'Jane Doe',
			publishedAt:'2016-04-10'
		}
	}
})
//结果：
	- 0.title:How to do lists in Vue
	- 1.author:Jane Doe
	- 2.publishedAt:2016-04-10
```
* 为了给Vue一个提示，以便他能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每一项提供一个唯一key attribute(字符串或者数值类型)
* 数组更新方法
	- push() 可向数组的末尾添加一个或多个元素，并返回新的长度
	- pop() 用于删除并返回数组的最后一个元素
	- shift() 用于删除数组中的第一个元素并返回删除元素的值
	- unshift() 可向数组的开头添加一个或多个元素，并返回新的长度
	- splice() 向/从数组中添加/删除项目，并返回被删除的项目
```javascript
arrayObject.splice(index,howmany,item1,…,itemX)
```
	- sort() //该方法用于对数组的元素进行排序
```javascript
function sortNumber(a,b)
{
	return a - b
}
var arr = ['123','34','66','6','888','9'];
console.log("原数组："+arr);
console.log("新数组："+arr.sort(sortNumber));
![](vue基础_files/1.png)

function compare(prop){ //比较数组对象中某个属性值进行排列
	return function(a,b){
		var value1 = a[prop];
		var value2 = b[prop];
		return value1 - value2;
	}
}
```
	- reverse() //用于颠倒数组中元素的顺序
* 替换数组：总返回一个新数组
	- filter() //创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素
	- concat() //用于连接两个或多个数组 。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本
	- slice() //可从已有数组中返回选定的元素
* Vue不能检测出数组和对象的变化
* v-for索引列表可以使用computed里面的方法:
```javascript
<li v-for="n in evenNumbers">{{ n }}</li>
data:{
	numbers:[1,2,3,4,5]
},
computed:{
	evenNumbers:function(){
		return this.numbers.filter(function(number){
			return number % 2 === 0
		})
	}
}
// 在计算属性不适用的情况下：
<ul v-if="set in sets">
<li v-for="n in evenNumbers">{{ n }}</li>
</ul>
data:{
	sets:[[1,2,3,4,5],[6,7,8,9,10]]
},
methods:{
	even:function(numbers){
		return numbers.filter(function(number){
			return number % 2 === 0
		})
	}
}
```
* v-on事件修饰符
	- .stop //阻止单击事件继续传播
	- .prevent //提交时间不再重新加载界面
	- .capture //内部元素触发的事件现在此处理，然后才交由内部元素进行处理
	- .self //事件不是从内部元素触发的
	- .once //点击事件只会触发一次
	- .passive
* label中的for属性 checkbox复选框中v-model属性(双向绑定)
```javascript
// 复选框
<input type="checkbox" id="jack" value="jack" v-model="checkNames">
<lable for="jack">jack</lable>
<input type="checkbox" id="john" value="john" v-model="checkNames">
<lable for="john">john</lable>
<input type="checkbox" id="mike" value="mike" v-model="checkNames">
<lable for="mike">mike</lable>
new Vue({
	el:'...',
	data:{
		checkNames:[]
	}
})
// 单选框
<input type="radio" id="jack" value="jack" v-model="checkNames">
<lable for="jack">jack</lable>
<input type="radio" id="john" value="john" v-model="checkNames">
<lable for="john">john</lable>
<input type="radio" id="mike" value="mike" v-model="checkNames">
<lable for="mike">mike</lable>
new Vue({
	el:'...',
	data:{
		checkNames:''
	}
})
```
* v-model修饰符
	- v-model.lazy //在change时间之后进行同步
	- v-model.number //自动将用户输入值转为数值类型
	- v-model.trim //自动过滤用户输入的首尾空白字符
* Vue组件注册及使用
```javascript
Vue.component('blog-post',{
	props:['title'],
	data:function(){
		return{
			count:0
		}
	},
	
	template:'<h3 v-on:click="$emit('enlarge-text')">{{title}}</h3>' //监听子组件事件
})

<blog-post v-on:enlarge-text="postFontSize+=0.1" title="my journy with Vue"></blog-post>

// 使用事件抛出一个值
Vue.component('blog-post',{
	props:['title'],
	data:function(){
		return{
			postFonSize:1
		}
	},
	
	template:'<h3 v-on:click="$emit('enlarge-text',0.1)">{{title}}</h3>' //监听子组件事件
})
// 通过$event访问到被抛出的值
<blog-post v-on:enlarge-text="postFontSize+=$event" :style="{fontSize:postFonSize + 'em'}" title="my journy with Vue"></blog-post>
// 如果事件处理是一个方法
<blog-post v-on:enlarge-text="onEnlargeText" title="my journy with Vue"></blog-post>
// 那么这个值将作为第一个参数传入这个方法
method:{
	onEnlargeText:function(enlargeAmount){
		this.postFontsize += enlargeAmount
	}
}
// 可以使用is attribute属性调用组件
<div is="blog-post" v-on:enlarge-text="onEnlargeText" title="my journy with Vue"></div>
```
* 事件名使用kebab-case命名法,因为v-on事件监听器在DOM模板中会被自动转换为全小写

