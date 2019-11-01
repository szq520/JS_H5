## 引入外部字体

```css
@font-face {
  font-family: "YourFont";
  src: url(http://www.yoursite.com/siyuanfont.otf);
}
p {
  font-family: "YourFont", Helvetica, Arial;
}
```

!> 不建议这么引用，如此引用字体会导致用户在打开网页时需要加载几十MB的字体文件，这对于用户体验是灾难性的。中文字体的 web fonts 技术还不成熟，到目前也有几家公司提供这样的服务，英文字体由于一共就24个字母加上一些符号，所以 web fonts 比较流行。

<br><br><br>

## 线性渐变和径向渐变
---

> 线性渐变

```css
/* (渐变角度, 起始颜色 范围, 结束颜色 范围) */
background-image: linear-gradient(90deg, yellow 0%, green 50%, blue 100%);
```

> 径向渐变

```css
/* (水平半径 垂直半径 at 圆心横坐标 圆心纵坐标, 起始颜色, 结束颜色) */
background-image: radial-gradient(600px at 100px 50px, yellow, green);
```

<br><br><br>

## css动画与过渡
---

```css
/*设置要调用动画的名称*/
animation-name: move;
/*动画执行的时间*/
animation-duration: 2s;
/*执行次数 (infinite|1)*/
animation-iteration-count: 3;
/*等待时间*/
animation-delay: 1s;
/*匀速执行动画*/
animation-timing-function: linear;
/*动画逆波*/
animation-direction: alternate;
/*设置动画执行时间之外的状态(原地停止)*/
animation-fill-mode: forwards;

/*鼠标悬停的时候暂停*/
.box:hover {
  animation-play-state: paused;
}

@keyframes move {
  form {
    transform: translateX(0px);
  }
  to {
    transform: translateX(300px);
  }
}
```

#### 过渡（补间动画）

> 过渡属于一种特殊的动画

```css
/* 参与过渡的属性 */
transition-property: all;
/* 设置过渡执行的事件 */
transition-duration: 2s;
/* 过渡执行的速度类型 */
transition-timing-function: linear | ease | ease-in | ease-out | ease-in-out;
/* 过渡延迟执行时间 */
transition-delay: 2s;
```

> 一般过渡是不会这样分着写的，过于冗余，而是像下面这样连写

```css
/* 过渡连写(过渡属性, 执行时间, 延迟时间, 速度类型) */
transition: all 5s 1s linear;
/* 多个过渡特效 */
transition: width 1s ease, height 1s 1s ease;
```

<br><br><br>

## 2D转换与3D转换
---

#### 2D转换 transform

> 位移

```css
/* 位移(水平方向, [垂直方向]) */
transform: translate(50%);
```

!> 小技巧：translate可以搭配绝对定位实现块元素水平居中

```css
div {
  position: absolute;
  left: 50%;
  transform: translate(-50%);
}
```

> 旋转

```css
/* 旋转(旋转原点默认是元素的中心) */
transform: rotate(30deg);
```

这个旋转原点的位置也是可以更改的

```css
/* 设置旋转原点(可以设置center、px、半分比) */
transform-origin: 50px 50px;
```

> 缩放

```css
/* 缩放(两个值时表示宽度和高度) */
transform: scale(1.5);
```

> 倾斜（了解）

```css
/* 倾斜(倾斜也可以指定倾斜原点) */
transform: skew(30deg);
```

!> 2d转换这些属性也可以连写，但顺序会影响其转换效果

#### 3D转换

> 3D转换需要给父元素添加一条属性，才能有比较明显的效果

```css
/* 透视(一般是添加给父元素) */
perspective: 1000px;
```
透视可以将一个2D平面，在转换的过程当中，呈现3D立体的效果

> 透视有两种写法

- 作为一个属性，设置给父元素，作用于所有3D转换的子元素
- 作为transform属性的一个值，做用于元素自身

> 3d位移

```
/* 3d位移(分别对应x轴, y轴, z轴进行位移) */
transform: translateX(10px);
transform: translateY(20px);
transform: translateZ(30px);
/* 3d位移连写(x, y, z) */
transform: translate3d(10px, 20px, 30px);
```

> 3d旋转

```css
/* 3d旋转(分别是x,y,z轴旋转) */
transform: rotateX(45deg);
transform: rotateY(45deg);
transform: rotateZ(45deg);
/* 3d旋转连写 */
transform: rotate3d(45deg, 45deg, 45deg);
```

> 3d缩放（了解）

```css
/* 3d缩放 */
transform: scaleX(0.5);
transform: scaleY(0.5);
transform: scaleZ(0.5);
/* 3d缩放连写 */
transform: scale3d(0.5, 0.5, 0.5);
```

> 3d倾斜（了解）

```css
/* 3d倾斜 */
transform: skewX();
transform: skewY();
```

#### 左手坐标系

!> 左手大拇指（Z轴）指向自己，食指（X轴）指向右侧，中指（Y轴）指向下方

<br><br><br>

## 渐变色字体、镂空字体

> 文件渐变色的宽度或高度，取决于父级块元素的宽高

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
  .box {
    /* 渐变颜色 */
    background:-webkit-linear-gradient(top,#fff,#000);
    /* 使文字产生镂空效果 */
    -webkit-background-clip:text;
    /* 使字体变的透明 */
    -webkit-text-fill-color:transparent;
  }
  </style>
</head>
<body>
  <div class="box"><h1>这行字体是渐变色</h1></div>
</body>
</html>
```

!> 经过测试，谷歌火狐可以兼容并使用，IE11 和 IE Edge 则给我们翻了个白眼
