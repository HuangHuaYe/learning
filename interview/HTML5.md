# HTML5 基础面试题

## DOCTYPE 的作用

告诉浏览器用哪个标准HTML规范来渲染,不写或者写错都浏览器都会以混杂模式渲染.

- 混杂模式: 比较宽松的渲染模式
- 标准模式: 以标准规范来渲染

## link 和 @import 导入样式表的区别

1. link引用CSS时候，页面载入时同时加载；@import需要在页面完全加载以后加载，而且@import被引用的CSS会等到引用它的CSS文件被加载完才加载
2. link是xhtml标签，无兼容问题；@import是在css2.1提出来的，低版本的浏览器不支持
3. link支持使用javascript控制去改变样式，而@import不支持
3. link方式的样式的权重高于@import的权重
3. @import在html使用时候需要`<style type="text/css">`标签

## 外边句合并

两个元素的`margin-bottom`和`margin-top`会发生合并的情况

### 兄弟元素计算方式

- 全都为正值: 取最大值
- 全都是负值: 取最大值的绝对值,然后0减去此绝对值
- 一正一负: 取两者绝对值,最大的减去最小的

#### 解决办法

- 底部元素添加属性: `float: left`
- 底部元素添加属性: `position: absolute/fixed`
- 上下元素统一用一个元素确定间隔

### 父子元素计算防止

- 父元素没有设置border、padding、inline-content、clearance的时候

#### 解决办法

- 父元素添加上面提到的属性
- 子元素添加`float: left`或者`display: inline-block`

## 元素BFC

BFC(block format content)有以下的一些特性.

- BFC会阻止垂直外边距合并
- BFC内部不回重叠浮动元素
- BFC内部可以包含浮动

### 让元素成为BFC的方法

- float为left|right
- overflow为 hidden|auto|scroll
- display为 table-cell|table-caption|inline-block
- position为 absolute|fixed

## 清除浮动终极解决方案

```css
.floatfix{
    *zoom:1;
    // 兼容IE6、7,这样设置似的元素进入hasLayout的状态
    // hasLayout的确是
}
.floatfix:after{
    content:"";
    display:table;
    clear:both;
}
```

## 居中

### 绝对定位
```html
<div class="outer">
    <span>我想居中显示</span>
</div>
<style>
    .outer{
        width:300px;
        height:300px;
        position:relative;
        background-color:#ccc;
    }
    span{
        float:left;
        position:absolute;
        backgroond-color:red;
        top:50%;
        left:50%;
        transform:translate(-50%,-50%);
    }
</style>
```

### table-cell 属性定位

```html
<div class="outer">        
    <img src="nz.jpg" alt="">    
</div>
<style>        
    .outer{            
        width: 300px;           
        height: 300px;            
        border: 1px solid #cccccc;            
        display: table-cell;            
        text-align: center;            
        vertical-align: middle;        
    }        
    img{            
        width: 150px;            
        height: 150px;        
    }    
</style>
```

## 回流和重绘

回流是浏览器重新绘制整个页面的意思,重绘是浏览器对某个元素进行绘制的意思,比如颜色.

### 如何避免

#### CSS

- 避免使用table布局。
- 尽可能在DOM树的最末端改变class。
- 避免设置多层内联样式。
- 将动画效果应用到position属性为absolute或fixed的元素上。
- 避免使用CSS表达式（例如：calc()）。

#### JavaScript

- 避免频繁操作样式，最好一次性重写style属性，或者将样式列表定义为class并一次性更改class属性。
- 避免频繁操作DOM，创建一个documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中。
- 也可以先为元素设置display: none，操作结束后再把它显示出来。因为在display属性为none的元素上进行的DOM操作不会引发回流和重绘。
- 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
- 对具有复杂动画的元素使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁回流。

