# Kotlin_Study
1.变量
// 包格式 和 java 一致
package com.ymc.hellokotlin

fun main(args: Array<String>) {
    println("Hello world")
    println(max(2,3))
}

fun max(a:Int ,b:Int):Int{
    return if(a>b) a else b;
}
