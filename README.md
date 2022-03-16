# Kotlin_Study
记录Kotlin学习过程

# Kotlin介绍  
Kotlin 是一个基于JVM 的新的编程语言，由 JetBrains 开发  
Kotlin可以编译成Java字节码，也可以编译成JavaScript，方便在没有JVM的设备上运行  
Kotlin已正式成为Android官方支持开发语言  

相对于java的优势:  
比Java更安全，能够静态检测常见的陷阱。如：引用空指针  
比Java更简洁  
源代码开源  

# 一. Hello Kotlin  

![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin1.png)  

1. main函数不需要在class中就可以运行  
2. fun代表一个函数 后面跟的是函数名称，参数列表和返回值类型  
3. 函数中参数的写法 参数名称：参数类型（与java相反）  
4. 函数的返回值是在后边的（和java刚好相反的）当然 有返回值 也可以不写返回类型（前提是：只有表达式体 函数返回类型可以省略，如果是代码块体函数就必须要 写明函数返回类型），因为kotlin 通过 类型推导 也是可以知道返回值类型的  
5. system.out.println 被包装为 println  
6. 在行末可以省略 分号 （类似 js）  
7. 看到max函数中 if类似于三元表达式 kotlin中，if 是有结果值的表达式  
8. 如果返回值 类似于 java 中的 void 则可以写成 :Unit ，当然也可以省略不写  

  在kotlin 中，除了部分循环（for do 和 do/while）大多控制结构都是表达式，是有返回值的。另一方面 java 中的赋值语句为表达式，而kotlin 中则为语句。与Java定义包名一样，在源文件的开头定义包名：但是不同的是，包名和文件夹路径可以不一致：源文件可以放在项目的任意位置，当然也不建议这样搞，自己何苦为难自己。。。  

# 二. 变量  

## 2.1 基础用法  

kotlin变量的声明方式与Java中声明变量有很大的区别，而且必须使用var或val关键字。其中：  
  var: 用此关键字声明的变量表示可变变量，即可读且可写。相当于Java中普通变量  
  val: 用此关键字声明的变量表示不可变变量，即可读且不可写。相当于Java中用final修饰的变量  
  *** 官方推荐** 尽量使用val 声明变量，使程序更接近函数式编程风格  
  
  定义格式： 关键字 变量名: 数据类型 = xxx  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin4.png)  
  
  其中。var和val是Kotlin中定义变量必须使用的关键字。  
  每一行代码的结束可以省略掉分号;，这一点是和Java不同的地方。当然，第一次写可能会有一点不习惯。 
  print()与println()都是打印方法，后者打印完成之后会换一行。此两个方法和Java的打印方法是一模一样的。  
  $符号表示引用的意思。这里理解为字符串模板  
  
## 2.2 在类中声明以及声明可空变量  

  只有在顶层声明的情况下是可以不用实例化的。但是在实际开发当中，一般都是在一个类中去定义变量，这种情况被称为声明类的属性。  
  其特点如下：必须初始化，如果不初始化，需使用lateinit关键字。
  
  声明可空变量  
  在Java中，当我们声明一个变量不必关心这个变量是否为空，在使用这个变量的时候几乎上都会判断其是否为空增加程序的安全性。这样的习惯是极好的。但是无形中也增加了一定的代码量。有时候这样的代码还极有可能是无用的废代码。然而在Kotlin中当我们可以确定这个属性或变量一定不为空时，我们就用上面讲解到的去定义变量。否则就把它声明为可空变量。   
  
  定义：var/val 变量名 ： 类型? = null/确定的值  
  
  可空变量的特点：  
  在声明的时候一定用标准的声明格式定义。不能用可推断类型的简写。  
  变量类型后面的?符号不能省略。不然就和普通的变量没区别了。  
  其初始化的值可以为null或确定的变量值。 
  
## 2.3 后期初始化与延迟初始化  
  
  当在类中定义一个变量（属性）的时候是必须初始化的。这在平时的实际开发中能满足大部分的需求。但是还是有一些特殊的场景中不能满足。比如说：Android开发中对组件变量的声明与赋值，以及在使用Dagger2注解变量等。这就需要Kotlin中特有的后期初始化属性来满足这个需求了。  
  
  声明后期初始化属性的特点：  
  使用lateinit关键字  
  必须是可读且可写的变量，即用var声明的变量  
  不能声明于可空变量。  
  不能声明于基本数据类型变量。例：Int、Float、Double等，注意：String类型是可以的。  
  声明后，在使用该变量前必须赋值，不然会抛出UninitializedPropertyAccessException异常。  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin5.png)  
  
  延迟初始化：指当程序在第一次使用到这个变量（属性）的时候在初始化。  
  声明延迟初始化属性的特点：  
  使用lazy{}高阶函数，不能用于类型推断。且该函数在变量的数据类型后面，用by链接。  
  必须是只读变量，即用val声明的变量。
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin6.png)  
  
# 三. 常量   

  Kotlin中声明常量的方式和在Java中声明常量的方式有很大的区别。这里举例说明：  
  Kotlin中使用val时候对应的Java代码：  
  Kotlin中的 val numA = 6   等价于  Java中的：public final int numA = 6  
  
  Kotlin中只用val修饰还不是常量，它只能是一个不能修改的变量。那么常量怎么定义呢？其实很简单，在val关键字前面加上const关键字。  
  即：const val NUM_A = 6  
  const只能修饰val，不能修饰var  
  
  声明常量的三种正确方式：  
  在顶层声明  
  在object修饰的类中声明，在kotlin中称为对象声明，它相当于Java中一种形式的单例类  
  在伴生对象中声明  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin7.png)   
  
 # 四. 注释  
 
 Kotlin中的注释几乎和Java没什么区别。唯一的区别在于Kotlin中的多行注释中可以嵌套多行注释，而Java中是不能的。  
 
 1. 单行注释  两个斜杠开头表示单行注释（//）  
 2. 多行注释（块注释）  以斜杠加星号开头（/*），同时以星号加斜杠结尾（*/），中间这是要注释的代码块！  
 3. 多行注释嵌套  kotlin中块注释的级联使用   在Java中使用上面的注释代码直接报错。  
 
 ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin8.png)  
 
 4. 类注释、方法注释   和Java是一样的  

 ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin9.png)  
 
 # 四. 数据类型  
 
 ## 4.1 数值类型  
 
 ### 4.1.1  
 
   Kotlin中的数字的内置类型（接近与Java），其关键字为：  
   Byte=> 字节 => 8位  
   Short => 短整型 => 16位  
   Int => 整型 => 32位  
   Long => 长整型 => 64位  
   Float => 浮点型 => 32位  
   Double => 双精度浮点型 => 64位  
   
   ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin10.png)  
   
 ### 4.1.2 进制数  
 
   二进制数  var h = 0b00001011   h => 11   
  八进制数（Kotlin不支持）  
  十进制数    var k = 123    k => 123   
  十六进制数   var g = 0x0F    g => 15   
  
 ### 4.1.3 数字类型字面常量的下划线  
 
  作用：分割数字进行分组，使数字常量更易读  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin11.png)  
  
 ### 4.1.4 装箱与拆箱  
 
  在Kotlin中，存在数字的装箱，但是不存在拆箱。因为Kotlin是没有基本数据类型的，Kotlin是万般皆对象的原则。故不存在和`Java`中的类似`int`是数据类型，`Integer`是整型的引用类型。 
  
  
 
  
   
   
 
 
 
  
  
 
  
  
  
  
  
