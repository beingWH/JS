# JS学习笔记

## 基础JS

### JS语句

1. 分号`;` 分隔语句，可选
2. 代码块`{}` 语句序列按代码块执行
3. 大小写敏感
4. 空格忽略，以下效果等同
	```JS
	var name="hello";
	var name= "hello";
	```
5. 代码行折析，以下效果等同
	```JS
	document.write("hello world!")
	document.write("hello \
	world!")
	```
6. 注释 行注释为`//`，段注释为`/**/`

### JS变量

1. 变量声明使用`var`，首次声明一个变量时，如未赋值，变量为`undefined`类型
2. 一条语句，多个变量
	```JS
	var name="Gates",age=56,job="CEO";
	```
3. 重新声明JS变量
	如果重新声明JS变量，变量值不会丢失，以下两句执行后，变量值仍为"Volvo"
	```JS
	var carname="Volvo";
	var carname;
	```
### JS数据类型
	
**JS拥有动态类型，相同变量可以用作不同的类型**

1. JS字符串 `''`或`""`来包裹均可
2. JS数字 `34`,`34.00`,`123e5`,`123e-5`
3. JS布尔 `true`,`false`
4. JS数组
	```JS
	var cars=new Array();
	cars[0]="Audi";
	cars[1]="BMW";
	cars[2]="Volvo";
	//也可使用以下形式
	var cars=new Array("Audi","BMW","Volvo");
	//也可使用以下形式
	var cars=["Audi","BMW","Volvo"];
	```
5. JS对象
	对象由花括号分隔，在括号内部，对象的属性以名称和值对的形式`name:value`来定义。属性由逗号隔开
	```JS
	var person={firstname:"Bill",lastname:"Gates",id:5566};
	//也可以使用这样的形式
	var person={
	firstname:"Bill",
	lastname:"Gates",
	id:5566
	};
	```
6. undefined与null
	Undefined这个值表示变量不含有值，可以通过将变量的值设置为null来清空变量。

7. 声明变量类型
	当您声明新变量时，可以使用关键词 "new" 来声明其类型：
	```JS
	var carname=new String;
	var x=new Number;
	var y=new Boolean;
	var cars=new Array;//等同于var cars=new Array()
	var person=new Object;//等同于var person=new Object()
	```
	JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象。

### JS对象

JS中所有变量均为对象，对象具有属性和方法，如
```JS
var txt="Hello";
txt.length=5; //属性
txt.indexof();
txt.replace();
txt.search();//方法
```
如下方式，创建对象，并添加属性
```JS
person=new Object();
person.firstname="Bill";
person.lastname="Gates";
person.age=56;
```

## JS面向对象

### 对象构造方式
1. 基于Object
	```JS
	person=new Object();
	person.firstname="Bill";
	person.lastname="Gates";
	person.age=56;
	person.getName=function(){
	return this.firstname+' '+this.lastname;
	}
	```
2. 对象字变量方式
	```JS
	var person={
	firstname:"Bill"
	lastname:"Gates",
	age:56,
	getName:function(){return this.firstname+' '+this.lastname;}
	}
	```
### 对象属性类型
1. 数据属性

	数据属性包含四个参数特征：

	- [[configurable]]:表示能否使用delete操作符删除从而重新定义，或能否修改为访问器属性。默认为true
	- [[Enumberable]]:表示是否可通过for-in循环返回属性。默认true
	- [[Writable]]:表示是否可修改属性的值。默认true
	- [[Value]]:包含该属性的数据值。读取/写入都是该值。默认为undefined

	要修改对象属性的默认特征（默认都为true)，可调用Object.defineProperty()方法，它接收三个参数：属性所在对象，属性名和一个描述符对象（必须是：configurable、enumberable、writable和value，可设置一个或多个值）。
	```JS
	var person = {};
	Object.defineProperty(person, 'name', {
    	configurable: false,
   	 writable: false,
    	value: 'Jack'
		});
	alert(person.name);//Jack
	delete person.name;
	person.name = 'lily';
	alert(person.name);//Jack
	```
2. 访问器属性

	它主要包括一对getter和setter函数，在读取访问器属性时，会调用getter返回有效值；写入访问器属性时，调用setter，写入新值；该属性有以下4个特征：
	
	- [[Configurable]]:是否可通过delete操作符删除重新定义属性；
	- [[Numberable]]:是否可通过for-in循环查找该属性；
	- [[Get]]:读取属性时调用，默认：undefined;
	- [[Set]]:写入属性时调用，默认：undefined;
	
	访问器属性不能直接定义，必须使用defineProperty()来定义，如下：
	```JS
	var person = {
    _age: 18
	};
	Object.defineProperty(person, 'isAdult', {
    	get: function () {
        	if (this._age >= 18) {
          	 return true;
       	 } else {
           	 return false;
        	}
    	}
	});
	alert(person.isAdult?'成年':'未成年');//成年
	```

	从上面可知，定义访问器属性时getter与setter函数不是必须的,并且，在定义getter与setter时不能指定属性的configurable及writable特性；也可以通过方法的方式来表示：
	```JS
	var person = {};
	Object.defineProperties(person,{
    	_age:{
        	value:19
    	},
    	isAdult:{
        	get: function () {
            	if (this._age >= 18) {
               	 return true;
            	} else {
               	 return false;
           	 }
       	 }
    	}
	});
	alert(person.isAdult?'成年':'未成年');//成年
	```	
### 创建对象

1. 工厂模式
	```JS
	function createPerson(name,age,job){
	var o=new Object();
	o.name=name;
	o.age=age;
	o.job=job;
	o.getName=function(){return this.name;}
	return o;
	}
	var person=createPerson('Jack',19,'Software Engineer');
	```
2. 构造函数模式
	```JS
	fuction Person(name,age,job){
	this.name=name;
	this.age=age;
	this.job=job;
	this.getName=function(){return this.name;}
	}
	var person=createPerson('Jack',19,'Software Engineer');
	```

**工厂模式与构造函数模式有一个缺点，就是每次新建对象，都会实例化方法实例（person1.getName与person2.getName是两个不同的方法实例），造成内存浪费。**

3. 原型模式
	JS每个函数都有一个prototype(原型)属性，这个属性是一个指针，指向一个对象，它是所有通过new操作符使用函数创建的实例的原型对象。原型对象最大特点是，所有对象实例共享它所包含的属性和方法，也就是说，**所有在原型对象中创建的属性或方法都直接被所有对象实例共享**。

	```JS
	//类似于C#或JAVA中的构造函数中赋值
	function Person(){
	}
	Person.prototype.name = 'Jack';//使用原型来添加属性
	Person.prototype.age = 29;
	Person.prototype.getName = function(){
	    return this.name;
	}
	var person1 = new Person();
	alert(person1.getName());//Jack
	var person2 = new Person();
	alert(person1.getName === person2.getName);//true;共享一个原型对象的方法
	```

	 原型是指向原型对象的，这个原型对象与构造函数没有太大关系，唯一的关系是函数的prototype是指向这个原型对象！而基于构造函数创建的对象实例也包含一个内部指针为：[[prototype]]指向原型对象。

     实例属性或方法的访问过程是一次搜索过程：

	- 首先从对象实例本身开始，如果找到属性就直接返回该属性值；
	- 如果实例本身不存在要查找属性，就继续搜索指针指向的原型对象，在其中查找给定名字的属性，如果有就返回；
		
     基于以上分析，原型模式创建的对象实例，其属性是共享原型对象的；但也可以自己实例中再进行定义，在查找时，就不从原型对象获取，而是根据搜索原则，得到本实例的返回；简单来说，就是**实例中属性会屏蔽原型对象中的属性**。

4. 组合构造函数及原型模式

	目前最为常用的定义类型方式，是组合构造函数模式与原型模式。构造函数模式用于定义实例的属性，而原型模式用于定义方法和共享的属性。结果，每个实例都会有自己的一份实例属性的副本，但同时又共享着对方方法的引用，最大限度的节约内存。此外，组合模式还支持向构造函数传递参数，可谓是集两家之所长。

	```JS
	function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.lessons = ['Math', 'Physics'];
	}
	Person.prototype = {
    	constructor: Person,//原型字面量方式会将对象的constructor变为Object，此外强制指回Person
   	 	getName: function () {
        		return this.name;
    		},
		name:wanghuan
	}
	var person1 = new Person('Jack', 19, 'SoftWare Engneer');
	person1.lessons.push('Biology');
	var person2 = new Person('Lily', 39, 'Mechanical Engneer');
	alert(person1.lessons);//Math,Physics,Biology
	alert(person2.lessons);//Math,Physics
	alert(person1.getName === person2.getName);//true,//共享原型中定义方法
	```

## JS语法
1. JS函数
	函数定义
	```JS
	function fuctionName(arg1,arg2){
		//代码段
	}
	```
2. JS运算符
	
	运算符|描述|例子
	:----|:---:|:---:
	++|累加|x=++y
	--|递减|x=--y
	+=|加等|x+=y
	-=|减等|
	*=|乘等|
	/=|除等|
	%=|余等|
	===|全等（值和类型）|x===5为true；x==="5"为false

3. If...else
	```JS
	if(){

	}else{

	}

	if(){

	}else if(){
	
	}else{
	
	}
	```
4. Switch
	```JS
	switch(n){
	case 1:代码块;break;
	case 2:代码块;break;
	default:代码块;
	}
	```
5. For
	```JS
	for(var i=0;i<cars.length;i++){
		代码块
	}
	// 多变量
	for(var i=0,len=cars.length;i<len;i++){
		代码块
	}
	//变量不在循环类声明时
	var i=2,len=cars.length;
	for(;i<len;i++){
		代码块
	}
	```
6. For/In
	用于遍历对象的属性
	```JS
	var person={fname:"John",lname:"Doe",age:25};
	for(x in person){
		txt=txt+person[x];
	}
	```
7. while
	```JS
	while(条件){
		代码块
	}
	```
	循环数组中所有值
	```JS
	cars=["BMW","Volvo","Saab","Ford"];
	var i=0;
	while (cars[i])
	{
		document.write(cars[i] + "<br>");
		i++;
	}
	
	//等同于
	cars=["BMW","Volvo","Saab","Ford"];
	var i=0;
	for (;cars[i];)
	{
		document.write(cars[i] + "<br>");
		i++;
	}
	```
8. break/continue
	同其他语言
	JS语句标记跳出
	```JS
	cars=["BMW","Volvo","Saab","Ford"];
	list:
	{
	document.write(cars[0] + "<br>");
	document.write(cars[1] + "<br>");
	document.write(cars[2] + "<br>");
	break list;
	document.write(cars[3] + "<br>");
	document.write(cars[4] + "<br>");
	document.write(cars[5] + "<br>");
	}
	```
9. JS错误
	```JS
	try{
	  	var x=document.getElementById("demo").value;
		if(x=="")    throw "empty";
  		if(isNaN(x)) throw "not a number";
  		if(x>10)     throw "too high";
  		if(x<5)      throw "too low";
	}
	catch(err){
  		var y=document.getElementById("mess");
  		y.innerHTML="Error: " + err + ".";
	}
	```
10. JS验证

## JS正则表达式
