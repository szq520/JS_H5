## 什么是BFC
---

?> `定义`: BFC是一种属性, 是一个独立的块级渲染区域, 该区域可以独立的约束块级盒子的布局, 且与外部区域无关

- BFC的形成条件

  - 浮动元素

  - 绝对定位元素

  - `display: inline-block` `table-cells` `table-captions`

  - `overflow`除了默认属性`visible`以外的值

- BFC的作用

  - `清除浮动`

  - 不被浮动元素所覆盖

  - 阻止外边距`margin`塌陷

<br>
<br>
<br>

## 标准模式(Quirks)和怪异模式(Standards)的区别
---

- 定义

  - 标准模式是浏览器按W3C标准解析代码
  - 怪异模式是低版本IE使用的解析渲染方式

- 区别

  - `盒模型尺寸的计算方式不同`

    - 标准模式的宽度就是内容的宽度
    - 怪异模式的宽度是内容宽度+内边距+边框宽度

  - `行内元素宽高`

    - 标准模式下行内元素设定不起效果
    - 怪异模式下设置宽高是有效果的

  - `字体样式继承`

    - 标准模式下字体样式可以继承
    - 怪异模式下`table`元素的字体样式不能继承

<br>
<br>
<br>

<!--
## CSS 尺寸属性
---

| 属性 | 描述
| --- | ---
| height | 设置元素高度
| max-height | 设置元素的最大高度
| max-width | 设置元素的最大宽度
| min-height | 设置元素的最小高度
| min-width | 设置元素的最小宽度
| width | 设置元素的宽度

<br>

## Font 字体属性
---

| 属性 | 描述
| --- | ---
| font | 在一个声明中设置所有字体属性
| font-family | 规定文本的字体系列
| font-size | 规定文本的字体尺寸
| font-style | 规定文本的字体样式
| font-weight | 规定字体的粗细
-->

<br>

## 盒子模型
---

| 属性 | 描述
| --- | ---
| border | 在一个声明中设置所有的边框属性
| border-radius | 边框圆角
| margin | 在一个声明中设置所有外边距属性
| padding | 在一个声明中设置所有内边距属性
| box-shadow | 向方框添加一个或多个阴影

```
none 无边框
hidden 隐藏边框 IE不支持
solid 实线
double 双边框
dotted 点线
dashed 虚线
```

<br>

## background
---

| 属性 | 描述 |
| --- | ---
| background | 在一个声明中设置所有的背景属性
| background-attachment | 设置背景图像是否固定或者随着页面的其余部分滚动
| background-color | 设置元素的背景颜色
| background-image | 设置元素的背景图像
| background-position | 设置背景图像的开始位置
| background-repeat | 设置是否及如何重复背景图像
| background-clip | 规定背景的绘制区域
| background-origin | 规定背景图片的定位区域
| background-size | 规定背景图片的尺寸

<br><br><br>

## 文本溢出隐藏
---

> 单行文本隐藏

```css
/* 核心代码 */
p {
 overflow: hidden;
 text-overflow:ellipsis;
 white-space: nowrap;
}
```

!> 效果展示如下，需要注意一点！那就是父容器必须有宽度，不然内容仍然会撑开容器

<p style="width: 300px; border: 1px solid red; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">Vue是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。</p>
<p style="width: 300px; border: 1px solid red; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">jQuery是一个高效、精简并且功能丰富的 JavaScript 工具库。它提供的API易于使用且兼容众多浏览器，这让诸如HTML文档遍历和操作、事件处理、动画和Ajax操作更加简单。</p>
<p style="width: 300px; border: 1px solid red; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">Zepto是一个轻量级的针对现代高级浏览器的JavaScript库，它与jQuery有着类似的API。 如果你会用 jQuery，那么你也会用Zepto。</p>

<br><br>

> 多行文本隐藏（只兼容webkit）

```css
p {
 display: -webkit-box;
 -webkit-box-orient: vertical;
/* 指定显示多少行 */
 -webkit-line-clamp: 3;
 overflow: hidden;
}
```

!> 效果展示如下，在第三行的结尾处，多余的文字被隐藏起来，但是该效果暂时只兼容webkit内核的浏览器

<p style="width: 300px; border: 1px solid red; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 3; overflow: hidden;">Vue是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。</p>
<p style="width: 300px; border: 1px solid red; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 3; overflow: hidden;">jQuery是一个高效、精简并且功能丰富的 JavaScript 工具库。它提供的API易于使用且兼容众多浏览器，这让诸如HTML文档遍历和操作、事件处理、动画和Ajax操作更加简单。</p>
<p style="width: 300px; border: 1px solid red; display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 3; overflow: hidden;">Zepto是一个轻量级的针对现代高级浏览器（移动端）的JavaScript库，它与jQuery有着及其类似的API。 如果你会用 jQuery，那么你也会用Zepto。</p>

<br><br><br>

## placeholder 兼容代码

```css
/* 兼容谷歌和Opera */
input::-webkit-input-placeholder {
  color: red;
}
/* 兼容火狐 19+ */
input::-moz-placeholder {
  color: red;
}
/* 兼容火狐 4-18 */
input:-moz-placeholder {
  color: red;
}
/* 兼容IE Edge */
input::-ms-input-placeholder {
  color: red;
}
/* 兼容IE 10-11 */
input:-ms-input-placeholder {
  color: red;
}
```


