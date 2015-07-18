# Swift

## #The Basics
Int Double Float Bool String
Array Set Dictionary

#### Constants and Variables
`let a = 0` // 使用let声明constants
`var b = 1` // 使用var声明variables

#### Type annotations
`var a: String` // 将a声明为指定类型

#### Naming Constants and Variables
常量与变量名不能包含数学符号，箭头，保留的（或者非法的）Unicode 码位，连线与制表符。也不能以数字开头，但是可以在常量与变量名的其他地方包含数字。

### 分号
Swift不强制使用分好，除非要在一行里面使用多行语句。

### 整数和小数
==UInt== 和 ==Int==，使用==UInt8 (Int8)、UInt16、UInt32、UInt64==分别表示不同整数类型。
`UInt8.min`
`UInt8.max`
浮点数使用==Double==和==Float==

#### 数值字面量
* 一个十进制数，没有前缀
* 一个二进制数，前缀是0b
* 一个八进制数，前缀是0o
* 一个十六进制数，前缀是0x

##### 十进制指数，exp
* 1.25e2 表示 1.25 × 10^2，等于 125.0
* 1.25e-2 表示 1.25 × 10^-2，等于 0.0125
* 0xFp2 表示 15 × 2^2，等于 60.0
* 0xFp-2 表示 15 × 2^-2，等于 3.75

