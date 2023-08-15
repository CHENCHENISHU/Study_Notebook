# JS学习计划

## 7月23日：js基础

> 主要内容：



1. 现在主要使用let(变量)和const(常量)

2. 主要输入输出手段
   
   ```javascript
    //输出
           document.write('文档内输出内容')
           document.write('<h1>h1标签</h1>')
           //alert和promt先执行
           alert('弹出')
           console.log('控制台输出')
    //输入
           prompt('请输入年龄')
   ```

3. 模板字符串
   
   ```javascript
           let name = 19;
   //这里模板字符串输出时要加``
           document.write(`我叫${name}`)
           document.write(typeof name)
   //字符串拼接''和“”要单独或者使用\转义
           document.write("你好啊'嘉然'")
           document.write('你好啊"嘉然"')
           document.write('你好啊\'嘉然\'')
   ```
   
   

4. 转换
   
   | 转换类型             | 转换方法              |
   | ---------------- | ----------------- |
   | **显式转换**(转换为数字)  | Number()          |
   |                  | parse             |
   | **显式转换**(转换为字符串) | String            |
   |                  | .toString括号里可以跟进制 |
   | **隐式转换**(转换为数字)  | +可以解析转换成Number    |
   | **隐式转换**(转换为字符串) | 任何数据和字符串相加都是字符串   |
   
   

5. 今日作业
   
   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
   </head>
   <style>
       h2 {
           text-align: center;
       }
   
       table {
           /* 合并边框 */
           border-collapse: collapse;
           height: 80px;
           margin: 0 auto;
           text-align: center;
       }
   
       th {
           /* 先上下，再左右 */
           padding: 20px 10px;
       }
   
       td {
   
           padding: 20px 5px;
       }
   
       table,
       th,
       td {
           border: 1px solid black;
       }
   </style>
   
   <body>
       <script>
           let name = prompt('请输入商品名称')
           let price = +prompt('请输入商品价格')
           let num = +prompt('请输入商品数量')
           let priceAll = price * num
           let address = prompt('请输入收货地址')
           document.write(`
           <h2>订单付款确认页面</h2>
               <table>
                   <tr>
                       <th>商品名称</th>
                       <th>商品价格</th>
                       <th>商品数量</th>
                       <th>总价</th>
                       <th>收货地址</th>
                   </tr>
                   <tr>
                       <td>${name}</td>
                       <td>${price}</td>
                       <td>${num}</td>
                       <td>${priceAll}</td>
                       <td>${address}</td>
                   </tr>
               </table>
           `)
       </script>
   
   </body>
   
   </html>
   ```

## 8月3日

1. 优先使用const，建议数组和对象使用const声明，不修改地址就行

## 8月4日

### 事件监听

元素.addEventListener('事件类型',要执行的函数)

事件源：获取dom对象

事件类型：什么方式，click

事件调用的函数：要做什么事

之前的写法落后且重写会造成覆盖，add这种不会

### 鼠标事件

click	鼠标点击

mouseenter	鼠标经过

mouseleave	鼠标离开

### 焦点事件

focus	获得焦点

blur	失去焦点

### 键盘事件

Keydown	键盘按下触发

Keyup	键盘抬起触发

### 文本事件

input	用户输入事件



## 8.14事件流

从大到小捕获（父到子）

Dom.addEventLisnter('触发机制'，function,是否采用捕获（true）)

### 冒泡

从小到大冒泡（子到父）主要使用

一个元素触发事件后，依次向上调用同名事件

### 阻止冒泡

事件对象.stopPropagation()阻止流动传播

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .father{
            width: 500px;
            height: 500px;
            background-color: pink;
        }
        .son{
            width: 200px;
            height: 200px;
            background-color: #fff;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son"></div>
    </div>
    <script>
        const father = document.querySelector('.father')
        const son = document.querySelector('.son')
        father.addEventListener('click',function(){
            alert('我是爸爸')
        })
        son.addEventListener('click',function(e){
            alert('我是儿子')
            e.stopPropagation()
        })
       
        document.addEventListener('click',function(){
            alert('我是爷爷')
        })

    </script>
</body>
</html>
```

阻止默认事件

e.preventDefault()

```javascript
const btn = document.querySelector('button')
        btn.addEventListener('click',function(e){
            e.preventDefault()
        })
```





### 事件解绑

removeEventListener(事件类型，事件处理函数，获取捕获或冒泡阶段)

```javascript
const btn = document.querySelector('button')
        btn.addEventListener('click',fn)
        btn.removeEventListener('click',fn)

        function fn(){
            alert('点击一次')
        }
```

 匿名函数无法被解绑

 mouseover、mouseout会触发冒泡

mouseenter、mouseleave不会



### 事件委托

给父级注册，之后用事件属性e,e.target是类型，可以使用e.target.tagName判断是否是自己想要的类型

```javascript
  const tab = document.querySelector('.tab ul')
        tab.addEventListener('click',function(e){
            if(e.target.tagName==='A'){
                document.querySelector('.tab .active').classList.remove('active')
                e.target.classList.add('active')
                // console.log(e.target.dataset.id);
                // 这里要把此id转换为数字型
                const id = +e.target.dataset.id
                console.log(id);
                // 排他思想，去除之前的active
                document.querySelector('.tab-content .active').classList.remove('active')
                
                // console.log(document.querySelector(`.tab-content .item:nth-child(2)`));
                document.querySelector(`.tab-content .item:nth-child(${id+1})`).classList.add('active')
            }
        })
```



### 页面滚动

scrollTop和scrollLeft获取数字 

```javascript
// window.addEventListener('scroll',function(){
        //     console.log('滚');
        // })

        // scrollLeft和scrollTop(属性)
        document.querySelector('div').addEventListener('scroll',function(){
            //被卷去的头部
            console.log(this.scrollTop);
        })

        window.addEventListener('scroll',function(){
            //可以被读取和修改，是数字型的
           console.log( document.documentElement.scrollTop);
        })
```

window.scrollTo(x,y)可以控制滚动到目标位置



### 页面尺寸

clientHeight

clientWidth


```javascript
    window.addEventListener('resize',function(){
        let w = document.documentElement.clientWidth
        let h = document.documentElement.clientHeight
        console.log(w,h);
    })
```



> offsetWidth和offsetHeight

内容+padding+border

> offsetTop，offsetLeft

带有定位的父级

如果都没有以文档左上角为准



浏览器的大小

```javascript
window.addEventListener('resize',function(){
            let w = document.documentElement.clientWidth
            let h = document.documentElement.clientHeight
            console.log(w,h);
        })
```





### 总结使用

| 属性                      | 作用                                     | 说名                                                         |
| ------------------------- | ---------------------------------------- | ------------------------------------------------------------ |
| scrollLeft和scrollTop     | 被卷去的头部和左侧                       | 配合页面滚动来写，可读写的属性（可以）                       |
| clientWidth和clientHeight | 获得元素宽度和高度                       | 不包含border，margin，滚动条，用于js获取元素大小，只读属性（不可赋值） |
| offsetWidth和offsetHeight | 获取元素宽度和高度                       | 包含border、padding、滚动条等，只读                          |
| offsetLeft和offsetTop     | 获取元素距离自己定位父级元素的左、上距离 | 获取元素位置时使用，只读属性                                 |



> 电梯导航实例

```javascript
<script>

    //第一大模块,页面滑动可以显示和隐藏
    (function(){
      //得到中间的焦点图
    const entry  = document.querySelector('.xtx_entry')
    const elevator = document.querySelector('.xtx-elevator')
    //1.页面滚动大于300px,显示电梯导航
    //2.页面添加滚动事件
    window.addEventListener('scroll',function(){
      const n = document.documentElement.scrollTop
      // opacity指定此元素的不透明度
      if(n>=300){
        elevator.style.opacity=1
      }else{
        elevator.style.opacity=0
      }
      elevator.style.opacity = n >=entry.offsetTop?1:0
    })

    //点击返回页面顶部
    const backTop = document.querySelector('#backTop')
    backTop.addEventListener('click',function(){
      // document.documentElement.scrollTop=0
      window.scrollTo(0,0)
    })
    })();
    
    // 第二模块
    (function(){
      //2.点击页面可滑动
      const list = document.querySelector('.xtx-elevator-list')
      list.addEventListener('click',function(e){
        // console.log(11);
        if(e.target.tagName==='A'&&e.target.dataset.name){
          //排他思想
          const old = document.querySelector('.xtx-elevator-list .active')
        
          if(old) old.classList.remove('active')

          e.target.classList.add('active')

          //获取当前模块的大模块类名
          const name = document.querySelector(`.xtx_goods_${e.target.dataset.name}`)

          console.log(e.target.dataset.name);
          console.log(name);
          document.documentElement.scrollTop =name.offsetTop
        
        }
      })


      //3.页面滚动
      window.addEventListener('scroll',function(){
        //3.1先移除类
        const old = document.querySelector('.xtx-elevator-list .active')
        if(old) old.classList.remove('active')

        //获取各个大盒子距离
        const goodsNew = document.querySelector('.xtx_goods_new').offsetTop
        const goodsPopular = document.querySelector('.xtx_goods_popular').offsetTop
        const goodsBrand = document.querySelector('.xtx_goods_brand').offsetTop
        const goodsTopic = document.querySelector('.xtx_goods_topic').offsetTop
        // console.log(goodsNew,goodsBrand,goodsCategory,goodsTopic);
        // 页面卷入的距离
        const top = document.documentElement.scrollTop
        if(top>=goodsNew&&top<goodsPopular){
          document.querySelector('[data-name=new]').classList.add('active')
        }else if(top>=goodsPopular&&top<goodsBrand){
          document.querySelector('[data-name=popular]').classList.add('active')
        }else if(top>=goodsBrand&&top<goodsTopic){
          document.querySelector('[data-name=brand]').classList.add('active')
        }else if(top>=goodsTopic){
          document.querySelector('[data-name=topic]').classList.add('active')
        }
   
      })
      


          
    })()
  </script>

```

获取元素位置另一种方法

```javascript
<script>
    const div = document.querySelector('div')
    console.log(div.getBoundingClientRect());
</script>
```

