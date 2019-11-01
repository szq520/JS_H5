#### 开发常见问题

```js
1. 对象替换键值对 ,替换-键
  let data= {id:11,name: "张三"}
  let keyMap = {id: "序列",name: "姓名"}
  let objs = Object.keys(data).reduce((newData, key) => {
  	let newKey = keyMap[key] || key
  	newData[newKey] = data[key]
  	return newData
  }, {})
  console.log(objs) //{序列: 11, 姓名: "张三"}
```