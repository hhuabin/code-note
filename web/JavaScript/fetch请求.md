# fetch 关注分离的设计思想

1. 联系服务器
2. 将信息封装在 response.json() 中



## 基本用法

```javascript
fetch('/api1/users/search')
.then(response => {
    console.log('联系服务器成功了');
    return response.json()
},error => {
    console.log('联系服务器失败了',error);
    return new Promise(()=>{})
})
.then(response => {
    console.log('获取数据成功了',response);
},error => {
    console.log('获取数据失败了',error);
})
```

部分优化：

```javascript
fetch('/api1/users/search')
.then(response => {
    console.log('联系服务器成功了');
    return response.json()
})
.then(response => {
    console.log('获取数据成功了',response);
})
.catch(error => {
    console.error(error);
})
```

请求优化：

```javascript
try {
    const response= await fetch('/api1/users/search')
    const data = await response.json()
    console.log(data);
} catch (error) {
    console.log('请求出错',error);
}
```



### 响应类型

**JSON 响应**：

```javascript
response.json().then(data => console.log(data));
```

**文本响应**：

```javascript
response.text().then(text => console.log(text));
```

**Blob (二进制) 响应**：

```javascript
response.blob().then(blob => {
    const url = URL.createObjectURL(blob);
    console.log(url);
});
```

**FormData 响应**：

```javascript
response.formData().then(formData => console.log(formData));
```



## 请求方法

`fetch` 默认使用 `GET` 方法。如果你需要使用其他方法，比如 `POST`、`PUT`、`DELETE`，可以通过传递第二个参数对象来指定



## POST

```javascript
fetch('https://api.example.com/data', {
    method: 'POST',   // 请求方法
    headers: {
    	'Content-Type': 'application/json',  // 指定发送 JSON 数据
    },
    body: JSON.stringify({
        name: 'John',
        age: 30
    }),  // 请求体内容
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));


fetch('https://api.example.com/data', {
    method: 'POST',            // HTTP 请求方法，例如：GET, POST, PUT, DELETE
    headers: {                 // 请求头信息，指定数据格式
        'Content-Type': 'application/json', 
        'Authorization': 'Bearer token',  // 如果需要 token 认证
    },
    body: JSON.stringify({
        title: 'Post title',
        body: 'Post content'
    }),                        // 请求体，发送数据
    mode: 'cors',              // 跨域请求设置，默认 'cors'
    credentials: 'include',    // 携带 cookie，'omit' 表示不携带，'same-origin' 表示同源携带
    cache: 'no-cache',         // 缓存模式，例如：default, no-cache, reload, force-cache
    redirect: 'follow',        // 重定向模式，例如：manual, follow, error
    referrerPolicy: 'no-referrer',  // 引用策略
})
.then(response => {
	if (!response.ok) {
		throw new Error(`HTTP error! Status: ${response.status}`);
    }
	return response.json()
})
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

- mode

  1. **`cors`**（默认）：允许跨域请求，但要求服务器允许（通过设置 `Access-Control-Allow-Origin` 头）
  2. **`no-cors`**：允许跨域请求，但你无法读取响应内容，只能用于加载图片、脚本等静态资源，不能用于获取 JSON 数据
  3. **`same-origin`**：要求请求的资源与页面来源相同，否则请求会被阻止

  如果服务器没有配置跨域，那么mode配置成什么都不好使，一般使用默认的`cors`即可



## 取消请求

虽然 `fetch` 本身不提供取消请求的机制，但你可以通过 `AbortController` 来实现取消请求的功能

```javascript
const controller = new AbortController();
const signal = controller.signal;

fetch('https://api.example.com/data', { signal })
.then(response => response.json())
.then(data => console.log(data))
.catch(error => {
    if (error.name === 'AbortError') {
    	console.log('请求被取消');
    } else {
    	console.error('Fetch error:', error);
    }
});

// 取消请求
controller.abort();
```

