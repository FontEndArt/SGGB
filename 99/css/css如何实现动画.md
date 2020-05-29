# css 如何实现动画

CSS动画是由 transition 和 animation (过渡 和 动画) 这两大部分组成的.


## Transition
Transition 主要为样式的改变提供一个补间动画用来过渡. 在 CSS 引入 transition 这个概念之前, CSS是没有时间轴这个概念的, 所有的改变, 都是即时完成的.

CSS3 Transition (过渡) 是元素从一种样式逐渐改变为另一种的效果。


### 使用 Transition 的注意事项
要实现过渡效果, 至少要规定两点:

- 规定你想要把动画效果添加到哪个属性上

- 规定动画效果的时长


### 语法

具体的使用语法如下:

```css
img {
    transition: 1s 1s height ease;
    /* 语法: transition: property duration timing-function delay; */
}

img{
    transition-property: height; // 属性(all指的是全部属性变化的时候都会播放过渡动画)
    transition-duration: 1s; // 动画时长
    transition-delay: 1s; // 延时等待时长
    transition-timing-function: ease; // 动画的时间曲线
    transition-timing-function: cubic-bezier(.83,.97,.05,1.44); // 动画的时间曲线可以使用贝塞尔函数
}
```

### 应用场景

比如我们想要让鼠标进入box的时候, box的宽度由100px变为200px, 离开时恢复原状, 则示例如下:

```css
.box {
    transition: 1s 1s height ease;
    /* 语法: transition: property duration timing-function delay; */
}
```

## Animation
除了 Transition 以外 CSS还提供了 Animation 来进行一些复杂的动画.

**动画是使元素从一种样式逐渐变化为另一种样式的效果。**

Animation 是CSS3增加的属性, 用来给元素增加动画.

**你可以使用动画改变任意多的样式任意多的次数。**

我们通常通过 `@keyframes AnimateName {}` 来定义一个动画, 然后使用 Animation 属性来调用它.


### Animation 的基本用法

```css
.box {
    animation: move 5s infinite;
    /* 语法: animation: name duration timing-function delay iteration-count direction; */
}
```

animation 属性是一个简写属性，用于设置六个动画属性：

- animation-name

    + keyframename | none (定义的动画 keyframe 的名称 | 无动画效果)

    + 我们定义的动画名称

- animation-duration

    + time ( 1s | 100ms )

    + 默认值 0;

    + 完成动画所花费的时间, 以秒或者毫秒计

- animation-timing-function

    + linear | ease | ease-in | ease-out | ease-in-out | cubic-bezier(n,n,n,n) 

        + linear: 从头到尾速度相同

        + ease: 默认动画效果, 从低速开始加速, 在结束前变慢.

        + ease-in: 动画以低速开始

        + ease-out: 动画以低速结束

        + ease-in-out: 动画以低速开始和结束

        + cubic-bezier(n,n,n,n): 贝塞尔曲线, 其中的 n 可能的值是 0-1的数值

    + 完成动画的动画曲线

- animation-delay

    + time ( 1s | 100ms )

    + 默认值 0;

    + 动画开始之前的延迟

- animation-iteration-count

    + num | infinite (播放次数的数值 | 无限播放);

    + 动画应该播放的次数

- animation-direction

    + normal | alternate (正常播放 | 反向轮流)

    + 是否轮流反向执行动画, 比如一个块从左到右完成一个运动动画, 结束后是否从右到左返回

- animation-play-state

    + paused | running (动画已暂停 | 动画正在播放);

    + 可以在js中这样使用来暂停动画: `object.style.animationPlayState="paused"`

    + 规定动画正在运行还是暂停

- animation-fill-mode

    + none | forwards | backwards | both;

        + none: 不改变默认行为。

        + forwards: 当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。

        + backwards: 在 `animation-delay` 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。

        + both: 向前和向后填充模式都被应用。

    + 规定动画在播放之前或之后，其动画效果是否可见。


### @keyframes 如何定义一个动画

```css
/* 定义一个动画 */
@keyframe move {
    from {
        left: 0px
    }
    to {
        left: 100px
    }
}


/* 定义动画的另一种方式 */
@keyframe move {
    0% {
        left: 0px
    }
    50% {
        left: 50px
    }
    100% {
        left: 100px
    }
}
```

我们可以通过设置 ***百分比*** 来更好的控制每个时间阶段中的动画.


### 使用css动画的一些注意事项

- 在使用动画的时候, 至少要定义动画的名称和动画的时长.

- Internet Explorer 9，以及更早的版本，不支持 @keyframe 规则或 animation 属性

- 在使用时候记得补全各个浏览器的前缀

- 为了得到最佳的浏览器支持，在定义 `@keyframe` 的时候应该始终定义 `0%` 和 `100%` 选择器
