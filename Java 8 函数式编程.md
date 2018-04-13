# Java 8 函数式编程

## lambda表达式

### 语法

Java 中的 Lambda 表达式通常使用 `(argument) -> (body)` 语法书写，例如：

```
(arg1, arg2...) -> { body }

(type1 arg1, type2 arg2...) -> { body }
```

以下是一些 Lambda 表达式的例子：

```
(int a, int b) -> {  return a + b; }

() -> System.out.println("Hello World");

(String s) -> { System.out.println(s); }

() -> 42

() -> { return 3.1415 };
```

- 一个 Lambda 表达式可以有零个或多个参数
- 参数的类型既可以明确声明，也可以根据上下文来推断。例如：`(int a)`与`(a)`效果相同
- 所有参数需包含在圆括号内，参数之间用逗号相隔。例如：`(a, b)` 或 `(int a, int b)` 或 `(String a, int b, float c)`
- 空圆括号代表参数集为空。例如：`() -> 42`
- 当只有一个参数，且其类型可推导时，圆括号（）可省略。例如：`a -> return a*a`
- Lambda 表达式的主体可包含零条或多条语句
- 如果 Lambda 表达式的主体只有一条语句，花括号{}可省略。匿名函数的返回类型与该主体表达式一致
- 如果 Lambda 表达式的主体包含一条以上语句，则表达式必须包含在花括号{}中（形成代码块）。匿名函数的返回类型与代码块的返回类型一致，若没有返回则为空



#### 方法引用



### 函数式接口



### 和闭包区别

### 和匿名内部类区别

使用匿名类与 Lambda 表达式的一大区别在于关键词的使用。对于匿名类，关键词 `this` 解读为匿名类，而对于 Lambda 表达式，关键词 `this` 解读为写就 Lambda 的外部类。

Lambda 表达式与匿名类的另一不同在于两者的编译方法。Java 编译器编译 Lambda 表达式并将他们转化为类里面的私有函数，它使用 Java 7 中新加的 `invokedynamic` 指令动态绑定该方法，关于 Java 如何将 Lambda 表达式编译为字节码，Tal Weiss 写了一篇[很好的文章](http://www.takipiblog.com/2014/01/16/compiling-Lambda-expressions-scala-vs-java-8/)。

### 背景



## Stream

