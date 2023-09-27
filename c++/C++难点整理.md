# C++难点



## 指针&&引用：

| 名词             | 赋值与初始化                       |                      | 功能                                                       |
| ---------------- | ---------------------------------- | -------------------- | ---------------------------------------------------------- |
| 指针指向变量     | 1.int *p=0；int sc = 100；p=&sc    |                      |                                                            |
|                  | 2.int *p = &sc                     |                      |                                                            |
| 常量指针指向变量 | 1.int sc = 100;int *const p =&sc   | 声明时就必须初始化， | 无法修改p自身，地址无法修改，可以修改指向的值，            |
| 指针指向常量     | 1.const int *p; int sc=100; p =&sc |                      | 可以修改指针自身，就是存的地址，但无法使用指针修改指向的值 |
| 常量指针指向常量 | 1.const int* const p = &sc         |                      | 无法修改指针自身，无法使用指针修改指向的值                 |



> 函数参数：

```c++
//1.引用传递：函数中改变值
void swap(&x,&y){
    int temp = x;
    x = y;
    y = temp;
}
int a = 1
int b = 2
swap(a,b);
//a = 2, b =1;引用传递直接改变原来的值
​
//2.常量引用传递;不会改变实参
void display(const vector<string> &vec){
    for(vector<string>::const_iterater iter = vec.begin();
        iter!=vec.end();
        iter++)
    {
        cout<<*iter<<endl;
    }
}
display(vec);
//仅会展示，在里面不能进行修改
​
​
//3.返回引用
string &refToElement(vector<string> &vec,int i)
{
    return vec[i];
}
​
//返回的引用赋值给一个变量,不能修改值，这里是对此处的值进行一个复制
string str = refToElement(vec,1);
​
//返回引用赋值给另一个引用
string &pStr = refToElement(vec.2);
​
//可以通过这个新引用修改值
pStr = “新值”;
```



> 函数传指针



> 类

private：在基类可访问，派生类不可访问，main中不可访问

protected：基类可，派生类可，main不可

保护继承：基类的public成员在派生类变成protected



> 数组与指针：

1.

地址[num]被编译器解释为      *（第几个元素的地址+num）

a[5] = {1,2,3,4,5}

*p =&a[2]

p[0]=3

p[1]=4

p[2]=5



2.

在main声明数组后，sizeof



> 变量指针引用

变量是什么?变量就是一个在程序执行过程中可以改变的量。<

换一个角度，变量是一块内存区域的名字，它代表了这块内存区域，当我们对变量进行修改的时候，会引起内存区域中内容的改变。

在计算机看来，内存区域根本就不存在什么名字，它仅有的标志就是它的地址，因此我们若想修改一块内存区域的内容，只有知道他的地址才能实现。

所谓的变量只不过是编译器给我们进行的一种抽象，让我们不必去了解更多的细节，降低我们的思维跨度而已。

程序员拥有引用，但编译器仅拥有指针(地址)。

引用的底层机制实际上是和指针一样的。不要相信有别名，不要认为引用可以节省一个指针的空间，因为这一切不会发生，编译器还是会把引用解释为指针。引用和指针本质上没有区别。“



> 函数返回值的引用

```c++
#include <iostream>

using namespace std;


//这里返回值返回一个引用，代表传一个地址，如果不用引用接收，是创建一个新对象，用引用接收就是还是原来的值，const约束是为了防止下面代码的直接修改值
const int& func_Add(int &a)
{
    a++;
    return a;
}

int main()
{
    int a=0;
    //没用引用接收就是创建了一个新对象
    int b = func_Add(a);
    const int &c = func_Add(a);
    cout<<a<<" "<<&a<<endl;
    cout<<b<<" "<<&b<<endl;
    cout<<c<<" "<<&c<<endl;

    // func_Add(a)=10;加上了const约束不能修改了
    cout<<a<<" "<<&a<<endl;
    return 0;
}
```

如果函数形参是const修饰，返回一个这个const修饰的对象，那么函数返回值也要是const



> 显示转换

Cg g = Cg(8);显式转换

Cg g =(Cg)8;显式转

Cg g = 8；隐式转

Cg g;

g=8;



构造函数加explicit关闭隐式转换



> 继承

派生类可以使用基类的成员，成员函数

![image-20230918203342160](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230918203342160.png)

