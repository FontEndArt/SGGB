
## 防抖
> 其实防抖这个解释，做过学生的都应该会比较了解。因为老师在讲课的时候，遇到课堂里疯狂讨论的时候（叽里呱啦）。总会有个惯性操作：等我们什么时候不吵了，我们就下课（很熟悉吧！）。老师很烦躁，疯狂有一些学生在不断的发表言论，然后这个时候安静下来了，老师舒服了，开心了，然后又有一些人在唧唧歪歪，老师又不开心了，恢复了“等什么时候不吵了”的情况，然后又多上了20分钟的课，最后才真正的下课了。
**引出定义：防抖，为了控制一些重复的操作（讨论），为了避免后面执行的操作过多。记住关键的一点，当又出现操作了，就会重置之前的操作，重新计时等待**

```
function debounce(fn, wait, imm = false) {
  let timer = null;
  return function () {
    let context = this;
    let arg = arguments;
    let ret = "";
    if (timer) clearTimeout(timer); // 重新即时
    if (imm) {
      var callnow = !timer;
      timer = setTimeout(function () {
        timer = null;
      }, wait);
      if (callnow) ret = fn.apply(context, arguments);
    } else {
      setTimeout(() => {
        fn.apply(context, arguments);
      }, wait);
    }
    return ret;
  };
}

```

## 节流

> 这个要比防抖好理解的多，就是控制一段时间的输出的量，参考每天挤地铁


```
function throttle(fn, wait) {
    let timer = null;
    return function () {
        var context = this; 
        var args = arguments;
        if (!timer) {
            timer = setTimeout(() => {
                fn.apply(context, [...args]);
                timer = null
            }, wait)
        }
    }
}
```
