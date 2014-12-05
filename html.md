## HTML 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### 细则

* 尽可能地简化 HTML 结构。<br/>
  理由：太复杂的结构难以维护。
* 所有标签和属性名称一律小写。<br/>
  理由：如果不这么做可能导致与 Angular 的不兼容。
* 属性值一律使用双引号。<br/>
  理由：统一是必须的，难道会有人想统一成单引号？
* 在没有特殊需求的情况下不省略可选的结束标签。<br/>
  理由：这样更容易看出标签的范围，但是要注意下面这种特殊情况。
  
```HTML
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
```HTML
<svg width="200" height="200">
  <!-- 如果此处 rect 末尾没有斜杠会产生嵌套关系，使 circle 无法显示 -->
  <rect width="200" height="200" fill="#000" />
  <circle cx="100" cy="100" r="100" fill="#fff" />
</svg>
```
* 建议自结束标签包含属性时在结束的斜杆前面加空格。<br/>
  理由：这是 XHTML 规范？其实我只是觉得这样比较漂亮。
```HTML
<input type="text" />
<hr/>
```
* 建议无值属性不写等号和值。<br/>
  理由：这个真没必要写，不过 DOM 操作时可能会写。
```HTML
<input type="checkbox" checked />
<script src="···" async defer></script>
```
