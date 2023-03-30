# 浏览器兼容

> 【内容引自】：
>
> 【[掘金](https://juejin.cn/)｜[去追光](https://juejin.cn/user/4054654615555854)｜[浏览器的兼容问题及解决方案整理（建议收藏）](https://juejin.cn/post/6972937716660961317)】

**1、`CSS Hack` **&#x20;

使用 `hacker` 可以把浏览器分为3类：IE6；IE7和遨游；其他（IE8 Chrome ff Safari opera等）\
（1）IE6认识的 `hacker` 是 下划线 `_`  和星号 `*` \
（2）IE7和遨游认识的 `hacker` 是 星号 `*` \
如： `height:300px;*height:200px;_height:100px;` \
（1）IE6浏览器在读到 `height:300px` 的时候会认为高时 `300px` \
继续往下读，他也认识 `*heihgt` ， 所以当IE6读到 `*height:200px` 的时候会覆盖掉前一条的相冲突设置，认为高度是 `200px` 。\
继续往下读，IE6还认识 `_height` ,所以他又会覆盖掉 `200px` 高的设置，把高度设置为 `100px` 。\
（2）IE7和遨游也是一样的从高度 `300px` 的设置往下读。当它们读到 `*height:200px` 的时候就停下了，因为它们不认识 `_height` 。\
所以它们会把高度解析为 `200px` ，剩下的浏览器只认识第一个 `height:300px` ;\
所以他们会把高度解析为 `300px` 。因为优先级相同且想冲突的属性设置后一个会覆盖掉前一个，所以书写的次序是很重要的。\
&#x20;

**2、CSS 样式兼容不同浏览器问题**

所有浏览器通用： `height: 100px;` \
IE6 专用： `_height: 100px;` 或者 `*height: 100px;` \
IE7 专用： `*+height: 100px;` \
IE7、FF 共用： `height: 100px !important;` \
以下两种方法几乎能解决现今所有兼容：\
（1） `!important` \
随着IE7对 `!important` 的支持, `!important` 方法现在只针对IE6的兼容(注意写法，记得该声明位置需要提前)

```css
.box {
  width: 100px !important; /* IE7+FF */
  width: 80px; /* IE6 */
}
```

(2)IE6/IE77对FireFox \<from 针对FireFox ie6 ie7的css样式>\
`*+html` 与 `*html`  是IE特有的标签，FireFox 暂不支持。而 `*+html` 又为 IE7特有标签。

```css
.box { width: 120px; } /* FireFox */
*html .box { width: 80px;} /* ie6 fixed */
*+html .box { width: 60px;} /* ie7 fixed, 注意顺序 */
```

&#x20;**3、万能 `float`  闭合(非常重要) 可以用这个解决多个 `div` 对齐时的间距不对**

将以下代码加入 `Global CSS`  中，给需要闭合的 `div` 加上 `class="clearfix"`  即可，屡试不爽。\
代码：

```css
<style>
/* Clear Fix */
.clearfix:after {
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
    display: inline-block;
}
/* Hide from IE Mac \*/
.clearfix {
    display:block;
}
/* End hide from IE Mac */
/* end of clearfix */
</style>
```

**4、其他兼容技巧**

1. Firefox下给 `div`  设置 `padding`  后会导致 `width`  和 `height`  增加, 但IE不会(可用 `!important` 解决)
2. 居中问题：
   1. &#x20;垂直居中将 `line-height`  设置为当前 `div`  相同的高度, 再通过 `vetical-align: middle` ( 注意内容不要换行）
   2. 水平居中： `margin: 0 auto;` (当然不是万能)
3. 若需给 `a`  标签内内容加上 样式，需要设置 `display: block;` (常见于导航标签)
4. Firefox 和 IE 对 BOX 理解的差异导致相差 `2px`  的还有设为 `float` 的 `div` 在 ie下 `margin` 加倍等问题
5. `ul` 标签在 FF 下面默认有 `list-style`  和 `padding` 最好事先声明，以避免不必要的麻烦(常见于导航标签和内容列表)
6. 作为外部 `wrapper`  的 `div`  不要定死高度，最好还加上 `overflow: hidden` 以达到高度自适应

**5、兼容代码：兼容最推荐的模式。**

```css
/* FF */
.submitbutton {
    float: left;
    width: 40px;
    height: 57px;
    margin-top: 24px;
    margin-right: 12px;
}
/* IE6 */
*html .submitbutton {
    margin-top: 21px;
}
/* IE7 */
*+html .submitbutton {
    margin-top: 21px;
}
```

**6、兼容 `CSS` 方法**

做兼容页面的方法是：每写一小段代码（布局中的一行或者一块）我们都要在不同的浏览器中看是否兼容，当然熟练到一定的程度就没这么麻烦了。\
建议经常会碰到兼容性问题的新手使用。很多兼容性问题都是因为浏览器对标签的默认属性解析不同造成的，只要我们稍加设置都能轻松地解决这些兼容问题。\
如果我们熟悉标签的默认属性的话，就能很好的理解为什么会出现兼容问题以及怎么去解决这些兼容问题。

#### 六、其它CSS兼容

**1、不同浏览器的标签默认`margin` 和 `padding` 不同**

问题说明：随便写几个标签，不加样式控制的情况下，各自的 `margin` 和 `padding` 差异较大。\
解决方案： `CSS: *{margin: 0;padding:0;}`&#x20;

**2、块属性标签 `float` 后，又有横行的 `margin` 情况下，在IE6显示 `margin` 比设置的大**

问题说明：常见症状是IE6中后面的一块被顶到下一行（ `float` 布局最常见的浏览器兼容问题）\
解决方案：在 `float` 的标签样式控制中加入 `display:inline;`  将其转化为行内属性\
备注：我们最常用的就是 `div+CSS` 布局了，而 `div`就是一个典型的块属性标签，横向布局的时候我们通常都是用 `div float` 实现的，横向的间距设置如果用 `margin` 实现，这就是一个必然会碰到的兼容性问题。

**3、较小高度标签（一般小于 `10px` ）问题**

问题说明：IE6、7和遨游里这个标签的高度不受控制，超出自己设置的高度\
解决方案：给超出高度的标签设置 `overflow:hidden;` 或者设置行高 `line-height`  小于你设置的高度。\
备注：这种情况一般出现在我们设置小圆角背景的标签里。出现这个问题的原因是IE8之前的浏览器都会给标签一个最小默认的行高的高度。即使你的标签是空的，这个标签的高度还是会达到默认的行高。

**4、行内属性标签，设置 `display:block` 后采用 `float` 布局，又有横行的 `margin` 的情况，IE6间距 `bug` **&#x20;

问题说明：IE6里的间距比超过设置的间距\
解决方案：在 `display:block;` 后面加入 `display:inline;display:table;` \
备注：行内属性标签，为了设置宽高，我们需要设置 `display:block;` (除了 `input` 标签比较特殊)。\
在用 `float` 布局并有横向的 `margin` 后，在IE6下，他就具有了块属性 `float` 后的横向 `margin` 的 `bug` 。\
不过因为它本身就是行内属性标签，所以我们再加上 `display:inline` 的话，它的高宽就不可设了。\
这时候我们还需要在 `display:inline` 后面加入 `display:talbe` 。

**5、图片默认有间距**

问题说明：几个 `img` 标签放在一起的时候，有些浏览器会有默认的间距，加了问题一中提到的通配符也不起作用。\
解决方案：使用 `float` 属性为 `img` 布局\
备注：因为 `img` 标签是行内属性标签，所以只要不超出容器宽度， `img` 标签都会排在一行里，但是部分浏览器的 `img` 标签之间会有个间距。去掉这个间距使用 `float` 是正道。

**6、标签最低高度设置 `min-height` 不兼容**

问题说明：因为 `min-height` 本身就是一个不兼容的 `CSS` 属性，所以设置 `min-height` 时不能很好的被各个浏览器兼容\
解决方案：如果我们要设置一个标签的最小高度 `200px` ，需要进行的设置为：

```css
{ 
  min-height: 200px; 
  height: auto !important; 
  height: 200px; 
  overflow:visible;
 }
```

备注：在B/S系统前端开时，有很多情况下我们又这种需求。当内容小于一个值（如 `300px` ）时。容器的高度为 `300px` ；当内容高度大于这个值时，容器高度被撑高，而不是出现滚动条。这时候我们就会面临这个兼容性问题。

**7、CSS 布局中的居中问题**

问题说明： 首先在父级元素定义 `text-align: center;` 这个的意思就是在父级元素内的内容居中；对于IE这样设定就已经可以了。但在mozilla中不能居中。\
解决办法：在子元素定义时候设定时再加上 `margin-right: auto; margin-left: auto;`&#x20;

**8、IE浮动产生的双倍距离**

```css
#box { 
  float: left; 
  width: 100px; 
  margin: 0 0 0 100px; // 这种情况之下IE会产生200px的距离
  display: inline; // 使浮动忽略
}
```

这里细说一下 `block`， `inline` 两个元素\
`Block` 元素的特点是：总是在新行上开始，高度、宽度、行高、边距都可以控制(块元素)\
`Inline` 元素的特点是：和其他元素在同一行上，不可控制(内嵌元素)

```css
#box { 
  display: block; // 可以为内嵌元素模拟为块元素 
  display: inline; // 实现同一行排列的的效果 
  diplay: table;
}
```

**9、IE与宽度和高度的问题**

IE不认得 `min-` 这个定义，但实际上它把正常的 `width` 和 `height` 当作有 `min` 的情况来使。\
这样问题就大了，如果只用宽度和高度，正常的浏览器里这两个值就不会变，如果只用 `min-width` 和 `min-height` 的话，IE下面根本等于没有设置宽度和高度。\
比如要设置背景图片，这个宽度是比较重 要的。\
解决方案：要解决这个问题，可以这样：

```css
#box { 
  width: 80px; 
  height: 35px;
}
html>body #box {
  width: auto; 
  height: auto; 
  min-width: 80px; 
  min-height: 35px;
}
```

**10、页面的最小宽度**

`min-width` 是个非常方便的 `CSS` 命令，它可以指定元素最小也不能小于某个宽度，这样就能保证排版一直正确。\
但IE不认得这个，而它实际上把 `width` 当做最小宽度来使。\
为了让这一命令在IE上也能用，可以把一个 `<div>`  放到 `<body>`  标签下，然后为 `div` 指定一个类，然后 `CSS` 这样设计：

```css
#containe r{
    min-width: 600px;
    width: e-xpression(document.body.clientWidth < 600? "600px": "auto");
}
```

第一个 `min-width` 是正常的；\
但第2行的 `width` 使用了 `JavaScript` ，这只有IE才认得，这也会让你的 `HTML` 文档不太正规。它实际上通过 `JavaScript` 的判断来实现最小宽度。

**11、清除浮动**

```css
.box {
  display: table;
  // 将对象作为块元素级的表格显示
}
// 或者
.box {
  clear: both;
}
```

或者加入 `:after` （伪对象）,设置在对象后发生的内容，通常和 `content` 配合使用，IE不支持此伪对象，\
非IE 浏览器支持，所以并不影响到IE/WIN浏览器。

```css
……#box:after {
  content: “.”;
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
```

**12、 `DIV` 浮动IE文本产生 `3px` 的 `bug` **&#x20;

左边对象浮动，右边采用外补丁的左边距来定位，右边对象内的文本会离左边有 `3px` 的间距。

```css
#box {
  float: left;
  width: 800px;
}
#left {
  float: left;
  width: 50%;
}
#right {
  width: 50%;
}
*html #left {
  margin-right: -3px; // 这句是关键
}
```

**13、IE捉迷藏的问题**

当 `div` 应用复杂的时候每个栏中又有一些链接， `div` 等这个时候容易发生捉迷藏的问题。\
有些内容显示不出来，当鼠标选择这个区域是发现内容确实在页面。\
解决方案：对 `#layout` 使用 `line-height` 属性或者给 `#layout` 使用固定高和宽。页面结构尽量简单。

**14、高度不适应**

高度不适应是当内层对象的高度发生变化时外层高度不能自动进行调节，特别是当内层对象使用 `margin`  或 `padding`  时。例：

```html
<div id=”box”>
	<p>p对象中的内容</p>
</div>
```

`CSS` ：

```css
#box {
  background-color: #eee; 
}
#box p {
  margin-top: 20px;
  margin-bottom: 20px; 
  text-align: center; 
}
```

解决方案：在 `p` 对象上下各加 `2` 个空的 `div` 对象 `CSS` 代码： `.1{ height: 0px; overflow: hidden; }` 或者为 `DIV` 加上 `border` 属性。

**15、`cursor` 属性问题**

`cursor: hand;` VS `cursor: pointer;` \
问题说明：FireFox不支持 `hand`，但IE支持 `pointer` 。\
解决方法：统一使用 `pointer`。

**16、对盒模型的解析不一致**

* 对 `border` 的解析不一致，如：`box.style { width: 100px; border: 1px; }`；IE理解为 `box.width = 100px;`；Firefox 理解为 `box.width = 100 + 1*2 = 102px;  // 加上边框2px`

解决方案：`div { margin: 30px !important; margin: 28px; }` 注意这两个 `margin` 的顺序一定不能写反， IE不能识别 `!important` 这个属性，但别的浏览器可以识别。所以在IE下其实解释成这样：`div{ maring: 30px; margin: 28px; }` 重复定义的话按照最后一个来执行，所以不可以只写 `margin: XXpx !important;`

* IE5 和 IE6 的盒模型解释不一致。IE5下 `div{ width: 300px; margin: 0 10px 0 10px; }` 其中 `div` 的宽度会被解释为 `300px-10px(右填充)-10px(左填充)`，最终 `div` 的宽度为 `280px` ，而在IE6和其他浏览器上宽度则是以 `300px+10px(右填充)+10px(左填充)=320px` 来计算的。

解决方案：做如下修改 `div { width: 300px !important; width /**/: 340px; margin: 0 10px 0 10px; }`\
17、`ul` 和 `ol` 列表缩进问题\
消除 `ul`、`ol` 等列表的缩进时，样式应写成：`list-style: none; margin: 0px; padding: 0px;`\
经验证，在IE中，设置 `margin: 0px;` 可以去除列表的上下左右缩进、空白以及列表编号或圆点，设置 `padding` 对样式没有影响；\
在 Firefox 中，设置 `margin: 0px;` 仅仅可以去除上下的空白，设置 `padding: 0px;` 后仅仅可以去掉左右缩进，还必须设置 `list- style: none;` 才能去除列表编号或圆点。也就是说，在IE中仅仅设置 `margin: 0px;` 即可达到最终效果，而在Firefox中必须同时设置 `margin: 0px;`、 `padding: 0px;` 以及 `list-style: none;` 三项才能达到最终效果。

**17、为什么无法定义 `1px` 左右高度的容器**

IE6下这个问题是因为默认的行高造成的；解决的技巧也有很多：\
例如：`overflow: hidden;` `zoom: 0.08` `line-height: 1px;`

**18、链接(`a`标签)的边框与背景**

`a` 链接加边框和背景色，需设置 `display: block;` 同时设置 `float: left;` 保证不换行。参照 `menubar`, 给 `a` 和 `menubar` 设置高度是为了避免底边显示错位，若不设 `height`, 可以在 `menubar` 中插入一个空格。\
19、超链接访问过后 `hover` 样式就不出现的问题\
问题说明：被点击访问过的超链接样式不在具有 `hover` 和 `active`了\
解决技巧是改变CSS属性的排列顺序: L-V-H-A ；\
`<style type="text/css"> <!-- a:link {} a:visited {} a:hover {} a:active {} --> </style>`
