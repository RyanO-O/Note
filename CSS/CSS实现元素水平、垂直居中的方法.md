## 一、 水平居中
**行内元素和块级元素处理方法不一样**

### 1. 行内元素居中
先看其父元素是不是块级元素，是就直接设置父元素text-align: center;
```css
.parent {
    text-align: center;
}
```
否则，先设置父元素为块级元素，再设置center
```css
.parent {
    display:block;
    text-align: center;
}
```
### 2. 块级元素居中
先看宽度确不确定，确定的话，直接margin: 0 auto;
```css
.son {
    margin: 0 auto;
}
```
复制代码1.2.2 子元素含 float
.parent{
    width:fit-content;
    margin:0 auto;
}

.son {
    float: left;
}
复制代码1.2.3 Flex 弹性盒子
1） flex 2012版
.parent {
    display: flex;
    justify-content: center;
}
复制代码2）flex 2009版
.parent {
    display: box;
    box-orient: horizontal;
    box-pack: center;
}
复制代码1.2.4 绝对定位
1）transform
.son {
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
}
复制代码2）left: 50%
.son {
    position: absolute;
    width: 宽度;
    left: 50%;
    margin-left: -0.5*宽度
}
复制代码3）left/right: 0
.son {
    position: absolute;
    width: 宽度;
    left: 0;
    right: 0;
    margin: 0 auto;
}

