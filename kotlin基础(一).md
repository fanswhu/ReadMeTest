#### 函数定义



1. 函数定义使用关键字fun

2. 参数格式   参数：类型

   ```kotlin
   fun sum(a: Int, b: Int): Int {   // Int 参数，返回值 Int
       return a + b
   }
   ```

   

3. 如果是表达式作为函数体，返回类型自动推断     **如果是public方法，则必须写返回类型**

   ```kotlin
   fun sum(a: Int, b: Int) = a + b
   
   public fun sum(a: Int, b: Int): Int = a + b   // public 方法则必须明确写出返回类型
   ```

   

4. 无返回值的函数

   ```kotlin
   fun printSum(a: Int, b: Int): Unit { 
       print(a + b)
   }
   
   
   // 如果是返回 Unit类型，则可以省略(对于public方法也是这样)：
   public fun printSum(a: Int, b: Int) { 
       print(a + b)
   }
   ```

   

5. 可变长参数函数

   函数的变长参数可以使用**vararg**进行标识

   ```kotlin
   fun vars(vararg v:Int){
       for(vt in v){
           print(vt)
       }
   }
   
   //测试
   fun main(args:Array<String>){
       vars(1,2,3,4) //输出1，2，3，4，5
   }
   ```

   

6. lambda(匿名函数)

   

   ```kotlin
   
   
   ```



#### 常量以及变量的定义

​	可变变量定义关键字：var

​	var    <变量名> ：<类型>  =  <初始值>



​	不可变变量定义关键字：val   （只能被赋值一次的变量，类似于java中final修饰的变量）

​	val    <不可变变量名> ：<类型>  =  <初始值>



​	常量与变量都可以没有初始值，但是被引用前一定要初始化。



​	编译器支持自动类型推断，即声明时可以不指定变量类型,由编译器自动类型推断	

```kotlin
var a :Int = 1
var b = 1 //由编译器自动推断
var c :Int //如果不在声明时初始化，则必须指定类型
c =1
```



#### 字符串模板

​	$varName表示一个变量值

​	${varName.fun()}表示变量的方法返回值

```
var a = 1
var b = "a is $a"
a = 2
var c = "${b.replace("is","was")},but now is $a"
```

​	b 的值为“ a is 1”

​	c 的值为"a was 1,but now is 2"



#### NULL检查机制

​	kotlin 的空安全设计，对于声明可为空的参数，在使用时要进行空判断处理，有两种处理方式，字段后加!!像java一样抛异常，另一种	字段后加？可不做处理，返回值为null或配合?:做空判断处理

```kotlin
//后面加？号表示可为空
var age:String?  = "23"

//抛出空指针异常
var age1 = age!!.toInt()

// 不做处理返回null
var age2 = age?.toInt()

//age为空返回-1
var age3 = age?.toInt()?:-1

```

​	当一个引用可能为null时，对应类型声明，必须明确的标注可为null

```kotlin
// 当str的内容不是一个整数时，返回null
fun paseInt(str:String):Int?{
    // todo
}
```



#### 类型检测以及自动类型转换

​	我们可以用is运算符来检测对象一个表达式是否某类型的一个实例（类似于java中的 instanceof关键字）

```kotlin
fun getStrLength(obj:Any):Int?{
    if(obj is String){
        // 做过类型判断以后，obj会被自动转换为String类型
        return obj.length
    }
    
    // 还有一种判非的方法
    if(obj !is String){
        // todo
    }
    return null
}
```

​	或者

```kotlin
fun getStrLength(obj:Any):Int?{
     if(obj !is String){
     	return null
     }
     //这里自动转换为String
     return obj.length
}
```

​	还可以

```kotlin
fun getStrLength(obj:Any):Int?{
    // 表达式右边被自动转换成String
    if(obj is String && obj.length >0){
        return obj.length
    }
    return 0
	
}
```



#### 区间

​	区间表达式操作符：..  ,rangeTo, in , !in

​	区间是为可比较类型定义的，但对于整形原生型，有一个优化的实现

​	实例：

```kotlin
for(i in 1..4){
    print i//输出1，2，3，4
}

for (i in 4..1){
    print i //什么都不输出 
}

for (i in 1..4 step 2){
    print i  // 使用step指定步长，输出1，3
}

for (i in 4 downTo 1 step 2){
    print i // downto 降序输出 输出 4，2
}

// 使用until排除结束元素
for(i in 1 until 10){
    print i  //  输出1到9
}
```

