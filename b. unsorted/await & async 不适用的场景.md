##### 引言
尽管 await & async 方便了异步场景的书写，但在一些场景里，滥用该语法糖也会引起：
- 代码的执行效率，影响用户体验；
- 降低代码的可读性；

##### 分析
我们知道，await、async 是 ES6 出的语法糖，让我们可以用一种更简洁的方式写出基于[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)的异步行为，而无需刻意地链式调用`promise`。

```js
// 执行顺序 a=> b => c => d
let sort = 0

let asyncCall = (val, time) => {
	return new Promise(resolve => {
		setTimeout(() => {
			console.timeEnd(val)
			console.log(sort += 1, val)
			resolve()
		}, time)
	})
}

let a = () => asyncCall('a', 2000)
let b = () => asyncCall('b', 1500)
let c = () => asyncCall('c', 1000)
let d = () => asyncCall('d', 500)

// promise 的实现风格
a().then(() => {
	b().then(() => {
		c().then(() => {
			d().then(() => {})
		})
	})
})

// await 实现风格
await a()
await b()
await c()
await d()
```

当习惯使用 await 后，执行顺序稍加改变，你可能会写出这样的代码：

``` js
// a => b, c => d

;['a', 'b', 'c', 'd'].forEach(id => {
  console.time(id)
})

await a()
b()
await c()
d()

// 执行结果
a => 2s
c => 3s
b => 3.5s
c => 3.5s

// 分析结果
b、c、d => 都等待了 a 

// 转换成 promise 等同效果
a().then(() => {
	b().then()
	c().then(() => {
		d().then()
	})
})

// 建议直接写成
a().then(() => {
	b().then()
})
c().then(() => {
	d().then()
})

// 如果使用 await
let ab = async () => {
	await a()
	b()
}
let cd = async () => {
	await c()
	d()
}

ab()
cd()

```

##### 总结
await & async 

- 不适用于多个异步对的场景；
- 在多个异步对的场景下，用 promise 的回调写法可提高代码可读性；