### 基本数据类型

​	kotlin的基本数值类型包括：Byte Short Int Long Float Double

| 类型   | 长度 |
| ------ | ---- |
| Byte   | 8    |
| Short  | 16   |
| Int    | 32   |
| Long   | 64   |
| Float  | 32   |
| Double | 64   |

子符不属于基本数值类型，是一个独立的数值类型



### 比较两个数字

​	kotlin没有基础数据类型，只有封装的数字类型，你每定义的一个变量，其实kotlin帮你封装了一个对象，这样可以保证不出现空指针。数字类型也一样，所以在比较两个数字的时候，就有比较数据大小和比较两个对象是否相同的区别了。

​	在kotlin中，三个等号===表示比较对象地址，两个==表示比较两个值大小

​    

```kotlin
fun equalTest(args:Array<String){
    var a:Int = 1000
    println(a===a)//true,地址相等
    
    // 经过了装箱
    var b:Int? = a
    var c:Int? = a
    println(b == c) //值相等
    println(b === c)//地址不相等
}
```

### 类型转换

​	每种数据类型都有下面的这些方法，可以转化为其他的类型：

```kotlin
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
```

​	由于不同的表示方式，较小类型并不是较大类型的子类型，较小的类型不能隐式转换为较大的类型。 这意味着在不进行显式转换的情况下我们不能把 Byte 型值赋给一个 Int 变量。

​	

```kotlin
val b: Byte = 1 // OK, 字面值是静态检测的
val i: Int = b // 错误



val b: Byte = 1 // OK, 字面值是静态检测的
val i: Int = b.toInt() // OK
```

​	有些情况下也是可以使用自动类型转化的，前提是可以根据上下文环境推断出正确的数据类型而且数学操作符会做相应的重载。例如下面是正确的：

​	

```kotlin
val l = 1L + 3 // Long + Int => Long
```



### 位操作符

​	对于Int和Long类型，还有一系列的位操作符可以使用，分别是：

​	

```kotlin
shl(bits)  //左移位
shr(bits)  //右移位
ushr(bits) // 无符号右移位
and(bits) //与
or(bits)  //或
xor(bits) //异或
inv() //反向

```

### 字符串

 	和java一样字符串是不可变的。[]可以很方便获取字符串中某个字符，也可以通过for循环来遍历

​	 

```kotlin
for (c in str) {
    println(c)
}
```

​	kotlin 支持“”“三个引号扩起来的字符串，支持多行字符串，比如：

​	

```kotlin
fun main(args:Array<String>){
    var text = """
    多行字符串
    多行字符串
    ...
    """
    print(text)   //输出有一些前置空格
}
```

​	String 可以通过 trimMargin（）方法来删除多余的空白

​	

```kotlin
fun main(args:Array<String){
    var text = """
    |第一行
    |第二行
    |第三行
    """
    println(text.trimMargin()) // 前置空格删除了
}
```

​	默认 | 用作边界前缀，但你可以选择其他字符并作为参数传入，比如 trimMargin(">")。



## 字符串模板

​		上一节已经讲过 ” $var“ 与"${fun()}"的含义     

[kotlin第一节]: https://blog.csdn.net/qq_34097002/article/details/115715784

​		新增一个转义的妙用（$不支持转义符）

```kotlin
fun main(args: Array<String>) {
    val price = """
    ${'$'}9.99
    """
    println(price)  // 求值结果为 $9.99
}
```

