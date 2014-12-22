## HTML 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 统一符号

* 所有标签和属性名称一律小写。<br/>
  理由：如果不这么做可能导致与 Angular 的不兼容。
* 属性值一律使用双引号。<br/>
  理由：统一是必须的，难道会有人想统一成单引号？

### 可省略部分

* 在没有特殊需求的情况下不省略可选的结束标签。<br/>
  理由：这样更容易看出标签的范围，但是要注意下面这种特殊情况。

```html
<style>
li { display: inline-block; }
</style>
<ul>
  <li>1</li>
  <li>2</li>
</ul>
<ul>
  <li>1
  <li>2
</ul>
```

* 不省略可选的自结束标签末尾斜杠。<br/>
  理由：它会影响到外部标记语言的解析。

```html
<svg width="200" height="200">
  <!-- 如果此处 rect 末尾没有斜杠会产生嵌套关系，使 circle 无法显示 -->
  <rect width="200" height="200" fill="#000" />
  <circle cx="100" cy="100" r="100" fill="#fff" />
</svg>
```

* 建议自结束标签包含属性时在结束的斜杆前面加空格。<br/>
  理由：这是 XHTML 规范？其实我只是觉得这样比较漂亮。

```html
<input type="text" />
<hr/>
```

* 建议无值属性不写等号和值。<br/>
  理由：这个真没必要写，不过 DOM 操作时可能会写。

```html
<input type="checkbox" checked />
<script src="···" async defer></script>
```

* 所有 `<a>` 必须有 `href` 属性，如果用不到可以置为 `href="JavaScript:"`。<br/>
  理由：`href` 不是可选属性，只是浏览器能解析而已。

### 声明相关

* 使用 `<!DOCTYPE html>` 作为唯一的 DTD。<br/>
  理由：它简洁，并能在所有浏览器触发标准模式。
* 使用 `<meta charset="UTF-8" />` 指定文件编码。<br/>
  理由：只设置 `charset` 即可，不需要 `Content-Type`。
* 所有页面必须有 `<title>`，并尽可能地在不同页面使用不同的标题。<br/>
  理由：传统 SEO 考量，对于单页应用也可以增加用户体验。

### 结构相关

* 尽可能地简化 HTML 结构。<br/>
  理由：太复杂的结构难以维护。
* 严格遵守标签嵌套规则，禁止让标签出现在不正确的地方。<br/>
  理由：规范没有约束，未来版本可能不兼容。

```html
<!-- 禁止 -->
<dl>
  <dt>...</dt>
  <ul>
    <li>...</li>
  </ul>
</dl>

<!-- 允许 -->
<dl>
  <dt>...</dt>
  <dd>
    <ul>
      <li>...</li>
    </ul>
  </dd>
</dl>
```

### DOM 相关

* 建议不使用 Level 0 的事件绑定。<br/>
  理由：Level 0 的事件绑定是非规范的，而且容易发生冲突。

```html
<!-- 不建议 -->
<button id="btn" onclick="onBtnClick()">ELE</button>
<script>
var onBtnClick=function() {
  // ...
};
// 不建议
btn.onclick = onBtnClick;
</script>
```

但是，`addEventListener` / `attachEvent` 需要做兼容处理，推荐使用框架封装。

```js
// jQuery 方案
$("#btn").click(function() {
  // ...
});
```

```html
<!-- Angular 方案 -->
<button id="btn" ng-click="onBtnClick()">ELE</button>
```

* 不在视图中处理复杂逻辑，事件处理代码过长时做成函数。<br/>
  理由：在视图中堆积逻辑会影响代码阅读。

```html
<!-- 不推荐 -->
<button id="btn" ng-click="'此处省略100字'">ELE</button>
```
```html
<!-- 推荐 -->
<button id="btn" ng-click="onBtnClick()">ELE</button>
```
```js
module.controller('foo', ['$scope', function($scope) {
  // ...
  $scope.onBtnClick = function() {
    '此处省略100字';
  };
}]);
```

### 其它建议

* 给图片添加 `alt` 属性。
* 给无文字超连接添加 `title` 属性。
* 给可视听的替换型元素内添加描述。

```html
<audio>这是一段神奇的音效</audio>
<canvas>这是一个神奇的效果</canvas>
<iframe src="http://ele.me">这是 ele.me 的首页</iframe>
```
