
按照传统，照例先看下Kotlin的优点：
1. 和Java的无缝调用，这在初期不需要投入非常大的精力，即使遇到搞不定的坑，也不必担心影响业务开发的进度，直接换成java就好了
2. 大量的语法糖，使得代码非常的简洁，熟悉之后的开发效率也要高于Java。例如扩展函数，简单的封装再也不需要写一大堆Utils工具类，直接灵活的给某些类添加扩展方法就可以了。
3. 更加安全，Kotlin似乎比较想消灭空引用，在Java中，调用一个null对象会抛出NullPointException，在Kotlin中，不能为空的对象，例如String对象，会写成
```
var a: String? = "abc"
```    
这个时候只有变量为非空的时候才会调用方法
4. Anko有很多优点，传统的xml写UI时会出现的问题：
 - It is not typesafe
- It is not null-safe
- It forces you to write almost the same code for every layout you make
- XML is parsed on the device wasting CPU time and battery 渲染xml为对象过程耗时耗电
- Most of all, it allows no code reuse. 大部分不能重用
5. 虽然Java 8已经发布了，它包含了很多我们期待的像现代语言中那样的改善，但是我们Android开发者还是被迫在使用Java 7.这是因为法律的问题。
6. 一切kotlin函数都会返回一个值，如果没有指定，它就默认返回一个Unit类
7. Kotlin中的接口比Java（Java 8以前）中的强大多了，因为它们可以包含代码
