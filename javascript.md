## JavaScript 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 引号

使用单引用，这样可以跟 HTML 的双引号更好的一起工作。

### 空白与格式

在二元和三元运算符的符号与操作数之间添加空格，在非行末的 `,` `;` `}` 后添加空格，在 `{` 前添加空格。并在每个逻辑块中间添加空白行：

```js
// 不推荐
var foo='bar',hello=foo+2,test=true;
function hi(){
  // ...
}
if(foo&&hello){
  // ...
}else if(foo){
  // ...
}else if(! test){
  // ...
}

// 推荐
var foo = 'bar';
var hello = foo + 2;
var test = true;

function hi(arg1, arg2) {
  // ...
}

if(foo && hello) {
  // ...
} else if(foo) {
  // ...
} else if(!test) {
  // ...
}
```

### 注释

使用 `//` 作为注释符，可以使用 `/* */` 作为多行注释符。注释的位置尽量放在代码之上：


```js
var foo, hello; // 不推荐

// 推荐
var foo, hello;
```


### 不要为花括号另开一行

```js
// 不推荐
if(foo) 
{
  // ...
}
  
// 推荐
if(foo) {
  // ...
}
```


### var 语句

如果变量有初始赋值则使用单独的 `var`：

```js
// 不推荐
var hello = 1, world = 2;

//推荐
var hello = 1;
var world = 2;
var foo, fee, fxx;
```


### 变量的命名

使用以小写字母开头的驼峰命名（camelCase）法：

```js
// 不推荐
var foo_bar = 'hello eleme';
  
// 推荐
var fooBar = 'hello eleme';
```


### 常量大写

 ```js
// 不推荐
var prefix = 'http://api.ele.me/v1/';
  
// 推荐
var PREFIX = 'http://api.ele.me/v1/';
```


### 使用字面量

```js
// 不推荐
var str = new String('str');
var obj = new Object();
var array = new Array();
  
// 推荐
var str = '';
var  obj = {};
var array = [];
```


### 比较

没有特殊需求的情况下建议使用 `===` / `!==` 而非 `==` / `!=`。

