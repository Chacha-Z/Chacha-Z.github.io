---
title: Store.subscribe思考-用法、源码
date: 2021-03-23 21:41:03
categories:  
    - 前端
tags: 
	- React	
	- Redux
comments: true
---

Store.subscribe思考-用法、源码
<!--more-->

#### Axios安装

```
npm install axios --save
```

当组件输出到 DOM 后会执行 componentDidMount()钩子，也就是说我们可以在componentDidMount()内请求数据，并更新数据。请求的数据要放在state。

> 如遇CORS报错，在服务器端配置CORS
>
> 参考：https://blog.csdn.net/xxxxxxxxyz/article/details/99304796
>
> ​			https://www.jianshu.com/p/1a277d16cfdd

#### 发送单个请求

```
axios.post("http://ip:port/path", 
    {
		d: data
    },
).then((res)=>{
	console.log(res)
})
```

```
axios.post({
	method: 'POST',
	url: 'http://ip:port/path',
	data: {
		d: data
	},
}).then((res)=>{
	console.log(res)
})
```

```
const request = axios.create({
	baseURL: 'http://ip:port'
})
request({
	method: 'POST',
	url: '/path',
	data: {
		d: data
	},
}).then((res)=>{
	console.log(res)
})
```

#### 发送多个请求

```
axios.all([
	axios.get('http://IP:port/path'), 
	axios.get('http://IP:port/path'), 
	axios.get('http://IP:port/path')
]).then(axios.spread((res1, res2, res3) => {
        let rawData1 = res1.data.results
        let rawData2 = res2.data.results
        let rawData3 = res3.data.results
      })
).catch(function (error) {
        console.log(error);
      })
```

