
## 媒体查询
---

设置mate标签，引入兼容代码，实现响应式布局

```html
<!--  width = device-width    宽度等于当前设备的宽度    -->
<!--  initial-scale           初始的缩放比例            -->
<!--  minimum-scale           允许用户缩放到的最小比例  -->
<!--  maximum-scale           允许用户缩放到的最大比例  -->
<!--  user-scalable           用户是否可以手动缩放      -->

<!-- 响应式布局 -->
<meta name="viewport" content="width=device-width, user-scalable=0, initital-scale=1.0, minimum-scale=1, minimum-scale=1, maximum-scale=1">
<!-- 强制IE浏览器使用最新模式 -->
<meta http-equiv="X-UA-Compatible" content="IE=Edge，chrome=1">
<!-- 强制多核浏览器使用 webkit 内核 (好像只有360支持) -->
<meta name="renderer" content="webkit">
<!-- 让 IE8 能够使用 H5 新标签 -->
<!-- 让 IE8 能实现响应式布局 -->
<!--[if lt IE 9]>
  <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
  <script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
<![endif]-->
```

> 媒体查询该如何使用?

- srceen 表示电脑屏幕，平板设备，智能手机
- min-width: 320px 表示大于320px
- max-width: 640px 表示小于640px

```css
@media only screen and (min-width: 320px) and (max-width: 359px) {
  html {
    font-size: 12.8px;
  }
}
```

<br><br><br>

## 伸缩盒子
---

```css
/*该盒子是一个伸缩盒子*/
display: flex;（给直接父元素）
```

> 设置主轴方向

```css
/*水平方向，从左向右*/
flex-direction: row;
/*水平方向，从右向左*/
flex-direction: row-reverse;
/*垂直方向，从上到下*/
flex-direction: column;
/*垂直方向，从下到上*/
flex-direction: column-reverse;
```

> 设置子元素在主轴的对齐方式

```css
/*向开始的方向对齐*/
justify-content: flex-start;
/*向结束的方向对齐*/
justify-content: flex-end;
/*居中对齐*/
justify-content: center;
/*环绕对齐*/
justify-content: space-around;
/*两边对齐，中间居中*/
justify-content: space-between;
```

> 设置子元素在侧轴的对齐方式

```css
/*侧轴开始的*/
align-items: flex-start;
/*结束方向*/
align-items: flex-end;
/*居中*/
align-items: center;
/*拉伸*/
align-items: stretch;
```

> 控制是非换行显示

```css
/*默认不换行*/
flex-wrap: nowrap;
/*换行*/
flex-wrap: wrap;
```

> 换行后的对齐方式

```css
/*整体向开始方向对齐*/
align-content: flex-start;
/*整体向结束方向对齐*/
align-content: flex-end;
/*整体居中显示*/
align-content: center;
/*整体环绕*/
align-content: space-around;
/*整体两笔对齐，中间居中*/
align-content: space-between;
/*整体拉伸*/
align-content: stretch;
```

> 伸缩布局中元素的相关属性

```css
/*排序，order值越大，子元素越靠后*/
order: 1;
/*用来设置子元素在父元素中的所占比例*/
.b1 {
  flex: 1;
}
.b2 { /*等比例分成三份*/
  flex: 2;
}
```

<br>
<br>
<br>

## Flexible
---

Flexible 是目前手机淘宝团队使用的移动适配方案，原理是通过js来调整html的字体大小，然后通过rem来实现响应式布局

<br>

##### **准备工作**

- 方案1 使用阿里云CDN （推荐用法）

```js
<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
```

- 方案2 通过github下载到本地

`https://github.com/amfe/lib-flexible`

```js
// 然后引入其中的js文件
<script src="index.min.js"></script>
```

<br>

##### **rem布局原理**

rem 是相对于根元素的字体大小的单位

假设我们的设计稿的宽度是320px，而 html 的 font-size 大小设置为32px，则 1rem 则等于32px

<table style="text-align: center;">
<tbody>
<tr>
<td>设备宽度</td>
<td>320px</td>
<td>375px</td>
<td>414px</td>
<td>640px</td>
</tr>
<tr>
<td>根元素字体大小</td>
<td>32px</td>
<td>37.5px</td>
<td>41.4px</td>
<td>64px</td>
</tr>
<tr>
<td>实际输入的rem</td>
<td>1 rem</td>
<td>1 rem</td>
<td>1 rem</td>
<td>1 rem</td>
</tr>
<tr>
<td>页面实际显示的大小</td>
<td>32px</td>
<td>37.5px</td>
<td>41.4px</td>
<td>64px</td>
</tr>
</tbody>
</table>

这样可以清晰的看到，rem的值并不是固定的，他是根据视窗的宽度变化进行自动调整的，这样不同的屏幕宽度，也可以看到相似的效果

##### **注意事项**

段落或文本的字体大小最好使用px作为单位，这是为了避免rem换算之后产生13px、15px、17px这样令人尴尬的尺寸

!> `flexible`会根据不同的设备添加不同的`data-dpr`值，对此，就可以使用`data-dpr`来进行区分不同`dpr`下的文本字体大小

```css
/* 默认dpr为1时的字体大小 */
div {
 width: 1rem; 
 height: 0.4rem;
 font-size: 12px; 
}
/* dpr为2时的字体大小 */
[data-dpr="2"] div {
 font-size: 24px;
}
/* dpr为3时字体的大小 */
[data-dpr="3"] div {
 font-size: 36px;
}
```

设备像素比`（device pixel ratio）`简称为`dpr`，其公式为

> 设备像素比 ＝ 物理像素 / 设备独立像素

!> 在js中，可以通过`window.devicePixelRatio`获取到当前设备的dpr。然后通过CSS的`-webkit-device-pixel-ratio`，`-webkit-min-device-pixel-ratio`和`-webkit-max-device-pixel-ratio`进行媒体查询，对不同dpr的设备做适配

当然也可以通过代码进行强制指定 dpr 的值，不过并不推荐这样做

```html
<meta name="flexible" content="initial-dpr=1" />
```