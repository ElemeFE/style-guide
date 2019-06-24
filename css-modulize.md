## CSS 模块化命名规则

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 声明

兼容 IE 8 以上浏览器。

### 基本命名

**类名使用完整英文单词或抽掉空格的英文词组。**

```CSS
/* 推荐 */
.module {}
.helloworld {}

/* 不推荐 */
.konnichiwa {} /* 非英文单词会导致大家无法正常阅读 */
.modl {} /* 每个人的缩写未必一致，会造成不统一 */
.hello-world {} /* 类名请只使用一个没有分隔[-_]的词 */
```

驼峰写法或下划线分割单词的写法都存在一个问题，我们的主观无法判断单词的分割。比如`yellowgreen`这个单词，如果使用分单词的写法可能被写成`yellowGreen`或`yello_green`，造成风格不统一。

当然，抽掉空格也会带来另外的问题，比如`a synchronous request`和`asynchronous request`的意思是完全相反的，这时候抽掉空格就会出问题。不过这种情况是开发者们可以主动避免的，在代码 review 时也可以找出存在歧义的命名。

另外，在能确保准确描述目标元素的情况下，尽可能地让类名更加简短。

```CSS
.form-submit {} /* 推荐 */
.form-submittingbutton {} /* 不推荐 */
```

组件名称尽量使用名词或抽掉空格的名词性词组，这样可以降低冲突的可能性。

**有且仅当有层级关系时使用“-”连接，比如组件内的元素类名采用组件名“-”子类名的形式：**

```HTML
<div class="uploader">
  <input type="text" class="uploader-text" />
  <input type="button" class="uploader-button" />
</div>
```

这时选择器在 CSS 中应该平行地定义，以便降低优先级，便于覆写。

```CSS
.uploader {}
.uploader-text {}
.uploader-button {}
```

不要求类名的层级结构和 HTML 保持一致。

```HTML
<div class="grid">
  <div>
    <div class="grid-caption">
      <div class="grid-caption-text"></div>
      <div class="grid-caption-button"></div>
    </div>
  </div>
  <ul class="grid-row">
    <li class="grid-cell"></li>
  </ul>
</div>
```

允许模块穿插使用。

```HTML
<div class="header">
  <div class="container"> <!-- 穿插一个别的组件 -->
    <div class="header-logo"></div>
    <div class="header-nav"></div>
  </div>
</div>
```

但不建议在高层级中放置低层级元素，这样会破坏逻辑。

```HTML
<div class="module">
  <div class="module-caption">
    <div class="module-caption-content"> <!-- 推荐:低层嵌入高层 -->
      <div class="module-text"></div> <!-- 不建议:高层嵌入低层 -->
    </div>
    <!-- 允许:同级嵌套 -->
    <div class="module-captioncontent">
      <div class="module-text"></div>
    </div>
  </div>
</div>
```

### 保持结构灵活性

我们的设计应该尽可能地让样式可以用于更多标签。

```HTML
<style>
.section {}
.section-head {}
.section-body {}
</style>
<div class="section">
  <div class="section-head"></div>
  <div class="section-body"></div>
</div>
<dl class="section">
  <dt class="section-head"></dt>
  <dd class="section-body"></dd>
</dl>
```

甚至可以任意调整结构。

```HTML
<style>
.article {}
.article-main {}
.article-title {}
</style>
<div class="article">
  <div class="article-main">
    <div class="article-title">
      <!-- ... -->
    </div>
    <!-- ... -->
  </div>
</div>
<div class="article">
  <div class="article-title">
    <!-- ... -->
  </div>
  <div class="article-main">
    <!-- ... -->
  </div>
</div>
```

### 样式修饰

一个组件可能有多种状态多种样式，可以在组件上添加修饰符来选择所需的样式。

在先前的命名规范中“-”被用于表示组件与其后代元素的关系。如果此处再使用“-”，逻辑上可能造成混乱。

考虑到这些修饰符可能和组件名冲突，在词法上推荐使用状态名词或形容词。

```HTML
<div class="popup success">
  blah blah blah
</div>
<div class="popup warning">
  blah blah blah
</div>
<div class="popup error">
  blah blah blah
</div>
```

在选择器中使用多类来声明其样式。

```CSS
.popup.success {}
.popup.warning {}
.popup.error {}
```

这样可以避免嵌套的冲突问题。
