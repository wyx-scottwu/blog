# mask

`mask`元素内，元素`fill`为`black`时，其覆盖位置其他元素不可见，反之为`white`时可见

这里需要注意的是，不可见指的是当前`mask`内的元素，而不是`mask`外的元素，如下`demo`

{% embed url="https://codepen.io/wyx-scottwu/pen/MWxJZKw" %}

{% hint style="info" %}
在上面demo中，path元素fill为black，所以其位置所在的内容不可见，可以看见path所在区域内容被“挖空”，相反text元素fill为white时，其所在区域被覆盖，而其描边颜色由于为black，所以该段文字描边所覆盖区域也被“挖空”
{% endhint %}
