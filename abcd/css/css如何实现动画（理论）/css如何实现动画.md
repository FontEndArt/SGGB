css实现动画，现在有了css3以后，基本有以下两种常用的纯css动画实现方式：


一、使用transition(过渡)实现动画：

	transition(过渡)——>这个的效果是能够从一个值过渡到另外一个值，举个栗子就是，让一个元素的宽自动从0px过渡到100px，过渡可以设置过渡的线性效果和过渡时长，过渡时长控制该效果在多少时间内完成，所以加上了时长以后，就会有了动态的动画视觉效果。
	
	需要注意的是，transition值比如是数值型才会有过渡效果，比如一个元素的width;0px，设置过渡为width:100px; 从数值0到数值100这种的就可以，举一个没有效果的栗子：元素默认的width:auto; 设置过渡为width:100px;  从auto(非数值型)到数值100，这种的是不会产生过渡效果的，元素会在指定的过渡时长后直接宽度变成100。
	
	transition可以改变一切只要是数值形式的css样式，比如：width、height、padding、margin、font-size、border-width等。
	一般使用transition都是通过一些事件给指定元素添加一个class名称，这个class里面就是所设定需要过渡的样式效果，不能在页面渲染加载的时候直接在css中写上transition，这样页面加载的话会直接执行了过渡动画，如果元素不在第一屏，或者还未加载显示，就看不到过渡动画了。
	
	transition也可以选择指定样式过渡，比如只过渡元素的width和height,也可以过渡所有，所有的话就不需要一个个的写，直接写all即可。
	
	
	
二、使用animation(动画)实现动画：

	严格来说animation才是真正作用与css动画的，animation相比于transition来说，比transition会更加灵活多变，transition只能指定一个值到另外一个值的过渡，但是animation可以设置一个值到另外一个值再到一个值再再再到一个值的变化。
	
	animation在使用的时候需要先进行动画创建，使用@keyframes创建，然后在元素的css中使用animation调用刚才所创建的动画，animation好处在于可以设置0%-100%之前任何一个时间段的效果，比如：0%的时候width:10px，50%的时候width:30px，80%的时候width:70%，100%的时候width:100%。
	
	animation与transition相同，都是只能设置为数值的样式才会有动画效果，非数值的不会产生动画效果。