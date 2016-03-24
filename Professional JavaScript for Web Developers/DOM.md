一、Node类型
	1、JS中所有节点类型都继承自Node类型
	2、属性：(1) nodeName：保存的是元素的标签名
			 (2) nodeValue：保存的是null
			 (3) childNodes：保存的都是子节点，有一个NodeLise对象（类似arguments），根据子元素数量动态的变化，NodeList有length属性，可以通过Array.prototype.slice()转化成数组 
			 (4) parentNode：指向文档树父节点
			 (5) previousSibling：访问前一节点
			 (6) nextSibling：访问下一个节点
			 (7) ownerDocument：可以直接访问文档节点(document)
	3、操作节点方法：
			 (1) appendChild()：向列表末尾添加一个尾节点
			 (2) insertBefore(待插入节点,参照点)：在参照点前面插入，插入节点被方法返回
			 (3) replaceChild(带插入节点，替换点)：将原来的节点替换掉，并返回，被替换的节点并没有删除，依然在文档中，只不过位置没了（类似指针）
			 (4) removeChild()：删除节点，并返回，跟replaceChild一样
	4、其他方法：
			 (1) cloneNode()：复制后的节点副本是属于document的，没有给其指定父节点，可以通过appendChild等指定父节点。ture时执行深复制，复制节点和整个子节点树,deepList中保存着深复制得到的副本。flase时执行浅复制，只复制节点本身，shallowList中保存着浅复制的副本。（IE中执行复制会复制事件处理程序）。
			 (2) normalize()：处理文档树中的文本节点，有空白文本节点则删除，有相邻文本节点则合并
	5、其他：由于IE还未公开Node类型构造函数，建议将nodeType和数字值比较来鉴定DOM类型

二、Document类型
	1、document对象是HTMLDocument（继承自Document）的一个实例，nodeType值为9
	2、属性：(1) documentElement：指向<html>元素，同document.childNodes[0]
		 	 (2) body：指向<body>元素
		 	 (3) doctype：指向<!DOCTYPE>,IE8及以前解释为注释节点，IE9和火狐则认为是文档的第一个节点，其他会解析为DocumentType节点，不出现在document.childNodes中
		 	 (4) title：指向<title>
		 	 (5) URL：指向页面完整的URL
		 	 (6) domain：指向页面的域名。
		 	 		<1> domain+iframe实现跨域：将每个页面的domain设置成相同的值就可以实现这些框架中的子页面实现跨域
		 	 		<2> 一旦由松散域名(baidu.com)改成紧绷的(image.baidu.com)就不能再修改回去了
		 	 (7) referrer：保存着连接到当前页的前一个页面的URL
		 	 (8) implementation：规定一个hasFeature()，检测浏览器是否支持相应版本号DOM功能,var a = document.implementation.hasFeature("CSS","3.0");
		 	 (9) anchors：所有带name的<a>
		 	 (10) applets：所有<applet>
		 	 (11) forms：所有<form>
		 	 (12) images：所有<img>
		 	 (13) links：所有带href的<a>
	3、方法：(1) getElementById()：若页面中出现相同的ID值，只会返回文档中ID值第一次出现的元素。IE7机7-会将name和ID值相同的表单元素也返回，不要让name和ID相同
			 (2) getElementsByTagName()：包含一个HTMLCollection对象（类似arguments）
			 (3) getElementsByName()：返回带有给定name值的所有元素，相同name值的单选按钮只有一个会给浏览器，返回一个HTMLCollection对象.namedItem()只会取得一项
			 (4) write()：注意"</script>"会解释为脚本块结束，应该添加转义字符,"<\/script>"。如果文档加载完后调用，会重写页面
			 (5) writeln()：在字符串末尾加\n换行
			 (6) open()
			 (7) close()
	4、其他：(1) <!--第一条注释-->
					<html></html>
				<!--第二条-->
				火狐会直接省略掉，IE9及9+会为两者创建为document.childNodes注释节点，其他则不管.
			 (2) document对象是只读的
	问题：document对象和Document对象有什么不同
三、Element类型
	1、nodeType为1
	2、所有HTML元素都由HTMLElement类型表示，HTMLElement继承自Element
	3、属性：(1) tagName：跟nodeName属性是一样的，返回的是大写的标签名
			 (2) id
			 (3) title：对它的修改只有在鼠标移动到这个元素上面的时候才能显示出来
			 (4) className
			 (5) style
			 (6) onclick等事件
			 (7) attribute属性：包含NameNodeMap，与NodeList类似。元素的每一个特性都由一个Attr节点表示，每个节点都保存在NameNodeMap对象中，且拥有
			 		<1> getNamedItem()方法
			 		<2> removeNamedItem():返回被删除节点
			 		<3> setNamedItem()
			 		<4> item()
			 		<5> specified()：除了IE，其他浏览器此值都为true。
	4、方法：(1) getAttribute()：取得元素特性、也可以取得自定义特性，一般在获取自定义属性时才用。
					<1> 自定义特性需要加data-前缀，除了IE，自定义属性不会添加到DOM中去
					<2> 通过element.style获取的和getAttribute()获取的值不一样，前者返回对象，后者返回字符串
					<3> 通过element.onclick获取的和getAttribute()获取的值不一样，前者返回JS函数，后者返回字符串
					<4> 通过div.luoxiao = "luoxiao";console.log(div.getAttribute("luoxiao"));//null，值为null。。因为并不会添加到DOM中，所以获取不到。所有的特性都是属性。
			 (2) setAttribute(name,value)：特性存在则替换，不存在则创建
			 (3) removeAttribute()：删除元素的特性
			 (4) createElement()：带有ownerDocument属性（不添加到dom中的话，不在页面显示）
			 (5) getElementsByTagName()：
	5、其他：(1) 遍历元素特性：
					function outputAttribute(element){
						var pairs = new Array(),
							attrName,
							attrValue,
							i,
							len;
						for(i = 0;len = element.attributes.length;i < len;i ++){
							attrName = element.attribute[i].nodeName;
							attrValue = element.atttribute[i].nodeValue;
							if(element.attributes[i].specified){
								pairs.push(attrName + "=\"" + attrValue + "\"");
							}
						}
					}
	问题：元素的特性和属性的区别：
			<div name="" class=""></div>。
			这里的name和class就是特性，属性指的是元素自带的，比如div.id,div.name,div.className。所有的特性都是属性
四、Text类型
	1、nodeType为3
	2、属性：(1) length
	3、方法：(1) createTextNode():创建新文本节点，带有ownerDocument属性（不添加到dom中的话，不在页面显示）
			 (2) normalize()：在包含两个或多个文本节点的父元素上调用，会把所有文本节点合并成一个。
			 (3) splitText()：按照指定的位置分隔nodeValue的值
五、Comment类型
	1、nodeType为8，与Text类型继承相同的基类
	2、属性：(1) data属性：获取注释内容
			 (2) nodeValue属性：同上
	3、方法：(1) createTextNode():创建新文本节点，带有ownerDocument属性（不添加到dom中的话，不在页面显示）
			 (2) normalize()：在包含两个或多个文本节点的父元素上调用，会把所有文本节点合并成一个。
			 (3) createComment()：创建注释节点并写入注释
六、DocumentFragment类型
	1、nodeType为11，继承了Node的所有方法
	2、相当于一个仓库，创建的html可以放到这里，然后一起添加到DOM中，每执行添加一次，浏览器会渲染一次，所以最好一次性一起添加。
七、Attr类型
	1、nodeType为2
	2、属性：(1) name:
			 (2) value:
			 (3) specified:区别是在代码中指定的还是默认的
	3、方法：(1) createAttribute()：创建特性节点document.createAttribute
	4、类似Element类型
八、其他
	1、<script>标签在IE中不允许DOM访问其子节点
	2、加载外部样式文本的过程是异步的，加载样式与执行JS代码没有固定的次序
	3、尽量减少NodeList的访问次数，每次访问都是基于文档的查询，每次调用DOM操作都会调用NodeList，所以减少DOM操作
	4、所有其他类型都继承自Node类型



DOM扩展
一、选择符API
	1、querySelector()
	2、querySelectorAll()：返回一个NodeList实例，通过类似对一组元素快照来解决动态查询的问题，避免了NodeList的性能问题
	3、matchesSelector()：匹配则返回true，由于兼容性的问题，所以解决兼容性的包装函数为：
		function matchesSelector(element,selector){
			if(element.matchesSelector){
				return element.matchesSelector(selector);
			}else if(element.msMatchesSelector){
				return element.msMatchesSelector(selector);
			}else if(element.mozMatchesSelector){
				return element.mozMatchesSelector(selector);
			}else if(element.webktiMatchesSelector){
				return element.webktiMatchesSelector(selector);
			}else{
				throw new Error("Not supported");
			}
		}
	4、原理：CSS解析器和树查询在浏览器内部通过编译代码执行，极大地提高了性能
二、元素遍历
	Element API新加了一下属性：
		(1) childElementCount
		(2) firstElementChild
		(3) lastElementChild
		(4) previousElementSibling
		(5) nextElementSibling
	遍历：
		var i,
			len,
			child = element.firstElementChild;
		while(child != element.lastElementChild){
			processChild(child);
			child = child.nextElementSibling;
		}
三、HTML5
	1、与类相关的扩充
		(1) getElementsByClassName()：返回NodeList，在元素上调用该方法，会返回后代中匹配的元素，同样具有性能问题
		(2) classList：是DOMTokenList实例，获取到类名并操作类名，拥有的方法如下
				<1> add()：div.classList.add("disabled")；
				<2> contains()
				<3> remove()
				<4> toggle()：存在则删除，不存在则添加
	2、焦点管理
		(1) activeElement：始终引用DOM中当前获得了焦点的元素。
				<1> 元素获取焦点的方式：页面加载、用户输入、调用focus()
				<2> 文档刚加载完时，document.activeElement中保存的是document.body的引用，文档加载期间，document.activeElement值为null
		(2) hasFocus()：确定文档是否获得了焦点
	3、HTMLDocument
		(1) readyState：loading正在加载文档，complete完成加载文档。
		(2) compatMode：告诉开发人员浏览器采用了哪种渲染模式。标准模式下为CSS1Compat，混杂模式下为BackCompat
		(3) head：引用<head>，建议var head = document.head || document.getElementsByTagName('head')[0];
		(2) 问题：为什么实现readyState必须要借助onload事件
	4、字符集属性
		(1) charset：文档实际用的字符集
		(2) defaultCharset：浏览器和操作系统默认的文档字符集
	5、自定义属性
		(1) dataset：添加了自定义属性后，可以通过这个属性来获取，它是DOMStringMap的一个实例，每一个data-name都有一个没有data-前缀的与之对应的属性，比如：div.dataset.myname == data-name