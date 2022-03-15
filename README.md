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

# 二. 变量
