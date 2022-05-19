# css世界
## display
display:block 由外在的“块级盒子” 和内在的“块级容器盒子”组成。</br> display:inline-block 由外在的“内联盒子”和内 在的“块级容器盒子”组成。inline-block 的元素既能和图文一行显示， 又能直接设置 width/height。</br> 每个元素都两个盒子， 外在盒子1和内在盒子。外在盒子负责元素是可以一行显示，还是只能换行显示;内在盒子负责 宽高、内容呈现什么的 </br> 
##  外部尺寸与流体特性 (块级)
原则：无宽度、无图片、无浮动 </br> 
举个栗子：
```
.nav {
       width: 240px;
}
.nav-a {
		display: block;
		/* 200px = 240px - 10px*2 - 10px*2 */
		width: 200px; 
		padding: 9px 10px;
		...
}
```
建议 ： 外部元素设定宽度，内部元素 由margin、border、 padding 自动分配空间。
## 内部尺寸与流体特性 （内联）
 内部尺寸: 元素的尺寸由内部的元素决定, 而非由外部的容器决定。 </br> 	 	 	
 如何快速判断一个元素使用的是否 为“内部尺寸”呢?很简单，假如这个元素里面没有内容，宽度就是 0，那就是应用的“内部尺寸”。</br> 	
 1.包裹性</br>
  页面某个模块的文字内容是动态的，可能是几个字，也可能是一句话。然 后，希望文字少的时候居中显示，文字超过一行的时候居左显示。

  ```
	  .box {
      text-align: center;
    }
		.content {
      display: inline-block;
      text-align: left;
		}
  ```
2.首选最小宽度</br>
指元素最适合的最小宽度，在css世界里，图片和文字的权重远大于布局。</br>
具体表现规则为：
· 中文最小宽度为每个汉字的宽度。  · 西方文字最小宽度由特定的连续的英文字符单元决定。并不是所有的英文字符都会组成连续单元， 一般会终止于空格(普通空格)、短横线、问号以 及其他非英文字符等。  						 		 如果想让英文字符和中文一样，每一个字符都用最小宽度单元，可以试试使用css中的word-break:break-all。· 类似图片这样的替换元素的最小宽度就是该元素内容。.ao {
      display: inline-block;
      width: 0;
    }
.ao:before {
       content: "love你love";
       outline: 2px solid #cd0000;
       color: #fff;
    }  3.  最大宽度。    最大的宽度就是元素可以有的最大宽度。"最大宽度"实际等同于"包裹性"元素设置white-space:nowrap声明后的宽度。最后的宽度是第一个"连续内联盒子"的宽度。 width值作用的细节	width:auto 默认值div { 
width: 100px; 
}
问，100px 的宽度是如何作用到这个<div>元素上的?width 是作用在"内在盒子"上这个"内在盒子"又被分成了4个盒子，分别是content box、padding box、border box和margin box。宽度分离:.father {
        width: 180px;
}
.son {
        margin: 0 20px;
        padding: 20px;
        border: 1px solid;
}宽度无死循环场景<div class="box">
<img src="1.jpg">
<span class="text">红色背景是父级</span>
</div> 
.box {
      display: inline-block;
      white-space: nowrap;
      background-color: #cd0000;
 }
 .text {
      display: inline-block;
      width: 100%;
      background-color: #34538b;
      color: #fff;
}浏览器渲染原理：首先，先下载文档内容，加载头部的 样式资源(如果有的话)，然后按照从上而下、自外而内的顺序渲染 DOM 内容。套用本例就是， 先渲染父元素，后渲染子元素，是有先后顺序的。因此，当渲染到父元素的时候，子元素的 width:100%并没有渲染，宽度就是图片加文字内容的宽度;等渲染到文字这个子元素的时候， 父元素宽度已经固定，此时的 width:100%就是已经固定好的父元素的宽度。宽度不够怎么 办?溢出就好了，overflow 属性就是为此而生的。