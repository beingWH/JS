# JQ基础笔记
## JQ基础
### JQ选择器
1. JQ 元素选择器
	```JQ
	$("p") //选取<p>元素
	$("p.intro") //选取所有class="intro"的<p>元素
	$("p#demo") //选取所有id="demo"的<p>元素
	```
2. JQ 属性选择器
	```JQ
	$("[href]") //选取所有带有href属性的元素
	$("[href='#']") //选取所有带有href值等于"#"的元素
	$("[href!='#']") //选取所有带有href值不等于"#"的元素
	$("[href$='.jpg']") //选取所有href值以".jpg"结尾的元素
	```
3. JQ CSS选择器
	```JQ
	$("p").css("background-color","red")
	```
4. 更多实例
	```JQ
	$(this) //当前HTML元素
	$(".intro") //所有class="intro"的元素
	$("ul li:first") //每个<ul>的第一个<li>元素
	$("div#intro .head") //id="intro"的<div>元素中的所有class="head"的元素
	```
### JQ 事件

Event函数|绑定函数至
:-------|:--------
$(document).ready(function)|将函数绑定至文档的就绪事件（当文档完成加载时）
$(selector).click(function)|触发或将函数绑定到被选元素的点击事件
$(selector).dbclick(function)|触发或将函数绑定到被选元素的双击事件
$(selector).focus(function)|触发或将函数绑定到被选元素的获得焦点事件
$(selector).mouseover(function)|触发或将函数绑定到被选元素的鼠标悬停事件

### JQ 效果

1. 隐藏/显示
	- hide()
	- show()
	- toggle(speed,callback) 隐藏和显示之间切换,其中speed可选("slow","fast","1000")
2.  淡入/淡出
	- fadeIn(speed,callback)
	- fadeOut(speed,callback)
	- fadeToggle(speed,callback)
	- fadeTo(speed,opacity,callback) opacity为不透明度（值介于0与1之间）
3. 滑动
	- slideDown(speed,callback)
	- slideUp(speed,callback)
	- slideToggle(speed,callback)
4. 动画
	- animate({params},speed,callback)
5. 停止
	- stop(stopAll,goToEnd) 停止动画或效果
	可选的stopAll默认为false，该参数规定是否应该清除动画队列，当为false时，仅停止活动的动画，允许任何排入队列的动画向后执行；
	可选的gotToEnd参数规定是否立即完成当前动画，默认为false。
6. 回调
	- Callback,当动画100%完成后，即调用Callback函数
	```JQ
	$("p").hide(1000,function(){
	alert("The paragraph is now hidden");
	});
	```
7. 方法链接
	```JQ
	$("#p1").css("color","red").slideUp(2000).slideDown(2000); //"p1" 元素首先会变为红色，然后向上滑动，然后向下滑动
	$("#p1").css("color","red")
  		.slideUp(2000)
  		.slideDown(2000);
	```
### JQ HTML

1. JQ 获取

方法|解释|示例
:---|:---|:---
text()|设置或返回所选元素的文本内容|$('#test').text()
html()|设置或返回所选元素的html内容|$('#test').html()
val()|设置或返回表单字段的值|$('#test').val()
attr()|获取属性值|$("#test").attr("href")

2. JQ 设置

	2.1 直接设置
	```JQ
	$('#test').text("Hello World")
	$('#test').html("<b>Hello World</b>")
	$('#test').val("hello world")
	$("#w3s").attr("href","http://www.w3school.com.cn/jquery");
	$("button").click(function(){
 	$("#w3s").attr({
    	"href" : "http://www.w3school.com.cn/jquery",
    	"title" : "W3School jQuery Tutorial"
  		});
	```
	2.2 回调设置
	```JQ
	$("#test1").text(function(i,origText){
    	return "Old text: " + origText + " New text: Hello world!
    	(index: " + i + ")";
  		});

	$("#test2").html(function(i,origText){
    	return "Old html: " + origText + " New html: Hello <b>world!</b>
    	(index: " + i + ")";
  		});
  	$("#w3s").attr("href", function(i,origValue){
    	return origValue + "/jquery";
 		 });
	```
3. JQ 添加与删除
	
方法|解释|示例
:---|:---|:---
append()|被选元素的结尾插入内容|append(txt1,txt2,txt3,...)
prepend()|被选元素的开头插入内容|prepend(txt1,txt2,txt3,...)
after()|被选元素之后插入内容|after(txt1,txt2,txt3,...)
before()|被选元素之前插入内容|before(txt1,txt2,txt3,...)
remove()|删除被选元素及其子元素|
empty()|删除被选元素的子元素|
remove(selector)|删除过滤的被选元素|$("p").remove(".italic")/删除 class="italic" 的所有 <p> 元素

4. JQ CSS类

	4.1 在HTML中嵌入CSS
	```JQ
	<head>
	<script src="/jquery/jquery-1.11.1.min.js"></script>
	<script>
		$(document).ready(function(){
  			$("button").click(function(){
   			$("h1,h2,p").addClass("blue");
    		$("div").addClass("important");
 		 });
		});
	</script>
	//css 样式嵌入在head中
	<style type="text/css">
	.important
	{
		font-weight:bold;
		font-size:xx-large;
	}
	.blue
	{
		color:blue;
	}
	</style>
	</head>
	
	```
	4.2 css方法
	- addClass() 例如：$("h1,h2,p").addClass("blue")
	- removeClass() 例如：$("h1,h2,p").removeClass("blue")
	- toggleClass() 例如：$("h1,h2,p").toggleClass("blue")
	- css()
		- css() 例如$("p").css("background-color")获取属性值
		- css("propertyname","value") 例如$("p").css("background-color","yellow")设置属性值
		- css({"p":"v","p":"v",...})设置多个属性

### JQ AXAJ

1. JQ -load()方法
	load() 方法通过 AJAX 请求从服务器加载数据，并把返回的数据放置到指定的元素中。
	```JQ
	load(url,data,function(response,status,xhr))
	```
	参数|描述
	:---|:---
	url|必需，规定要将请求发送到哪个url
	data|可选，规定连同请求发送到服务器的数据(post)
	function|可选，规定当请求完成时运行的函数
	
	function(response,status,xhr)
	- response 包含来自请求的结果数据
	- status 包含请求的状态(success,notmodified,error,timeout,parsererror)
	- xhr 包含XMLHttpRequest对象
	
	load()与get()的区别
	- load可以通过url来从服务器加载特定过滤器的数据
		```JQ
		$("#result").load("ajax/test.html #container");
		//从ajax/test.html中加载id=container的片段
		
		$("#feeds").load("feeds.php", {limit: 25}, function(){
  			alert("The last 25 entries in the feed have been loaded");
			});//post方式发送参数并在成功时显示信息

		$("button").click(function(){
  			$("#div1").load("demo_test.txt",function(responseTxt,statusTxt,xhr){
   			 if(statusTxt=="success")
     		 alert("外部内容加载成功！");
   			 if(statusTxt=="error")
      			alert("Error: "+xhr.status+": "+xhr.statusText);
 			 });
			});// 完整用例
		```

2. JQ -get()方法
	
	```JQ
	$.get(URL,callback);
	//示例
	$("button").click(function(){
  		$.get("demo_test.asp",function(data,status){
    		alert("Data: " + data + "\nStatus: " + status);
  		});
	});
	```
3. JQ -post()方法
	```JQ
	$.post(URL,data,callback);
	//示例
	$("button").click(function(){
 		$.post("demo_test_post.asp",
  		{
   		 	name:"Donald Duck",
    		city:"Duckburg"
  		},
  		function(data,status){
    		alert("Data: " + data + "\nStatus: " + status);
  		});
	});
	```
4. JQ -getJSON()方法
	```JQ
	jQuery.getJSON(url,data,success(data,status,xhr))
	//示例
	$.getJSON("test.js", { name: "John", time: "2pm" }, function(json){
  		alert("JSON Data: " + json.users[3].name);
	});
	```
5. JQ -getScript()方法
	```JQ
	jQuery.getScript(url,success(response,status))
	//示例
	$.getScript("test.js", function(){
  		alert("Script loaded and executed.");
	});
	```	
6. JQ -ajax()方法
	该方法是 jQuery 底层 AJAX 实现。简单易用的高层实现见 $.get, $.post 等。$.ajax() 返回其创建的 XMLHttpRequest 对象。大多数情况下你无需直接操作该函数，除非你需要操作不常用的选项，以获得更多的灵活性。
	```JQ
	$.ajax({settings1:"value1",settings2:"value2",...})
	//示例
	 $.ajax({
                type: "Post",
                url: "/TestBlock/CloseTest",
                data: '{"station":"6#"}',
                contentType: "application/json",
                dataType: "Json",
                success: function (data) {
                    $("#teststate-6").removeClass();
                    $("#teststate-6").addClass("fa fa-stop");
                    alert(data);
                },
                error: function (XMLHttpRequest, textStatus, errorThrown) {
                        alert("error:" + textStatus);
                }
            });
	```