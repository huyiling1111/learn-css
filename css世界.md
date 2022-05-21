也可参考[https://segmentfault.com/a/1190000017069985](https://segmentfault.com/a/1190000017069985)
<a name="hWpzZ"></a>
### display
display:block 由外在的“块级盒子” 和内在的“块级容器盒子”组成。<br />display:inline-block 由外在的“内联盒子”和内 在的“块级容器盒子”组成。inline-block 的元素既能和图文一行显示， 又能直接设置 width/height。<br />每个元素都两个盒子， 外在盒子1和内在盒子。外在盒子负责元素是可以一行显示，还是只能换行显示;内在盒子负责 宽高、内容呈现什么的  
<a name="tnszW"></a>
### 外部尺寸与流体特性 (块级)
原则：无宽度、无图片、无浮动<br />举个栗子：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651458617611-ba9ef9a3-769d-477f-8552-a44734f7e828.png#clientId=u51197338-5ccc-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=336&id=uf148e7c4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=672&originWidth=690&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54612&status=done&style=none&taskId=ubd936e34-3ea3-4008-84fb-d4d6b7615f3&title=&width=345)
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
<a name="HNqD1"></a>
### 内部尺寸与流体特性 （内联）
 内部尺寸: 元素的尺寸由内部的元素决定, 而非由外部的容器决定。  	 	 	<br />如何快速判断一个元素使用的是否 为“内部尺寸”呢?很简单，假如这个元素里面没有内容，宽度就是 0，那就是应用的“内部尺寸”。<br />1.包裹性<br /> 页面某个模块的文字内容是动态的，可能是几个字，也可能是一句话。然 后，希望文字少的时候居中显示，文字超过一行的时候居左显示。
```
.box {
      text-align: center;
}
.content {
      display: inline-block;
      text-align: left;
}
```
2.首选最小宽度<br />指元素最适合的最小宽度，在css世界里，图片和文字的权重远大于布局。<br />具体表现规则为：<br />· 中文最小宽度为每个汉字的宽度。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651579650188-d5ca3d0d-bb96-461b-afdf-11961df20896.png#clientId=u818b531b-0513-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=216&id=u778ea5bb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=432&originWidth=506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=104759&status=done&style=none&taskId=u3f8a9581-2414-46a8-8845-9ba3ffc5e3d&title=&width=253)<br />  · 西方文字最小宽度由特定的连续的英文字符单元决定。并不是所有的英文字符都会组成连续单元， 一般会终止于空格(普通空格)、短横线、问号以 及其他非英文字符等。  						<br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651581368197-8e77bdea-9459-42af-a361-c7773f8dd08e.png#clientId=u818b531b-0513-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=169&id=u4fa846bc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=338&originWidth=506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=100791&status=done&style=none&taskId=u4efb8ffe-fce3-491d-8195-be99a1bc5c7&title=&width=253)		<br /> 如果想让英文字符和中文一样，每一个字符都用最小宽度单元，可以试试使用css中的word-break:break-all。<br />· 类似图片这样的替换元素的最小宽度就是该元素内容。
```
.ao {
      display: inline-block;
      width: 0;
    }
.ao:before {
       content: "love你love";
       outline: 2px solid #cd0000;
       color: #fff;
    }
```
  ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651584059838-c09ea6d4-e775-408a-85ce-fc11ca297db0.png#clientId=u818b531b-0513-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=134&id=u8ab8adff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=268&originWidth=598&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77027&status=done&style=none&taskId=u24711bf6-e2b7-4be7-834a-a8734ec836e&title=&width=299)<br />3.  最大宽度。 <br />   最大的宽度就是元素可以有的最大宽度。"最大宽度"实际等同于"包裹性"元素设置white-space:nowrap声明后的宽度。<br />最后的宽度是第一个"连续内联盒子"的宽度。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651584570009-36431d90-349f-486f-8f54-720d37819a7e.png#clientId=u818b531b-0513-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=212&id=u7cf6660c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=424&originWidth=1486&originalType=binary&ratio=1&rotation=0&showTitle=false&size=438931&status=done&style=none&taskId=uc8968a0d-af0c-4d0f-83b9-7874c19a864&title=&width=743)
<a name="QubEv"></a>
###  width值作用的细节	
width:auto 默认值
```
div { 
width: 100px; 
}

```
问，100px 的宽度是如何作用到这个<div>元素上的?<br />width 是作用在"内在盒子"上<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651586776728-e1000984-3d73-46d1-afa6-8cce04f5df67.png#clientId=u818b531b-0513-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=276&id=u3cb894ae&margin=%5Bobject%20Object%5D&name=image.png&originHeight=552&originWidth=618&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43375&status=done&style=none&taskId=u62072acf-3175-4827-a61c-4b94f3f0cc6&title=&width=309)<br />这个"内在盒子"又被分成了4个盒子，分别是content box、padding box、border box和margin box。<br />宽度分离:
```
.father {
        width: 180px;
}
.son {
        margin: 0 20px;
        padding: 20px;
        border: 1px solid;
}
```
宽度无死循环场景
```
<div class="box">
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
}
```
浏览器渲染原理：<br />首先，先下载文档内容，加载头部的 样式资源(如果有的话)，然后按照从上而下、自外而内的顺序渲染 DOM 内容。套用本例就是， 先渲染父元素，后渲染子元素，是有先后顺序的。因此，当渲染到父元素的时候，子元素的 width:100%并没有渲染，宽度就是图片加文字内容的宽度;等渲染到文字这个子元素的时候， 父元素宽度已经固定，此时的 width:100%就是已经固定好的父元素的宽度。宽度不够怎么 办?溢出就好了，overflow 属性就是为此而生的。
<a name="dwAGu"></a>
### auto和100%区别
height:auto，是指根据块内内容自动调节高度。<br />height:100%，是指其相对父块高度而定义的高度，也就是按照离它最近且有定义高度的父层的高度来定义高度。
<a name="XfRBz"></a>
### 父height:auto，子height:100%无效的情况
height还width:auto还有一个典型的区别在于，width即使为auto，其子元素使用百分比值也是可以的。<br />但如果是height:auto，那么其子元素若使用height:100%就会被忽略。<br />这是为什么呢？<br />因为规范如此：<br />如果包含块的高度没有显示指定（即高度由内容决定），并且该元素不是绝对定位元素，则计算值为auto。<br />而auto*100/100=NaN<br />那么为什么宽度就行呢？因为宽度并没有实际的规范这种情况下为auto，属于未定义行为，而各浏览器厂商一致决定将其解析为了具体的数值而不是auto<br />超越**!important**，超越最大<br />超越!important 指的是 max-width 会覆盖 width。<br />min-width覆盖max-width。
<a name="CTbpR"></a>
### 任意高度元素的展开收起动画技术
生硬地展开和收起
```
.element { 
 height: 0; 
 overflow: hidden; 
 transition: height .25s; 
} 
.element.active { 
 height: auto; /* 没有 transition 效果，只是生硬地展开 */ 
}
```
过渡地展开和收起
```
.element { 
 max-height: 0; 
 overflow: hidden; 
 transition: max-height .25s; 
} 
.element.active { 
 max-height: 666px; /* 一个足够大的最大高度值 */ 
}
```
注意：	max- height 值越大使用 场景越多，但是，如果 max-height 值太大，在收起的时候可能会有“效果延迟”的问 题，比方说，我们展开的元素高度是 100 像素，而 max-height 是 1000 像素，动画时间 是 250 ms，假设我们动画函数是线性的，则前 225 ms 我们是看不到收起效果的，因为 max-height从 1000 像素到 100 像素变化这段时间，元素不会有区域被隐藏，会给人动 画延迟 225 ms 的感觉。	
<a name="MTvMR"></a>
###  内联元素 
从作用上来讲，块级负责结构，内联负责内容。<br />图片和文字，是最典型的内联元素。
<a name="Knqf3"></a>
#### 1.从定义上看
“内联元素”的“内联”特指“外在盒子”是内联。inline-block 、inline-table、inline都是内联元素。
<a name="SKTE8"></a>
####  2.从表现看
“内联元素”的典型特征就是可以和文字在一行显示，因此，文字是内 联元素，图片是内联元素，按钮是内联元素，输入框、下拉框等原生表单控件也是内联元素。<br />有个疑问？<br />浮动元素貌似也是可以和文字在一个水平上显示的，是不是浮动元素也是内联级别的呢？不是的。实际上，浮动元素和后面的文字并不在一行显示，浮动元素已经在文档流之外了。证据就是，当后面文字足够多的时候，文字并不是在浮动元素的下面，而是继续在后面。这就说明，浮动元素和后面文字不在一行，只是它们恰好站在了一起而已。真相是，浮动元素会生成“块盒子”，这就是后话了。
<a name="QGUsh"></a>
### 内联世界深入的基础—内联盒模型
下面是一段很普通的html，实际包含了很多盒子。
```
<p>这是一行普通的文字，这里有个 <em>em</em> 标签。</p>
```
<a name="Tp41B"></a>
#### （1）内容区域(content area) 
 内容区域指一种围绕文字看不见的盒子，其大小仅受字符本身 特性控制，本质上是一个字符盒子(character box);但是有些元素，如图片这样的替换元素，其内 容显然不是文字，不存在字符盒子之类的，因此，对于这些元素，内容区域可以看成元素自身。 <br />我们可以把文本选中的背景色区域作为内容区域 <br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651997661586-60668f53-0d47-4b56-acbf-920ddfa055d6.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=73&id=u7aa9708d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=146&originWidth=744&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63905&status=done&style=none&taskId=ufc774de6-a15e-48da-a620-08df5581a9c&title=&width=372)
<a name="Jq3K4"></a>
#### （2）内联盒子(inline box) 
“内联盒子”不会让内容成块显示，而是排成一行,  该盒子又可以细分为“内联盒子”和“匿名内联盒子”两类: <br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651998438471-c592a4b8-8233-49cf-8157-6e394f96fecb.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=30&id=uf3b1e87f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=60&originWidth=838&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23128&status=done&style=none&taskId=uca883a3d-8c09-4aee-8eea-2fe425ebd11&title=&width=419)		<br /> 如果外部含内联标签(<span>、<a>和<em>等)，则属于“内联盒子”(实线框标注);如 果是个光秃秃的文字，则属于“匿名内联盒子”(虚线框标注，注意：并不是所有光秃秃的文字都是匿名内联盒子，取决于前后的标签是内联还是块级)。 
<a name="jo9C9"></a>
####    (3)  行框盒子(line box)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1651998699343-d3b16edf-67e2-4c2d-829a-690c7218a2b1.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=28&id=u7b4e15b9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=56&originWidth=908&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22407&status=done&style=none&taskId=uf6dd3861-bf96-43a2-943c-da57b4b042c&title=&width=454)
<a name="A8PWF"></a>
###   幽灵空白节点 
在 HTML5 文档声明 中，内联元素的所有解析和渲染表现就如同每个行框盒子的前面有一个“空白节点”一样。 <br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652008742106-74ab52e1-0b69-4b0b-afdf-1cbe39a96f2f.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=286&id=u5098148e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=572&originWidth=482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=171063&status=done&style=none&taskId=ude2fa6a0-3835-47e6-b443-a2b3307331d&title=&width=241) 		<br />结论：“幽灵空白节点” 是一个存在于每个“行框盒子”前面，同时具有该元素的字体和行高属性的 0 宽度的内联盒。 
<a name="DrOKI"></a>
###  盒尺寸四大家族 
 盒尺寸中的 4 个盒子 content box、padding box、border box 和 margin box 分别对应 CSS 世 界中的 content、padding、border 和 margin 属性，我把这 4 个属性称为“盒尺寸四大家族” 。<br />注意：这里提到的content box和border box  与盒模型的ontent box和border box 两个概念。
<a name="v52iC"></a>
#### 1. content 与替换元素 (vertical-align特性)
什么是替换元素？<br /> 根据“外在盒子”是内联还是块级我们可以把元素分为内联元素和块级元素，而根据是否具有可替换内容，我们也可以把元素分为替换元素和非替换元素。 <br />通过修改某个属性值呈现的内容就可以被替换的元素就称为“替换元素”， 因此，`<img>`、`<object>`、`<video>`、`<iframe>`或者表单元素`<textarea>`和`<input>`都是典型 的替换元素。 <br />举个栗子：
```
<img src="1.jpg">
// 如果我们把上面的 1.jpg 换成 2.jpg，图片就会替换
```
替换元素还有其他特性：<br />(1) 内容的外观不受页面上的 CSS 的影响。如何更改替换元素本身的外观?需要类似 appearance 属性，或者浏览器自 身暴露的一些样式接口，例如::-ms-check{}可以更改高版本 IE 浏览器下单复选框的内间距、背景色等样式，但是直接 input[type='checkbox']{}却无法更改内间距、背 景色等样式。 <br />(2)有自己的尺寸。在 Web 中，很多替换元素在没有明确尺寸设定的情况下，其默认的尺 寸(不包括边框)是 300 像素×150 像素，如`<video>`、`<iframe>`或者`<canvas>`等，也有少 部分替换元素为 0 像素，如<img>图片，而表单元素的替换元素的尺寸则和浏览器有关，没有 明显的规律。 <br />(3)在很多 CSS 属性上有自己的一套表现规则。比较具有代表性的就是 vertical-align 属性，对于替换元素和非替换元素，vertical-align 属性值的解释是不一样的。比方说 vertical-align 的默认值的 baseline，很简单的属性值，基线之意，被定义为字符 x 的 下边缘，在西方语言体系里近乎常识，几乎无人不知，但是到了替换元素那里就不适用了。为 什么呢?因为替换元素的内容往往不可能含有字符 x，于是替换元素的基线就被硬生生定义成 了元素的下边缘。 <br />下面提个简单问题:下拉框`<select>`是不是替换元素?答案:是的。 <br />我们可以对照一下“替换元素”的一些特点:首先，内容可替换，例如我们设置 multiple 属性，下拉直接变成了展开的直选多选模式;其次，基本样式外部 CSS 很难改变;最后，它有 自己的尺寸，基线也是下边缘等。 
`<a name="Z6VgS"></a>`
####  2.替换元素的默认 display 值 
所有的替换元素都是内联水平元素，也就是替换元素和替换元素、替换元素和文字都是可 以在一行显示的。但是，替换元素默认的 display 值却是不一样的。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652022025578-8c6c02f1-b609-46d2-a88f-8b92c1dcd528.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=342&id=ucc7dce7a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=684&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=353799&status=done&style=none&taskId=u8b8523fe-fdb7-49cf-9b26-d4dd517d5ea&title=&width=793)					 				
<a name="L7QW9"></a>
#### 3.替换元素的尺寸计算规则 
替换元素的尺寸从内而外分为 3 类：固有尺寸、HTML 尺寸和 CSS 尺寸。<br />权重级别为 CSS 尺寸>HTML 尺寸>固有尺寸。<br />(1）固有尺寸指的是替换内容原本的尺寸。<br />(2）HTML 尺寸相当于`<img>`的 width 和 height 属性、`<input> `的 size 属性、`<textarea>`的 cols 和 rows 属性等。<br />(3）css尺寸相当于 
```
img { width: 200px; height: 150px; } //最终图片所呈现的宽高就是 200 像素×150 像素。
<img src="1.jpg" width="128" height="96">
```
Web 开发的时候，为了提高加载性能以及节约带宽费用，首屏以下的图片就会通过滚屏加 载的方式异步加载，然后，这个即将被异步加载的图片为了布局稳健、体验良好，往往会使用 一张透明的图片占位。例如: 
```
<img src="transparent.png">
```
实际上，这个透明的占位图片也是多余的资源，我们直接：
```
<img>
```
 然后配合下面的 CSS 可以实现一样的效果：
```
img { visibility: hidden; } 
img[src] { visibility: visible; } //带有src属性的img标签设定样式
```
<a name="nQvIl"></a>
####  4.	利用content属性做图片切换的效果	
注意：content属性只是改变的是视觉效果，并不能另存为图片。而以下的例子上最后存的图片还是带有笑脸的那张。	
```
<img src="laugh.png">
img:hover { 
 content: url(laugh-tear.png); 
}
//该实例中，
我们鼠标经过笑脸，笑脸会飙出眼泪，就是通过 CSS 的 content 属性直接替换
<img>的替换内容实现的。
```
移动端的图片 建议用SVG矢量图片 		
<a name="ZCU43"></a>
###  5. content与替换元素关系剖析
**content属性**生成的内容都是**替换元素**

- content生成的文本是**无法选中、无法复制;无法被屏幕阅读设备读取**，也**无法被搜索引擎抓取**;替换的仅仅是**视觉层**
- **content动态生成值无法获取**
<a name="qFfk6"></a>
### 6. content 内容生成技术
清除浮动<br />content字符内容生成<br />content图片生成
```
div:before { 　 content: url(1.jpg); }
```
content attr属性值内容生成（比较常用）
```
img::after {
　  /* 生成alt信息 */
　  content: attr(alt); 
　  /* 其他CSS略 */
}

```
字体图标<br />理解content计数器
<a name="zZpfZ"></a>
### 温和的 padding 属性 
<a name="OeNxI"></a>
#### padding 与元素的尺寸
css 有很多其他场景或属性会出现这种不影响其他元素布局而是出现层叠效果的现象。<br />比如，relative 元素的定位、盒阴影 box-shadow 以及 outline 等。这些层叠现象虽 然看似类似，但实际上是有区别的。其分为两类:一类是纯视觉层叠，不影响外部尺寸;另一 类则会影响外部尺寸。box-shadow 以及 outline 属于前者，而这里的 inline 元素和块级元素的padding 层叠属于后者。区分的方式很简单，如果父容器 overflow:auto，层叠区域超出父 容器的时候，没有滚动条出现，则是纯视觉的;如果出现滚动条，则会影响尺寸、影响布局。 <br /> <br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652418534296-30e8e334-2e39-4678-946a-2a07f28abfc8.png#clientId=u11f4f272-0120-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=294&id=u55a78b7b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=367&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23494&status=done&style=none&taskId=ub6047d98-6b3e-4ca4-bbbd-2229e851975&title=&width=1536)<br />例子: 利用内联元素的 padding 实现高度可控的分隔线。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652418666313-e7a86cd7-fb04-4dc8-b3a1-44b5346c15a8.png#clientId=u11f4f272-0120-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=47&id=u9b327ba7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=59&originWidth=164&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2883&status=done&style=none&taskId=u70641a07-1529-4649-9d8c-4360da4d460&title=&width=131.2)	
```

.demo{
}

a + a:before { 
 content: ""; 
 font-size: 0; 
 padding: 10px 3px 1px; 
 margin-left: 6px;
 border-left: 1px solid gray; 
}
<div class="demo"><a href="">登录</a><a href="">注册</a></div>
```
<a name="vuGZI"></a>
#### padding 的百分比值 
padding 属性是不支持负值的， 但padding支持百分比值，但百分比值无论是水平方向还是垂直方向均是相对于宽度计算的! 
```
.box {
         border: 2px dashed #cd0000;
}
span {
       padding: 50%;
       background-color: gray;
     }
<span>内有文字若干</span>
```
对于内联元素，其 padding 是会断行的,也就是 padding 区域是跟着内联盒模型中的行框盒子走的，上面的例子由于文字比较多，一行显示不了，于是“若干”两字换到了下一行， 于是，原本的 padding 区域也跟着一起掉下来了，根据后来居上的层叠规则，“内有”两字自 然就正好被覆盖，于是看不见了;同时，规则的矩形区域因为换行，也变成了五条边;至于宽 度和外部容器盒子不一样宽，那是自然的，如果没有任何文字内容，那自然宽度正好和容器一 致;现在有“内有文字若干”这 6 个字，实际宽度是容器宽度和这 6 个字宽度的总和，换行后 的宽度要想和容器宽度一样，那可真要靠极好的人品了。 <br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652536113116-d4284695-f8f5-4185-a806-2ea0db0b0d00.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=284&id=u70a54725&margin=%5Bobject%20Object%5D&name=image.png&originHeight=568&originWidth=510&originalType=binary&ratio=1&rotation=0&showTitle=false&size=119583&status=done&style=none&taskId=ue207ccd6-de32-42cf-b38a-e5b1efb85ae&title=&width=255)			
<a name="nX3XP"></a>
#### padding 与图形绘制 
 padding 属性和 background-clip 属性配合。
```
 .icon-menu {
       display: inline-block;
       width: 140px; height: 10px;
       padding: 35px 0;
       border-top: 10px solid;
       border-bottom: 10px solid;
       background-color: currentColor;
       background-clip: content-box;
}

```
 	
```
.icon-dot {
       display: inline-block;
       width: 100px; height: 100px;
       padding: 10px;
       border: 10px solid;
       border-radius: 50%;
       background-color: currentColor;
       background-clip: content-box;
}
```
   


![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652586463427-5ea332e8-0c2a-4d77-8458-e73deff175b3.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=214&id=ua3553efc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=428&originWidth=1008&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154589&status=done&style=none&taskId=u8fcd7e3c-8c10-46e2-8a4f-8e9393e685c&title=&width=504)	




`<a name="KWTKd"></a>`
###  激进的 margin 属性 
`<a name="vfjUS"></a>`
#### margin 与元素尺寸以及相关布局  						 					 				
对于padding，元素设定了 width 或者保持“包裹性”的时候，会改变元素可视尺寸。则margin相反，元素设定了 width 值或者保持“包裹性”的时候，margin 对尺寸没有 影响，只有元素是“充分利用可用空间”状态的时候，margin 才可以改变元素的可视尺寸。  						<br /> 	
		
```
 <div class="father">
       <div class="son"></div>
</div>
 <div class="father1">
</div>
.father { width: 300px; height:10px; background:red} 
.son {height:20px; margin: 0 -20px; background:green}
.father1{width:50px; height:70px; background:yellow}
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2340024/1652587733229-f38f7bd4-59d7-4f33-b2f6-195250f0abdb.png#clientId=uf37f3237-7498-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=257&id=ub49bdbec&margin=%5Bobject%20Object%5D&name=image.png&originHeight=514&originWidth=652&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11161&status=done&style=none&taskId=u3a16c413-869c-4e08-b00d-8abe2166e4f&title=&width=326) 	 						<br /> 如图所示，绿色部分左侧超出了红色最左侧的宽度。但对于flex布局，绿色的元素尺寸(概念问题查css世界第97页)是不会超出红色的。绿色的外部尺寸左侧（受margin影响）是会超出红色左侧。<br />所以说只要元素的尺寸表现符合“充分利用可用空间”，无论是垂直方向还是水 平方向，都可以通过 margin 改变尺寸。 <br />CSS 世界默认的流方向是水平方向，因此，对于普通流体元素，margin 只能改变元素水 平方向尺寸;但是，对于具有拉伸特性的绝对定位元素，则水平或垂直方向都可以，因为此时 的尺寸表现符合“充分利用可用空间”。 
<a name="A2vsR"></a>
####  margin合并
块级元素的 margin-top和 margin-bottom有时会合并为单个外边距。(因为默认文档流是水平流，所以margin合并的就是垂直方向)<br />（1）相邻兄弟元素margin合并<br />p {margin: 1em 0;} <p>第一行</p><p>第二行</p> 第一行和第二行之间的间距还是1em<br />（2）父级和第一个子元素margin-top合并， 父级和最后一个子元素margin-bottom合并，例如
```
<div class="container">
    <h2>CSS世界</h2>
</div>

.container {
    max-width: 1920px;
    height: 384px;
    background: url(2.jpg) no-repeat left;
}
.container > h2 {
    font-size: 60px;
    margin-top: 100px; /*这里的原意是 标题 在图片中 下移100px,结果却变成了 图片 下移 100px*/
    /* 也就是 虽然是在 子元素上设置的 margin-top, 但实际就等于是在 父元素上设置了 margin-top*/
    color: #fff;
}
```
解决方法： 在 父元素添加：<br />.container {overflow: hidden;}<br />（3）空块级元素的margin合并
```

    .father { overflow: hidden; }
    .son { margin: 1em 0; }
    <div class="father">
       <div class="son"></div>
    </div>
```
 结果，此时.father 所在的这个父级<div>元素高度仅仅是 1em，因为.son 这个空<div>元 素的 margin-top 和 margin-bottom 合并在一起了。这也是上一节 margin:50%最终宽高 比是 2:1 的原因，因为垂直方向的上下 margin 值合二为一了，所以垂直方向的外部尺寸只有 水平方向的一半。  						<br />（4）margin合并的计算规则：<br /> 正正取最大，正负值相加，负负取最小

浏览器默认的字号大小是 16像素， 设置为 1em 就当前像素的1倍

因为margin的合并，在写代码的时候建议保留上下margin设置，例如 .list {margin-top: 15px; margin-bottom: 15px; } 而不是只写一个 .list {margin-top: 15px;}
<a name="t1dcE"></a>
#### margin: auto
(1) 如果一侧定值，一侧auto,则auto为剩余空间大小。<br /> (2)如果两侧均是auto,则平分剩余空间
```
.father { width: 300px;} 
.son { width: 200px; margin-right: 80px; margin-left: auto;}
//得到的结果是 左边距 20px,右边距80px
```


将上面的margin-right去掉 .son {width: 200px; margin-left: auto; } 则实现的效果正好是块级元素右对齐效果。 所以，如果想让某块状元素右对齐，除了使用 float: right;之外可以使用 margin-left:auto;<br />对应： margin-left:auto;对应text-align: right右对齐，<br />margin-right:auto对应text-align:left;左对齐<br />width: 200px; margin-left:auto; margin-right:auto;对应text-align: center;

水平、垂直都居中对齐:
```
.father { width: 300px; height: 150px; position: relative; background-color: #FF8C00; }
.son { position: absolute; top: 0;left: 0;right: 0;bottom: 0; width: 200px;height: 100px; margin: auto; background-color: #123456; }
```
