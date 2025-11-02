---
title: "kotlin"    # 显示在侧边栏的文本
order: 1            # 排序位置
collapsed: false     # 默认不折叠
---

# 章节内容...
目录

1. 为什么选择 Kotlin？
2. 搭建开发环境
3. 基础语法
   · Hello World
   · 变量与常量
   · 基本数据类型
   · 函数
4. 控制流
   · 条件语句
   · 循环
5. 面向对象编程
   · 类与对象
   · 继承
   · 数据类
6. 空安全
7. 高级特性
   · 扩展函数
   · Lambda 表达式与集合操作
8. 与 Java 互操作
9. 学习资源推荐

---

1. 为什么选择 Kotlin？

· 简洁: 大大减少了样板代码。例如，一个 POJO 类在 Java 中需要几十行，在 Kotlin 中一行即可。
· 安全: 著名的空安全设计，有效避免了令人头疼的 NullPointerException。
· 互操作性: 100% 与 Java 互通，可以在现有 Java 项目中无缝使用 Kotlin，并调用所有 Java 库。
· 工具友好: JetBrains 自家出品，与 IntelliJ IDEA（Android Studio 的基础）完美集成。
· 多平台: 不仅可以用于 Android 和服务器端，还可以编译成 JavaScript 或原生代码。

---

2. 搭建开发环境

最快上手的方式是使用 JetBrains 的在线 Playground：
Kotlin Playground

对于正式开发，推荐使用 IntelliJ IDEA（社区版免费）：

1. 下载并安装 IntelliJ IDEA。
2. 创建新项目时，选择 Kotlin -> JVM | IDEA。
3. 输入项目名，完成创建。

---

3. 基础语法

Hello World

这是每个程序员的起点。在 Kotlin 中，它非常简单：

```kotlin
fun main() {
    println("Hello, World!")
}
```

· fun： 关键字，用于声明函数。
· main： 程序入口点函数名。
· println： 打印一行并换行。

变量与常量

· 变量（可变）： 使用 var 声明。
· 常量（不可变）： 使用 val 声明（推荐优先使用 val）。

```kotlin
fun main() {
    // 变量，值可以改变
    var name: String = "Alice"
    name = "Bob" // 正确

    // 常量，值不可改变
    val age: Int = 25
    // age = 26 // 错误！Val cannot be reassigned

    // 类型推断：编译器可以自动推断类型，类型标注 ": Int" 可以省略
    val score = 100 // 自动推断为 Int 类型
    println("Name: $name, Age: $age, Score: $score") // 字符串模板
}
```

基本数据类型

Kotlin 中所有东西都是对象，没有像 Java 那样的基本数据类型。

· Int, Long, Short
· Float, Double
· Boolean
· Char
· String

```kotlin
val number: Int = 10
val bigNumber: Long = 100L
val pi: Double = 3.14
val isKotlinFun: Boolean = true
val letter: Char = 'A'
val text: String = "Kotlin"
```

函数

使用 fun 关键字声明函数。

```kotlin
// 带有两个 Int 参数和 Int 返回值的函数
fun sum(a: Int, b: Int): Int {
    return a + b
}

// 表达式函数体：当函数体只有一行时，可以简化
fun sumSimple(a: Int, b: Int): Int = a + b

// 返回值类型也可推断，可以省略
fun sumInferred(a: Int, b: Int) = a + b

// 无返回值的函数（Unit 类型，类似于 Java 的 void，可以省略）
fun printHello(): Unit {
    println("Hello")
}
// 等价于
fun printHelloSimplified() {
    println("Hello")
}

fun main() {
    val result = sum(5, 3)
    println("5 + 3 = $result")
}
```

---

4. 控制流

条件语句

if-else 在 Kotlin 中是一个表达式，可以有返回值。

```kotlin
fun maxOf(a: Int, b: Int): Int {
    return if (a > b) {
        a
    } else {
        b
    }
}
// 更简洁的写法
fun maxOfSimple(a: Int, b: Int) = if (a > b) a else b

fun main() {
    println(maxOf(10, 5))
}
```

when 表达式：强大的 switch-case 替代者。

```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1       -> "One"
        "Hello" -> "Greeting"
        is Long -> "Long type"
        !is String -> "Not a String"
        else    -> "Unknown"
    }

fun main() {
    println(describe(1))
    println(describe("Hello"))
    println(describe(1000L))
    println(describe(2.5))
}
```

循环

for 循环

```kotlin
fun main() {
    val items = listOf("apple", "banana", "kiwi")

    // 遍历集合
    for (item in items) {
        println(item)
    }

    // 使用索引
    for (index in items.indices) {
        println("item at $index is ${items[index]}")
    }

    // 遍历范围
    for (i in 1..5) { // 包括 5
        println(i)
    }
    for (i in 1 until 5) { // 不包括 5
        println(i)
    }
    for (i in 5 downTo 1) { // 倒序
        println(i)
    }
    for (i in 1..10 step 2) { // 步长为 2
        println(i)
    }
}
```

while 和 do-while 循环与 Java 相同。

---

5. 面向对象编程

类与对象

```kotlin
// 定义一个 Person 类
class Person(
    val name: String, // 只读属性，在构造函数中定义，自动生成 getter
    var age: Int      // 可写属性，自动生成 getter 和 setter
) {
    // 成员函数
    fun speak() {
        println("Hello, my name is $name.")
    }
}

fun main() {
    // 创建对象，无需 'new' 关键字
    val person = Person("Charlie", 30)
    println(person.name) // 直接访问属性
    person.age = 31      // 修改属性
    person.speak()       // 调用方法
}
```

继承

Kotlin 中默认所有类都是 final（不可继承）。要允许继承，需要使用 open 关键字。

```kotlin
// 基类必须标记为 open
open class Animal(val name: String) {
    open fun makeSound() { // 方法也必须标记为 open 才能被重写
        println("Some generic animal sound")
    }
}

// 使用 : 来继承，主构造函数调用父类构造函数
class Dog(name: String) : Animal(name) {
    override fun makeSound() { // 使用 override 关键字重写方法
        println("$name says: Woof!")
    }
}

fun main() {
    val dog = Dog("Rex")
    dog.makeSound()
}
```

数据类

用于只保存数据的类，使用 data 关键字。编译器会自动为您生成 equals(), hashCode(), toString(), copy() 等有用的方法。

```kotlin
// 一行代码定义一个数据类
data class User(val name: String, val email: String)

fun main() {
    val user1 = User("Alice", "alice@example.com")
    val user2 = User("Bob", "bob@example.com")
    val user3 = User("Alice", "alice@example.com")

    println(user1) // 自动生成漂亮的 toString()
    println(user1 == user3) // true，自动生成的 equals() 比较内容

    // 复制对象，并可选择性地修改某些属性
    val user1Copy = user1.copy(email = "new_email@example.com")
    println(user1Copy)

    // 解构声明
    val (name, email) = user1
    println("Name: $name, Email: $email")
}
```

---

6. 空安全

这是 Kotlin 最核心的特性之一。

· 默认情况下，类型不能为 null。
· 如果允许为 null，必须在类型后加 ?。

```kotlin
fun main() {
    var a: String = "hello"
    // a = null // 编译错误！

    var b: String? = "world"
    b = null // 正确

    // 访问可能为 null 的变量
    val lengthA = a.length // 安全，因为 a 不可能为 null

    // val lengthB = b.length // 编译错误！b 可能为 null

    // 安全调用：如果 b 为 null，则返回 null
    val lengthBSafe = b?.length
    println(lengthBSafe) // 输出 null

    // Elvis 操作符 ?: ： 如果左边为 null，则使用右边的默认值
    val lengthBElvis = b?.length ?: 0
    println(lengthBElvis) // 输出 0

    // 非空断言 !! ： 确信它不为 null，如果为 null 则抛出异常（慎用！）
    // val lengthBBang = b!!.length // 如果 b 为 null，这里会抛出 KotlinNullPointerException
}
```

---

7. 高级特性

扩展函数

可以在不修改原有类的情况下，为类添加新的函数。

```kotlin
// 为 String 类添加一个新的函数
fun String.addExcitement(): String {
    return this + "!!!"
}

fun main() {
    val greeting = "Hello"
    println(greeting.addExcitement()) // 输出 "Hello!!!"
}
```

Lambda 表达式与集合操作

Kotlin 提供了非常强大的函数式编程支持。

```kotlin
fun main() {
    val numbers = listOf(1, -2, 3, -4, 5, -6)

    // 过滤出正数
    val positives = numbers.filter { it > 0 } // it 是隐式参数名
    println(positives) // [1, 3, 5]

    // 将每个元素映射为其平方
    val squares = numbers.map { it * it }
    println(squares) // [1, 4, 9, 16, 25, 36]

    // 查找第一个正数
    val firstPositive = numbers.find { it > 0 }
    println(firstPositive) // 1

    // 对集合中的每个元素执行操作
    numbers.forEach { println("Number: $it") }
}
```

---

8. 与 Java 互操作

这是 Kotlin 的一大杀手锏。您可以直接在 Kotlin 代码中调用 Java 代码，反之亦然。

在 Kotlin 中调用 Java：

```java
// Java 类
public class JavaClass {
    public String getJavaMessage() {
        return "Message from Java";
    }
}
```

```kotlin
// Kotlin 代码
fun main() {
    val javaObj = JavaClass() // 就像创建 Kotlin 对象一样
    println(javaObj.javaMessage) // 直接调用方法，属性式访问
}
```

---

9. 学习资源推荐

· 官方文档: Kotlin 官方文档 - 最权威、最全面的学习资料。
· Kotlin Koans: Kotlin Koans - 一系列交互式编程练习，是入门的最佳实践。
· 书籍: 《Kotlin in Action》 - 由 Kotlin 核心开发者编写的经典书籍。
· Android 开发者官网: Android Kotlin 指南 - 如果你是 Android 开发者，这是必看内容。

希望这份教程能帮助您顺利开启 Kotlin 编程之旅！从 Hello World 开始，多动手实践，您会很快爱上这门语言的简洁与强大。
