# 📝 II N数之和

### `Q:` 请用算法实现，从给定的不重复的数组中，取出`N`个数，使其相加和为`M`。如：

```javascript

var arr = [1, 4, 7, 11, 9, 8, 10, 6];
var N = 3;
var M = 27;

Result:
[7, 11, 9], [11, 10, 6], [9, 8, 10]
```

### `A:` 用回溯算法

{% code overflow="wrap" lineNumbers="true" %}
```javascript
function sumNums(nums, n, m) {
    if(!nums?.length || nums.length < n) {
        return [];
    }
    // 储存结果
    const result = [];
    // 储存临时计算堆
    const tempStack = [];
    
    const backtrace = (startIndex) => {
        if(tempStack.length === n - 1) {
            let endIndex = nums.length - 1;
            while(startIndex <= endIndex) {
                const tempRes = tempStack.reduce((acc, cur) => acc + cur);
                const [startNum, endNum] = [nums[startIndex], nums[endIndex]];
                
                // 不重复数组 nums，如果出现符合预期的结果，便无需再往下计算。
                if(tempRes + startNum === m) {
                    result.push([].concat(tempStack, startNum));
                    break;
                }
                if(tempRes + endNum === m) {
                    result.push([].concat(tempStack, endNum));
                    break;
                }
                startIndex++;
                endIndex--;
            }
            return;
        }
        for(let i = startIndex; i < nums.length; i++) {
            tempStack.push(nums[i]);
            backtrace(i+1);
            tempStack.pop();
        }
    }
    
    backtrace(0);
    return result;
}
```
{% endcode %}
