## CSS之布局

### 一、补充：CSS零碎知识点

* 伪类和伪元素
* 媒体查询

#### 1.伪类和伪元素

##### 1.1伪类

>  伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的 。 虽然它和普通的 css 类相似，可以为已有的元素添加样式，但是它只有处于 DOM 树无法描述的状态下才能为元素添加样式，所以将其称为伪类 

**Dom树**：浏览器无法直接理解和使用HTML，所以需要将HTML转换为浏览器能够理解的结构，这个过程是由HTML解析器解析，解析后的结构就是DOM树。

为了更加直观理解DOM树，可以打开开发者工具，在控制台输入document回车，便可以看到一个完整的DOM结构，如下图所示：

![1](E:\13-webstudy-feidian\img\1.png)

![](http://www.alloyteam.com/wp-content/uploads/2016/05/%E4%BC%AA%E7%B1%BB.png)

* link（选择未访问的链接）
* visited（选择已访问过的链接）
* hover（选择鼠标指针悬停在其上的元素）
* active（选择活动的链接）
* focus（选择获取焦点的输入字段）

##### 1.2伪元素

>  伪元素用于创建一些不在文档树中的元素，并为其添加样式。  虽然用户可以看到这些文本，但是这些文本实际上不在文档树中。 

![](http://www.alloyteam.com/wp-content/uploads/2016/05/%E4%BC%AA%E5%85%83%E7%B4%A0.png)



#### 2.媒体查询

>  CSS3中的媒体查询让内容的呈现可以根据设备进行变化, 而不需要改变内容本身 

##### 语法

```css
@media not|only mediatype and (expressions) {
    CSS 代码...;
}
```

*  **not:** not是用来排除掉某些特定的设备的，比如 @media not print（非打印设备）。 
*  **only:** 用来定某种特别的媒体类型。 
*  **all:** 所有设备，这个应该经常看到。 
* 当expressions为true时，才会执行css代码

mediatype可选值

| 值     | 描述                             |
| ------ | -------------------------------- |
| all    | 用于所有多媒体类型设备           |
| print  | 用于打印机                       |
| screen | 用于电脑屏幕，平板，智能手机等。 |
| speech | 用于屏幕阅读器                   |

示例：

```css
@media all and (min-height: 670px){
                .footer {
                    position: fixed;
                }
            }
```



### 二、常见布局

![](https://user-gold-cdn.xitu.io/2017/8/21/395302ae7949d78570a6102e5ded1ff0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

* 水平垂直居中
* 两列布局
* 三列布局

#### 1.水平垂直居中

###### flex布局

html

```html
<div class="wrap">
    <div class="content"></div>
</div>
```

css

```css
.wrap{
      width: 100px;
      height: 100px;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: red;
}
.content{
      width: 20px;
      height: 20px;
      background-color: green;
}
```

###### 绝对定位

html

```html
<div class="wrap1">
    <div class="content1"></div>
</div>
```

css

```css
		.wrap1{
            margin-top: 3%;
            width: 100px;
            height: 100px;
            background-color: red;
            position: relative;
        }
        .content1{
            width: 20px;
            height: 20px;
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;
            background-color: green;
        }
```



#### 2.两列布局

###### 左边宽度固定，右边宽度自适应

html

```html
<div class="left"></div>
<div class="right"></div>
```

css

```css
.left{
      width: 100px;
      height: 100px;
      float: left;
      background-color: red;
}
.right{
      width: auto;
      height: 100px;
      background-color: green;
}
```



#### 3.三列布局

中间自适应、左右边固定

###### 圣杯布局

html

```html
    <div class="container">
        <div class="middle">啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦</div>
        <div class="con-left"></div>
        <div class="con-right"></div>
    </div>
```

css

```css
        .container{
            margin-top: 4%;
            padding: 0 200px;
            overflow: hidden;
        }
        .middle{
            width: 100%;
            background-color: green;
            height: 200px;
            float: left;
        }
        .con-left{
            background-color: red;
            width: 200px;
            height: 200px;
            float:left;
            margin-left: -100%;
            position: relative;
            left: -200px;
        }
        .con-right{
            background-color: hotpink;
            width: 200px;
            height: 200px;
            float: left;
            margin-left: -200px;
            position: relative;
            right: -200px;
        }
```

* 三者均设置浮动，且需要先渲染middle
* middle宽度设置为100%
* 设置负边距
* 设置content的padding
* 左右两个设置相对定位

但是当middle部分比两边的子面板宽度小时，布局就会乱掉。

###### 双飞翼布局

html

```html
    <div class="container1">
        <div class="middle1"><div class="middle-content">啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦</div></div>
        <div class="left1"></div>
        <div class="right1"></div>
    </div>
```

css

```css
        .middle1{
            height: 200px;
            width: 100%;
            float: left;
           
        }
        .middle-content{
            background-color: green;
            margin-left: 200px;
            margin-right: 200px;
            height: 200px;
        }
        .left1{
            height: 200px;
            width: 200px;
            float: left;
            background-color: red;
            margin-left: -100%;
        }
        .right1{
            height: 200px;
            width: 200px;
            float: left;
            background-color: hotpink;
            margin-left: -200px;
        }
```

* 三者均设置浮动，且需先渲染middle
* middle宽度设置为100%
* 设置负边距，变为一行
* 将middle包裹，内容设置外边距

### 参考：

***

* [总结伪类与伪元素]( http://www.alloyteam.com/2016/05/summary-of-pseudo-classes-and-pseudo-elements/#prettyPhoto )
* [Flex 布局教程：语法篇]( http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html )
* [【面试题】CSS知识点整理(附答案)](https://mp.weixin.qq.com/s/71L6138-H0wuUkxZtgrgDw)
* [CSS 常见布局方式]( https://juejin.im/post/599970f4518825243a78b9d5 )