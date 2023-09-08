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


//3.返回引用
string &refToElement(vector<string> &vec,int i)
{
    return vec[i];
}

//返回的引用赋值给一个变量,不能修改值，这里是对此处的值进行一个复制
string str = refToElement(vec,1);

//返回引用赋值给另一个引用
string &pStr = refToElement(vec.2);

//可以通过这个新引用修改值
pStr = “新值”;
```



> 函数传指针



