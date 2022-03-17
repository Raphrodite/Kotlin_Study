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
 
 # 五. 数据类型  
 
 ## 5.1 数值类型  
 
 ### 5.1.1  
 
   Kotlin中的数字的内置类型（接近与Java），其关键字为：  
   Byte=> 字节 => 8位  
   Short => 短整型 => 16位  
   Int => 整型 => 32位  
   Long => 长整型 => 64位  
   Float => 浮点型 => 32位  
   Double => 双精度浮点型 => 64位  
   
   ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin10.png)  
   
 ### 5.1.2 进制数  
 
   二进制数  var h = 0b00001011   h => 11   
  八进制数（Kotlin不支持）  
  十进制数    var k = 123    k => 123   
  十六进制数   var g = 0x0F    g => 15   
  
 ### 5.1.3 数字类型字面常量的下划线  
 
  作用：分割数字进行分组，使数字常量更易读  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin11.png)  
  
 ### 5.1.4 装箱与拆箱  
 
  在Kotlin中，存在数字的装箱，但是不存在拆箱。因为Kotlin是没有基本数据类型的，Kotlin是万般皆对象的原则。故不存在和`Java`中的类似`int`是数据类型，`Integer`是整型的引用类型。 
  
  在Kotlin中要实现装箱操作。首先要了解可空引用。即类似Int?(只限数值类型)这样的。  
  
  val numValue: Int = 123  
  //装箱的过程，其实装箱之后其值是没有变化的  
  val numValueBox: Int? = numValue  
  println("装箱后： numValueBox => $numValueBox")  
  输出结果为：  
  装箱后： numValueBox => 123
  
  两个数值的比较:  
  判断两个数值是否相等（==）,判断两个数值在内存中的地址是否相等（===）,其实上面的装箱操作之后其内存中的地址根据其数据类型的数值范围而定。  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin12.png)   
  
  ### 5.1.5 转换  
  
   显式转换  
   较小的类型不会被隐式转换为更大的类型，故而系统提供了显式转换。提供的显式转换方法如下：  
   toByte() => 转换为字节型  
   toShort() => 转换为短整型  
   toInt() => 转换为整型  
   toLong() => 转换为长整型  
   toFloat() => 转换为浮点型    
   toDouble() => 转换为双精度浮点型  
   toChar() => 转换为字符型  
   toString() => 转换为字符串型  
   
   隐式转换  
   类型是从上下文推断出来的，即算术运算则被重载为适当的转换  
   
   // 30L + 12 -> Long + Int => Long  
   val num = 30L + 12  
   print(num)  
   输出结果为：    
   42  
   
  ### 5.1.6 位运算符
   
   Kotlin中对于按位操作，和Java是有很大的差别的。Kotlin中没有特殊的字符，但是只能命名为可以以中缀形式调用的函数，下列是按位操作的完整列表(仅适用于整形（Int）和长整形（Long）)：  
   shl(bits) => 有符号向左移 (类似Java的&lt;&lt;)  
   shr(bits) => 有符号向右移 (类似Java的&gt;&gt;)  
   ushr(bits) => 无符号向右移 (类似Java的&gt;&gt;&gt;)  
   and(bits) => 位运算符 and (同Java中的按位与)  
   or(bits) => 位运算符 or (同Java中的按位或)  
   xor(bits) => 位运算符 xor (同Java中的按位异或)  
   inv() => 位运算符 按位取反 (同Java中的按位取反)  
   
 ## 5.2 布尔类型 
 
  Boolean关键字表示布尔类型，并且其值有true和false
  逻辑操作符（与Java相同）:  
  ' || ' => 逻辑或（或者）  
  ' && ' => 逻辑与（并且）  
  ' ! ' => 逻辑非（取反）  
  
 ## 5.3 字符型
 
  Char为表示字符型，字符变量用单引号（‘ ’）表示。并且不能直接视为数字，不过可以显式转换为数字。  
  
  显式转换为其他类型  
  字符型的变量不仅可以转换为数字，同时也可转换为其他类型  
  
  除了可以转换类型外，当变量为英文字母时还支持大小写转换。 
  大写 toUpperCase()  小写 toLowerCase()  当字符变量不为英文字母时，转换无效  
  
  同Java一样，使用某些特殊的字符时，要使用转义。下列是支持的转义序列：  
  \t => 表示制表符   
  \n => 表示换行符  
  \b => 表示退格键（键盘上的Back建）  
  \r => 表示键盘上的Enter键  
  \ => 表示反斜杠  
  \' => 表示单引号  
  \" => 表示双引号  
  \$ => 表示美元符号，如果不转义在kotlin中就表示变量的引用了  
  其他的任何字符请使用Unicode转义序列语法。例：'\uFF00'  
  
 ## 5.4 字符串类型（String）  
 
  String表示字符串类型。其是不可变的。所以字符串的元素可以通过索引操作的字符：str[index]来访问。可以使用for循环迭代字符串：  
  其中str[index]中的str为要目标字符串，index为索引  
  
  字符串字面量  
  在Kotlin中， 字符串字面量有两种类型：  
  包含转义字符的字符串 转义包括（\t、\n等）,不包含转义字符串的也同属此类型  
  包含任意字符的字符串 由三重引号（""" …. """）表示  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin13.png)   
  
  可以使用trimMargin()函数删除前导空格 ，默认使用符号(|)作为距前缀，当然也可以使用其他字符。例：右尖括号（>）、左尖括号（<）等。  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin14.png)  
  
  字符串模板：  使用字符串模板的符号为（$）。在$符号后面加上变量名或大括号中的表达式  
  
 ## 5.5 数组型（Array）  
 
  Kotlin中数组由Array<T>表示，创建数组的3个函数：  
  arrayOf()  
  arrayOfNulls()  
  工厂函数（Array()）  
  
  1. arrayOf()  创建一个数组，参数是一个可变参数的泛型对象  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin15.png)  
  
  2. arrayOfNulls()  用于创建一个指定数据类型且可以为空元素的给定元素个数的数组  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin16.png)  
  
  3. 工厂函数  
  使用一个工厂函数Array()，它使用数组大小和返回给定其索引的每个数组元素的初始值的函数。  
  Array() => 第一个参数表示数组元素的个数，第二个参数则为使用其元素下标组成的表达式  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin17.png)   
  
  4. 原始类型数组  
  Kotlin还有专门的类来表示原始类型的数组，没有装箱开销，它们分别是： 
  ByteArray => 表示字节型数组  
  ShortArray => 表示短整型数组  
  IntArray => 表示整型数组  
  LongArray => 表示长整型数组  
  BooleanArray => 表示布尔型数组  
  CharArray => 表示字符型数组  
  FloatArray => 表示浮点型数组  
  DoubleArray => 表示双精度浮点型数组  
  Kotlin中不支持字符串类型这种原始类型数组，可以看源码Arrays.kt这个类中并没有字符串数组的声明。而源码中StringArray.kt这个类并不是声明字符串型数组的。  
  
 # 六. 控制语句  
  
  # 6.1 if语句  
  
  在Kotlin中的if语句和Java还是还是有一定的区别的，它能在Java中更灵活，除了能实现Java写法外，还可以实现表达式（实现三元运算符），及作为一个块的运用。   
  
  Kotlin中的三元运算符  
  在Kotlin中其实是不存在三元运算符(condition ? then : else)这种操作的。  
  那是因为if语句的特性(if表达式会返回一个值)故而不需要三元运算符。  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin18.png)  
  
  Kotlin中的if可以作为一个表达式并返回一个值。  
  
  作为一个块结构，并且最后一句表达式为块的值  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin19.png)  
  
 # 6.2 for语句  
  
  Kotlin废除了Java中的for(初始值;条件；增减步长)这个规则。但是Kotlin中对于for循环语句新增了其他的规则，来满足刚提到的规则。  
  for循环提供迭代器用来遍历任何东西  
  for循环数组被编译为一个基于索引的循环，它不会创建一个迭代器对象  
  
 # 6.2.1 新增的规则，去满足for(初始值;条件;增减步长)这个规则  
  
  递增:  
  关键字：until  
  范围：until[n,m) => 即大于等于n,小于m  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin20.png)  
  
  递减：  
  关键字：downTo  
  范围：downTo[n,m] => 即小于等于n,大于等于m ,n &gt; m  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin21.png)  
  
  符号（' .. '） 表示递增的循环的另外一种操作  
  使用符号( '..').  
  范围：..[n,m]=> 即大于等于n，小于等于m  
  和until的区别，一是简便性。二是范围的不同。  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin22.png)  
  
  设置步长：  
  关键字：step  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin23.png)   
  
 # 6.2.2 迭代  
  
  for循环提供一个迭代器用来遍历任何东西。  
  for循环数组被编译为一个基于索引的循环，它不会创建一个迭代器对象  
  
  1. 遍历字符串  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin24.png)  
  
  2. 遍历数组  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin25.png)  
  
  3. 使用数组的indices属性遍历  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin26.png)  
  
  4. 使用数组的withIndex()方法遍历  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin27.png)  
  
  5. 迭代器遍历  
  其一般和while循环一起使用  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin28.png)  
  
  6. foreach遍历  
  
  ![images](https://github.com/Raphrodite/Kotlin_Study/blob/main/images/kotlin29.png)  
  
 # 6.3 when语句  
  
  在Kotlin中已经废除掉了Java中的switch语句。而新增了when(exp){}语句。  
  when语句不仅可以替代掉switch语句，而且比switch语句更加强大  
  
  
  
  
