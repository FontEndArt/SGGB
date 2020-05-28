# css 如何实现动画

CSS动画是由 transition 和 animation (过渡 和 动画) 这两大部分组成的.


## Transition
Transition 主要为样式的改变提供一个补间动画用来过渡. 在 CSS 引入 transition 这个概念之前, CSS是没有时间轴这个概念的, 所有的改变, 都是即时完成的.

CSS3 Transition (过渡) 是元素从一种样式逐渐改变为另一种的效果。

要实现过渡效果, 至少要规定两点:

- 规定你想要把动画效果添加到哪个属性上
- 规定动画效果的时长


具体的使用语法如下:

```css
img {
    transition: 1s 1s height ease;
    /* 语法: transition: property duration timing-function delay; */
}

img{
    transition-property: height; // 属性
    transition-duration: 1s; // 动画时长
    transition-delay: 1s; // 延时等待时长
    transition-timing-function: ease; // 动画的时间曲线
    transition-timing-function: cubic-bezier(.83,.97,.05,1.44); // 动画的时间曲线可以使用贝塞尔函数
}
```


比如我们想要让鼠标进入box的时候, box的宽度由100px变为200px, 离开时恢复原状, 则示例如下:

```css
.box {
    transition: 1s 1s height ease;
    /* 语法: transition: property duration timing-function delay; */
}

```


CSS提供了 Animate 来进行一些复杂动画