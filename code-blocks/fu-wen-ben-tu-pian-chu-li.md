---
description: from chat-gpt-3.5
---

# 📃 富文本图片处理

```typescript
function addStyleToImgTags(htmlString: string, styleToAdd: string): string {
    // 匹配图片标签的正则表达式
    const imgRegex: RegExp = /<img[^>]+>/g;

    // 使用正则表达式找到所有的图片标签
    const imgTags: RegExpMatchArray | null = htmlString.match(imgRegex);

    // 如果没有匹配到图片标签，直接返回原始字符串
    if (!imgTags) {
        return htmlString;
    }

    // 对每个图片标签添加style属性
    for (const imgTag of imgTags) {
        let modifiedImgTag = imgTag;

        // 如果当前图片标签没有style属性，则直接添加style属性
        if (!modifiedImgTag.includes('style="')) {
            modifiedImgTag = modifiedImgTag.replace('>', ` style="${styleToAdd}">`);
        } else {
            // 如果当前图片标签已经有style属性，则将要添加的样式追加到已有的样式中
            modifiedImgTag = modifiedImgTag.replace('style="', `style="${styleToAdd}; `);
        }
        // 用带有更新style属性的图片标签替换原始标签
        htmlString = htmlString.replace(imgTag, modifiedImgTag);
    }

    return htmlString;
}

// 示例用法
const htmlString: string = '<p>This is an image: <img src="example.jpg" style="border: 1px solid black;"></p>';
const styleToAdd: string = 'width: 200px; height: auto;';
const htmlWithStyle: string = addStyleToImgTags(htmlString, styleToAdd);
console.log(htmlWithStyle);

```
