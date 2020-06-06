## 2020-06-04 - 一面, 了解过模块化开发吗？AMD 和 CMD 是什么？它们有哪些区别？

### 模块化

> 是指将一个复杂的问题，自顶向下逐层讲系统分成若干个模块的过程，有多种属性，分别反映其内部的一部分特性。

**模块化开发**

在实际的项目上，可以将一个完整的项目，分成若干个模块，然后由开发人员去担任其中一个模块的开发者，最后去组成一个完整的系统

**好处**

1. 一个模块的人员只专心负责一个模块的内容，增加了开发的进度和效果，减少块与块之间的冲突
2. 每个模块可以自由拆分和组装
3. 减少了命名空间的冲突

### AMD 和 CMD 的定义和区别
**AMD**

> Asynchronous Module Definition(异步模块定义)，是`RequireJS`在推广的过程中对模块化的规范产出的，推崇的是**异步引入和依赖前置**

1. define函数定义模块，第一个参数为定义模块的标识，如果不传会默认为文件名，第二个参数是一个模块数组，第三个参数是回调函数
2. 然后通过`return`来返回所需要导出的内容
```
define('Fn',['moduleA'],function(moduleItem){
    function Fn(){
        moduleItem.alert('AMD') // alert为模块内部内置的方法
    }
    return {
        Fn: Fn
    }
})
```

3. 然后可以通过`require`来引入模块

```
require(['Fn','moduleB'],function(Fn,moduleB){
    Fn.Fn()
})
```
**解决的问题**

1. 多个JS可能有依赖关系，被依赖的文件需要早于它依赖的模块定义
2. 同步JS加载的时候，浏览器页面渲染会停止

**CMD**
> Common Module Definition(通用模块管理)，是`SeaJS`在推广的过程中产生的，推崇的是**就近加载：即即用即加载，这是一个同步的概念，但是模块本身的加载可以是一个异步的过程**

1. define来定义模块
```
define(function(require,exports,module){
    var value1 = require('./xxx')
    console.log(value1.xxx)
    var value2 = require('./xxx')
    exports.value = value
    modules.exports = {
        value: value
    }
})
```
### 补充 ES6 和 nodejs

**ES6**
```
export 导出
export default 导出一个模块
import 引入
```
**输出方式：**
1. export 输出多个
2. export default输出一个模块

**加载**
可以单独加载模块中其中一个方法

**加载时机**
解析阶段，就会生成接口并对外输出

**值的变化**
向外输出的是值的引用，只要值发生了变化，加载的值也会发生变化

**this的指向**
this指向undefined

**commonJS**

```
exports 导出
module.exports 输出一个模块
require引入模块
```

**加载的时机**
执行的时候加载整个模块

**值的变化**
输出的值是拷贝的，已经加载的值是拷贝的，会使用缓冲，即原来模块的值发生改变，不会影响其他模块引用这个模块的值
**this的指向**
指向当前这个模块

### 浏览器模块导入的原理
通过在html创建`script`来引入需要的模块
script的优点
1. 可以缓存当前加载的模块