
## 微信开发常见问题

 ##### 小程序常见问题
```js
1. 小程序域名必须是：https;
2. wx.navigateTo无法跳转tabar的页面，必须使用wx.switchTab跳转
3. 去掉button的灰色圆角边框 :button::after{dispaly:none} （主要是button的伪元素设置了样式）
4. 微信小程序ios端overflow:auto滚动卡顿
  (1)overflow:auto;-webkit-overflow-scrolling: touch;
  (2)<scroll-view scroll-y style="height: 200px;"></scroll-view> 
     <!--使用 scroll-view 一定要给height-->
    
```

```js
 5.微信小程序底部菜单栏 
      buttonclick: function () {
          wx: wx.showActionSheet({//底部菜单栏可覆盖导航栏
            itemList: ['item1', 'item2', 'item3'],
             itemColor: '',
             success: function (res) {
              if (!res.cancel) {
                console.log(res.tapIndex);
               }
              },
              fail: function (res) { },
            complete: function (res) { },
        })
      }, 

```

```js
6.
```


```
7.
```