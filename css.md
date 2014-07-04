# ELEME CSS/LESS/SASS Style Guide

1. [基本约定](1.-基本约定)
2. [书写规范](2.-书写规范)
3. [命名](3.-命名)
4. [组织](4.-组织)
5. [注释](5.-注释)
6. [HACK](6.-HACK)

## 1. 基本约定

- js用class必须只能用下划线`_`来分割单词：`.submit_btn`
- css样式用class必须用连字符`-`分割单词：`.rst-comment-btn`
- js/css共用class必须加`.ui_`前缀并且只能用下划线`_`分割单词：`.ui_disabled`
- 在css里尽量避免用id，以便class覆盖，少用`!important`

## 2. 书写规范

1. 缩进**1 tab = 2 spaces**。
2. 选择器和`{`之间必须有空格，`display:`和value间必须有空格，`}`必须单独一行。
    ``` css
    // DEPRECATED
    .block{
    display:block;
    background:white;}

    // RECOMMENDED
    .block {
      display: block;
      background: white;
    }
    ```
3. 有引号的情况下都用双引号：`content: ""`、`url("")`、`font-family: "Microsoft Yahei"`等。
    ``` css
    // DEPRECATED
    .block {
      background-image: url(path/to/img);
      font-family: 'Microsoft Yahei', sans-serif;
    }
    .block:after {
      content: '';
      clear: both;
    }

    // RECOMMENDED
    .block {
      background-image: url("path/to/img");
      font-family: "Microsoft Yahei", sans-serif;
    }
    .block:after {
      content: "";
      clear: both;
    }
    ```
4. 在可以合并的时候合并写多个properties。
    ``` css
    // DEPRECATED
    .block {
      border-top-left-radius: 3px;
      border-top-right-radius: 2px;
      border-bottom-right-radius: 1px;
      border-bottom-left-radius: 0px;
      font-weight: bold;
      font-size: 16px;
      line-height: 1.6;
      font-family: "Helvetica Neue", Arial, sans-serif;
    }

    // RECOMMENDED
    .block {
      border-radius: 3px 2px 1px 0;
      font: bold 16px/1.6 "Helvetica Neue", Arial, sans-serif;
    }
    ```
5. 过多层级影响渲染效率，所以尽量把class层级控制在三层内。
    参考：[efficiently rendering css](http://css-tricks.com/efficiently-rendering-css/)、[css explan](https://josh.github.io/css-explain/)。
    ``` scss
    // DEPRECATED
    form {
      padding: 10px;
        div {
          margin: 10px 0;
            label {
              position: relative;
                [type="radio"] {
                  display: none;
              }
          }
        }
    }

    // RECOMMENDED
    .form {
      padding: 10px;
    }
    .form-group {
      margin: 10px 0;
     }
    .form-label {
      position: relative;
    }
    .form-radio {
      display: none;
    }
    ```
6. 有嵌套时，优先写`&:hover`等伪类，其次`&.class`，再次`> .class`，最次`  .class `
    ``` sass
    // EXAMPLE
    .block
      background: black
      color: white
      &:hover
        background: gray
      &.clicked
        background: wheat
      > .title
        font-size: 2em
      .highlight
        font-weight: bold
    ```
7. 在写`.css`/`.less`/`.scss`时，多重value尽量分行写。
    由于目前`.sass`的严格缩进问题，暂时不支持这类格式化分行缩进。
    ``` scss
    // DEPRECATED
    $colors: (default: blue, success: green, warning: orange, error: red);
    .block {
      background: white;
      box-shadow: 0 0 0 rgba(#000, 0.1), 1px 1px 0 rgba(#000, 0.2), 2px 2px 0 rgba(#000, 0.3), 3px 3px 0 rgba(#000, 0.4), 4px 4px 0 rgba(#000, 0.5);
    }

    // RECOMMENDED
    $colors: (
      default: blue,
      success: green,
      warning: orange,
      error: red
    );
    .block {
      background: white;
      box-shadow: 0 0 0 rgba(#000, 0.1),
                  1px 1px 0 rgba(#000, 0.2),
                  2px 2px 0 rgba(#000, 0.3),
                  3px 3px 0 rgba(#000, 0.4),
                  4px 4px 0 rgba(#000, 0.5);
    }
    ```

## 3. 命名

1. 不用拼音
2. 把信息装到名字里，用具体对象名字来命名（patch class除外），不用css样式来命名。
    ``` css
    // DEPRECATED
    .a {}
    .line-one {}
    .yellow-title {}

    // RECOMMENDED
    .user-avater {}
    .introduction {}
    .highlight-title {}
    ```
3. 在class名字太长的时候，可以缩写，缩写规则基本为取单词缩写或首字母。
    ``` sass
    // EXPAMPLE
    /*
     * .restaurant-menu-list
     * => .rst-menu-list || .rmenu-list
     * .profile-user-introduction-text
     * => .pusr-intro-txt || .pusr-itxt
     */
    ```
4. class的第一个单词通常为父级元素或module的名字，避免用常见classname
    ``` css
    // DEPRECATED
    .dish {}
    .user {}

    // RECOMMENDED
    .rst-dish {}
    .fav-dish {}
    .topbar-user {}
    .profile-user {}
    ```

### 通用组件命名

通用组件包括：
- ui类，格式化、模块化的样式库专用class
    ``` css
    // EXAMPLE
    .ui-form {}
    .ui-input {}
    .ui-btn {}
    ```
- 功能类，js中使用的class/id。因为和ui相关，为了在js内和其他class/id做区分，所以带`.ui_`前缀表明有该class有css样式。
    ``` sass
    // EXAMPLE
    .menu-dropdown
      display: none
      &.ui_toggled
        display: block

    .rst-drawer
      position: absolute
      top: 0
      left: 0
      width: 0
      overflow: hidden
      transition: width 0.5s
      &.ui_slidein
        width: 400px
    ```
- 补丁类，只修改某个样式属性，在现有某class基础上做小部分定制
    ``` sass
    // EXAMPLE
    .clear-margin
      margin: 0 !important

    .categ-title
      margin: 0 0 10px
      color: #666
      &.patch-sub
        color: #999
        font-size: 0.8em
    ```
    ``` html
    <h2 class="categ-title">Hello World</h2>
    <h3 class="categ-title patch-sub">Hello World</h3>
    <h4 class="categ-title patch-sub clear-margin">Hello World</h4>
    ```

    但**不能**全用patch class进行写样式
    ``` html
    // DONT
    <div class="p10 mb10 group"></div>
    ```

## 4. 组织

1. 基本css组织方式按照业务逻辑，桌面端除全局一份基础css文件外，一个功能模块一份配置css文件；移动端网站一份css文件；单页活动、app内嵌网页每页一份css。
2. sass项目中，以`module_name.sass`作为一份配置文件（Primary file），实际样式文件放在`ModuleName`文件夹下，并以前缀下划线的方式命名`_file_name.sass`（partial file）。
3. 页面样式比较少的时候，可以不用开folder，直接在配置sass文件内写样式。
4. 每份sass文件尽量控制在100行左右，超过150行的最好考虑拆分sass文件。
5. 灵活组织sass文件保证维护方便。

参考：[How to structure a Sass project](http://thesassway.com/beginner/how-to-structure-a-sass-project)

```
css/
|
|-- base.sass                   # Primary file：全局基础 css 文件，import 了 base/ 文件夹下所有文件
|-- base/                       # 管理全局基础样式库
|   |-- _variables.sass         # 全局变量，比如配色、图片url等
|   |-- _functions.sass         # 基础 sass functions
|   |-- _mixins.sass            # 基础 sass mixins
|   |-- _extends.sass           # 基础 sass extends
|   |-- _eleme_normalize.sass   # 自定义 normalization
|   |-- _controls.sass          # js插件相关样式，如 modal、dropdown 等
|   |-- _commons.sass           # 基础补丁样式，如 .clear-margin, .mtb10, .float-l, .group 等
|   |-- _miscs.sass             # 基础组件样式，如 .site-flash, .symbol-rmb, .caret
|   |-- _icons.sass             # 其他独立组件
|   ...
|
|-- modules_1.sass                      # 对应html或php里某个module的module配置文件
|-- modules_1/                          # module 样式库
|   |-- _base.sass                      # 该module 内基础样式
|   |-- _page_1.sass                    # module内的page，如果module只有一个页面，则可以为页面内的partial。
|   |-- _page_2.sass                    # 同上
|   |-- page_folder/                    # 如果单页内容比较多，如餐厅页，可以增加二级文件夹来管理sass
|   |   |-- _page_partial.sass          # 页面内的partial
|   |   ...
|   ...
|
|-- vendor/               # 库文件
|   |-- _normalize.scss
|   |-- _jquery.ui.core.scss
|   ...
...
```

## 5. 注释

1. 模块注释用`/* ... */`， 单行注释用`// ...`
    ``` sass
    /*
     * Linear Gradient Mixin
     *
     * browser support: webkit, webkit legacy, standard
     * with flat background fallback
     */
    =linear-gradient($deg, $color1, $color2, $fallback: "")
      // getMiddleColor() returns one middle color
      background-color: getMiddleColor($c1, $c2, $fallback)
      ...
    ```
2. 开发过程中经常使用使用关键字`TODO`、`FIXME`、`XXX`
    ```
    /* TODO: How about auto-correcting small spelling errors? */
    /* FIXME: This won't work if the file is missing. */
    /* XXX: This method badly needs refactoring: should switch by core type. <mbp> */
    ```


## 6. HACK

1. 能不写hack就不写hack，IE下的排版问题大多是代码里的问题，并不一定需要hack，从重写代码入手解决。
2. 只在用css3的新特性时考虑hack，并且正确使用modernizr进行优雅回退。

* * *
欢迎完善指正补充。
