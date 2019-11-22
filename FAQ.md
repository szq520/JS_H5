 ##### 常见问题-常用方法!

>对象替换键值对 ,替换-键名称

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

>ios端fixed定位底部 键盘弹起 ,fixed不生效

````js
1.移动端fixed定位按钮在底部，键盘弹起，底部按钮顶上去
   <v-footer class="vfooter" v-show="isOriginHei"/>
    data() {
       return {
         screenHeight: document.body.clientHeight, // 这里是给到了一个默认值 （这个很重要），
         originHeight: document.body.clientHeight, //默认高度在watch里拿来做比较
         isOriginHei: true // 这个属性是固定定位按钮的显隐开关
       };
     },
	 mounted() {
	     const that = this;
	     window.onresize = () => {
	       return (() => {
	         window.screenHeight = document.body.clientHeight;
	         that.screenHeight = window.screenHeight;
	       })();
	     };
	   },
	   watch: {
	     screenHeight(val) {
	       if (this.originHeight != val) {
	         this.isOriginHei = false;
	       } else {
	         this.isOriginHei = true;
	       }
	     }
	   }
````

  
>iview 打包不显示问题修复

 ```js
  找到 build 目录下 webpack.prod.conf.js 文件，
   rules: utils.styleLoaders({
    sourceMap: config.build.productionSourceMap,
    extract: ture,
    usePostCSS: true
    })
  把extract改成false即可
 ```
 
 >数组对象以指定类型去重
 
 ```js
   function arrayUnique2(arr, name) {
         let hash = {};
         return arr.reduce(function (item, next) {
         hash[next[name]] ? '' : hash[next[name]] = true && item.push(next);
         return item;
         }, []);
       }
   arr = arrayUnique2( 数组,'指定元素');
 ```
 
 