[TOC]


记录一些Less的特性


# 变量


## 声明变量


通过 **@paramName: value** 声明一个变量，如：


```less
@width: 100px;
@height: 10px;
@area: @width * @height;
@color: red;
```


## 使用变量


### 通常当作css的值使用


[**@paramName **](/paramName )** ** 放在css中的value的位置，如：


```less
#header {
  width: @width;
  height: @height;
  background-color: @color;
}
```


### 用在选择器名字


用在选择器上需要加花括号 **@{paramName}** ，如：


```less
@selector-name: header;

.@{selector-name} {
  width: @width;
  height: @height;
}
```


### 用在url路径中


用在路径中同样是 **@{paramName}** 的方式，如：


```less
@image-url: '/assest/img';

#header {
  // 题外话：url中图片写在前面的覆盖写在后面的，本例中 img1 覆盖 img2 
  background-image: url("@{image-url}/img1.jpg"), url("@{image-url}/img2.jpg");
}
```


### 用在import声明中


用在import语法中同样是 **@{paramName}** 的方式， 如：


```less
@theme: "/theme";

@import "@{theme}/light-mode.less";
```


### 用在属性中


用在属性中同样是 **@{paramName}** 的方式，但是要不要加引号，貌似是不用加，因为官方的例子就是不用加， 如：


```less
@property-name-color: color;

#header {
  @{property-name-color}: red;
  background-@{property-name-color}: red;
}
```


### 变量名的连续调用


连续的@符号可以将一个变量的值作为变量名来使用，如：


```less
@primary: red;

.section {
  @color: primary;
  
  .element {
    // 这里会被编译成 color: green
    color: @@color
  }
}
```


### 变量的延迟计算


变量在使用前不需要提前声明，也可以在使用后再声明


```less
.lazy-eval {
  color: @var;
}

@var: @a;
@a: 200px;
```


### 变量的作用域以及覆盖


变量的作用域类似于js的作用域，而当前作用域下的最后一次声明会最终变为变量的值，跟CSS的变量的规则相同，如下：


```less
@var: 0;
.class {
  @var 1;
  .part {
    @var: 2;
    // three: 3;
    three: @var;
    @var 3;
  }
  // one: 1;
  one: @var;
}
```


### 把属性作为变量


使用 **$prop** 语法可以直接把属性作为变量，如：


```less
#header {
  color: red;
  // background-color: red;
  background-color: $color;
}
```


需要注意的是，$prop的写法也会覆盖


```less
.block {
  color: red; 
  .inner {
    // background-color: blue;
    background-color: $color; 
  }
  color: blue;  
}
```


### 变量的覆盖会动态影响函数的计算


```less
@base-color: blue;
@dark-color: darken(@base-color, 10%);

@import "other-libiary.less";
@base-color: red;


#header {
  // 这里的 color 是 dark red
  color: @dark-color;
}
```


# 父类选择器


使用`&`代表父类选择器


```less
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```


### 生成重复的类名


```less

.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
```


### 重复 &


&代表的是嵌套父类以空格间隔，如：


```less

.grand {
  .parent {
    & > & {
      color: red;
    }

    & & {
      color: green;
    }

    && {
      color: blue;
    }

    &, &ish {
      color: cyan;
    }
  }
}
```


会被编译成


```less

.grand .parent > .grand .parent {
  color: red;
}
.grand .parent .grand .parent {
  color: green;
}
.grand .parent.grand .parent {
  color: blue;
}
.grand .parent,
.grand .parentish {
  color: cyan;
}
```


这里 `&`  代表 `.grand .parent`


### 改变选择器顺序


反正 & 代表的是父选择器的拼接，所以基本可以放在任何地方


跟在子选择器后面就改变了选择器的排列顺序，如下：


```less

.header {
  .menu {
    border-radius: 5px;
    .no-borderradius & {
      background-image: url('images/button-background.png');
    }
  }
}
```


### Combinatorial Explosion


> & can also be used to generate every possible permutation of selectors in a comma separated list:



```less

p, a, ul, li {
  border-top: 2px dotted #366;
  & + & {
    border-top: 0;
  }
}
```


会被编译成：


```less

p,
a,
ul,
li {
  border-top: 2px dotted #366;
}
p + p,
p + a,
p + ul,
p + li,
a + p,
a + a,
a + ul,
a + li,
ul + p,
ul + a,
ul + ul,
ul + li,
li + p,
li + a,
li + ul,
li + li {
  border-top: 0;
}
```


# 继承


```less
nav ul {
  &:extend(.inline);
  background: blue;
}
```


会被编译成：


```less
nav ul {
  background: blue;
}
.inline,
nav ul {
  color: red;
}
```


显而易见


> `:extend(.inline)` 会把 `nav ul` 插入到 `inline` 出现的地方



## extend语法


写法有点像伪类, 括号里的 `all` 关键字是可选的, 加上 `all` 关键字有点像数组方法的 `find`


```less
.a:extend(.b) {}

// 或

.a {
  &:extend(.b);
}
```


带 `all` 关键字


```less
.c:extend(.d all) {
  // extends all instances of ".d" e.g. ".x.d" or ".d.x"
  // 选择器里出现 .d 的都会被继承, 如 .x.d 或 .d.x
}
```


若想继承多个选择器可以使用 `,` （逗号） 分隔


```less

.e:extend(.f, .g) {}

// 等同于
.e:extend(.f) {}
.e:extend(.g) {}
```


### 伪类&多个继承


比较复杂的情况，继承必须放在最后


```less
.big-bucket:extend(.bucket),
.big-bucket:extend(div pre), // 继承带选择器
.big-bucket:extend(div pre:hover), // 也可以带伪类
// 允许多个继承, 且extend要放在最后
.big-bag:hover :extend(.bag) :extend(.bag1), {
  // body
}
```


### 规则集（Ruleset可能叫这个名字吧🐶 ）内继承


```less
pre:hover,
.some-class {
  &:extend(div pre);
}

// 相当于

pre:hover:extend(div pre),
.some-class:extend(div pre) {}
```


### 嵌套选择器的继承


```less
.bucket {
  tr { // nested ruleset with target selector
    color: blue;
  }
}
.some-class:extend(.bucket tr) {} // nested ruleset is recognized
```


会被编译成


```less
.bucket tr,
.some-class {
  color: blue;
}
```


### 精细匹配继承


`:extend(.class)` 不会匹配 `.a.class` , `.class.a` ,  `.class > .a` ,  `*.class`


虽然 `link:hover:visited` 和 `link:visited:hover` 作用是相同的, 但是 `:extend(link:visited:hover)` 不会匹配  `link:hover:visited`


#### nth 表达式


nth表达式 `1n+3` 和 `n+3` 是相同的，但是 `:extend(:nth-child(n+3))` 不会匹配 `:nth-child(1n+3)`


#### 属性选择器


```less
[title=identifier] {
  color: blue;
}
[title='identifier'] {
  color: blue;
}
[title="identifier"] {
  color: blue;
}

.noQuote:extend([title=identifier]) {}
.singleQuote:extend([title='identifier']) {}
.doubleQuote:extend([title="identifier"]) {}
```


会被编译成


```less
[title=identifier],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title='identifier'],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title="identifier"],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}
```


### `all` 关键字


```less
.a.b.test,
.test.c {
  color: orange;
}
.test {
  &:hover {
    color: green;
  }
}

.replacement:extend(.test all) {}
```


会被编译成


```less
.a.b.test,
.test.c,
.a.b.replacement,
.replacement.c {
  color: orange;
}
.test:hover,
.replacement:hover {
  color: green;
}
```


### 带变量的继承


**如果选择器带变量，那么将不会继承！**


如：


```less
@variable: .bucket;
@{variable} { // interpolated selector
  color: blue;
}
.some-class:extend(.bucket) {} // does nothing, no match is found

// 或

.bucket {
  color: blue;
}
.some-class:extend(@{variable}) {} // interpolated selector matches nothing
@variable: .bucket;
```


但是继承语句跟在变量选择器的后面是可以的


如：


```less
.bucket {
  color: blue;
}
@{variable}:extend(.bucket) {}
@variable: .selector;
```


会被编译成


```less
.bucket, .selector {
  color: blue;
}
```


### @media标签内的继承


> 目前，`:extend` 只会匹配在相同 `@media` 标签中的声明



```less
@media print {
  .screenClass:extend(.selector) {} // extend inside media
  .selector { // 这里是起作用的
    color: black;
  }
}
// 下面的不起作用
.selector { 
  color: red;
}
@media screen {
  .selector {
    color: blue;
  }
}
```


上面会被编译成


```less
@media print {
  .selector,
  .screenClass { /*  ruleset inside the same media was extended */
    color: black;
  }
}
.selector { /* ruleset on top of style sheet was ignored */
  color: red;
}
@media screen {
  .selector { /* ruleset inside another media was ignored */
    color: blue;
  }
}
```


[@media ](/media ) 嵌套的情况也不会起作用 


```less
@media screen {
  .screenClass:extend(.selector) {} // extend inside media
  @media (min-width: 1023px) {
    .selector {  // 这里认为不在同一个@media内
      color: blue;
    }
  }
}
```


**但是，写在最顶层的继承规则会在@media中起作用**


例如：


```less
@media screen {
  .selector {  /* ruleset inside nested media - top level extend works */
    color: blue;
  }
  @media (min-width: 1023px) {
    .selector {  /* ruleset inside nested media - top level extend works */
      color: blue;
    }
  }
}

.topLevel:extend(.selector) {} /* top level extend matches everything */
```


会被编译成


```less
@media screen {
  .selector,
  .topLevel { /* ruleset inside media was extended */
    color: blue;
  }
}
@media screen and (min-width: 1023px) {
  .selector,
  .topLevel { /* ruleset inside nested media was extended */
    color: blue;
  }
}
```


### 重复检查


很遗憾，目前不会做重复检查


```less
.alert-info,
.widget {
  /* declarations */
}

.alert:extend(.alert-info, .widget) {}
```


会被编译成


```less
.alert-info,
.widget,
.alert,
.alert {
  /* declarations */
}
```


# 合并


merge 特性允许将多个属性中的值聚合到耽搁属性下，对 background 和 transform 很有用


```less
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}

.mixin() {
  transform+_: scale(2);
}
.myclass {
  .mixin();
  transform+_: rotate(15deg);
}
```


会被编译成


```less
.myclass {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}

.myclass {
  transform: scale(2) rotate(15deg);
}
```


# 嵌套指令和冒泡


`media` 或 `keyframe` 也能作为选择器被嵌套使用，指令会被放到顶部，并且会保持与其他选择器的排列顺序，如：


```less

.screen-color {
  @media screen {
    color: green;
    @media (min-width: 768px) {
      color: red;
    }
  }
  @media tv {
    color: black;
  }
}
```


会被编译为


```less

@media screen {
  .screen-color {
    color: green;
  }
}
@media screen and (min-width: 768px) {
  .screen-color {
    color: red;
  }
}
@media tv {
  .screen-color {
    color: black;
  }
}
```


# Mixins


## 重用已有的样式


### 常规用法


```less

.a, #b {
  color: red;
}
.mixin-class {
  // .a; 同样生效, 但不推荐, 可能会在以后的版本中去掉
  .a();
}
.mixin-id {
  #b();
}
```


### 只用作mix


如果希望一个样式单纯的用做mix，就用圆括号结尾，如：


```less
.my-mixin {
  color: black;
}
// 不会被编译成css
.my-other-mixin() {
  background: white;
}
.class {
  .my-mixin();
  .my-other-mixin();
}
```


上述代码会被编译成：


```less
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
```


### 命名空间


命名空间可以减少命名冲突，也是组织mix的一种方式


```less
#outer() {
  .inner {
    color: red;
  }
}

.c {
  #outer > .inner();
  // 以下写法有同样的效果
  // #outer > .inner();
	// #outer .inner();
	// #outer.inner();
}
```


### 受保护的明明空间


如果明明空间受保护，那么只有当条件返回为true时才会使用由它定义的mixin


```less
#namespace when (@mode = huge) {
  .mixin() { /* */ }
}

#namespace {
  .mixin() when (@mode = huge) { /* */ }
}
```


`default` 函数会假定所有的嵌套和mixin有同样的值


```less
#sp_1 when (default()) {
  #sp_2 when (default()) {
    .mixin() when not(default()) { /* */ }
  }
}
```


### !import 关键字


mixin后面加 `!import` 会给所有的属性都加上


```less
.foo (@bg: #f5f5f5, @color: #900) {
  background: @bg;
  color: @color;
}
.unimportant {
  .foo();
}
.important {
  .foo() !important;
}
```


会被编译成


```less
.unimportant {
  background: #f5f5f5;
  color: #900;
}
.important {
  background: #f5f5f5 !important;
  color: #900 !important;
}
```


### mixin传参
mixin 接收参数
```less
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
// 参数也可以有默认值
.border-radius(@radius: 5px) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```
使用这个带参数的mixin
```less

#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
```
​

