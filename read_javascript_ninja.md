[TOC]

# 函数是根基

### 构造器的超能力
当new 一个对象的时候，如下特殊行为会发生：
* 创建一个空的对象
* 把this参数传递给构造器对象，作为构造器的函数上下文
* 如果没有显式的返回值，新创建的构造器对象作为构造器的返回值进行返回

**构造器的返回值范围两种，一种是值类型，则会把新创建的构造器对象作为返回值；另一种是返回引用类型，则会把引用类型作为返回值**

```javascript
// 1.返回值类型
var a = function() {
  this.a = 'a'
  return ''
} 
var b = new a()
```

![输出a和b的结果](https://raw.githubusercontent.com/outofhadoop/macFile/master/a%2Cb1上午11.39.56.png)

```javascript
// 2.返回引用类型的情况
var a = function() {
  this.a = 'a'
  return {
    c: 'c'
  }
}

var b = new a()

```

![引用类型返回值](https://raw.githubusercontent.com/outofhadoop/macFile/master/a%2Cb2 上午11.45.48.png)



### 匿名函数

##### 常见示例：

* 作为Dom0级事件处理函数

```javascript
window.onload = function () {
  // do something
}
```

* 作为复杂类型的值

```javascript
obj.fnc = function() {
  // do something
}
```

* 作为callback

```javascript
setTimeout(function () {
	// do something 
})
```

* 作为返回值

```javascript
function backFnc () {
  return function() {
    // do something
  }
}
```



### 将函数视为对象

##### 函数存储

**缓存一组独立的函数：**

```javascript
let store = {
  nextIndex: 1,
  cache: {},
  add (fn) {
    if (fn && !fn.id) {
      this.cache[this.nextIndex] = fn;
      fn.id = this.nextIndex++;
      console.log('cache success')
    } else {
      console.log('cached!')
    }
  }
};
let fnc = function(){
  // do something
};
store.add(fnc);
store.add(fnc)
```

![运行缓存函数代码结果](https://raw.githubusercontent.com/outofhadoop/macFile/master/屏幕快照 2019-09-17 下午5.31.54.png)



**缓存昂贵的计算结果**

示例函数：计算素数

```javascript
let isPrime = function(value) {
  if (!isPrime.answer) {
    isPrime.answer = {}
  }
  if (isPrime.answer[value] != null) {
    return isPrime.answer[value]
  }
  let prime = value != 1;
  for (let i = 2; i < value; i ++) {
    if (value % i == 0) {
      prime = false;
      break;
    } 
    return isPrime.answer[value] = prime;
  }
}
```



### arguments

> 所有的函数都隐式传递了**arguments**这一重要内置参数，使得函数有能力处理任意数量的参数

##### merge对象属性

```javascript
function merge (root) {
  for(let i = 1; i < arguments.length; i++) {
    for(let key in arguments[i]) {
      root[key] = arguments[i][key]
    }
  }
  return root
}
```



##### 函数重载

```javascript
/**
 * @description 为一个对象添加可重载函数
 * @param {Object} obj 需要添加重载函数的对象
 * @param {String} name 函数名
 * @param {Function} fn 重载函数
 */
function addMethods(obj, name, fn) {
  let old = obj[name]
  if (fn.length === arguments.length) {
    return fn.apply(this, arguments)
  } else if (typeof old === 'function') {
    return old.apply(this, arguments)
  }
}

let testObj = {}
addMethods(testObj, 'fn', function() {
  console.log('0');
})
addMethods(testObj, 'fn', function(param) {
  console.log('1')
})
addMethods(testObj, 'fn', function(param, param1) {
  console.log('2')
})
testObj.fn()
testObj.fn(1)
testObj.fn(1, 2)
```

### 函数判断（类型判断）

```javascript
// 判断函数
let fn = function(){}
Object.prototype.toString.call(fn) === "[object Function]"

// 判断字符串
let str = ""
Object.prototype.toString.call(str) === "[object String]"

// 判断数字
let num = 1  // 对于 NaN, Infinity 都是同样的结果
Object.prototype.toString.call(num) === "[object Number]"

// 判断Boolean
let boo = false
Object.prototype.toString.call(boo) === "[object Boolean]"

// 判断对象
let obj = {}
Object.prototype.toString.call(obj) === "[object Object]"

// 判断数组
let arr = []
Object.prototype.toString.call(arr) === "[object Array]"

// 判断Symbol
let sym = Symbol('sym')
Object.prototype.toString.call(sym) === "[object Symbol]"

// 判断Null
let nul = null
Object.prototype.toString.call(nul) === "[object Null]"

// 判断undefined
let undef
Object.prototype.toString.call(undef) === "[object Undefined]"

// 判断BigInt
let big = BigInt(123)
Object.prototype.toString.call(big) === "[object BigInt]"

// 判断Date对象
let date = new Date()
Object.prototype.toString.call(date) === "[object Date]"

let regexp = RegExp('')
Object.prototype.toString.call(regexp) === "[object RegExp]"

// DOM元素 超链接
let anchorDom = document.createElement('a')
Object.prototype.toString.call(anchorDom) === "[object HTMLAnchorElement]"

// DOM Attr
let domAttr = document.createAttribute('src')
Object.prototype.toString.call(domAttr) === "[object Attr]"

// 注释节点
let comment = document.createComment('注释内容')
Object.prototype.toString.call(comment) === "[object Comment]"

// DOM Button
let button = document.createElement('button')
Object.prototype.toString.call(button) === "[object HTMLButtonElement]"

/**
 * @todo DOM对象有很多，暂不写全，在另一个文件补全
 **/

// 浏览器Window对象
let win = window
Object.prototype.toString.call(window) === "[object Window]"


```



### 使用闭包

##### 私有变量

私有变量很多运用在ES5的面向对象编程：

```javascript
function primaryParam () {
  // 私有变量
  let pri = 0;
  this.add = function() {
    pri++
  }
  this.getPri = function () {
    return pri
  }
}

```



##### bind polify

```javascript
// Prototype库中的bind函数
function bind() {
  let fn = this, args = Array.prototype.slice.call(arguments), object = args.shift()
  return function () {
    return fn.apply(object, args.concat(Array.prototype.slice.call(arguments)))
  }
}
```



##### 偏函数（函数柯理化）

```javascript
Function.prototype.curry = function () {
  let fn = this,
      args = Array.prototype.slice.call(arguments)
  return function () {
    return fn.apply(this, args.concat(Array.prototype.slice.call(arguments)))
  }
}
```



### 原型与面向对象

##### 使用constructor实例化一个新对象

```javascript
function Ninja() {}

var ninja = new Ninja()

var ninja2 = new ninja.constructor()

console.log(ninja2 instanceof Ninja) // 结果： true
console.log(ninja2 !== ninja) // 结果：true
```



### 函数作为构造函数时避免直接调用报错

**通过arguments.callee可以得到当前执行函数的引用，但需要注意，callee即将在新的JavaScript中废弃，并且不支持严格模式！ **

```javascript
function User(first, last) {
	if (!(this instanceof arguments.callee)) {
		return new arguments.callee
  }
  this.name = first + last
}
```





### 线程和定时器

##### 管理多个程序的中央定时器

定时器只能在浏览器环境下运行！！

```javascript
const timers = {
  
  timerID: 0, // 存储定时器ID，清除定时器时使用
  timers: [], // 定时器队列
  
  // 向队列中添加执行函数，仅可以向后添加
  add (fn) {
    this.timers.push(fn);
  },
  
  // 开始定时器
  start () {
    if (this.timerID) return;
    (function runNext(){
      if (timers.timers.length > 0) {
        for (let i = 0; i < timers.timers.length; i++ ) {
        	// 如果执行函数返回值为false，则在队列中清除
          if (timers.timers[i]() === false) {
						timers.timers.splice(i, 1);
            i--;
          }
        }
        timers.timerID = setTimeout(runNext, 0);
      }
      
    })();
  },
  
  stop () {
    clearTimeout(this.timerID);
    this.timerID = 0;
  }
  
}
```



### 运行时代码求值

##### eval方法进行求值

```javascript
eval('5 + 5') // 10
eval('var a = 5') // undefined
// 在eval中声明的变量会在运行时添加到作用域链中
console.log(a) // 5
window.a // 5

eval('3+4;5+6') // 11

var a = eval('{name: 2}') 
a === 2 // true

// 括号里也可以是函数或者其他
var a = eval('({name: 2})')
a.name === 2 // true

// eval JSON转化
var a = '{"name": "aaa"}'
var jsonA = eval(`(${a})`) // jsonA.name === 'aaa'
```

##### 全局作用域下的求值

```javascript
// 通过向dom中插入script来添加全局变量
function globalEval(data) {
  // 去除前导和尾部的空白字符
  data = data.replace(/^\s*|\s*$/g, '');
  if (data) {
    // document.documentElement: 总是返回<html>的只读属性
    var head = document.getElementsByTagName('head')[0] || document.documentElement,
        script = document.createElement('script');
    script.type = 'text/javascript';
    script.text = data;
    head.append(script);
    head.removeChild(script);
  }
}
```

##### 函数反编译检测

```javascript
// 检测浏览器是否支持函数反编译
var FUNCTION_DECOMPIATION = /abc(.|\n)*xyz/.test(function(abc){xyz})
```



### with语句

```javascript
var use = 'other'
var katana = {
  isSharp: true,
  use: function() {
    this.isSharp = !this.isSharp
  }
}

with (katana) {
	use !== 'other' && typeof use == 'function' // true
  // 执行环境的上下文并没有改变
  this !== katana
}

// 在赋值时优先考虑全局变量
with(katana) {
  with (window) {
    // 例如再给use变量赋值时，就会优先修改掉window下面的
  }
}
```

### DOM特性和DOM属性

```javascript
var image = document.getElementsByTagName('img')
image.src = '../../none.png' // 这里../../none.png是一个不存在的路径
image.getAttribute('src') // 结果为""
```

##### 跨浏览器命名

> 在大多数浏览器中都可以用class获取到class特性，但IE却要使用className。这可能是因为该属性的名称是className，所以在IE中，特性名称和属性名称是一致的。

##### 命名限制

> 特性（attribute），表示为传给DOM方法的字符串，其命名规范是非常自由的，但属性名称，由于可以作为标识符使用点表示法进行访问，所以其命名规范是受限的，属性名称必须符合标识符的规则，而且还有一些保留关键字也不能使用。

下表展示了一些差异的例子：

> | 特性名称（Attribute） | 属性名称（Property） |
> | :-------------------- | :------------------- |
> | for                   | htmlFor              |
> | class                 | className            |
> | readonly              | readOnly             |
> | maxlength             | maxLength            |
> | cellspacing           | cellSpacing          |
> | rowspan               | rowSpan              |
> | colspan               | colSpan              |
> | tabindex              | tabIndex             |
> | ellpadding            | cellPadding          |
> | usemap                | useMap               |
> | frameborder           | frameBorder          |
> | contenteditable       | contentEditable      |
> |                       |                      |

##### 检测XML

```javascript
function isXML(elem) {
  return (elem.ownerDocument || elem.documentElement.nodeName.toLowerCase() !== 'html')
}
```

##### DOM中的id/name膨胀

> ”五大“浏览器都会将表单input元素的id和name特性作为<form>元素的属性值引用。产生的这些属性会主动覆盖form元素上已经存在的同名属性
>
> 此外，IE浏览器不仅会替换属性值，甚至还会替换该属性上的特性值

```javascript
// 为解决这一问题，可以获取描述元素特性本身的原始DOM节点
// 例如获取action的值：
var actionValue = element.getAttributeNode("action").nodeValue
```

##### URL规范化

> 在所有的现代浏览器中，有一个违反最少意外原则的”特性“：在访问一个引用了URL的属性时（例如，href、src或action），该URL值会自动将原值转换成完整规范的URL

##### type陷阱

> IE8以及之前的版本对<input>元素的type特性的影响，没有任何合理的解决方案。一旦<input>元素被插入到文档，它的type特性就不能再改变。

##### table index问题

> 对于已经声明的tab index的元素，也许可以使用tabIndex属性或tabindex特性获取元素的tab index值；但如果没有显示声明，tabIndex会返回0，而tabIndex特性则返回null，这就是说，如果不显示设置tab index，我们就无法获取到一个元素的tab index

##### float样式属性

> 因为float是JavaScript的保留字。浏览器需要提供另外一个名称代替，几乎所有的浏览器都使用的cssFloat这个名称作为替代名称，但IE浏览器却选择使用styleFloat。

##### opacity透明度

> 如果将opacity指定为 .5 ，原始支持opacity的浏览器就会将该值规范为0.5 ， 而不原始支持opacity的浏览器则直接返回原有的形式 .5。

##### 获取计算样式

```javascript
function fetchComputedStyle(element, property) {
  if (window.getComputedStyle) {
    
		var computedStyles = window.getComputedStyle(element);
    
    if (computedStyles) {
      property = property.replace(/([A-Z])/g, '-$1').toLowerCase();
      return computedStyles.getPropertyValue(property);
    }
  } else if (element.currentStyle) {
    property = property.replace(
    	/-([a-z])/ig,
      function (all, letter) { return letter.toUpperCase(); }
    );
    return element.currentStyle[property];
  }
}
```

### 不老事件

##### 绑定和解绑事件处理程序

> 在DOM Level 2 Event Model 下，对于兼容DOM的现代浏览器，我们绑定和解绑事件处理程序使用的是addEventListener() 和 removeEventListener() 方法；而对IE老版本（IE9之前的版本）使用的则是attachEvent() 和 detachEvent() 方法。

```javascript
if (document.addEventListener) {
  this.addEvent = function (elem, type, fn) {
    elem.addEventListener(type, fn, false);
    return fn;
  };
  
  this.removeEvent = function (elem, type, fn) {
    elem.removeEventListener(type, fn, false);
  }
} else if (document.attachEvent) {
  this.addEvent = function (elem, type, fn) {
    var bound = function () {
      return fn.apply(elem, arguments);
    };
    elem.attachEvent("on", + type, bound);
    return bound;
  }
  
  this.removeEvent = function (elem, type, fn) {
    elem.detachEvent('on' + type, fn);
  }
  
}
```

##### Event对象

> 我们需要在老版本浏览器里被迫处理的IE Model，在很多方面和DOM Model都不相同。其中之一就是让Event对象的实例在处理程序中可用。

> 如下DOM Model中的一些重要属性，在该过程进行了‘修复’。

* target---表示事件原始源的属性
* relatedTarget---事件触发时的关联元素（如mouseover或者mouseout），在IE中则是toElement和fromElement。
* preventDefault---该属性在IE Model中是不存在的其阻止默认浏览器行为的发生。在IE中阻止默认浏览器行为的发生时，需要将returnValue属性设置为false。
* pageX和pageY---这两个属性在IE Model中不存在。他们提供鼠标相对于整个文档的位置，但可以很容易的从其他信息中获取。在IE中， clientX/Y提供鼠标相对于窗口的位置，而scrollTop/Left则给出了文档滚动的位置，并且clientTop/Left给出了文档的便宜量。综合这三个属性，我们可以得出最后的pageX/Y值。
* which---相当于键盘事件时所按键的键盘码。在IE Model中，可以通过charCode和keyCode属性获取到。
* button---表示鼠标事件发生时，用户单击的鼠标按键。IE Model  使用了位掩码（左单击是1，右单击是2，中间单击是4）所以需要将其转换成DOM Model的等价值（分别是0，1，2）。

```javascript
function fixEvent(event) {
  function returnTrue() {return true;}
  function returnFalse() {return false;}
  
  if (!event || event.stopPropagation) {
    var old = event || window.event;
    
    // Clone the old object so that we can modify the values
    event = {};
    
    for (var prop in old) {
      event[prop] = old[prop];
    }
    
    // The event occurred on this element
    if (!event.target) {
      event.target = event.srcElement || document;
    }
    
    // Handle which other element the event is related to
    event.relatedTarget = event.fromElement === event.target ?
      	event.toElement : event.fromElement;
    
    // Stop the default browser action
    event.preventDefault = function () {
      event.returnValue = false;
      event.isDefaultPrevented = returnTrue;
    }
    
    // Stop the event from bubbling
    event.stopPropagation = function () {
      event.cancelBubble = true;
      event.isPropagationStopped = returnTrue;
    }
    
    event.isPropagationStopped = returnFalse;
    
    // Stop the event from bubblind and executing other handlers
    event.stopImmediatePropagation = function () {
      this.isImmediatePropagationStopped = returnTrue;
     	this.stopPropagation();
    }
    
    event.isImmediatePropagationStopped = returnFalse;
    
    // Handle mouse position
    if (event.clientX != null) {
      var doc = document.documentElement, body = document.body;
      
      event.pageX = event.clientX + 
        (doc && doc.scrollLeft || body && body.scrollLeft || 0) -
        (doc && doc.clientLeft || body && body.clientLeft || 0);
      event.pageY = event.clientY + 
        (doc && doc.scrollTop || body && body.scrollTop || 0) - 
        (doc && doc.clientTop) || body && body.clientTop || 0);
      
    }
    
    // Handle key press 
    event.which = event.charCode || event.keyCode;
    
    // Fix button for mouse clicks;
    // 0 == left; 1 == middle; 2 == right;
    if (event.button != null) {
      event.button = (event.button & 1 ? 0 :
                       (event.button & 4 ? 1: 
                        (event.button & 2 ? 2 : 0)));
      
    }
  }
  return event;
}
```

##### 处理程序的管理

> 不将事件处理程序直接绑定在元素上是有利的。如果我们使用一个中间事件处理程序，并将所有的处理程序都保存在一个单独的对象上，我们可以最大化的控制处理过程。除此之外，我们还能做到以下几点。
>
> * 规范处理程序的上下文
> * 修复Event对象的属性
> * 处理垃圾回收
> * 过滤触发或删除以下处理程序
> * 解绑特定类型的所有事件
> * 克隆事件处理程序

```javascript
// 创建作用域存储对象
(function() {
  var cache = {},
      guidCounter = 1,
      expando = "data" + (new Date()).getTime();
  this.getData = function (elem) {
    var guid = elem[expando];
    if (!guid) {
      guid = elem[expando] = guidCounter++;
      cache[guid] = {};
    }
    return cache[guid];
  }
  
  this.removeData = function(elem) {
    var guid = elem[expando];
    if (!guid) return;
    delete cache[guid];
    try {
      delete elem[expando];
    } catch(e) {
      if (elem.removeAttribute) {
        elem.removeAttribute(expando);
      }
    }
  }
})();
```

##### 绑定事件处理程序

> 编写一个函数来处理绑定事件，而不是直接绑定处理程序，可以让我们有机会来跟踪处理程序并且在处理流程中进行拦截操作。

```javascript
(function(){
  var nextGuid = 1;
  
  this.addEvent = function (elem, type, fn) {
    // getData即为上面函数的getData方法👆
    // 获取相关数据块
    var data = getData(elem);
    // 创建处理程序存储
    if (!data.handlers) data.handlers = {};
    // 使用type创建该type对应的数组
    if (!data.handlers[type])
      data.handlers[type] = [];
    
    // 标记函数
    if (!fn.guid) 
      fn.guid = nextGuid ++ ;
    // 将处理程序添加到列表中
    data.handlers[type].push(fn);
    
    // 创建事件调度器
    if (!data.dispatcher) {
      data.disabled = false;
      data.dispatcher = function (event) {
        if (data.disabled) 
          return;
        // fixEvent在Event对象里有写，用来对事件对象做IE兼容
        event = fixEvent(event);
        // 调用注册的处理程序
        var handlers = data.handlers[event.type];
        if (handlers) {
          for (var n = 0; n < handlers.length; n++) {
            handlers[n].call(elem, event);
          }
        }
      }
    }
    
    // 注册调度器
    if (data.handlers[type].length == 1) {
      if (document.addEventListener) {
        elem.addEventListener(type, data.dispatcher, false);
      } else if (document.attachEvent) {
        elem.attachEvent('on', + type, data.dispatcher);
      }
    }
    
  }
})();
```

##### 解绑事件处理程序



```javascript
function tidyUp (elem, type) {
  // 空对象判断
  function isEmpty(object) {
    for (var prop in object) {
      return false;
    }
    return true;
  }
  
  var data = getData(elem);
  // 检测某一事件类型的处理程序
  if (data.handlers[type].length === 0) {
    delete data.handlers[type];
    if (data.removeEventListener) {
      elem.removeEventListener(type, data.dispatcher, false);
    } else if (document.detachEvent) {
      elem.detachEvent('on' + type, data.dispatcher);
    }
  }
  // 判断是否还有其他事件类型的处理程序
  if (isEmpty(data.handlers)) {
    delete data.handlers;
    delete data.dispatcher;
  }
  if (isEmpty(data)) {
    removeData(elem);
  }
}

this.removeEvent = function (elem, type, fn) {
  var data = getData(elem);
  if (!data.handlers) 
    return;
  var removeType = function(t) {
    data.handlers[t] = [];
    tidyUp(elem, t);
  };
  if (!type) {
    for (var t in data.handlers) 
      removeType(t);
    return;
  }
}
```



##### 事件触发

```javascript
function triggerEvent (elem, event) {
  // 获取元素数据及元素的父元素（用于冒泡）
  var elemData = getData(elem),
      parent = elem.parentNode || elem.ownerDocument;
  // 如果传入的是字符串就为此创建一个event对象
  if (typeof event === 'string') {
    event = {type: event, target: elem}
  }
  // 对event对象进行规范化，fixEvent函数在上面有写
  event = fixEvent(event);
  // 如果传入的元素有事件调度器，就执行该类型的处理程序
  if (elemData.dispatcher) {
    elemData.dispatcher.call(elem, event);
  }
  // 除非显示停止冒泡，一直调用该函数，将事件向上冒泡到DOM上
  if (parent && !event.isPropagationStopped()) {
    triggerEvent(parent, event);
  } else if (!parent && !event.isDefaultPrevented()) {  // 如果DOM到顶了就触发默认行为
    var targetData = getData(event.target);
    // 判断模板元素有没有该事件的默认行为
    if (event.target[event.type]) {
      // 在模板元素上临时禁用事件调度器，因为已经支持了处理程序
      targetData.disabled = true;
      // 执行默认行为
      event.target[event.type]();
      targetData.disabled = false;
    }
    
  }
}
```



##### 冒泡与委托

