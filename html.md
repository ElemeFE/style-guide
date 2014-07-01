## HTML/Template Style Guide

在实际项目中，HTML 大多由模板生成，在「饿了么」我们使用 [Twig](http://twig.sensiolabs.org/) 作为后端输出的模板。


### 1. DTD

使用 `<!DOCTYPE html>` 作为唯一的 DTD，简洁，并能在所有浏览器触发标准模式。

### 2. 使用双引号

```html
<!-- 不推荐 -->
<button ng-click='hi(":)")'>Hi</button>

<!-- 推荐 -->
<button ng-click="hi(':)')">Hi</button>
```

### 3. 编码

在 `<head>` 中明确指定文件编码 `<meta charset="UTF-8">`。

### 4. 标签

在 HTML 文档的所有标签和属性应小写：

```html
<!-- 不推荐 -->
<A HREF="http://ele.me" TITLE="饿了么">ELE.ME</A>

<!-- 推荐 -->
<a href="http://ele.me" title="饿了么">ELE.ME</a>
```

尽可能保持标签的闭合：自闭合标签无需添加结尾的斜杆 `/`：

```html
<!-- 不推荐 -->
<p>hello world

<!-- 推荐 -->
<p>hello world</p>
```

```html
<!-- 不推荐 -->
<meta charset="UTF-8" />

<!-- 推荐 -->
<meta charset="UTF-8">
```

另外，在保持语义的同时，请用尽可能少标签来编写的的结构：

```html
<!-- 不推荐 -->
<ul>
  <li>
    <span>Lorem Ipsum</span>
    <p>Neque porro quisquam est qui dolorem ipsum quia dolor sit amet</p>
  <li>
  ...

<!-- 推荐 -->
<ul>
  <li>Lorem Ipsum
    <p>Neque porro quisquam est qui dolorem ipsum quia dolor sit amet</p>
  <li>
  ...
```

### 5. 语义

恰当地使用标签，标题对应 `h1~6`，引用对应 `blockquote`，简单的表格请直接使用 `table`，而不是到处 `div/span`：

```html
<!-- 不推荐 -->
<div>ELE.ME Code Style Guide</div>
<div>The description is blah blah blah....</div>

<!-- 推荐 -->
<h1>ELE.ME Code Style Guide</h1>
<p>The description is blah blah blah....</p>
```

语义是呈现形式，也包含行为，比如 `a` 被设计为页面之间的联系，在能用它来进行跳转的情况下，尽可能按照浏览器行为来编写代码，不要使用其他替代方式：

```html
<!-- 不推荐 -->
<div onclick="window.location = http://ele.me">ELE.ME</a>

<!-- 推荐 -->
<a href="http://ele.me">ELE.ME</a>
```

### 6. 分离表现与行为

尽可能不要添加行内样式和脚本，你可以定义一个钩子（如 `class="abc"`）以便在 CSS 或者 JS 中对其进行样式和行为的定义：

```html
<!-- 不推荐 -->
<div onclick="alert(this.textContent)" style="color:red" class="abc">ELE.ME</a>
<style>.abc{font-size: 12px}</style>

<!-- 推荐 -->
<div class="abc"></div>
```
