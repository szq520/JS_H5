

> 好乱, 傻傻的分不清, 整理一下...

## 结构伪类选择器
---

```css
/* 第一个元素 */
:first-child {}

/* 最后一个元素 */
:last-child {}

/* 前三个元素 */
:nth-child(-n+3) {}

/* 奇数元素 */
:nth-child(odd) {}

/* 偶数元素 */
:nth-child(even) {}

/* 倒数第n个元素 */
:nth-child(n) {}
```

<br>

## 目标伪类选择器
---

```css
/* 当被锚链接触发时生效 */
:target { 
  color: red; 
}
```

<br>

## 伪元素选择器
---

```css
/* 选中第一行元素 */
::first-line {}

/* 选中第一个字母或汉字 */
::first-letter {}

/* 鼠标选中的一块区域 */
::selection {}
```

<br>

## 伪元素
---

```css
/* 元素之前 */
::after {
content: "";
}

/* 元素之后 */
::before {
content: "";
}
```

<br>

## 伪类
---

```css
/* a标签的样式,但IE低版本不兼容 */
a:link {}

/* a标签访问过后的样式 */
a:visited {}

/* a标签被激活的样式 */
a:active {}

/* 鼠标悬停样式 */
div:hover {}

/* 获取焦点时的样式 */
input:focus {}
```

<br>

## 属性选择器
---

```css
/* 类样式为nav的元素 */
[class="nav"] {}

/* 类样式为nav并且id为true的元素 */
[class="nav"][id="true"] {}

/* 类样式以某字母开头的元素 */
[class^="a"] {}

/* 类样式以某字母结尾的元素 */
[class$="z"] {}

/* 类样式包含某字母的元素 */
[class*="n"] {}
```
