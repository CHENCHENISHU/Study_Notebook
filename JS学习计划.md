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
