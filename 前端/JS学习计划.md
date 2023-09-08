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
                //toggle事件可以直接切换class
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

## 8/16

### DOM节点

![image-20230816201859349](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230816201859349.png)

类型：

元素节点

- 所有标签：body、div
- html根节点

属性节点

- 所有属性比如href

文本节点

- 所有文本

其他



> 兄弟节点

```html
 <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
    <script>
        const li2 = document.querySelector('ul li:nth-child(2)')
        console.log(li2.previousElementSibling);//上一个兄弟
        console.log(li2.nextElementSibling);//下一个兄弟
    </script>

    
```



> 父节点

```html
<body>
    <div class="dad">
        <div class="baby"></div>
    </div>
    <script>
        const baby = document.querySelector('.baby')
        console.log(baby.parentNode);

        // childNodes获取所有子节点，文本节点（空格、换行）、注释节点
        //children属性获取所有元素节点、返回伪数组
        console.log(baby.parentNode.children[0]);
    </script>
</body>
```



> 增加节点

```html
<body>
    <ul></ul>
    <script>
        //1.创建节点
        // const div =   document.createElement('div')
         //2.追加节点
        // 父元素.appendChild(div)
        //2.1插入到父元素得最后一个子元素
        // document.body.appendChild(div)
        // console.log(div);

        const ul =document.querySelector('ul')
        const li = document.createElement('li')
        li.innerHTML='我是li'
        //2.2插入到某个子元素得前面
        // insertBefore(插入的元素,放到哪个元素前面)
        ul.insertBefore(li,ul.children[0])

    </script>
</body> 
```



> 复制节点

```html
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        // 元素.cloneNode(true)有true会把值也拿过来，没有的话只会拿标签
        //1.克隆节点
        const ul = document.querySelector('ul')
        const LI1= ul.children[0].cloneNode(true)
        console.log(LI1);
        //2.追加
        ul.appendChild(LI1)
    </script>
</body>
```



> 删除节点

```html
<ul>
        <li>没用得</li>
    </ul>
    <script>
        const ul =document.querySelector('ul')
        // 删除节点 父元素.removeChild(子元素)
        ul.removeChild(ul.children[0])
    </script>
```



MOBILE事件

touchstart手指触摸到一个dom元素触发

touchmove手指在一个dom元素上滑动时触发

touchend手指在一个dom元素上移开触发



### window对象

BOM浏览器对象模型

![image-20230818200348610](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230818200348610.png) 

document，alert(),console.log()都是window得属性，window对象下属性和方法调用可以省略window

### 定时器

延迟函数

setTimeOut(function(){

},毫秒数)

只执行一次

### 同步和异步

同步在主线程执行，形成执行栈

异步通过回调函数执行

1. 普通事件，click，resize
2. 资源加载，load，error
3. 定时器，setInterval，setTimeout

异步任务相关添加到任务队列中

> 执行机制

![image-20230818202234946](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230818202234946.png)

![image-20230818202551729](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230818202551729.png)

event loop

### location对象

location.href可以跳转页面

```javascript
<a href="http://www.bilibili.com"></a>
    <script>
        const jump = document.querySelector('a')
        let i = 5
       let a = setInterval(function(){
            jump.innerHTML=
            `
            支付成功,${i--}秒后跳转
            `
            if (i===0) {
                clearInterval(a)
                location.href='http://www.bilibili.com'
                
            }
        },1000)
            
        
    </script>
```

location.search

可以获得页面提交的值,获得地址中？后得内容

location.hash

获取地址中哈希值，#后得内容

```javascript
	<a href="#/my">我的</a>
    <a href="#/friend">下载</a>
    <a href="#/download">我的</a>
```



### navigatiuon对象

```javascript
// 检测 userAgent（浏览器信息）
        !(function () {
            const userAgent = navigator.userAgent
            // 验证是否为Android或iPhone
            const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
            const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
            // 如果是Android或iPhone，则跳转至移动站点
            if (android || iphone) {
                location.href = 'http://m.itcast.cn'
            }
        })()
```

### histroy对象

```javascript
<button>后退</button>
    <button>前进</button>
    <script>
        const back = document.querySelector('button:first-child')
        const forward =back.nextElementSibling
        back.addEventListener('click',function(){
            // history.back()
            history.go(-1)
        })
        forward.addEventListener('click',function(){
            history.forward()
            history.go(1)
        })
    </script>
```

## 8/19

## 本地存储  

### localStorage

```javascript
*//存一个名字*

*// localStorage.setItem('键','值')*

localStorage.setItem('uname','嘉然')

*//获取*

console.log(localStorage.getItem('uname'));

*//删除*

localStorage.removeItem('uname')
*//改
localStorage.setItem('uname','贝拉 ')
```

本地存储只能存字符串；获取时都是字符串

在本地存储可以查看



> 存取复杂类型

```javascript
const obj ={
            name:'jiaran',
            age:18
        }
        localStorage.setItem('obj',JSON.stringify(obj))
        console.log(localStorage.getItem('obj'));
        console.log(JSON.parse(localStorage.getItem('obj')));
```



> 字符串拼接使用：map()和join()数组方法实现字符串拼接

### map：

遍历数组处理数据，返回新数组

join:

把数组中所有元素转换为一个字符串

```javascript
<script>
        const arr = ['red', 'blue', 'pink']

        const newArr = arr.map(function (ele, index) {

            return ele + '颜色'
        })
        console.log(newArr);

        //默认逗号分隔
        console.log(newArr.join());//red颜色,blue颜色,pink颜色
</script>
```



## 8/20

正则表达式

```javascript
<script>
        const str = '我在学前端'

        const reg = /前端/

        //reg是规则，后面是被检查
        console.log(reg.test(str));
        //true

        console.log(reg.exec(str));
        //返回字符串，搜索功能，找到返回数组，没找到返回空
</script>
```



### 元字符：

> 1.边界符

表示位置，开头和结尾，必须用什么开头，用什么结尾

| 边界符 | 说明                     |
| ------ | ------------------------ |
| ^      | 匹配行首的文本(以谁开始) |
| $      | 匹配行尾的文本(以谁结束) |

^和$在一起，表示必须是精确匹配，^你好$表示只能是‘你好’

> 2.量词

表示重复次数

| 量词  | 说明                 |
| ----- | -------------------- |
| *     | 重复0次或多次        |
| +     | 重复一次或多次       |
| ？    | 重复零次或一次       |
| {n}   | 重复n次              |
| {n,}  | 重复n次或大于等于n次 |
| {n,m} | 重复n到m次           |

```javascript
		//大于或等于0次
		console.log(/^哈$/.test('哈'));//true
        console.log(/^哈*$/.test(''));//true
        console.log(/^哈*$/.test('哈哈'));//true
        console.log(/^哈*$/.test('二哈傻'));//false
        console.log(/^哈*$/.test('哈很傻'));//false
        console.log(/^哈*$/.test('哈很哈'));//false
```



> 3.字符类

\d表示0~9

1. []匹配字符集合

   [^a-z]匹配除了26个小写字母之外其他任何单个字符

   ```javascript
   <script>
           console.log(/[abc]/.test('beila'));//true，只要有abc中一个字符，就匹配成功
   
    		console.log(/[a-z]/.test('beila'))//true
   
   		//只能输入一个字符且为大小写1和数字
   		console.log(/^[a-zA-Z0-9]$/.test('b'))//true
   		
   </script>
   ```

2. .匹配除了换行符外任何单个字符

3. 预定义：简写方式

   | 预定类 | 说明                                                       |
   | ------ | ---------------------------------------------------------- |
   | \d     | 匹配0-9任一数字，相当于[0-9]                               |
   | \D     | 匹配所有0-9以外字符，相当于[^0-9]                          |
   | \w     | 匹配任意的字母，数字和下划线，相当于[A-Za-z0-9_]           |
   | \W     | 除所有字母、数字和下划线以外的字符，相当于[^A-Za-z0-9_]    |
   | \s     | 匹配空格（包括换行符、制表符、空格符）、相等于[\t\r\n\v\f] |
   | \S     | 匹配非空格的字符，相当于[^\t\r\n\v\f]                      |

   日期格式：^\d{4}-\d{1,2}-\d{1,2}



## 8/21

### 作用域

规定变量能被访问的范围

1. 局部作用域

   函数作用域：函数内部

2. 全局作用域

### 闭包

内层函数+外层函数的变量

可以封闭数据，数据私有，外部可以访问函数内部的变量

```javascript
<script>
        //闭包，封闭数据，
        // function outer(){
        //     let i = 1
        //     function fn(){
        //         console.log(i);
        //     }
        //     return fn
        // }
        // const fun = outer()
        // fun() //1


        //统计函数调用
        // let i =1
        // function fn(){
        //     i++
        //     console.log(i);
        // }

        function count() {
            let i = 1
            function fn() {
                i++
                console.log(i);
            }
            return fn
        }
        const fun2 = count()
        
    </script>
```

### 函数参数

> 动态参数：

```javascript
<script>
        //不知多少参数
        function  getSum(){
    		//伪数组
            console.log(arguments);
        }
        getSum(2,3)
    </script>
```

> 剩余参数：

```javascript
 <script>
        function getSum(a,b,...arr){
     		//获得的是真数组
            console.log(arr);
        }
        getSum(1,2,3)
  </script>
```



### 展开运算符

不修改原数组

```javascript
<script>
        const arr = [1,2,3,4,5]
        console.log(...arr);
        //数组最大值
        console.log(Math.max(...arr));//5

        //合并数组
        const arr1 = [7,8,9]
        const arr2 = [...arr,...arr1]
        console.log(...arr2);
    </script>
```



### 箭头函数



```javascript
<script>
        const fn = function () {
            console.log(123);
        }
        //箭头函数基本语法
        const fn2 = () => {
            console.log(123);
        }
        fn2()

        //传参，当只有一个参数，可以省略小括号
        const fn3 = (x) => {
            console.log(x);
        }

        //一行代码时可以省略大括号
        const fn4 = (x) => console.log(x);

        //直接返回值
        const fn5 = (x) => x + x;
        console.log(fn5(2));//4

        //直接返回对象
        const fn6 = uname => ({uname:uname});
        console.log(fn6('嘉然'));//4

    </script>
```



```javascript
<script>
        const user = {
            name:'嘉然',
            sleep:function(){
                console.log(this);//指向user
                const fn=()=>{
                    console.log(this);//指向user
                    //箭头函数里没有this会向上层去找
                }
            fn()
            }
        }
        user.sleep()
    </script>
```

### 数组解构

```javascript
<script>
        const arr = [100,60,80]
        const [max,min,avg] = arr 
        console.log(max,min,avg);

        const [a,b,...c] = [1,2,3,4,5,6]
        console.log(a,b,c);//1,2,[3,4,5,6]
</script>
```

### 对象解构

```javascript
<script>
        const obj = {
            uname:'chenxiang',
            age:20

        }

        //属性名和变量名必须相同
        const {uname,age } = {uname:'chenxiang',age:20 }
        console.log(uname,age);

        const {name:uname,age} ={name:'佩奇',age:6}
            console.log(uname);

        const [{name:uname,age}] = [{name:'佩奇',age:6}]
        console.log(uname);

        const pig ={
            name:'佩奇',
            family:{
                mother:'猪妈妈',
                father:'猪爸爸',
                brother:'乔治'
            },
            age:6
        }

        //多级对象解构
        const {name,family:{mother,father,brother}}=pig
        console.log(name);
        console.log(mother);
        console.log(father);
        console.log(brother);
    </script>
```

### foreach



```javascript
被遍历的数组.forEach(function(当前数组元素,当前元素索引)){
	函数体
}
//索引号可写可不写
```



## 8/25

### 对象

> 创建对象：

1.const obj={ }

2.const 0bj = new Object({

})

3.构造函数创建：

```javascript
   <script>
        function Pig(name,age,gender){
            this.name=name
            this.age = age
            this.gender = gender
        }
        const pege = new Pig('佩奇',6,'女')
        console.log(pege);
    </script>
```



> 静态成员：

```javascript
<script>
        function Pig(name){
            this.name = name
        }
        Pig.eyes = 2
        Pig.sayHi = function () {
            console.log(this);
        }
        Pig.sayHi()
    </script>
```



> Object常用静态方法：

1.Object.keys(对象):

2.Object.values(对象)

3.Object.assign(oo，o)把o拷贝给oo

获取对象所有属性名



> Array

1.Array.forEach()遍历数组,查找遍历数组元素

2.Array.filter()过滤数组，返回的筛选满足条件的数组元素

3.Array.map()迭代数组，返回处理后的数组元素，想要使用返回的新数组

4.Array.reduce(function(上一次值，当前值){}，初始值)累计器，返回累计处理的结果，求和等

Array.reduce(function(){}，初始值)

![image-20230825173134338](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230825173134338.png)



> String

![image-20230825173252258](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230825173252258.png)



> Number

![image-20230825174110816](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230825174110816.png)



## 8月26

原型：公共属性写在构造方法里，公共方法写原型方法

```javascript
<script>
        function Star(name,age) {
            this.name = name
            this.age = age
        }
        Star.prototype.sing = function () {
            console.log('唱歌');
        }
        const dj = new Star('顶针',18)
        const wy = new Star('王源',20)
        console.log(wy.sing===dj.sing);
    </script>
```

constructor指回原本的构造函数的this



![image-20230827142427952](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230827142427952.png)



### 拷贝

> 浅拷贝：

只拷贝外层的

const obj = { }

const o1 ={...obj}

拷贝外层和内部

const o2 = { }

Object.assign(o,obj)



> 深拷贝

暂时不会



> 处理异常

throw

try/catch捕获异常

debugger



### this指向

普通函数的this指向：谁调用，就是谁

和箭头函数：外层的this，并不存在this



> 改变this

call

apply

bind



### 性能优化

debounce

防抖：单位时间内，频繁触发事件，只执行最后一次
