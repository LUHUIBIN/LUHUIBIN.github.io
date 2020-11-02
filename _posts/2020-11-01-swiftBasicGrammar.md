---
layout:     post
title:      swiftBasicGrammer
subtitle:   
date:       2020-11-01
author:     HB
header-img:
catalog: true
tags:
    - programming
---
source : [网易云课堂swift](https://study.163.com/course/courseMain.htm?courseId=1006380014)
#### 1常亮变量与数据类型
```swift
//变量
var str = "hello playground"    
var name = "spike.lu"
var age = 21
var height = 175.0
name = "joy"
height = 178.9

//常量
let sex = "男"
let hometown = "rizhao"
//sex = "女"  // 报错

//数据类型
var currentYear: Int = 2020
var doubleResult: Float = 8/6

```




#### 2函数及元祖的声明和使用
```swift
//函数的声明
func sayHello(){
	print("hello,world!")
}

//函数的参数
func sum(number1: Int,number2:Int){
		let result = number1 + number2
		print("\(number1) + \(number2) = \(result)")
}
sum(number1: 1,number2:2)
sum(number1: 3,number2:4)

//函数返回值
func square(number: Int) ->Int{
		return number * number
}
print(square(number:10))

//函数的外部参数名和内部参数名
func flight(from departure: String, to arrival: String){
		print("这是一趟\(departure) 飞往\(arrival)的航班")
}
flight(from: "上海", to:"武汉")

func cube(_ number: Int) -> Int{     //通过下划线来替代外部函数名,这样diaoyong函数时更加方便
		return number * number * number
}
print(cube(2))

//元组
var mountain = ("珠穆朗玛峰", 8848.43, "中国与尼泊尔的边境线上")
let (n, h, p) = mountain
print("\(n)高\(h)米,位于\(p)")

let(justname, _, andposition) = mountain  // _ 用于忽略一些参数
print("\(justname)位于\(andposition)")

```


#### 3逻辑运算符
```swift
// &&
var usernameIsRight = true
var passwordIsRight = true
var login = usernameIsRight && passwordIsRight
//||
var password = true
var touchID = false
var phoneUnlock = password || touchID

//条件语句
//if
var age = 12
if age < 18 {
	print("您未满18岁，已纳入防沉迷系统")
}
//if语句的else分句
var number = -10
if number < 0{
	print("\(number)是一个负数")
}else{
	print("\(number)不是一个负数")
}
//switch
switch trafficlight{
case "red":
	print("红灯，停车等待")
case "green":
	print("绿灯，可以通行")
case "yellow":
	print("即将变灯")
default:
	print("交通信号灯故障")
}

//范围
let closeRange = 1...5
let halfOpenRange = 1..<5
let rangeToMax = 18...
let rangeFromMin = ...18

switch score{
case 0..<60:
	print("不及格")
case 60..<80:
	print("及格")
case 80...100:
	print("优秀")
default:
	print("分数无效")
}
```



#### 4可选类型的含义，声明和使用
```swift
//可选类型
var hello = "hello world"
var stringToNumber = Double(hello)   //当可选类型没有值时为nil

var stringOfNumber = "123"
stringToNumber = Double(stringOfNumber) //123
print(stringToNumber!) //"optional(123.0)"   当可选类型有值时  此处的值为一个可选类型的值,                       

var job: String?   //可选类型无法进行类型推断,所以必须进行类型标注.声明可选类型的时候如果没有赋值的话默认为nil


//强制解析
var optionalNumber: Int? = 2
var sum = optionalNumber! + 3
print(optionalNumber!)

//print(job!) //  报错 -  展开一个空的可选类型              可选类型在没有值的时候是不能进行强制解析的

//空合运算符
print(job ?? "没有工作") //对可选类型的值进行判断，当可选类型的值为nil时，使用提供的默认值。当可选类型有值的时候，就会自动将可选类型的值展开并使用它会
job = "工程师"
print(job ?? "没有工作")

//隐式解析
var optionalDecimal: Double! = 2.5  //在隐式类型始终有值的情况下，自动解析。
optionalDecimal = optionalDecimal + 3

optionalDecimal = nil
//optionalDecimal +3  //报错 - 展开一个空的可选类型

```





#### 5枚举、类和结构体的声明和使用（上）
```swift
// 枚举
enum Direction{
	case east
	case west
	case south
	case north
}

enum AppleOS{
	case iOS,macOS,watchOS,tvOS
}

var walk = Direction.north  
print(walk)
walk = .east
print(walk)

//使用switch 语句匹配枚举值
switch walk{
case .east:
	print("正在往东走")
case .west:
	print("正在往西走")
case .south:
	print("正在往南走")
case .north:
	print("正在往北走")
} // 因为case语句罗列出了所有的可能性所以不需要default语句了


// 类和结构体的声明
struct Resolution {
	var width = 0
	var height = 0
}
class Player{
	var name = ""
	var HP = 100
	var ATK = 30
}
//类和结构体的实例化
var resolution = Resolution()

var player1 = Player()
var player2 = Player()

//属性的访问和修改
resolution.width = 1920
resolution.height = 1080

player1.name = "玩家1"
player2.name = "玩家2"

player1.HP -= player2.ATK
print("\(player1.name)受到\(player2.name)的攻击，剩余血量\(player1.HP)")


```


#### 6枚举类和结构体的声明和使用下
```swift
//将一个结构体实例对象赋值给一个变量后，改变这个变量的属性值，原本的结构体实例对象的值不受影响，
//将一个类实例对象赋值给一个变量后，改变这个变量的属性值，原本的类实例对象的值随之改变，因为两个变量共同引用同一个实例对象

//构造函数
class Box{
	var length: Double
	var width: Double
	var height: Double

	init(length: Double, width: Double, height: Double){
		self.length = length
		self.width = width
		self.height = height
	}

	init(cube sidelength: Double){
		length = sidelength
		width = sidelength
		height = sidelength
	}
}

let box = Box(length : 3, width : 2, height : 1)
let cube = Box(cube: 6)

```
