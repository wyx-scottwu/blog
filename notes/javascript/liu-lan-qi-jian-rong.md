# 浏览器兼容

> 【内容引自】：
>
> 【[掘金](https://juejin.cn/)｜[去追光](https://juejin.cn/user/4054654615555854)｜[浏览器的兼容问题及解决方案整理（建议收藏）](https://juejin.cn/post/6972937716660961317)】

**1、`addEventListener` 与 `attachEvent` 区别**

`attachEvent` ——兼容：IE7、IE8；不兼容firefox、chrome、IE9、IE10、IE11、safari、opera。\
`addEventListener`——兼容：firefox、chrome、IE、safari、opera；不兼容IE7、IE8\
解决方案：

```
function addEvent(elm, evType, fn, useCapture) {
  if (elm.addEventListener) { // W3C标准
    elm.addEventListener(evType, fn, useCapture);
    return true;
  } else if (elm.attachEvent) { // IE
    var r = elm.attachEvent('on' + evType, fn); // IE5+
    return r;
  } else {
    elm['on' + evType] = fn; // DOM事件
  }
}
复制代码
```

**2、`document.formName.item("itemName")` 问题**

问题说明：IE下，可以使用 `document.formName.item("itemName")` 或 `document.formName.elements ["elementName"]`；Firefox 下，只能使用 `document.formName.elements["elementName"]`。\
解决方案：统一使用 `document.formName.elements["elementName"]`。

**3、集合类对象问题**

问题说明：IE下，可以使用 `()` 或 `[]` 获取集合类对象；Firefox下，只能使用 `[ ]` 获取集合类对象。\
解决方案：统一使用 `[]` 获取集合类对象。

**4、自定义属性问题**

问题说明：IE下，可以使用获取常规属性的方法来获取自定义属性，也可以使用 `getAttribute()` 获取自定义属性；Firefox下，只能使用 `getAttribute()` 获取自定义属性。\
解决方案：统一通过 `getAttribute()` 获取自定义属性。

**5、`eval("idName")` 问题**

问题说明：IE下，可以使用 `eval("idName")` 或 `getElementById("idName")` 来取得 `id` 为 `idName` 的HTML对象；Firefox下，只能使用 `getElementById("idName")` 来取得 `id` 为 `idName` 的HTML对象。\
解决方案：统一用 `getElementById("idName")` 来取得 `id` 为 `idName` 的HTML对象。

**6、变量名与某HTML对象ID相同的问题**

问题说明：IE下，HTML对象的ID可以作为 `document` 的下属对象变量名直接使用，Firefox下则不能；Firefox下，可以使用与HTML对象ID相同的变量名，IE下则不能。\
解决方案：使用 `document.getElementById("idName")` 代替 `document.idName`。最好不要取HTML对象ID相同的变量名，以减少错误；在声明变量时，一律加上 `var` 关键字，以避免歧义。

**7、`const` 问题**

问题说明：Firefox下，可以使用 `const` 关键字或 `var` 关键字来定义常量；IE下，只能使用 `var` 关键字来定义常量。\
解决方案：统一使用 `var` 关键字来定义常量。

**8、`input.type`属性问题**

问题说明：IE下 `input.type` 属性为只读；但是Firefox下 `input.type` 属性为读写。\
解决方案：不修改 `input.type` 属性。如果必须要修改，可以先隐藏原来的 `input`，然后在同样的位置再插入一个新的 `input` 元素。

**9、`window.event` 问题**

问题说明：`window.event` 只能在IE下运行，而不能在Firefox下运行，这是因为Firefox的 `event` 只能在事件发生的现场使用。\
解决方案：在事件发生的函数上加上 `event` 参数，在函数体内(假设形参为 `evt` )使用 `var myEvent = evt?evt:(window.event? window.event:null)`\
示例：

```
<input type="button" onclick="doSomething(event)"/>
<script language="javascript"> 
  function doSomething(evt) {
		var myEvent = evt ? evt :(window.event ? window.event : null);
		…
	}
</script>
复制代码
```

**10、`event.x` 与 `event.y` 问题**

问题说明：IE下，`event` 对象有 `x`、`y` 属性，但是没有 `pageX`、`pageY`属性；Firefox下，`event` 对象有`pageX`、`pageY`属性，但是没有 `x`、`y`属性。\
解决方案：`var myX = event.x ? event.x : event.pageX; var myY = event.y ? event.y:event.pageY;`\
如果考虑第8条问题，就改用 `myEvent` 代替 `event` 即可。

**11、`event.srcElement` 问题**

问题说明：IE下，`event` 对象有 `srcElement` 属性，但是没有 `target` 属性；Firefox下，`event` 对象有`target` 属性，但是没有 `srcElement` 属性。\
解决方案：使用 `srcObj = event.srcElement ? event.srcElement : event.target;`\
如果考虑第8条问题，就改用 `myEvent` 代替 `event` 即可。

**12、`window.location.href` 问题**

问题说明：IE或者Firefox2.0.x下，可以使用 `window.location` 或 `window.location.href`；Firefox1.5.x下，只能使用 `window.location`。\
解决方案：使用 `window.location` 来代替 `window.location.href` 。当然也可以考虑使用 `location.replace()`方法。

**13、模态和非模态窗口问题**

问题说明：IE下，可以通过 `showModalDialog` 和 `showModelessDialog` 打开模态和非模态窗口；Firefox下则不能。\
解决方案：直接使用 `window.open(pageURL,name,parameters)` 方式打开新窗口。\
如果需要将子窗口中的参数传递回父窗口，可以在子窗口中使用 `window.opener` 来访问父窗口。如果需要父窗口控制子窗口的话，使用 `var subWindow = window.open(pageURL,name,parameters);` 来获得新开的窗口对象。

**14、`frame` 和 `iframe` 问题**

以下面的 `frame`为例：\
(1)访问 `frame` 对象\
IE：使用 `window.frameId` 或者 `window.frameName` 来访问这个 `frame` 对象；\
Firefox：使用 `window.frameName` 来访问这个 `frame` 对象；\
解决方案：统一使用 `window.document.getElementById("frameId")` 来访问这个 `frame` 对象；\
(2)切换 `frame` 内容\
在IE和Firefox中都可以使用 `window.document.getElementById("frameId").src = "webjx.com.html"` 或`window.frameName.location = "webjx.com.html"` 来切换 `frame` 的内容；\
如果需要将 `frame` 中的参数传回父窗口，可以在 `frame` 中使用 `parent` 关键字来访问父窗口。

**15、事件委托方法**

问题说明：IE下，使用 `document.body.onload = inject;` ， 其中 `function inject()` 在这之前已被实现；在Firefox下，使用 `document.body.onload = inject();`\
解决方案：统一使用 `document.body.onload=new Function("inject()");` 或者 `document.body.onload = function(){}`\
\[注意] `Function` 和 `function` 的区别

**16、用 `setAttribute` 设置事件**

```
var obj = document.getElementById("objId");
obj.setAttribute("onclick", "funcitonname()");
复制代码
```

FireFox 支持，IE不支持。\
解决方案：IE中必须用点记法来引用所需的事件处理程序,并且要用赋予匿名函数；如下：

```
var obj = document.getElementById("objId");
obj.onclic k= function(){ fucntionname(); };
复制代码
```

这种方法所有浏览器都支持

**17、访问的父元素的区别**

问题说明：在IE下，使用 `obj.parentElement` 或 `obj.parentNode` 访问 `obj` 的父结点；在FireFox下，使用`obj.parentNode` 访问 `obj` 的父结点。\
解决方案：因为FireFox与IE都支持DOM，因此统一使用 `obj.parentNode` 来访问 `obj` 的父结点。

**18、`innerText` 的问题.**

问题说明：`innerText` 在IE中能正常工作，但是 `innerText` 在FireFox中却不行。\
解决方案：在非IE浏览器中使用 `textContent` 代替 `innerText`。\
示例：

```
if (navigator.appName.indexOf("Explorer") > -1) {
  document.getElementById("element").innerText = "my text";
} else {
  document.getElementById("element").textContent = "my text";
}
复制代码
```

\[注] `innerHTML` 同时被IE、FireFox等浏览器支持，其他的，如 `outerHTML` 等只被IE支持，最好不用。

**19、`Table` 操作问题**

问题说明：IE、FireFox以及其它浏览器对于 `table` 标签的操作都各不相同，在IE中不允许对 `table` 和 `tr` 的`innerHTML` 赋值，使用js 增加一个 `tr` 时，使用 `appendChild` 方法也不管用。`document.appendChild` 在往表里插入行时FireFox支持，IE不支持\
解决方案：把行插入到 `tbody`中，不要直接插入到表解决方法：

```
// 向table追加一个空行：
var row = otable.insertRow(-1);
var cell = document.createElement("td"); 
cell.innerHTML = "";
cell.className = "XXXX"; 
row.appendChild(cell);
复制代码
```

\[注] 建议使用JS框架集来操作 `table`，如JQuery。

**20、对象宽高赋值问题**

问题说明：FireFox中类似 `obj.style.height = imgObj.height` 的语句无效。\
解决方案：统一使用`obj.style.height = imgObj.height + "px";`

**21、`setAttribute("style", "color: red;")`**

FireFox支持(除了IE，现在所有浏览器都支持)，IE不支持\
解决方案：不用 `setAttribute("style", "color : red;")`\
而用 `object.style.cssText = "color: red;"`(这写法也有例外)\
最好的办法是上面种方法都用上，万无一失

**22、类名设置 `setAttribute("class", "styleClass")`**

FireFox支持，IE不支持(指定属性名为 `class`，IE不会设置元素的 `class` 属性，相反只使用 `setAttribute` 时IE自动识 `classname` 属性)\
解决方案：\
`setAttribute("class", "styleClass")`\
`setAttribute("className", "styleClass")`\
或者直接 `object.className= "styleClass";`\
IE和FF都支持 `object.className`。

**23、建立单选钮**

```
// IE以外的浏览器
var rdo = document.createElement("input");
rdo.setAttribute("type", "radio"); 
rdo.setAttribute("name", "radiobtn"); 
rdo.setAttribute("value", "checked");
// IE
var rdo = document.createElement("<input name="radiobtn" type="radio" value="checked" />");
复制代码
```

解决方案：\
这一点区别和前面的都不一样。这次完全不同，所以找不到共同的办法来解决，那么只有 `IF-ELSE`了\
万幸的是，IE可以识别出 `document` 的 `uniqueID` 属性，别的浏览器都不可以识别出这一属性。问题解决。\
​
