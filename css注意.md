# css学习

## 1.选择器

> class选择器

```html
.search-index{}
```

> id选择器

```html
#search-index{}
```

> 属性选择器

```html
 <style>
     /* 下面这两种都是属性选择器
         */
        /* input[value]{
            color: red;
        } */
        input[type=password]{
            color: red;
        }
     
    </style>
</head>
<body>
    <input type="text" value="123" data-id="0">
    <input type="password">
    <script>
        const input = document.querySelector('input[value]')
        console.log(input.dataset);
        console.log(input.dataset.id);
        //此处也是属性选择器
        document.querySelector('[data-id=0]')
    </script>
</body>
```

> 伪类选择器

before，after都是双引号在前，意思明确，就是元素之前和之后

```
.search::before{

}
```

> 当选择一个特别的class时可以先选父再选子

```
.focus img{}
```

> 通配符

```
* {
  margin: 0;                    /* 定义外边距*/
  padding: 0;                   /* 定义内边距*/
}
```

清除所有HTML标记的默认边距





## 2.常用的一些css属性

先罗列一些自己常用的

> 比如body上使用的

```css
body{
    /*这里设置的浏览器放大缩小时支持的最宽与最窄宽度*/
    max-width: 540px;
    min-width: 320px;
    /*设置边距*/
    /*1.四个值时是上、右、下、左*/
    /*2.三个值是上、左右、下*/
    /*3.两个值是上下、左右*/
    margin: 0 auto;
   	/*字体与颜色*/
    font: normal 14px/1.5 Tahoma,"Lucida Grande",Verdana,"Microsoft Yahei",STXIihei,hei;
    color: #000;
    /*背景颜色*/
    background-color: #f2f2f2;
    /*设置假如子的元素超出父盒子后，该怎么做，此处是隐藏*/
    overflow-x:hidden ;
    /*transparent代表全透明黑色*/
    /*可以用opacity设置透明，1是不透明，0直接就无了*/
    -webkit-tap-highlight-color: transparent;
    height: 2000px;
}
```

> 平时使用在各个组件上

```css
.search-index{
    /* 固定fixed ，与父级无关，以屏幕为准*/
    /*display后跟的元素常有none、block、flex、list-item、*/
    display: flex;
    /*见如下表*/
    position: fixed;
    top:0 ;
    left: 50%;
    /* 移动自己的像素值 */
    -webkit-transform: translate(-50%);
    transform: translate(-50%);
    width: 100%;
    height: 44px;
    max-width: 540px;
    min-width: 320px;
    background-color: #f6f6f6;
    /*边框设置参数分别是像素宽度、边框风格、颜色*/
    /*dotted solid double dashed*/
    /*点、实线、双线、虚线*/
    /**同时它也可以像margin那样设置/
    border-top: 1px solid #ccc;
    border-bottom:1px solid #ccc ;
}
```

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| absolute | 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
| fixed    | 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
| relative | 生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。想对于一个元素的正常位置 |
| static   | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 |
| inherit  | 规定应该从父元素继承 position 属性的值。                     |

子绝父相



这里注意消除无序列表的点是list-style，消除超链接的是text-decoration

还有需要设置box-sizing：border-box方便计算

```css
ul{
    list-style: none;
    margin: 0;
    padding: 0;
}

a{
    text-decoration: none;
}

div{
    /* 写css3新增特性，没有设置这个的话，
    每次width和height设置的是content，
    不加margin，border，pading，
    每次要自己计算，
    加了这个就会把padding和border算在content里，
    不需要手动调整*/
    box-sizing: border-box;
}
```



```css
.search{
    position: relative;
    height: 26px;
    border: 1px solid #ccc;
    flex: 1;
    /*设置字体大小、颜色*/
    font-size: 12px;
    color: #666;
	/* 不能把边框算进去，这里设置的是行高 */
    line-height: 24px;
    margin: 7px 10px;
    padding-left: 25px;
    /* 设置边框圆角 */
    border-radius: 5px;
    /* 设置阴影 依次是水平、垂直、模糊、颜色*/
    box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
}
```

```
box-shadow: h-shadow v-shadow blur spread color inset;
```

| 值         | 描述                                     |
| :--------- | :--------------------------------------- |
| *h-shadow* | 必需。水平阴影的位置。允许负值。         |
| *v-shadow* | 必需。垂直阴影的位置。允许负值。         |
| *blur*     | 可选。模糊距离。                         |
| *spread*   | 可选。阴影的尺寸。                       |
| *color*    | 可选。阴影的颜色。请参阅 CSS 颜色值。    |
| inset      | 可选。将外部阴影 (outset) 改为内部阴影。 |



```css
.search::before{
  position: absolute;
  top: 1px;
  left: 5px;

  margin: 5px;
    /*content 属性与 :before 及 :after 伪元素配合使用，来插入生成内容。*/
  content: "";
  width: 15px;
  height: 15px;
    /*这里设置图片，无重复，当前图片内的一部分*/
  background: url(../images/sprite.png) no-repeat -59px -279px;
    /*设置图片大小：高度，宽度*/
  background-size: 104px auto;

}
```



```css
.local-nav{
    height: 64px;
    background-color: #fff;
    margin: 3px 4px;
    /*设置变宽圆角*/
    border-radius: 5px;
    display: flex;
}
```

可以设置元素，选中命名为-1，-2，-3的元素

```css
.local-nav li [class^="local-nav-icon"]{
    width: 32px;
    height: 32px;
    background-color: pink;
    margin-top: 8px;
    background: url(../images/localnav_bg.png) no-repeat 0 0;
    /* 设置缩放，宽度32 高度auto */
    background-size: 32px auto;
}

.local-nav li .local-nav-icon-icon2{
    background-position: 0 -32px;
}
.local-nav li .local-nav-icon-icon3{
    background-position: 0 -64px;
}
.local-nav li .local-nav-icon-icon4{
    background-position: 0 -96px;
}
.local-nav li .local-nav-icon-icon5{
    background-position: 0 -128px;
}
```



```css

/*设置背景渐变，参数为（从哪里开始），（开始颜色）,（结束颜色），前面加前缀-webkit-*/
.nav-common:nth-child(1){
    background: -webkit-linear-gradient(left,pink,red);
}
```

暂时需要用到这些，等到下次遇到不会的再继续写今日2023、8、15