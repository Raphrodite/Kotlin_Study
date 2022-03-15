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

![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin1.png)

# 一. Hello Kotlin  
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
  
  已知值的属性可以使用 const 修饰符标记为 编译期常量。需要满足如下几种条件: (类似 java 中的 constanUtil 中的 常量值)  
  位于顶层或者是 object 的一个成员  
  用 String 或原生类型 值初始化  
  没有自定义 getter  
  
  const val SUBSYSTEM_KEY: String = "key"
  
  $是Kotlin字符串拼接的语法  
  var name: String = "123"  
  println("Hello world $name")   // $变量 输出 Hello world 123  
  
  自定义访问器  类似于javaBean  在属性中重写getter  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin2.png)  
  
  在Kotlin中的val修饰的变量不能说是不可变的，而只能说仅仅具有可读权限。  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin3.png)  
  
  
 
  
  
  
  
  
