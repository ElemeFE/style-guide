## SASS 代码风格

### 基本设置

* 2 空格缩进
* UTF-8 编码

### zindex使用规范

`zindex.scss` 用来统一项目中的 z-index 值，方便管理 z-index 的层级关系，避免 z-index 的值过大或者层级相互覆盖。

```SASS
$zindexlist:
  searchbox                /* 搜索框 */
  premiumsign              /* 在rstblock中显示的品牌馆图标 */
  dropbox                  /* 显示信息的hover浮动框 */
  sidebar                  /* 右侧栏 */
  toolbardropbox           /* 右侧栏显示信息的hover浮动框 */
  modalshade               /* 浮动弹出框遮罩 */
  modal                    /* 浮动弹出框 */
```

`$zindexlist` 中的数组元素决定 z-index 值，从上到下 z-index 值越大，层级越高。

#####使用方法：

```SASS
@include zindex($ele);
```

* `$ele` 参数值，需要在 `$zindexlist` 中定义数组元素，注意变量的位置；
* 也可以使用 `$zindexlist` 中的已经定义的数组元素，但需要注意以后增删改不会有影响；
* 只支持正数，负数还是按照普通的方式。