[TOC]



#### 类声明

- 使用关键字class声明
- 类声明 = 类名+类头（指定其类型参数，主构造函数等）[可选]+**花括号包裹的类体[可选]**

#### 构造函数

- 一个主构造函数：类头的一部分，跟在类名后面
- 多个次构造函数：类体的一部分属一般函数

```kotlin
class Test constructor(var name:String){
	init{
		println("name:$name")
	}
}
```

- 类如果有一个主构造函数，则每个次构造函数，必须委托给主构造函数：可直接委托，或间接委托通过其他次构造函数委托

- 委托用this关键字

  ```kotlin
  class Test(var age:int){
      constructor(name:String,age:int):this(age)
  }
  ```

  

#### 函数声明

 	

```kotlin
// 没有返回值可不写返回类型
fun 函数名（参数名：参数类型）：返回类型{
    
}
```

#### 调用超类实现

- 派生类中可以使用super调用超类函数实现
- 在一个内部类中访问外部类的超类，super@Rectangle.draw()
- 为表示从哪个超类型继承的实现以消除歧义，使用尖括号中超类型名限定的super，如super<Base>

#### 幕后字段

- **使用field标识符在访问器中使用，并且只能在属性的访问器中使用**
- 并不是所有属性都会有幕后字段，需满足以下条件之一：属性至少一个访问器使用默认访问器， 自定义访问器通过field引用幕后字段。
- 自定义属性时，借用其他属性赋值，就没有幕后字段
- Kotlin中定义的变量，要么是定义时就初始化，要么就定义成抽象的

#### 幕后属性

我们希望一个属性对外只读，对内可读写。我们将这个属性称之为幕后属性。如：

```kotlin
private var _student:Map<String,Int>? = null
var student
	get(){
        if(_student == null ){
            _student  = HashMap()
            return _student?:throw AsserttError("null error")
        }
    }
```

幕后属性在Kotlin的集合中用的比较多，Collection中有个size字段，size对外是只读的，size的值根据集合的元素的个数的改变而改变，这是在集合内部实现的，这用幕后属性非常方便



属性的访问是通过它的访问器getter和setter, 你可以改变getter和setter 的可见性，比如在setter前添加`private`,那么这个setter就是私有的。

#### 接口

- 接口中可以定义抽象/非抽象方法；

- 接口中可以定义抽象属性/非抽象属性，但是接口中的非抽象属性是没有幕后字段（filed）的，因此需要为之提供get-set方法。
- kotlin接口中的非抽象成员（方法、属性）可使用public|private两种访问权限修饰（java中自动为接口成员提供public修饰，如果指定访问权限也只能是public），抽象成员只能使用public修饰；
- 接口不可以包含构造器和初始化块，但接口可包含：方法（抽象方法/非抽象方法）、属性（抽象属性/非抽象属性）、嵌套类（或嵌套接口、嵌套枚举）;
- kotlin接口抽象成员的abstract关键字可以省略（抽象类的抽象成员不能省略）；
- 接口不能实例化，但可以用来声明变量，通过该变量可以赋值给Any（向上转型，因为接口的子类对象一定是Any的子类）；
- 接口的实现类实现该接口的抽象成员只能是public修饰。

```kotlin
interface IPeople{
    var sex
    var num:Int
    var age
    	get() = num
    fun read()
    fun eat(){
        println("eat")
    }
}

class Women(override var num:Int):Ipeople{
    override var sex = "women"
    Override fun read(){
        println("$sex read")
    }
}
```

#### 数据类

声明数据类

```kotlin
data class <类名> <(主构造函数参数列表)> [:继承类和实现接口] [(/*类体*/)]

```

**主构造函数的参数列表必须使用`val`或`var`声明为类属性，而且要求 至少有一个，否则无法通过编译。**

数据类的功能：

- 自动声明与构造参数同名的参数字段
- 自动实现每个属性的存取器方法（get/set)
- 自动提供equal方法比较两个数据对象是否相等
- 自动提供copy方法复制数据对象
- 自动提供toString方法
- 数据类不可以声明为抽象`abstract`、开放`open`、密封`sealed`、内部`inner`
- 数据类不能继承其他类，但可实现接口。

```kotlin
// 数据解构
var (name,age) = p
println("$name,$age")
```



