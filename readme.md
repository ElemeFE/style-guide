## 饿了么代码格式指南

**It's dangerous to go alone**，为了更好的协作，在新生产的代码或者在约定生效之后被修改的旧代码，作如下约定：

- 缩进：不混用 space 和 tab，在前端代码中使用 2-spaces 缩进
- 编码：UTF-8 ( no BOM ) 
- 在需要后续修改的代码，最好注释 TODO

```js
// TODO: blah blah bla...
function hello() {
  // ...
}
```

### # 前端相关

- Style Guide: [HTML](html.md) / [CSS](css.md) / [JavaScript](javascript.md)
- 兼容浏览器
  <table>
  <tr><th>平台</th><th>浏览器</th></tr>
  <tr><td>**Desktop**</td><td>IE8+ / FireFox / Chrome / Safari</td></tr>
  <tr><td>**Mobile**</td><td>WP8+ / Mobile Safari</td></tr>
  </table>
