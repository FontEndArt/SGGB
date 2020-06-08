2020-06-05 - 一面, 什么是重绘重排合成？怎么触发重绘或重排、合成，分别描述下？会产生性能问题吗？怎么规避？

## 网页的生成步骤
1. HTML被HTML解析器解析成DOM树
2. css则被css解析器解析成CSSOM树
3. 然后将CSSOM树和DOM树根据节点位置，进行生成，生成一个渲染树
4. 然后生成布局（flow），将所有渲染树上的节点进行平台合成
5. 然后paint到屏幕上

### 渲染

> 渲染就是将生成布局（重排，回流），然后绘制到屏幕上的这个过程（重绘）

在用户访问整个网站的时候，整个渲染的过程也可能会发生改变，但是不一定会两个步骤都会发生。

**重排，重绘**
1. 重排，网页中有某一个布局发生了改变，如:**margin**
2. 重绘，网页中有元素的外观可能发生了改变，如:**color**


> 综上所述，我们可以看到重排之后，一定会经历一次重绘：**重排一定会发生重绘，但是重绘不一定会发生重排**

### 重排
当DOM的变化影响元素的几何信息（DOM对象的位置和尺寸大小），浏览器需要重新计算元素的几何属性，将其放在界面中的正确位置，这个过程叫做重排

1. 添加或者删除一个可见的DOM元素
2. 元素的size发生改变，margin,padding,width,height
3. 内容发生改变，如input输入文字
4. 浏览器窗口尺寸发生改变
5. 计算offsetHeight或者offsetWidth的值
6. 设置style的值

**常见的引起重排的属性和方法：**
> width height | margin padding| display|border|position|overflow|clientWidth clientHeight clientTop clientLeft |offsetWidth offsetHeight offsetTop offsetLeft| scrollWidth scrollHeight scrollTop scrollLeft|scrollIntoView() scrollTo() getComputedStyle() getBoundingClientRect() scrollIntoViewIfNeeded()

#### 影响的范围
1. 全局的范围：从根节点开始，整个渲染树重新生成
2. 局部范围： 渲染树某个地方发生更改，要重新对这一小块进行重新生成

### 重绘
当一些或者一个元素的仅仅是外观发生了变化，但没有对渲染树的结构发生改变，这时候会执行重绘的过程

**常见引起重绘的的属性和方法：**
>  color 、border-style、visibility、background、text-decoration、background-image、background-position、background-repeat、outline-color、outline、outline-style、border-radius、outline-width、box-shadow、background-size



### 浏览器的渲染队列
当我们修改了页面的结构或者样式时，会发生重绘或者重排，浏览器会将这些操作放在一个渲染队列里面，**当这样操作达到了一定的数量或者队列存在达到一定的时间后**，浏览器会批量进行**重绘或者重排**，这叫做**合成**

```
div1.style.left = '20px';
div1.style.top = '20px';
div1.style.width = '20px';
div1.style.height = '20px';
```
**这段代码事实上只执行了一次重排**

### 强制刷新队列
- offsetTop, offsetLeft, offsetWidth, offsetHeight
- scrollTop, scrollLeft, scrollWidth, scrollHeight
- clientTop, clientLeft, clientWidth, clientHeight
- getComputedStyle(), 或者 IE的 currentStyle

在渲染队列如果出现了这些值的操作：获取，修改。浏览器为了给我们一个准确的值，会立刻执行渲染队列，进行重绘或者重排

### 重排优化
重排会让浏览器进行重新渲染和渲染树的构成，对浏览器的性能的消耗非常大，所以需要对这些操作进行优化

1. 分离读写操作

2. 样式集中改变

3. 缓存布局信息，也相当于读写分离

4. 离线改变dom

当要操作一个dom的时候，可以将dom首先`display:none`,然后去进行操作-> 然后通过`documentFragment`创建一个dom碎片，然后进行一系列的操作，最后将它添加到页面上，这样就执行了一次重排

5. position:fixed或者absolute
positon元素因为改变自身的时候，对页面上的元素没有直接副作用，所以引起的重排的范围会比较小

6. 启动GPU加速
GPU是`图像处理器`，`GPU硬件加速`指的是应用`GPU`的图形性能对浏览器的一些图形操作，交给`GPU`处理，`GPU`是专门为了处理图形设计的，所以在`速度`和`能耗`中有巨大的优势

GPU加速通常包括：
1. Canvas2D
2. 布局合成（Layout Compositing）
3. CSS3转换(transitions)
4. CSS3 3D转换（transforms）
5. WebGl
6. video