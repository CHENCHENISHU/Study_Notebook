# GO学习

## 1.go的数字类型、

> 整型

| 类型     | 描述                                         |
| ------ | ------------------------------------------ |
| uint8  | 0 到 255                                    |
| uint16 | 0 到 65535                                  |
| uint32 | 0 到 4294967295                             |
| uint64 | 0 到 18446744073709551615                   |
| int8   | -128 到 127                                 |
| int16  | -32768 到 32767                             |
| int32  | -2147483648 到 2147483647                   |
| int64  | -9223372036854775808 到 9223372036854775807 |



> 浮点型

| 类型         | 描述               |
| ---------- | ---------------- |
| float32    | IEEE-754 32位浮点型数 |
| float64    | IEEE-754 64位浮点型数 |
| complex64  | 32 位实数和虚数        |
| complex128 | 64 位实数和虚数        |



> 其他数字类型

| 类型      | 描述           |
| ------- | ------------ |
| byte    | 类似uint8      |
| rune    | 类似uint32     |
| uint    | 32或64位       |
| int     | 和uint一样大     |
| uintptr | 无符号整型，用于存放指针 |



## 2.语言变量/常量

> 声明变量

```go
  var i int
    var f float64
    var b bool
    var s string
    fmt.Printf("%v %v %v %q\n", i, f, b, s)//0 0 false ""
```

常用：

v_name := value



> 常量 

```go
   const LENGTH int = 10
   const WIDTH int = 5  
   var area int
   const a, b, c = 1, false, "str" //多重赋值

   area = LENGTH * WIDTH
   fmt.Printf("面积为 : %d", area)//50
   println()
   println(a, b, c)  1,false,str
```

**用作枚举**

```go
package main

import "unsafe"
const (
    a = "abc"
    b = len(a)
    c = unsafe.Sizeof(a)
)

func main(){
    println(a, b, c)//abc 3 16
}
```

**iota**

```go
const (
		a = iota//0
		B        //1
		c        //2
		d = "ha" //ha
		e        //ha
		F = 10    //10
		g        //10
		h = iota //7
		I        //8
	)
	fmt.Println(a, B, c, d, e, F, g, h, I)
```

出现iota，从0开始，以下都递增，遇到字符串(遇到**再次赋值**)以下都成字符串（再次赋值的值），直到再次遇到iota

**实例**

```go
const(
		aa=1<<iota//1 2^0
		bb=3<<iota//6 2^1
		cc//12 2^2
		dd//24 2^3
	)
```

<<n指左移多少位，二进制位

也等同于*(2^n)



## 3.运算符

### 算术运算符

| 运算符 | 描述  |
| --- | --- |
| +   | 相加  |
| -   | 相减  |
| *   | 相乘  |
| /   | 相除  |
| %   | 求余  |
| ++  | 自增  |
| --  | 自减  |

### 关系运算符

| 运算符 | 描述                                                              |
| --- | --------------------------------------------------------------- |
| ==  | 检查两个值是否相等，如果相等返回 True 否则返回 False                                |
| !=  | 检查两个值是否不相等，如果不相等返回 True 否则返回 False。 |
| >   | 检查左边值是否大于右边值，如果是返回 True 否则返回 False。                             |
| <   | 检查左边值是否小于右边值，如果是返回 True 否则返回 False。                             |
| >=  | 检查左边值是否大于等于右边值，如果是返回 True 否则返回 False。                           |
| <=  | 检查左边值是否小于等于右边值，如果是返回 True 否则返回 False。                           |

### 逻辑运算符

| 运算符 | 描述                                                |
| --- | ------------------------------------------------- |
| &&  | 逻辑 AND 运算符。 如果两边的操作数都是 True，则条件 True，否则为 False。   |
| |\| | 逻辑 OR 运算符。 如果两边的操作数有一个 True，则条件 True，否则为 False。   |
| ！   | 逻辑 NOT 运算符。 如果条件为 True，则逻辑 NOT 条件 False，否则为 True。 |

### 位运算符

| p   | q   | p&q | p\|q | p^q |
| --- | --- | --- | ---- | --- |
| 0   | 0   | 0   | 0    | 0   |
| 0   | 1   | 0   | 1    | 1   |
| 1   | 1   | 1   | 1    | 1   |
| 1   | 0   | 0   | 1    | 1   |

| 运算符 | 描述                                                                                    |
| --- | ------------------------------------------------------------------------------------- |
| &   | 按位与运算符"&"是双目运算符。 其功能是参与运算的两数各对应的二进位相与。                                                |
| |   | 按位或运算符"\|"是双目运算符。 其功能是参与运算的两数各对应的二进位相或                                                |
| ^   | 按位异或运算符"^"是双目运算符。 其功能是参与运算的两数各对应的二进位相异或，当两对应的二进位相异时，结果为1。                             |
| <<  | 左移运算符"<<"是双目运算符。左移n位就是乘以2的n次方。 其功能把"<<"左边的运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 |
| >>  | 右移运算符">>"是双目运算符。右移n位就是除以2的n次方。 其功能是把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数。           |

### 赋值运算符

| 运算符 | 描述                      |
| --- | ----------------------- |
| =   | 简单的赋值运算符，将一个表达式的值赋给一个左值 |
| +=  | 相加后再赋值                  |
| -=  | 相减后再赋值                  |
| *=  | 相乘后再赋值                  |
| /=  | 相除后再赋值                  |
| %=  | 求余后再赋值                  |
| <<= | 左移后赋值                   |
| >>= | 右移后赋值                   |
| &=  | 按位与后赋值                  |
| ^=  | 按位异或后赋值                 |
| |=  | 按位或后赋值                  |

### 其他

| 运算符 | 描述       |
| --- | -------- |
| &   | 返回变量存储地址 |
| *   | 指针变量。    |

## 4.条件语句

### if语句

```go
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 10
 
   /* 使用 if 语句判断布尔表达式 */
   if a < 20 {
       /* 如果条件为 true 则执行以下语句 */
       fmt.Printf("a 小于 20\n" )
   }
   fmt.Printf("a 的值为 : %d\n", a)
}
```



### if else语句

```go
package main

import "fmt"

func main() {
   /* 局部变量定义 */
   var a int = 100;
 
   /* 判断布尔表达式 */
   if a < 20 {
       /* 如果条件为 true 则执行以下语句 */
       fmt.Printf("a 小于 20\n" );
   } else {
       /* 如果条件为 false 则执行以下语句 */
       fmt.Printf("a 不小于 20\n" );
   }
   fmt.Printf("a 的值为 : %d\n", a);

}
```

### if嵌套

### switch语句

```go
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var grade string = "B"
   var marks int = 90

   switch marks {
      case 90: grade = "A"
      case 80: grade = "B"
      case 50,60,70 : grade = "C"
      default: grade = "D"  
   }

   switch {
      case grade == "A" :
         fmt.Printf("优秀!\n" )    
      case grade == "B", grade == "C" :
         fmt.Printf("良好\n" )      
      case grade == "D" :
         fmt.Printf("及格\n" )      
      case grade == "F":
         fmt.Printf("不及格\n" )
      default:
         fmt.Printf("差\n" );
   }
   fmt.Printf("你的等级是 %s\n", grade );      
}
```



> Type Switch

```go
switch x.(type){
    case type:
       statement(s);      
    case type:
       statement(s); 
    /* 你可以定义任意个数的case */
    default: /* 可选 */
       statement(s);
}
```

使用 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。

go语言的switch不需要每条语句后写break



### select语句

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	c1 := make(chan string)
	c2 := make(chan string)

	go func() {
		time.Sleep(1 * time.Second)
		c1 <- "ONE"
	}()

	go func() {
		time.Sleep(2 * time.Second)
		c2 <- "TWO"
	}()

	for i := 0; i < 2; i++ {
		select {
		case msg1 := <-c1:
			fmt.Println("received", msg1)
		case msg2 := <-c2:
			fmt.Println("received", msg2)
		}

	}
}
```

> 解释

创建两个通道c1和c2

select等待两个通道数据

以上实例启动两个协程从两个通道获取数据，如果两个通道没有可用数据，执行default子句



## 5.循环语句

### for循环

> 1. for init;condition;post{ } 和c语言的for循环一致

- init：赋值表达式，变量赋初值
- condition：关系表达式或逻辑表达式，循环控制
- post：赋值表达式，控制变量增量或减量

```go
for i := 0; i <= 10; i++ {
         sum += i
      }
```

```go
sum := 1
for ; sum <= 10; {
      sum += sum
   }
```
> ​	2.for condition{ } 和while一样

```go
for {
      sum++ // 无限循环下去
   }
```

> ​	3.for{ }

1. for-each range

   ```go
   package main
   import "fmt"
   
   func main() {
      strings := []string{"google", "runoob"}
      for i, s := range strings {
         fmt.Println(i, s)
      }
   
   
      numbers := [6]int{1, 2, 3, 5}
      for i,x:= range numbers {
         fmt.Printf("第 %d 位 x 的值 = %d\n", i,x)
      }  
   }
   ```

   

2. key和value

   ```go
   package main
   import "fmt"
   
   func main() {
       map1 := make(map[int]float32)
       map1[1] = 1.0
       map1[2] = 2.0
       map1[3] = 3.0
       map1[4] = 4.0
      
       // 读取 key 和 value
       for key, value := range map1 {
         fmt.Printf("key is: %d - value is: %f\n", key, value)
       }
   
       // 读取 key
       for key := range map1 {
         fmt.Printf("key is: %d\n", key)
       }
   
       // 读取 value
       for _, value := range map1 {
         fmt.Printf("value is: %f\n", value)
       }
   }
   ```

   

### 循环嵌套

### break

> 跳出当前循环，不执行下一次循环

### continue

> 跳出当前循环，执行下一次循环

### goto

> 跳过本次循环并到达goto后的语句



## 6.函数

```go
func function_name( [parameter list] ) [return_types] {
   函数体
}
```

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println(max(1, 2))

}

func max(num1, num2 int) int {
	var result int
	if num1 > num2 {
		result = num1
	} else {
		result = num2
	}
	return result
}
```

也可以返回多个值

可以通过引用传递来交换值

## 7.数组

> 初始化

```go
var arrayName [size]dataType
```

*var* arr  =[6]int {1,2,3,4,5,6}

```go
package main

import "fmt"

func main() {
   var n [10]int /* n 是一个长度为 10 的数组 */
   var i,j int

   /* 为数组 n 初始化元素 */        
   for i = 0; i < 10; i++ {
      n[i] = i + 100 /* 设置元素为 i + 100 */
   }

   /* 输出每个数组元素的值 */
   for j = 0; j < 10; j++ {
      fmt.Printf("Element[%d] = %d\n", j, n[j] )
   }
}
```

## 8.指针

n=1

可以用*p=n

p代表的是其地址

可以用&n表示

p=1，传入&n后的函数，相当于传入了n的地址，

可以直接改变值

> 多维数组

```go
package main

import "fmt"

func main() {
    // 创建空的二维数组
    animals := [][]string{}

    // 创建三一维数组，各数组长度不同
    row1 := []string{"fish", "shark", "eel"}
    row2 := []string{"bird"}
    row3 := []string{"lizard", "salamander"}

    // 使用 append() 函数将一维数组添加到二维数组中
    animals = append(animals, row1)
    animals = append(animals, row2)
    animals = append(animals, row3)

    // 循环输出
    for i := range animals {
        fmt.Printf("Row: %v\n", i)
        fmt.Println(animals[i])
    }
}
```



## 9.结构体

```go
package main

type books struct {
	title   string
	author  string
	subject string
	bookId  int
}

func main() {
	var book1 books

	book1.title = "go语言"
	book1.author = "嘉然"
	book1.subject = "程序"
	book1.bookId = 0
	println(book1.bookId)

}
```

> 指针值传递

```go
package main

import "fmt"

type books struct {
	title   string
	author  string
	subject string
	bookId  int
}

func main() {
	var book1 books

	book1.title = "go语言"
	book1.author = "嘉然"
	book1.subject = "程序"
	book1.bookId = 0
	printbook(&book1)

}

// 前面指形参 后面是类型
func printbook(book *books) {
	fmt.Println(book.bookId)
	fmt.Println(book.title)
	fmt.Println(book.author)
	fmt.Println(book.subject)
}
```

## 10.切片

### 定义切片

```go
var slice []type = make([]type,len)
slice :=make([]type ,len ,capacity)
```

指定一个数组来定义一个切片，len为长度，capacity为容量

### 切片初始化

```go
var arr = [6]int{1, 2, 3, 4, 5, 6}
	//[]是切片类型
	s := []int{1, 2, 3}
	//截取数组为切片
	s1 := arr[1:3]
	//可以使用make()初始化
	s2 := make([]int, 10, 10)
	fmt.Println(s, s1, s2)

```

### 常用函数

#### len()和cap()

```go
var num = make([]int, 3, 5)
fmt.Println(len(num), cap(num))
```

len指长度，cap指的是容量

> 深入cap

```go
package main

import "fmt"

func main() {
	nums := []int{1, 2, 3, 4, 5, 6}
	printslice(nums) //len=6 cap=6 slice=[1 2 3 4 5 6]

	num1 := nums[:3]
	printslice(num1) //len=3 cap=6 slice=[1 2 3]

	num2 := nums[2:5]
	printslice(num2) //len=3 cap=4 slice=[3 4 5]

}
func printslice(slice []int) {
	fmt.Printf("len=%d cap=%d slice=%v\n", len(slice), cap(slice), slice)
}
```

#### append()和copy()

```go
package main

import (
	"fmt"
)

func main() {
	var nums []int
	printSlice(nums)//len=0 cap=0 slice=[]

	nums = append(nums, 0)
	printSlice(nums) //len=1 cap=1 slice=[0]

	nums = append(nums, 1, 2, 3, 4)
	printSlice(nums) //len=5 cap=6 slice=[0 1 2 3 4]

	nums1 := make([]int, len(nums), (cap(nums))*2)
	copy(nums1, nums)
	printSlice(nums1) //len=5 cap=12 slice=[0 1 2 3 4]

}
func printSlice(slice []int) {
	fmt.Printf("len=%d cap=%d slice=%v\n", len(slice), cap(slice), slice)
}

```

## 11.范围Range

### 循环数组

```go
package main

import "fmt"

func main() {
	var pow = []int{1, 2, 3, 4, 5, 6, 7, 8}

	for i, v := range pow {
		fmt.Printf("数字索引为%d，数值为%d\n", i, v)
	}
}

```

### 循环map

```go
package main
import "fmt"

func main() {
    map1 := make(map[int]float32)
    map1[1] = 1.0
    map1[2] = 2.0
    map1[3] = 3.0
    map1[4] = 4.0
   
    // 读取 key 和 value
    for key, value := range map1 {
      fmt.Printf("key is: %d - value is: %f\n", key, value)
    }

    // 读取 key
    for key := range map1 {
      fmt.Printf("key is: %d\n", key)
    }

    // 读取 value
    for _, value := range map1 {
      fmt.Printf("value is: %f\n", value)
    }
}
```

## 12.map

```go
countryMap := map[string]string{"France": "Paris", "Italy": "Rome", "Japan": "Tokyo", "India": "New delhi"}
//直接添加就好了
	countryMap["China"] = "beijing"
	for capac := range countryMap {
		fmt.Println(capac, "首都是", countryMap[capac])
		/*
			China 首都是 beijing
			France 首都是 Paris
			Italy 首都是 Rome
			Japan 首都是 Tokyo
			India 首都是 New delhi
		*/
	}
```

```go
delete(countryMap, "Japan")
```

添加直接

countryMap["China"] = "beijing"

删除则

delete(countryMap, "Japan")，后面的是key

## 13.interface

```go
package main

import "fmt"

type Shape interface {
	area() float64
}

// 前面括号表示接收的参数，函数名表示返回值
func (r Rectangle) area() float64 {
	return r.width * r.height
}

type Rectangle struct {
	width  float64
	height float64
}

func main() {
	var rec1 Shape

	rec1 = Rectangle{width: 10.0, height: 20.0}
	var s float64
	s = rec1.area()
	fmt.Println(s)
}
```

首先是定义了一个shape接口，area()方法

定义一个Rectangle结构体，定义两个属性



main中定义rec1为shape类型

把Rectangle实例赋值给rec，用他使用area方法

