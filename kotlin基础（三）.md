### 条件控制

#### 	if表达式

```kotlin

// 作为表达式
val max = if (a > b) a else b

```

 	我们也可以把if表达式的结果赋值给一个变量

```kotlin
 var min = if(b<c){
 	println(b)
 	b
 }else{
 	println(c)
     c
 }
```

​	这也说明我们不需要像java那样拥有一个三元运算符,因为我们可以使用它来简单实现

```
var c = if(condition) a else b
```

​	

​	使用区间

```kotlin
if(num in 1..8){
    println("$num 在区间内")
}
```

####     when表达式

​		when将它的参数与所有的分支顺序条件作比较，直到满足条件

​		when既可以被当作表达式，也可以被当作语句使用。如果被当作表达式，符合条件的分支的值就是整个表达式的值，如果被当作语句使用，则忽略个别分支的值

​         when类似与java的switch操作符，其简单形式如下：

```kotlin
when(x){
    1->print("x == 1")
    2->print("x == 2")
    else ->{
        print("x既不是1，也不是2")
    }
}
```

在when中else类似于default

如果有多个分支处理是一样的，则可以把多个分支放在一起，用,号间隔

```kotlin
when(x){
    1,2,3->println("x==1或者x==2或者x==3")
    else ->{
        println("其他")
    }
	
}
```

我们也可以检测一个值在或者不在一个区间，集合中

```kotlin
when(x){
    in 1..5 ->println("在1到5之间")
    in valideNums ->println("x is valid")
    !in 5..10->println("不在5到10之间")
    else->println("else")
}
```

when也可以检测一个值的类型（is）

```kotlin
fun test(x:Any) = when(x){
    is String ->x.startsWith("perfix")
    else->false
}
```

when 也可以用来替代if else if链。如果不提供参数，所有的分支条件都是简单的布尔表达式，而当一个分支的条件为真时，则执行该条件

```kotlin
when{
    x.isodd()->print("x is odd")
    x.isEven()->print("x is even")
    else->print("x is funny")
}
```

when 中使用 **in** 运算符来判断集合内是否包含某实例：

```kotlin
fun main(args: Array<String>) {
    val items = setOf("apple", "banana", "kiwi")
    when {
        "orange" in items -> println("juicy")
        "apple" in items -> println("apple is fine too")
    }
}
```

### 循环控制

​	for循环可以对任何提供迭代器（iterator）的对象提供遍历

​	

```kotlin
for (item in collection)print(item)
```

   如果需要index则可以使用withIndex

​	

```kotlin
for((index,item) in array.withIndex()){
    println("$index,$item")
}
```

对集合进行迭代

```kotlin
fun main(args:Array<String>){
    var items = listof("hello","every","one","nice")
    
    for(item in items){
        println(item)
    }
    
    for(index in items.indices){
        println("item at $index is ${items[index]}")
    }
	
}
```



#### while 与 do while 循环

```kotlin
fun main(args :Array<String>){
    var x = 5;
    while(x>0){
        println(x--)
    }
    
    var y = 5
    do{
        println(x--)
    }while(x>0)
}
```

