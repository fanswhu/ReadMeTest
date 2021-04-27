[TOC]



### 扩展



#### 函数扩展

扩展函数可以在原有类添加新的方法，不会对原类进行修改，扩展函数定义形式：

```kotlin
fun recieverType.functionName(params){
    body
}
```

- recieverType 表示扩展的是哪个类

- functionName 表示扩展的函数名

- params 表示参数

  ```kotlin
  // 示例
  class Apple(var type:String)
  
  fun Apple.play(){
      println("型号$type 正在播放音频")
  }
  fun main(args:Array<String>){
     var apple = Apple("iphone 12 proMax")
      apple.play
  }
  ```

#### 伴生对象

在对象声明的前面加上companion关键字就成了伴生对象。**作用就是为其所在的外部类模拟静态成员**

```kotlin
// ObjectName 可省略
companion object ObjectName:[0-n个父类]{
    // 伴生对象体
}
```



#### 为伴生对象扩展成员

为伴生对象扩展成员，如果伴生对象有名字，则通过“**外部类.伴生对象名字.成员**”的方式扩展；

如果伴生对象没名字，则通过“**外部类.Companion.成员**”的方式扩展

```kotlin
class OutterClass{
    companion object{
        var name = "伴生对象属性"
        fun companionFun(){
            println("伴生对象方法")
        }
    }
}

// 为伴生对象扩展方法
fun OutterClass.Companion.test(){
    println("伴生对象的扩展方法")
}
//为伴生对象扩展变量
var OutterClass.extraParams:String
	get() = "伴生对象的变量"

fun main(args:Array<String>){
    println(OutterClass.name)
    OutterClass.companionFun()
    
     println(OutterClass.extraParams)
    OutterClass.test()
   
}
```
