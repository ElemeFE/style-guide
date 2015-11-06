## JavaScript 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 严格模式

建议打开严格模式，但不要依赖严格模式中语言特性的变化（仅当需要支持 IE8、IE9 时）

```js
'use strict';
```

### 引号

使用单引号，这样可以跟 HTML 的双引号更好的一起工作。

### 分号

在语句（Statement）的结尾加分号

```js

// 不建议
var fn = function() {
  // Long code
} // 没有分号

// 建议
var fn = function() {
  // Long code
}; // 这里有分号

```

以防万一，在可能有坑的地方手工加分号

```js

var f1 = function ff1() {
  return function() {
    return 1;
  };
} // 此处漏写分号
(function() { // 此处调用了上面的ff1，WAT
})();
console.log(f2); // 1

var f2 = function ff2() {
  return function() {
    return 1;
  };
} // 此处漏写分号
// IIFE
;(function() { // 注意前面的分号
})();
console.log(f2); // function

```

或者使用 `void function() {}()` 的写法，见下

### 空白与格式

在二元和三元运算符的符号与操作数之间添加空格，在非行末的 `,` `;` `}` 后添加空格，在 `{` 前添加空格。并在每个逻辑块中间添加空白行。
特别的，在 if、while 等关键字后加空格，与函数调用做区分

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

if (foo && hello) {
  // ...
} else if (foo) {
  // ...
} else if (!test) {
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

建议在今后需要完善的代码中注释以 `// TODO`。请在 TODO 后标注你要做的事

```js
if (condition) {
  console.log('尚未实现');
  // TODO: condition 成立时需要做额外的工作
}
```

### 不要为大括号另开一行

```js
// 不推荐
if (foo)
{
  // ...
}

// 推荐
if (foo) {
  // ...
}

// 不允许
return
{
  a: 1
};

// 一定要
return {
  a: 1
};
```

只有一行语句时允许不带括号，但需把语句紧跟当前行后

```js
if (foo) doSomething();
for (var i = 0; i < 10; i++) doSomething();
```

语句太长时写成两行，这时请加大括号

```js

// 不推荐
for (var i = 0; i < 10; i++)
  doSomething(aaaa, bbbb);

// 推荐
for (var i = 0; i < 10; i++) {
  doSomething(aaaa, bbbb);
}

// 因为某些人调试时喜欢注释代码，于是就出现了
for (var i = 0; i < 10; i++)
  // doSomething(aaaa, bbbb);

```

写 `else` 时不要另起一行

```js

// 不推荐
if (test) {
  things1();
  things2();
}
else {
  things3();
}

// 推荐
if (test) {
  things1();
  things2();
} else {
  things3();
}

```

### var 语句

#### 使用变量之前必须先定义，不要定义全局变量。

```js

// 变量 undefinedVar 从未定义过
undefinedVar = 1; // 严格模式中报错
console.log(global.undefinedVar); // 1

// 鉴于 js 中 var 的坑，可以在函数头统一定义所有变量（不强制，我也讨厌把变量定义堆一起。。。）
void function () {
  for (var i = 0; i < arr.length; ++i) {
    (function () {
      console.log(i); // undefined

      // 很长的代码，你已经忘记了之前做了什么
      for (var i = 0; i < 10; ++i) {
        // Do some other things
      }
    })();
  }
}();

// 小心 var 与 closure 合用时的坑
var elements = [ div1, div2, div3 ];
for (var i = 0; i < elements.length; ++i) {
  elements[i].addEventListener('event', function() {
    console.log(i); // 3
  });
}
```

#### 如果变量有初始赋值则使用单独的 `var`：

```js
// 禁止
var hello = 1, world = 2;

// 推荐
var hello = 1;
var world = 2;
var foo, fee, fxx;
```

另外强调，禁止使用下面这种风格的变量定义方式。

```js
// 禁止
var hello = arr.pop(),
    world = arr.pop();
```

```js
// 禁止
var hello = arr.pop()
  , world = arr.pop();
```

原因：

1. 当需要修改变量定义顺序时不容易做整行移动
2. 过不了 eslint 的 indent 验证

#### 变量的命名

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
// 不建议
var obj = new Object();
var array = new Array();

// 推荐
var obj = {};
var array = [];

// 鉴于 Array 构造函数的特殊性，不建议
var arr1 = new Array(4, 5, 6); // [4, 5, 6]

// 以免与下面混淆
var arr2 = new Array(4); // [ undefined * 4 ]
// 等价于（不推荐）
var arr3 = [];
arr3.length = 4;
// 等价于（不推荐）
var arr4 = [,,,,];
console.log('0' in arr2, '0' in arr3, '0' in arr4); // false, false, false

// 不推荐
var str = new String('str');
console.log(str === 'str'); // false

var bool = new Boolean(false);
if (bool) console.log('wat'); // wat

// 当真需要使用字面量包装类时，使用显式强制转换（请先三思）
var strObject = Object('str');
strObject.customProperty = someValue;

```

### 比较

建议使用 `===`/`!==` 而非 `==`/`!=`。

```js

// 不推荐
function foo(a) {
  if (a == 123) {
    // ...
  }
}

// 推荐
function foo(a) {
  a = Number(a);
  if (a === 123) {
    // ...
  }
}

```

`==` 的规则比较复杂，大家可能记不住。

```js
var a = '';

// false
if (a === 0);

// true
if (a == 0);
```

对于可能不存在的全局引用可以先做如此判断：

```js
if (typeof localStorage !== 'undefined') {
  // 此时访问 localStorage 绝对不会出现引用错误
}
```

或者

```js
if ('localStorage' in self) {
  // 此时访问 localStorage 绝对不会出现引用错误
}
```

但注意它们的区别

```js

var a = undefined;

// 判断一个全局变量是否有声明
'a' in self; // true

// 判断一个变量是否为 undefined 并将未声明的引用作为 undefined 处理
typeof a !== 'undefined'; // false

```

### 避免无必要的 `if` 语句、三元运算符

```js

var arr = [1, 2, 3];

// 不推荐
var flag1 = arr.length > 0 ? true : false;

// 不推荐
var flag2;
if (arr.length > 0) {
  flag2 = true;
} else {
  flag2 = false;
}

// 推荐
var flag3 = arr.length > 0;

```

### 合理的格式化三元运算符

```js

// 不推荐
var flag1 = veryLooooooooooonnnnggggggCondition ? resultWhenTruth : resultWhenFalsy;

// 推荐
var flag2 = veryLooooooooooonnnnggggggCondition
              ? resultWhenTruth
              : resultWhenFalsy;

```

### 复杂逻辑中建议使用显式转换

```js

+num === Number(num);
!!bool === Boolean(bool);
str + '' === String(str);

// 特别的
if (bool)
// 等价于
if (Boolean(bool))
// 故
if ([]) console.log('true'); // true
// 而
if ([] === true) console.log('true'); // 无输出

// 另外
if (Boolean(String(false))) console.log('true'); // true
// 这点在保存 localStorage 时需要注意

```

不要使用 parseInt 做整数转换，如需使用 parseInt，请给它传入第二个参数 10，避免老式浏览器的坑（IE8？）

```js
var floatValue = 123.456;

// 不要
var intValue = parseInt(floatValue);

// 可以用
var intValue2 = floatValue | 0;

// 更显然的
var intValue3 = Math.floor(floatValue);

```

特别地，使用 parseFloat 做部分转换

```js

// 例如有：
// <div id="div" style="width: 10px"></div>

var divWidth = getComputedStyle(document.getElementById('div')).width; // '10px'

console.log(parseFloat(divWidth)); // 10
console.log(Number(divWidth)); // NaN
console.log(+divWidth); // NaN

```

### 函数定义

建议使用表达式来定义函数，而不是函数语句。

```js
// 不推荐
function fee() {
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
var a = 1 // 此处无分号

+function() {
  return 2
}();

// 此处 a 的值为 3
```

### 避免嵌套过深

可以使用 `Promise` 解决深层嵌套问题：

```js
// 不推荐
async1(function() {
  // TODO 1
  async2(function() {
    // TODO 2
    async3(function() {
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

* 禁止使用未定义的变量
* 禁止使用 `eval`，非用不可时可以使用 `Function` 构造器替代。
* 禁止使用 `with` 语句。
* 禁止在块作用域中使用函数声明语句。

```js
if (true) {
  // 禁止
  function func1() {
    // ...
  }
  // 允许
  var func2 = function() {
    // ...
  };
}
```

* 禁止使用 8 进制词法

```js
// true
if (010 === 8);
```

* 禁止使用 `arguments` 映射

```js
void function(a) {
  arguments[0]++;
  // 此处 a 为 2
}(1);
```

* 禁止使用重名参数
* 禁止使用保留字做变量名如 `interface` 等
