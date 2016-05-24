
## Ajax 代码风格

#### 期待解决的问题

Ajax 请求目前项目有 `ng-resource` `vue-resource` `fetch` `XMLHttpRequest` 多种写法,
风格对阅读代码还协作开发有影响, 增加维护成本.

#### 推荐的解决方案

Fetch API 已经做到了很多的改进, 建议新项目以 `fetch` 为主处理 Ajax 请求.
但是在之上还加代码风格的约束, 方便阅读和维护代码.

Angular 项目中 `ng-resource` 使用不受影响.

推荐方案(初稿):

## Fetch API 参考文档

* fetch API https://davidwalsh.name/fetch
* Basic Fetch Request https://developers.google.com/web/updates/2015/03/introduction-to-fetch
* Using Fetch https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
* Fetch Living Standard https://fetch.spec.whatwg.org/#authentication-entries

## 建议写法

没有 options 参数的写法:

```js
fetch(`${APIHOST}/url/api`)
.then(function(response) {
	console.log(response.json());
}).catch(function(error) {
});
```

有 options 参数的写法:

```js
let options = {
  method: 'POST',
  body: JSON.stringify({
    name: info.name,
    phone: info.phone,
    address: info.address
  })
}

fetch(`${APIHOST}/users/${userId}/a/${id}`, options)
.then(function(response) {
	console.log(response.json());
}).catch(function(error) {
});
```

带 query string 的写法:

```js
fetch(`${APIHOST}/v1/init?a=${a}&b=${b}`)
.then(response => resolveFetch(response));

// 如果较长
var query = {
  latitude: latitude,
  longitude: longitude
};
fetch(`${APIHOST}/v1/init?${utils.queryString(query)}`)
.then(response => resolveFetch(response));
```

## 细节

```js
// 用声明式写法, 避免 options.x=y 写法
let options = {
  method: 'POST',
  body: JSON.stringify({
    name: info.name,
    phone: info.phone,
    address: info.address
  })
}

// fetch 的 url 要写明确, 保证看到 fetch 能马上看明白 url
fetch(`${APIHOST}/users/${userId}/a/${id}`, options)
// then, catch 写在一行开头, 避免出现在后面看不清楚
.then(function(response) {
	console.log(response.json());
}).catch(function(error) {
});
```

## 其他

有些共用代码需要抽象的, 看需要, 后面也尝试相互保持统一,
建议提交 `eleme-fetch-utils` 模块共同维护:

* 拼接 query string 的函数
* 管理 APIHOST 的函数
* 生成 `fetch` 的 options 参数中公用的参数
* ...
