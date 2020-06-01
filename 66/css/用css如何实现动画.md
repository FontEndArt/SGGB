### 用css如何实现动画

##### css实现动画主要有两类： transition, animate

---

    首先描述transition

    transition 包含 4个属性

    transition-property  规定设置过渡效果的css动画名称
    transition-duration  规定动画效果持续时间
    transition-timing-function  规定速度效果的速度曲线。
    transition-delay  定义过渡动画何时开始

    transition-property 实现方式
    假如说要实现一个宽度从100px - 200px变化的动画
    要实现宽度、高度或者位置移动，我们可以直接填写对应css属性名

    transition-property: width/height/left/right/all
    all代表所有

    首先我们定义了这个动画的表现方式

    然后我们再去定义 动画持续时间，例如 transition-duration: 0.5s

    接下来我们再去添加动画展示的速度曲线，  transition-timing-function

    transition-timing-function有6种曲线，分别是：
    linear： 匀速动画
    ease： 慢→快→慢
    ease-in： 以慢速开始的动画
    ease-out： 以慢速结束的动画
    ease-in-out： 慢速开始，慢速结束
    cubic-bezier(n,n,n,n)： 比较关键且特殊的一个动画曲线，俗称贝塞尔曲线

    知道了这几个动画曲线属性呢我们就先给添加一个匀速动画，transition-timing-function: linear

    最后再来个属性，动画从何时开始，假如我们页面加载完成后动画即开始，那 transition-delay: 0

    那么到这里，transition几个需要的属性已经设置完毕，那我们简单来写，
    transition: widthchange 0.5s linear;   最后一个何时开始为0 可不写，
    我们试验以后发现 成功完成动画


    接下来我们再来描述下animate