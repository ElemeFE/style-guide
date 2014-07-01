## JavaScript Style Guide

### 1. 引号

使用单引用，这样可以跟 HTML 的双引号更好的一起工作。

### 2. 空白

在 `=` 和各类操作符 ( `&&` `||` `+` 等) 的前后添加空格，在非行末的 `,` `;` `}` 后添加空格，在 `{` 前添加空格。并在每个逻辑块中间添加空白行：

```js
// 不推荐
var foo='bar',hello=foo+2;
function hi(){
  // ...
}
if(foo&&hello){
  // ...
}else if(foo){
  // ...
}else{
  // ...
}

// 推荐
var foo = 'bar', hello = foo + 2;

function hi(arg1, arg2) {
  // ...
}

if(foo && hello) {
  // ...
} else if(foo) {
  // ...
} else {
  // ...
}
```

### 3. 注释

使用 `//` 作为注释符，可以使用 `/* */` 作为多行注释符。注释的位置尽量放在代码之上，非不是代码行内：


```js
var foo='bar',hello=foo+2; // 不推荐

  
// 推荐
var foo = 'bar', hello = foo + 2;
```


### 4. 不要为花括号另开一行

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


### 5. 变量的命名

使用以小写字母开头的驼峰命名（camelCase）法：

```js
// 不推荐
var foo_bar = 'hello eleme';
  
// 推荐
var fooBar = 'hello eleme';
```


### 6. 常量大写

 ```js
// 不推荐
var prefix = 'http://api.ele.me/v1/';
  
// 推荐
var PREFIX = 'http://api.ele.me/v1/';
```


### 7. 避免嵌套太深

```js
// 不推荐
$(document.body).on('click', function() {
  $.get('/user', function doSomething(user) {
    // ...
  });
});

// 推荐
var doSomething = function(user) {};

$(document.body).on('click', function() {
  $.get('/user', doSomething);
});
```

### 8. 使用字面量

```js
// 不推荐
var str = new String('str')
  , obj = new Object()
  , array = new Array();
  
// 推荐
var str = '', obj = {}, array = [];
```


### 9. 比较

比较两个值的时候，尽可能使 `===` / `!==` 而非 `==` / `!=`。`===` 是更严格的方式，包括对比两个值的类型。


### 10. 条件判断

不需要直接对变量 `foo == true` 或者 `bar != false` 做这样的比较，你可以直接在条件判断中使用变量：

```js
// 不推荐
if(foo == true) alert('hello world');
  
// 推荐
if(foo) alert('hello world');
```

不过，如果判断的是一个不一定存在的变量，则最好先判断其是否存在：

```js
// 不推荐
if(localStorage) {}
  
// 推荐
if(typeof localStorage !== 'undefined') {}
```