## JavaScript 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 引号

使用单引号，这样可以跟 HTML 的双引号更好的一起工作。

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

使用 `//` 作为注释符，可以使用 `/* */` 作为多行注释符。注释符号与注释内容之间留空，注释的位置尽量放在代码之上：

```js
/*不推荐*/
//不推荐
; // 不推荐

/* 推荐 */
// 推荐
; 
```

建议在今后需要完善的代码中注释以 `// TODO`。

```js
if(true) {
  console.log("尚未实现");
  // TODO
}
```

### 不要为大括号另开一行

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

// 只有一行语句时允许不带括号
if(foo) doSomething();
for(var i = 0; i < 10; i++) doSomething();

// 语句太长时允许写成两行，但建议写在同一行
for(var i = 0; i < 10; i++)
  doSomething(aaaa, bbbb, cccc, dddd, eeee);
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
var Prefix = 'http://api.ele.me/v1/'
  
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
var obj = {};
var array = [];
```

### 比较

建议使用 `===`/`!==` 而非 `==`/`!=`。

```js
// 不推荐
function foo(a) {
  if(a == 123) {
    // ...
  }
}

// 推荐
function foo(a) {
  a = Number(a);
  if(a === 123) {
    // ...
  }
}
```

`==` 的规则比较复杂，大家可能记不住。


```js
var a = '';

// false
if(a === 0);

// true
if(a == 0);
```

对于可能不存在的全局引用可以先做如此判断：

```js
if(typeof localStorage !== 'undefined'){
  // 此时访问 localStorage 绝对不会出现引用错误
};
```

或者

```js
if('localStorage' in self){
  // 此时访问 localStorage 绝对不会出现引用错误
};
```

但注意它们的区别

```js
var a = undefined;

// true
// 判断一个全局变量是否有声明
"a" in self;

// false
// 判断一个变量是否为 undefined 并将未声明的引用作为 undefined 处理
typeof a !== 'undefined';

```

### var 语句

如果变量有初始赋值则使用单独的 `var`：

```js
// 不推荐
var hello = 1, world = 2;

// 推荐
var hello = 1;
var world = 2;
var foo, fee, fxx;
```

### 函数定义

建议使用表达式来定义函数，而不是函数语句。

```js
// 不推荐
function fee(){
  // ...
}

// 推荐
var foo = function() {
  // ...
};
```

因为函数语句是在进入作用域时声明，破坏了程序从上到下的执行顺序。可能出现定义在 `return` 后的情况。

```js
void function() {
  // 此处可以正常使用函数，但逻辑不清晰
  foo();
  
  return null;
  
  function foo() {};
}();

```

只引用一次的函数建议匿名定义，因为名称存在主观因素。

```js
// 不推荐
var foo = function() {
  // ...
};
element.onclick = foo;

// 推荐
element.onclick = function() {
  // ...
};
```

### 自执行函数

```js
// 不推荐
(function() {
  // ...
})();

+function() {
  // ...
}();

// 推荐
~function() {
  // ...
}();

// 推荐
void function() {
  // ...
}();
```

括号和加号不是上下文无关的，可能受到上文缺分号的影响而出现奇怪的问题，这些问题甚至不会报错，极难调试，所以不推荐此种用法，比如：

```js
var a = 1

+function() {
  return 2
}();

// 此处 a 的值为 3 
```

### 避免嵌套过深

可以使用 `Promise` 解决深层嵌套问题：

```js
// 不推荐
async1(function(){
  // TODO 1
  async2(function(){
    // TODO 2
    async3(function(){
      // TODO 3
    });
  });
});

// 推荐
Promise.resolve()
  .then(function() {
    return new Promise(function(resolve) {
      async1(resolve);
    });
  })
  .then(function() {
    // TODO 1
    return new Promise(function(resolve) {
      async2(resolve);
    });
  })
  .then(function() {
    // TODO 2
    return new Promise(function(resolve) {
      async3(resolve);
    });
  })
  .then(function() {
    // TODO 3
  });
```

### 禁止事项

* 禁止使用 `eval`，非用不可时可以使用 `Function` 构造器替代。
* 禁止使用 `with` 语句。
* 禁止在块作用域中使用函数声明语句。

```js
if(true) {
  // 禁止
  function func1() {
    // ...
  }
  // 允许
  var func2 = function(){
    // ...
  };
}
```

* 禁止使用 8 进制词法

```js
// true
if(010 === 8);
```

* 禁止使用 `arguments` 映射

```js
void function(a){
  arguments[0]++;
  // 此处 a 为 2
}(1);
```
