# Kotlin_Study
记录Kotlin学习过程

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
  考虑到kotlin 的变量声明是可以省略 类型的，所以kotlin 变量声明有别于java ，kotlin 变量声明顺序为 关键字 变量名称 类型（可不加），如果变量没有初始化 则需要明确表明 变量类型。  
  常量与变量都可以没有初始化值,但是在引用前必须初始化编译器支持自动类型判断,即声明时可以不指定类型,由编译器判断。如果不在声明的时候初始化则必须提供变量的类型。  
  
  val ：不可变引用 ，在val声明变量后不能再初始化之外再次赋值（java final）  
  var ：可变引用 ， 该类型变量可以随便赋值  
  *** 官方推荐** 尽量使用val 声明变量，使程序更接近函数式编程风格  
  
  1、可变变量的定义: var 关键字  
  var <变量名> : <变量类型> = <初始值>  
  2、不可变变量的定义: val 关键字， 不能进行二次赋值，类似Java中的final类型  
  val <常量名> : <常量类型> = <初始值>  
  
  已知值的属性可以使用 const 修饰符标记为 编译期常量。需要满足如下几种条件: (类似 java 中的 constanUtil 中的 常量值)  
  位于顶层或者是 object 的一个成员  
  用 String 或原生类型 值初始化  
  没有自定义 getter  
  
  const val SUBSYSTEM_KEY: String = "key"
  
  $是Kotlin字符串拼接的语法  
  var name: String = "123"  
  println("Hello world $name")   // $变量 输出 Hello world 123  
  
  自定义访问器  类似于javaBean  
  
  
  
  
  
  
