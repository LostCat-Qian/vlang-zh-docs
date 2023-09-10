# V 文档

(有关 V 标准库的文档,请参阅 https://modules.vlang.io/)

## 简介

V 是一种静态类型化的编译语言,旨在构建可维护的软件。

它类似于 Go 和 Oberon,同时也受到 Rust、Swift、Kotlin 和 Python 的影响。

V 是一种非常简单的语言。通读本文档只需要一个周末的时间,到时候你就基本掌握了这门语言。

这门语言提倡编写简单明晰的代码,尽量减少抽象。

尽管简单,V 也赋予开发者强大的能力。任何你能用其他语言做到的,在 V 里也可以实现。

## 源码安装 V

获取最新版本 V 的最佳方式,就是从源码安装。操作简单,只需几秒钟:

```bash
git clone https://github.com/vlang/v
cd v
make
# 注意:Windows 用户请在 cmd.exe 终端里运行 make.bat
```

更多详细信息,请参阅 README.md 的 [从源码安装 V](https://github.com/vlang/v/blob/master/README.md#installing-v-from-source) 部分。

## 升级 V 到最新版本

如果设备上已经安装了 V,可以使用 V 内置的自更新器将其升级到最新版本。 运行 `v up` 命令即可。

## 打包 V 以发布发行版

请参阅[打包 V 以发布发行版](https://claude.ai/chat/packaging_v_for_distributions.md) 的相关说明。

## 新手上路

通过任意以下命令,可以让 V 自动为你设置项目的基本结构:

- `v init` → 在当前文件夹添加所需文件,使其成为一个 V 项目
- `v new abc` → 在新文件夹 `abc` 中,创建一个新的项目(默认生成一个 "hello world" 项目)
- `v new abcd web` → 在新文件夹 `abcd` 中,使用 `vweb` 模板创建新项目

## 目录

<table> <tr><td width=33% valign=top>

- [Hello World 示例](#Hello-World)
- [运行包含多个文件的项目文件夹](#运行包含多个文件的项目文件夹)
- [注释](#注释)
- [函数](#函数)
  - [提升声明](#提升声明)
  - [返回多个值](#返回多个值)
- [符号可见性](#符号可见性)
- [变量](#变量)
  - [可变变量](#可变变量)
  - [初始化 vs 赋值](#初始化 vs 赋值)
  - [声明错误](#声明错误)
- [V 类型](#V 类型)
  - [基本类型](#基本类型)
  - [字符串](#字符串)
  - [符号](#符号)
  - [数字](#数字)
  - Array
    - [多维数组](#多维数组)
    - [数组方法](#数组方法)
    - [数组切片](#数组切片)
  - [固定大小数组](#固定大小数组)
  - [Map](#Maps)

</td><td width=33% valign=top>

- 模块导入
  - [选择性导入](#选择性导入)
  - [模块导入别名](#模块导入别名)
- 语句和表达式
  - [If](#if)
  - [Match](#Match)
  - [In 操作符](#In-操作符)
  - [For 循环](#For-循环)
  - [Defer](#defer)
  - [Goto](#goto)
- 结构体
  - [堆结构体](#堆结构体)
  - [默认字段值](#默认字段值)
  - [必填字段](#必填字段)
  - [简洁的结构体字面量语法](#简洁的结构体字面量语法)
  - [结构体更新语法](#结构体更新语法)
  - [结构体字面量后缀参数](#结构体字面量后缀参数)
  - [访问修饰符](#访问修饰符)
  - [匿名结构体](#匿名结构体)
  - [静态类型方法](#静态类型方法)
  - [[noinit\] 结构体](#noinit-结构体)
  - [方法](#方法)
  - [嵌入结构体](#嵌入结构体)
- [联合体](#联合体)

</td><td valign=top>

- 函数 2
  - [默认不可变函数参数](#默认不可变函数参数)
  - [可变参数](#可变参数)
  - [可变数量的参数](#可变数量的参数)
  - [匿名和高阶函数](#匿名和高阶函数)
  - [闭包](#闭包)
  - [参数评估顺序](#参数评估顺序)
- [引用](#引用)
- 常量
  - [需要模块前缀](#需要模块前缀)
- 内置函数
  - [println](#println)
  - [打印自定义类型](#打印自定义类型)
  - [运行时转储表达式](#运行时转储表达式)
- 模块
  - [创建模块](#创建模块)
  - [init 函数](#init-函数)

</td></tr> <tr><td width=33% valign=top>

- 类型声明
  - [类型别名](#类型别名)
  - [枚举](#枚举)
  - [函数类型](#函数类型)
  - [接口](#接口)
  - [和类型](#和类型)
  - Option/Result 类型和错误处理
    - [处理 Option/Result](#处理-optionresult)
  - [自定义错误类型](#自定义错误类型)
  - [泛型](#泛型)
- 并发
  - [生成并发任务](#生成并发任务)
  - [通道](#通道)
  - [共享对象](#共享对象)
- JSON
  - [解析 JSON](#解析-Json)
  - [编码 JSON](#编码-Json)
- 测试
  - [断言](#断言)
  - [带额外信息的断言](#带额外信息的断言)
  - [不会中断程序的断言](#不会中断程序的断言)
  - [测试文件](#测试文件)
  - [运行测试](#运行测试)
- 内存管理
  - [控制](#控制)
  - [栈和堆](#栈和堆)
- [ORM](#orm)
- 编写文档
  - [文档注释中的换行符](#文档注释中的换行符)

</td><td width=33% valign=top>

- 工具
  - [v fmt](#v-fmt)
  - [v shader](#v-shader)
  - [性能分析](#性能分析)
- 包管理
  - [包命令](#包命令)
  - [发布包](#发布包)
- 高级主题
  - [属性](#属性)
  - 条件编译
    - [编译时伪变量](#编译时伪变量)
    - [编译时反射](#编译时反射)
    - [编译时代码](#编译时代码)
    - [编译时类型](#编译时类型)
    - [特定环境的文件](#特定环境的文件)
  - [不安全的内存操作](#不安全的内存操作)
  - [包含引用字段的结构体](#包含引用字段的结构体)
  - [sizeof 和__offsetof](#sizeof-和__offsetof)
  - [有限的操作符重载](#有限的操作符重载)
  - [性能优化](#性能优化)
  - [原子操作](#原子操作)
  - [全局变量](#全局变量)
  - [交叉编译](#交叉编译)
  - 调试
    - [默认的 C 后端二进制文件](#默认的-c-后端二进制文件)
    - [原生后端二进制文件](#原生后端二进制文件)
    - [Javascript 后端](#javascript-后端)

</td><td valign=top>

- V 和 C
  - [在 V 中调用 C](#在-v-中调用-c)
  - [在 C 中调用 V](#在-c-中调用-v)
  - [传递 C 编译标志](#传递-c-编译标志)
  - [#pkgconfig](#pkgconfig)
  - [包含 C 代码](#包含-c-代码)
  - [C 类型](#c-类型)
  - [C 声明](#c-声明)
  - [导出到共享库](#导出到共享库)
  - [将 C 转换为 V](#将-c-转换为-v)
  - [解决 C 问题](#解决-c-问题)
- V 的其他特性
  - [内联汇编](#内联汇编)
  - [热代码重载](#热代码重载)
  - [V 中的跨平台 shell 脚本](#v-中的跨平台-shell-脚本)
  - [无扩展名的 Vsh 脚本](#无扩展名的-vsh-脚本)
- 附录
  - [附录一：关键字](#附录一：关键字)
  - [附录二：操作符](#附录二：操作符)

</td></tr> </table> 

<!-- 注:在代码栅栏后面可以使用几个特殊关键字: compile、cgen、live、ignore、failcompile、okfmt、oksyntax、badsyntax、wip、nofmt 更多详情,请执行:`v check-md` -->

## Hello World

```v
fn main() {
	println('hello world')
}
```

将以上代码保存到 `hello.v` 文件中。然后执行:`v run hello.v`。

> 这是假设你已经按[这里](https://github.com/vlang/v/blob/master/README.md#symlinking)所述,为 V 建立了符号链接。 如果你还没有建立符号链接,则需要手动输入 V 的路径。

恭喜你,刚刚编写并运行了第一个 V 程序!

你可以用 `v hello.v` 编译程序,而不执行它。 有关支持的所有命令,请查看 `v help`。

从上面的例子可以看出,函数是通过 `fn` 关键字声明的。 返回类型在函数名之后指定。在这个例子中,`main` 不返回任何内容,所以没有返回类型。

和 C、Go 以及 Rust 一样,`main` 是程序的入口点。

[`println`](#println) 是少数的[内置函数](#内置函数)之一。 它会将传递给它的值打印到标准输出。

对于单文件的程序,可以省略 `fn main()` 声明。这在编写小程序、"脚本"或刚学习语言时很有用。 为了简洁起见,本教程将跳过 `fn main()`。

这意味着 V 中的一个“Hello World”程序可以简单到只有:

```v
println('hello world')
```

> **注意** 如果你没有明确使用 `fn main() {}`,则需要确保在第一个变量赋值语句或顶层函数调用之前声明所有项, 因为 V 会将第一个赋值/函数调用之后的所有内容视为隐式 main 函数的一部分。

## 运行包含多个文件的项目文件夹

假设你有一个包含多个 .v 文件的文件夹,其中一个文件包含你的 `main()` 函数, 其他文件包含辅助函数。它们可能按主题组织,但仍然*尚未*足够结构化到可以作为独立的可重用模块, 你想将它们全部编译到一个程序中。

在其他语言中,你需要使用包含或构建系统来枚举所有文件,将它们分别编译成目标文件, 然后链接到一个最终的可执行文件。

然而,在 V 中你可以一次编译和运行整个包含 .v 文件的文件夹, 只需使用 `v run .`。传递参数也可以工作,所以你可以 执行:

`v run . --yourparam some_other_stuff`

上述操作首先会编译文件夹中的文件到一个程序(以你的文件夹/项目命名),然后以 `--yourparam some_other_stuff` 作为 CLI 参数执行该程序。

然后,你的程序可以像这样使用 CLI 参数:

```v
import os

println(os.args)
```

> **注意**
>  成功运行后,V 会删除生成的可执行文件。 如果想保留它,请使用 `v -keepc run .`,或者只手动编译 with `v .`。

> **注意** 
>
> 任何 V 编译器标志都应该在 `run` 命令*之前*传入。 源文件/文件夹之后的所有内容将按原样传递给程序 - V 不会对其进行处理。

## 注释

```v
// 这是单行注释
/*
这是多行注释
  /* 它可以嵌套 */  
*/
```

## 函数

```v
fn main() {
	println(add(77, 33))
	println(sub(100, 50))
}

fn add(x int, y int) int {
	return x + y
}

fn sub(x int, y int) int {
	return x - y
}
```

参数名在类型之后。这一点与其他大多数语言类似。

和 Go 以及 C 一样,函数不能重载。这简化了代码,提高了可维护性和可读性。

### 提升声明

函数可以在声明之前使用: `add` 和 `sub` 在 `main` 之后声明,但可以在 `main` 中调用。 这适用于 V 中的所有声明,消除了头文件的需要 或关心文件和声明的顺序。

### 返回多个值

```v
fn foo() (int, int) {
	return 2, 3 
}

a, b := foo()
println(a) // 2
println(b) // 3
c, _ := foo() // 用 `_` 忽略值
```

## 符号可见性

```v
pub fn public_function() {
}

fn private_function() {
}
```

函数默认是私有的(不导出)。要让其他[模块](#模块导入)可以使用它们,在前面加上 `pub`。 这同样适用于[结构体](#结构体)、[常量](#常量)和[类型](#类型声明)。

> **注意** 
>
> `pub` 只能在命名模块中使用。关于创建模块的信息,请参阅[模块](#模块)。

## 变量

```v
name := 'Bob'
age := 20
large_number := i64(9999999999)
println(name)
println(age)
println(large_number)
```

变量使用 `:=` 声明和初始化。这是在 V 中声明变量的惟一方式。 这意味着变量始终有一个初始值。

右侧的值推断出变量的类型。要选择不同的类型,请使用类型转换: 表达式 `T(v)` 将值 `v` 转换为类型 `T`。

与大多数其他语言不同,V 只允许在函数中定义变量。

默认不允许**全局变量**。有关详细信息,请参阅[全局变量](#全局变量)。

为了在不同代码库之间保持一致性,所有变量和函数名称必须使用 `snake_case` 风格,与类型名称不同,类型名称必须使用 `PascalCase`。

> **注意** 然而，V 不是一门纯函数式语言。

有一个编译器标志可以启用全局变量(`-enable-globals`),但这是面向低级应用程序的,如内核和驱动程序。

### 可变变量

```v
mut age := 20
println(age)
age = 21
println(age)
```

要改变变量的值,请使用 `=`。在 V 中,变量默认是不可变的。
 要能够改变变量的值,必须用 `mut` 声明它。

尝试在第一行删除 `mut` 然后编译该程序。

### 初始化 vs 赋值

请注意初始化 `:=` 和赋值 `=` 之间的区别非常重要。 `:=` 用于声明和初始化,`=` 用于赋值。

```v
fn main() {
	age = 21 // 错误:未声明 `age`
}
```

这段代码无法编译,因为变量 `age` 未被声明。 在 V 中,所有变量都需要声明。

```v
fn main() {
	age := 21
}
```

可以在一行中改变多个变量的值。 这样可以不使用中间变量交换值。

```v
mut a := 0
mut b := 1
println('${a}, ${b}') // 0, 1
a, b = b, a
println('${a}, ${b}') // 1, 0
```

### 声明错误

在开发模式下,编译器会警告你没有使用该变量 (你会得到一个“未使用的变量”警告)。 在生产模式下(通过 `-prod` 标志运行 V:`v -prod foo.v`), 它根本不会编译。

```v
fn main() {
	a := 10
	if true {
		a := 20 // 错误:重复定义 `a`
	}
	// 警告:未使用的变量 `a`
}
```

与大多数语言不同,V 不允许变量遮蔽。在父作用域中已经使用的名称声明变量会导致编译错误。

## V 类型

### 基本类型

```v
bool

string

i8    i16  int  i64      i128 (soon)  
u8    u16  u32  u64      u128 (soon)

rune // 表示一个 Unicode 代码点  

f32 f64

isize, usize // 平台相关,表示引用内存中任意位置所需的字节数

voidptr // 这主要用于 [C 互操作性](#v-和-c)  

any // 类似于 C 的 void* 和 Go 的 interface{}
```

> **注意** 与 C 和 Go 不同,`int` 始终是一个 32 位整数。

这里有一个例外情况:当一个操作数是另一个操作数数据范围内的小整数类型时,可以自动进行提升。 这些是允许的可能性:

```
   i8 → i16 → int → i64
                  ↘     ↘
                    f32 → f64
                  ↗     ↗
   u8 → u16 → u32 → u64 ⬎
      ↘     ↘     ↘      ptr
   i8 → i16 → int → i64 ⬏
```

例如一个 `int` 值可以自动转换为 `f64` 或 `i64`,但不能转换为 `u32` (因为对于负值来说,`u32` 会丢失符号信息)。
 但是,从 `int` 到 `f32` 的转换目前会自动进行(尽管对于大值可能会丢失精度)。

像 `123` 或 `4.56` 这样的字面量具有特殊的处理方式。它们不会导致类型提升, 但是默认分别为 `int` 和 `f64`,当必须决定其类型时:

```v
u := u16(12)
v := 13 + u    // v 的类型为 `u16` - 没有提升  
x := f32(45.6)
y := x + 3.14  // y 的类型为 `f32` - 没有提升
a := 75        // a 的类型为 `int` - int 字面量的默认类型
b := 14.7      // b 的类型为 `f64` - float 字面量的默认类型
c := u + a     // c 的类型为 `int` - 自动提升 `u` 的值
d := b + x     // d 的类型为 `f64` - 自动提升 `x` 的值
```

### 字符串

```v
name := 'Bob'  
assert name.len == 3       // 打印出 3
assert name[0] == u8(66) // 索引获得一个字节,u8(66) == `B`
assert name[1..3] == 'ob'  // 切片获得字符串 'ob'

// 转义代码
windows_newline := '\r\n'      // 像 C 语言一样转义特殊字符  
assert windows_newline.len == 2

// 使用 `\x##` 表示法直接指定任意字节,`#` 是十六进制数字
// aardvark_str := '\x61ardvark' 
// assert aardvark_str == 'aardvark'
assert '\xc0'[0] == u8(0xc0) 

// 或使用八进制转义 `\###` 表示法,`#` 是八进制数字
aardvark_str2 := '\141ardvark'
assert aardvark_str2 == 'aardvark'

// Unicode 可以直接指定为 `\u####`,`#` 是十六进制数字
// 并在内部转换为 UTF-8 表示  
star_str := '\u2605' // ★
assert star_str == '★'
assert star_str == '\xe2\x98\x85' // UTF-8 也可以这样指定
```

在 V 中,字符串是一个只读的字节数组。所有 Unicode 字符都使用 UTF-8 编码:

```v
s := 'hello 🌎' // 表情符号占用 4 个字节
assert s.len == 10  

arr := s.bytes() // 将 `string` 转换为 `[]u8`
assert arr.len == 10

s2 := arr.bytestr() // 将 `[]u8` 转换为 `string`
assert s2 == s
```

字符串值是不可变的。你不能修改元素:

```v
mut s := 'hello 🌎'
s[0] = `H` // 不允许
```

> 错误:因为 V 字符串是不可变的,所以不能给 s[i] 赋值

请注意,索引字符串会产生一个 `u8`(字节),而不是一个 `rune` 或另一个 `string`。 索引对应字符串中的*字节*,而不是 Unicode 代码点。如果你想将 `u8` 转换为 `string`,可以在 `u8` 上使用 `.ascii_str()` 方法:

```v
country := 'Netherlands'
println(country[0]) // 输出: 78
println(country[0].ascii_str()) // 输出: N
```

单引号和双引号都可以用来表示字符串。为了统一起见,`vfmt` 会将双引号转换为单引号,除非字符串本身包含单引号。

对于原始字符串,在前面加上 `r`。转义处理不会应用于原始字符串:

```v
s := r'hello\nworld' // `\n` 将作为两个字符保留
println(s) // "hello\nworld"
```

字符串可以轻松转换为整数:

```v
s := '42'
n := s.int() // 42

// 所有 int 字面量都支持  
assert '0xc3'.int() == 195
assert '0o10'.int() == 8 
assert '0b1111_0000_1010'.int() == 3850
assert '-0b1111_0000_1010'.int() == -3850
```

更高级的字符串处理和转换,请参考 [vlib/strconv](https://modules.vlang.io/strconv.html) 模块。

#### 字符串插值

基本的插值语法非常简单 - 在变量名前使用 `${`,后面使用`}`。变量会被转换为字符串并嵌入字面量中:

```v
name := 'Bob'
println('Hello, ${name}!') // Hello, Bob!
```

它也可以和字段一起使用:`'age = ${user.age}'`。你还可以使用更复杂的表达式:`'can register = ${user.age > 13}'`。

支持类似 C `printf()` 的格式说明符。`f`、`g`、`x`、`o`、`b` 等是可选的,用于指定输出格式。编译器会负责存储大小,所以不需要 `hd` 或 `llu`。

遵循此模式使用格式说明符:

```v
${varname:[flags][width][.precision][type]}
```

- flags:可以是以下零个或多个:- 表示在字段内左对齐输出,0 表示使用 `0` 作为填充字符,而不是默认的 `空格` 字符。

  > **注意**
  >  V 目前不支持 `'` 或 `#` 作为格式标志,并且 V 支持但不需要 `+` 来右对齐,因为这是默认情况。

- width:可以是整数值,描述输出的最小字段宽度。

- precision: `.` 后跟整数值,保证小数点后的数字精度(如果输入变量是浮点数)。如果变量是整数则忽略。

- type: `f` 和 `F` 指定输入为浮点数,应渲染为浮点数,`e` 和 `E` 指定输入为浮点数,应渲染为指数形式(部分损坏)。`g` 和 `G` 指定输入为浮点数 — 渲染器将对小值使用浮点数表示法,对大值使用指数表示法。`d` 指定输入为整数,应以十进制数字渲染。`x` 和 `X` 要求整数,并以十六进制数字渲染。`o` 要求整数,并以八进制数字渲染。`b` 要求整数,并以二进制数字渲染。`s` 要求字符串(几乎从不使用)。

  > **注意**
  >  当数字类型可以渲染字母时,如十六进制字符串或特殊值像 `infinity`,小写类型强制使用小写字母,大写类型强制使用大写字母。

  > **注意** 在大多数情况下,最好留空格式类型。默认情况下,浮点数将渲染为 `g`,整数将渲染为 `d`,`s` 几乎总是冗余的。 有三种情况建议指定类型:

  - 格式字符串在编译时解析,因此指定类型有助于检测错误
  - 格式字符串默认使用小写字母表示十六进制数字和 `e` 指数。使用大写类型强制使用大写十六进制数字和大写指数 `E`。
  - 格式字符串是从整数获取十六进制、二进制或八进制字符串的最方便的方法。

更多信息,请参阅 [格式占位符规范](https://en.wikipedia.org/wiki/Printf_format_string#Format_placeholder_specification)。

```v
x := 123.4567
println('[${x:.2}]') // 四舍五入到小数点后两位 => [123.46]  
println('[${x:10}]') // 用空格左对齐 => [   123.457]
println('[${int(x):-10}]') // 用空格右对齐 => [123       ] 
println('[${int(x):010}]') // 左侧用 0 填充 => [0000000123]
println('[${int(x):b}]') // 以二进制输出 => [1111011]
println('[${int(x):o}]') // 以八进制输出 => [173]  
println('[${int(x):X}]') // 以大写十六进制输出 => [7B]

println('[${10.0000:.2}]') // 去除末尾无意义的 0 => [10]
println('[${10.0000:.2f}]') // 显示末尾 0,即使它们不改变数字 => [10.00]
```

#### 字符串操作符

```v
name := 'Bob'
bobby := name + 'by' // + 用于连接字符串
println(bobby) // "Bobby"
mut s := 'hello '  
s += 'world' // `+=` 用于追加字符串
println(s) // "hello world"
```

V 中的所有操作符两个操作数必须为相同类型。不能将整数连接到字符串:

```v
age := 10
println('age = ' + age) // 不允许
```

> 错误:中缀表达式:不能将 `int`(右表达式)用作 `string`

我们需要 either 把 `age` 转换为 `string`:

```v
age := 11  
println('age = ' + age.str())
```

或者使用字符串插值(首选):

```v
age := 12
println('age = ${age}')
```

请参阅 [string](https://modules.vlang.io/index.html#string) 的所有方法, 以及相关模块 [strings](https://modules.vlang.io/strings.html)、 [strconv](https://modules.vlang.io/strconv.html)。

### 符号

一个 `rune` 表示一个 Unicode 字符,是 `u32` 的别名。 使用 <code>`</code> (反引号)表示:

```v
rocket := `🚀`
```

可以使用 `.str()` 方法将 `rune` 转换为 UTF-8 字符串。

```v
rocket := `🚀`
assert rocket.str() == '🚀'
```

可以使用 `.bytes()` 方法将 `rune` 转换为 UTF-8 字节。

```v
rocket := `🚀`
assert rocket.bytes() == [u8(0xf0), 0x9f, 0x9a, 0x80]
```

十六进制、Unicode 和八进制转义序列在 `rune` 字面量中也可以使用:

```v
assert `\x61` == `a`
assert `\141` == `a` 
assert `\u0061` == `a`

// 多字节字面量也可以使用
assert `\u2605` == `★`
assert `\u2605`.bytes() == [u8(0xe2), 0x98, 0x85]
assert `\xe2\x98\x85`.bytes() == [u8(0xe2), 0x98, 0x85]
assert `\342\230\205`.bytes() == [u8(0xe2), 0x98, 0x85]
```

请注意,`rune` 字面量使用与字符串相同的转义语法,但只能包含一个 Unicode 字符。 因此,如果代码不指定单个 Unicode 字符,将在编译时收到错误。

还要记住字符串按字节索引,而不是按 rune 索引,所以要当心:

```v
rocket_string := '🚀'
assert rocket_string[0] != `🚀`  
assert 'aloha!'[0] == `a`
```

字符串可以通过' .runes() '方法转换为符号。

```v
hello := 'Hello World 👋'
hello_runes := hello.runes() // [`H`, `e`, `l`, `l`, `o`, ` `, `W`, `o`, `r`, `l`, `d`, ` `, `👋`]
assert hello_runes.string() == hello
```

### 数字

```v
a := 123
```

This will assign the value of 123 to `a`. By default `a` will have the
type `int`.

You can also use hexadecimal, binary or octal notation for integer literals:

```v
a := 0x7B
b := 0b01111011
c := 0o173
```

All of these will be assigned the same value, 123. They will all have type
`int`, no matter what notation you used.

V also supports writing numbers with `_` as separator:

```v
num := 1_000_000 // same as 1000000
three := 0b0_11 // same as 0b11
float_num := 3_122.55 // same as 3122.55
hexa := 0xF_F // same as 255
oct := 0o17_3 // same as 0o173
```

If you want a different type of integer, you can use casting:

```v
a := i64(123)
b := u8(42)
c := i16(12345)
```

Assigning floating point numbers works the same way:

```v
f := 1.0
f1 := f64(3.14)
f2 := f32(3.14)
```

If you do not specify the type explicitly, by default float literals
will have the type of `f64`.

Float literals can also be declared as a power of ten:

```v
f0 := 42e1 // 420
f1 := 123e-2 // 1.23
f2 := 456e+2 // 45600
```

### 数组


数组是具有相同类型的数据元素的集合。数组字面量是用方括号括起来的表达式列表。单个元素可以使用 *index* 表达式访问。索引从 0 开始:

```v
mut nums := [1, 2, 3]
println(nums) // `[1, 2, 3]`
println(nums[0]) // `1`
println(nums[1]) // `2`

nums[1] = 5
println(nums) // `[1, 5, 3]`
```

<a id='array-operations'></a>

An element can be appended to the end of an array using the push operator `<<`.
It can also append an entire array.

```v
mut nums := [1, 2, 3]
nums << 4
println(nums) // "[1, 2, 3, 4]"

// append array
nums << [5, 6, 7]
println(nums) // "[1, 2, 3, 4, 5, 6, 7]"
```

```v
mut names := ['John']
names << 'Peter'
names << 'Sam'
// names << 10  <-- This will not compile. `names` is an array of strings.
```

`val in array` returns true if the array contains `val`. See [`in` operator](#in-operator).

```v
names := ['John', 'Peter', 'Sam']
println('Alex' in names) // "false"
```

#### 数组字段

数组有两个字段用于控制其"大小"：

- `len`：*长度* - 数组中预分配并初始化的元素数量。
- `cap`：*容量* - 为元素保留的内存空间量，但尚未初始化或计算为元素。数组可以增长到这个大小，而无需重新分配内存。通常情况下，V会自动处理这个字段，但也有一些情况下用户可能希望进行手动优化（参见[下文](https://chat.openai.com/?model=text-davinci-002-render-sha#array-initialization)）。

```v
mut nums := [1, 2, 3]
println(nums.len) // 输出 "3"
println(nums.cap) // 输出 "3" 或更大
nums = [] // 数组现在为空
println(nums.len) // 输出 "0"
```

`data` 是一个字段（类型为 `voidptr`），存储了第一个元素的地址。这是用于低级别的[`unsafe`](https://chat.openai.com/?model=text-davinci-002-render-sha#memory-unsafe-code)代码。

> **注意** 
>
> 字段是只读的，不能被用户修改。

#### 数组初始化

数组的类型由第一个元素决定：

- `[1, 2, 3]` 是一个整数数组 (`[]int`)。
- `['a', 'b']` 是一个字符串数组 (`[]string`)。

用户可以显式地为第一个元素指定类型：`[u8(16), 32, 64, 128]`。 V数组是同质的（所有元素必须具有相同的类型）。 这意味着像 `[1, 'a']` 这样的代码将无法编译。

上述语法对于已知元素数量较小的情况是可以的，但对于非常大或空的数组，有第二种初始化语法：

```v
mut a := []int{len: 10000, cap: 30000, init: 3}
```

这将创建一个包含10000个初始化为`3`的`int`元素的数组。为30000个元素预留了内存空间。参数 `len`、`cap` 和 `init` 是可选的； `len` 默认为 `0`，`init` 默认为元素类型的默认初始化值（对于数字类型为 `0`，对于 `string` 等为 `''`）。运行时系统确保容量不小于 `len`（即使明确指定了一个更小的值）：

```v
arr := []int{len: 5, init: -1}
// `arr == [-1, -1, -1, -1, -1]`, arr.cap == 5

// 声明一个空数组：
users := []int{}
```

设置容量可以提高向数组中添加元素的性能，因为可以避免重新分配：

```v
mut numbers := []int{cap: 1000}
println(numbers.len) // 输出 0
// 现在添加元素将不会重新分配
for i in 0 .. 1000 {
	numbers << i
}
```

> **注意** 
>
> 上述代码使用了一个[范围 `for` 循环](https://chat.openai.com/?model=text-davinci-002-render-sha#range-for)语句。

你可以通过访问 `index` 变量来初始化数组，它会给出如下所示的索引：

```v
count := []int{len: 4, init: index}
assert count == [0, 1, 2, 3]

mut square := []int{len: 6, init: index * index}
// square == [0, 1, 4, 9, 16, 25]
```

#### 数组类型

一个数组可以是以下类型之一：

| 类型         | 示例定义                             |
| ------------ | ------------------------------------ |
| 数字         | `[]int,[]i64`                        |
| 字符串       | `[]string`                           |
| 符文（字符） | `[]rune`                             |
| 布尔值       | `[]bool`                             |
| 数组         | `[][]int`                            |
| 结构体       | `[]MyStructName`                     |
| 通道         | `[]chan f64`                         |
| 函数         | `[]MyFunctionType` `[]fn (int) bool` |
| 接口         | `[]MyInterfaceName`                  |
| 合成类型     | `[]MySumTypeName`                    |
| 泛型类型     | `[]T`                                |
| 映射（字典） | `[]map[string]f64`                   |
| 枚举         | `[]MyEnumType`                       |
| 别名         | `[]MyAliasTypeName`                  |
| 线程         | `[]thread int`                       |
| 引用         | `[]&f64`                             |
| 共享         | `[]shared MyStructType`              |

**示例代码:**

此示例使用[结构体](#结构体)和[合成类型](#Sum Types (合成类型))来创建一个数组，可以处理不同类型（例如，点和线）的数据元素。

```v
struct Point {
	x int
	y int
}

struct Line {
	p1 Point
	p2 Point
}

type ObjectSumType = Line | Point

mut object_list := []ObjectSumType{}
object_list << Point{1, 1}
object_list << Line{
	p1: Point{3, 3}
	p2: Point{4, 4}
}
dump(object_list)
/*
object_list: [ObjectSumType(Point{
    x: 1
    y: 1
}), ObjectSumType(Line{
    p1: Point{
        x: 3
        y: 3
    }
    p2: Point{
        x: 4
        y: 4
    }
})]
*/
```

#### 多维数组

#### 多维数组

2维数组示例：

```v
mut a := [][]int{len: 2, init: []int{len: 3}}
a[0][1] = 2
println(a) // [[0, 2, 0], [0, 0, 0]]
```

3维数组示例：

```v
mut a := [][][]int{len: 2, init: [][]int{len: 3, init: []int{len: 2}}}
a[0][1][1] = 2
println(a) // [[[0, 0], [0, 2], [0, 0]], [[0, 0], [0, 0], [0, 0]]]
```

#### 数组方法

所有数组可以通过 `println(arr)` 轻松打印，并可以通过 `s := arr.str()` 转换为字符串。

使用 `.clone()` 可以复制数组中的数据：

```v
nums := [1, 2, 3]
nums_copy := nums.clone()
```

数组可以通过 `.filter()` 和 `.map()` 方法高效地进行筛选和映射：

```v
nums := [1, 2, 3, 4, 5, 6]
even := nums.filter(it % 2 == 0)
println(even) // [2, 4, 6]
// filter可以接受匿名函数
even_fn := nums.filter(fn (x int) bool {
	return x % 2 == 0
})
println(even_fn)
vCopy codewords := ['hello', 'world']
upper := words.map(it.to_upper())
println(upper) // ['HELLO', 'WORLD']
// map也可以接受匿名函数
upper_fn := words.map(fn (w string) string {
	return w.to_upper()
})
println(upper_fn) // ['HELLO', 'WORLD']
```

`it` 是一个内置变量，用于引用当前在filter/map方法中处理的元素。

此外，还可以使用 `.any()` 和 `.all()` 方法方便地测试满足条件的元素。

```v
nums := [1, 2, 3]
println(nums.any(it == 2)) // true
println(nums.all(it >= 2)) // false
```

还有一些用于数组的内置方法：

- `a.repeat(n)` 将数组元素重复 `n` 次
- `a.insert(i, val)` 在索引 `i` 处插入一个新元素 `val`，并将所有后续元素向右移动
- `a.insert(i, [3, 4, 5])` 插入多个元素
- `a.prepend(val)` 在开头插入一个值，等效于 `a.insert(0, val)`
- `a.prepend(arr)` 在开头插入数组 `arr` 的元素
- `a.trim(new_len)` 截断长度（如果 `new_length < a.len`，否则什么也不做）
- `a.clear()` 清空数组但不更改 `cap`（等效于 `a.trim(0)`）
- `a.delete_many(start, size)` 从索引 `start` 处移除 `size` 个连续元素 - 触发重新分配
- `a.delete(index)` 等效于 `a.delete_many(index, 1)`
- `a.delete_last()` 移除最后一个元素
- `a.first()` 等效于 `a[0]`
- `a.last()` 等效于 `a[a.len - 1]`
- `a.pop()` 移除并返回最后一个元素
- `a.reverse()` 生成一个以相反顺序排列的新数组
- `a.reverse_in_place()` 颠倒数组中元素的顺序
- `a.join(joiner)` 将字符串数组连接成一个字符串，使用 `joiner` 作为分隔符

查看 [array](https://modules.vlang.io/index.html#array) 的所有方法。

另请参阅 [vlib/arrays](https://modules.vlang.io/arrays.html)。

#### 数组排序

对所有类型的数组进行排序非常简单直观。特殊变量 `a` 和 `b` 在提供自定义排序条件时会被使用。

```v
mut numbers := [1, 3, 2]
numbers.sort() // 1, 2, 3
numbers.sort(a > b) // 3, 2, 1
vCopy codestruct User {
	age  int
	name string
}

mut users := [User{21, 'Bob'}, User{20, 'Zarkon'}, User{25, 'Alice'}]
users.sort(a.age < b.age) // 按 User.age int 字段排序
users.sort(a.name > b.name) // 按 User.name string 字段反向排序
```

V还支持自定义排序，通过 `sort_with_compare` 数组方法。它期望一个比较函数来定义排序顺序。可以用于根据自定义排序规则同时在多个字段上进行排序。 下面的代码对数组按 `name` 升序和 `age` 降序排序。

```v
struct User {
	age  int
	name string
}

mut users := [User{21, 'Bob'}, User{65, 'Bob'}, User{25, 'Alice'}]

custom_sort_fn := fn (a &User, b &User) int {
	// 当 a 在 b 前面时返回 -1
	// 当两者处于相同顺序时返回 0
	// 当 b 在 a 前面时返回 1
	if a.name == b.name {
		if a.age < b.age {
			return 1
		}
		if a.age > b.age {
			return -1
		}
		return 0
	}
	if a.name < b.name {
		return -1
	} else if a.name > b.name {
		return 1
	}
	return 0
}
users.sort_with_compare(custom_sort_fn)
```

#### 数组切片

切片是父数组的一部分。初始时它指向由 `..` 运算符分隔的两个索引之间的元素。右侧索引必须大于或等于左侧索引。

如果右侧索引缺失，将假定为数组长度。如果左侧索引缺失，则假定为0。

```v
nums := [0, 10, 20, 30, 40]
println(nums[1..4]) // [10, 20, 30]
println(nums[..4]) // [0, 10, 20, 30]
println(nums[1..]) // [10, 20, 30, 40]
```

在V中，切片本身也是数组（它们不是不同的类型）。因此，可以在它们上执行所有数组操作。例如，它们可以推送到具有相同类型的数组：

```v
array_1 := [3, 5, 4, 7, 6]
mut array_2 := [0, 1]
array_2 << array_1[..3]
println(array_2) // `[0, 1, 3, 5, 4]`
```

切片总是使用最小可能的容量创建 `cap == len`（参见[上文](https://chat.openai.com/?model=text-davinci-002-render-sha#array-initialization)中的 `cap`）， 无论父数组的容量或长度如何。因此，当大小增加时，它将立即重新分配并复制到另一个内存位置，从而变得独立于父数组（*在增长时复制*）。特别是向切片中添加元素并不会改变父数组：

```v
mut a := [0, 1, 2, 3, 4, 5]
mut b := a[2..4]
b[0] = 7 // `b[0]` 指向 `a[2]`
println(a) // `[0, 1, 7, 3, 4, 5]`
b << 9
// `b` 已经重新分配，并且现在独立于 `a`
println(a) // `[0, 1, 7, 3, 4, 5]` - 没有变化
println(b) // `[7, 3, 9]`
```

向父数组添加元素可能会使其与其子切片之间独立或不独立。行为取决于父数组的容量，并且是可以预测的：

```v
mut a := []int{len: 5, cap: 6, init: 2}
mut b := unsafe { a[1..4] }
a << 3
// 不会重新分配 - 适合于 `cap`
b[2] = 13 // 修改了 `a[3]`
a << 4
// a 已经重新分配，现在与 `b` 独立（超出了 `cap`）
b[1] = 3 // 在 `a` 中没有变化
println(a) // `[2, 2, 2, 13, 2, 3, 4]`
println(b) // `[2, 3, 13]`
```

如果你想立即获得一个独立的副本，你可以在切片上调用 `.clone()`：

```v
mut a := [0, 1, 2, 3, 4, 5]
mut b := a[2..4].clone()
b[0] = 7 // 注意：`b[0]` 不是指向 `a[2]`，因为没有使用 .clone() 的话，它将会指向 a[2]
println(a) // [0, 1, 2, 3, 4, 5]
println(b) // [7, 3]
```

##### 带有负索引的切片

#### 支持负索引的数组和字符串切片

V支持带有负索引的数组和字符串切片。 负索引从数组的末尾向开始计算，例如 `-3` 等同于 `array.len - 3`。 负切片与正常切片具有不同的语法，即你需要在数组名称和方括号之间添加一个 `gate`：`a#[..-3]`。 `gate` 指定这是一种不同类型的切片，并记住返回的切片 "锁定" 在数组内。 返回的切片始终是一个有效的数组，尽管可能为空：

```v
a := [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
println(a#[-3..]) // [7, 8, 9]
println(a#[-20..]) // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
println(a#[-20..-8]) // [0, 1]
println(a#[..-3]) // [0, 1, 2, 3, 4, 5, 6]

// 空数组
println(a#[-20..-10]) // []
println(a#[20..10]) // []
println(a#[20..30]) // []
```

#### 数组方法链式调用

你可以链式调用数组方法，如 `.filter()` 和 `.map()`，并使用内置变量 `it` 来实现经典的 `map/filter` 函数式编程范式：

```v
// 使用 filter、map 和负数数组切片
files := ['pippo.jpg', '01.bmp', '_v.txt', 'img_02.jpg', 'img_01.JPG']
filtered := files.filter(it#[-4..].to_lower() == '.jpg').map(it.to_upper())
// ['PIPPO.JPG', 'IMG_02.JPG', 'IMG_01.JPG']
```

### 固定大小数组

V还支持具有固定大小的数组。与普通数组不同，它们的长度是恒定的。你不能向它们添加元素，也不能缩小它们。你只能在原地修改它们的元素。

然而，访问固定大小数组的元素更高效，它们需要的内存比普通数组少，并且与普通数组不同，它们的数据位于堆栈上，因此如果你不想进行额外的堆分配，可以将它们用作缓冲区。

大多数方法被定义为在普通数组上工作，而不是在固定大小数组上工作。 你可以使用切片将固定大小数组转换为普通数组：

```v
mut fnums := [3]int{} // fnums 是一个具有3个元素的固定大小数组。
fnums[0] = 1
fnums[1] = 10
fnums[2] = 100
println(fnums) // => [1, 10, 100]
println(typeof(fnums).name) // => [3]int

fnums2 := [1, 10, 100]! // 执行相同操作的简短初始化语法（该语法可能会更改）

anums := fnums[..] // 与 `anums := fnums[0..fnums.len]` 相同
println(anums) // => [1, 10, 100]
println(typeof(anums).name) // => []int
```

请注意，切片将导致固定大小数组的数据被复制到新创建的普通数组中。

### Maps

```v
mut m := map[string]int{} // 一个键为 `string` 类型，值为 `int` 类型的映射
m['one'] = 1
m['two'] = 2
println(m['one']) // "1"
println(m['bad_key']) // "0"
println('bad_key' in m) // 使用 `in` 来检测是否存在该键
println(m.keys()) // ['one', 'two']
m.delete('two')
```

映射可以拥有 `string`、`rune`、整数、浮点数或 `voidptr` 类型的键。

可以使用以下简短的语法来初始化整个映射：

```v
numbers := {
	'one': 1
	'two': 2
}
println(numbers)
```

如果找不到键，则默认返回零值：

```v
sm := {
	'abc': 'xyz'
}
val := sm['bad_key']
println(val) // ''
```

```v
intm := {
	1: 1234
	2: 5678
}
s := intm[3]
println(s) // 0
```

还可以使用 `or {}` 块来处理不存在的键：

```v
mm := map[string]int{}
val := mm['bad_key'] or { panic('key not found') }
```

你还可以一次性检查键是否存在，并在键存在时获取其值：

```v
m := {
	'abc': 'def'
}
if v := m['abc'] {
	println('该键的映射值是: ${v}')
}
```

相同的选项检查也适用于数组：

```v
arr := [1, 2, 3]
large_index := 999
val := arr[large_index] or { panic('out of bounds') }
println(val)
// 如果你想*传播*访问错误，也可以这样做：
val2 := arr[333]!
println(val2)
```

V还支持嵌套映射：

```v
mut m := map[string]map[string]int{}
m['greet'] = {
	'Hello': 1
}
m['place'] = {
	'world': 2
}
m['code']['orange'] = 123
print(m)
```

映射是按插入顺序排序的，类似于Python中的字典。这是一种保证的语言特性，但将来可能会发生变化。

查看所有[映射的方法](https://modules.vlang.io/index.html#map)和[maps](https://modules.vlang.io/maps.html)。

## 模块导入

有关创建模块的信息，请参阅[模块](#modules)。

可以使用 `import` 关键字导入模块：

```v
import os

fn main() {
	// 从stdin读取文本
	name := os.input('请输入您的姓名：')
	println('你好，${name}！')
}
```

这个程序可以使用 `os` 模块中的任何公共定义，比如 `input` 函数。请参阅[标准库](https://modules.vlang.io/)文档以获取常见模块及其公共符号的列表。

默认情况下，每次调用外部函数时都必须指定模块前缀。起初可能会显得冗长，但这使得代码更易读和理解 - 总是清楚地知道正在调用哪个模块中的哪个函数。这在大型代码库中特别有用。

不允许循环导入模块，与Go语言类似。

### 选择性导入

您也可以直接从模块中导入特定的函数和类型：

```v
import os { input }

fn main() {
	// 从stdin读取文本
	name := input('请输入您的姓名：')
	println('你好，${name}！')
}
```

> **注意**
> 这也将导入模块本身。此外，不能用于常量 - 它们必须始终带有前缀。

您可以一次导入多个特定符号：

```v
import os { input, user_os }

name := input('请输入您的姓名：')
println('姓名：${name}')
current_os := user_os()
println('您的操作系统是${current_os}。')
```

### 模块导入别名

可以使用 `as` 关键字对任何导入的模块名称进行别名：

> **注意**
> 除非您已创建了 `mymod/sha256.v`，否则此示例将无法编译。

```v failcompile
import crypto.sha256
import mymod.sha256 as mysha256

fn main() {
	v_hash := sha256.sum('hi'.bytes()).hex()
	my_hash := mysha256.sum('hi'.bytes()).hex()
	assert my_hash == v_hash
}
```

您不能为导入的函数或类型设置别名。但是，您可以重新声明类型。

```v
import time
import math

type MyTime = time.Time

fn (mut t MyTime) century() int {
	return int(1.0 + math.trunc(f64(t.year) * 0.009999794661191))
}

fn main() {
	mut my_time := MyTime{
		year: 2020
		month: 12
		day: 25
	}
	println(time.new_time(my_time).utc_string())
	println('Century: ${my_time.century()}')
}
```

## 语句和表达式

### If

```v
a := 10
b := 20
if a < b {
	println('${a} < ${b}')
} else if a > b {
	println('${a} > ${b}')
} else {
	println('${a} == ${b}')
}
```

`if` 语句非常直观，与大多数其他语言类似。与其他类似C的语言不同，条件周围没有括号，大括号始终是必需的。

`if` 可以用作表达式：

```v
num := 777
s := if num % 2 == 0 { 'even' } else { 'odd' }
println(s)
// "odd"
```

您可以在任何可以使用 `or {}` 的地方使用“if解包”。这会将表达式的解包值绑定到一个变量，当该表达式既不是`none`也不是错误时。

```v
m := {
	'foo': 'bar'
}

// 处理缺少的键
if v := m['foo'] {
	println(v) // bar
} else {
	println('not found')
}
```

```v
fn res() !int {
	return 42
}

// 返回结果类型的函数
if v := res() {
	println(v)
}
```

```v
struct User {
	name string
}

arr := [User{'John'}]

// 带有变量赋值的 if 解包
u_name := if v := arr[0] {
	v.name
} else {
	'Unnamed'
}
println(u_name) // John
```

#### 类型检查和类型转换

您可以使用 `is` 和其否定形式 `!is` 来检查和判断当前和总和类型。

可以在 `if` 中执行：

```v cgen
struct Abc {
	val string
}

struct Xyz {
	foo string
}

type Alphabet = Abc | Xyz

x := Alphabet(Abc{'test'}) // 总和类型
if x is Abc {
	// x 会自动转为 Abc 类型，可以在这里使用
	println(x)
}
if x !is Abc {
	println('不是 Abc')
}
```

或使用 `match`：

```v oksyntax
match x {
	Abc {


		// x 会自动转为 Abc 类型，可以在这里使用
		println(x)
	}
	Xyz {
		// x 会自动转为 Xyz 类型，可以在这里使用
		println(x)
	}
}
```

这也适用于结构字段：

```v
struct MyStruct {
	x int
}

struct MyStruct2 {
	y string
}

type MySumType = MyStruct | MyStruct2

struct Abc {
	bar MySumType
}

x := Abc{
	bar: MyStruct{123} // MyStruct 将自动转换为 MySumType 类型
}
if x.bar is MyStruct {
	// x.bar 会自动转换
	println(x.bar)
} else if x.bar is MyStruct2 {
	new_var := x.bar as MyStruct2
	// ... 或者你可以使用 `as` 手动创建类型转换的别名：
	println(new_var)
}
match x.bar {
	MyStruct {
		// x.bar 会自动转换
		println(x.bar)
	}
	else {}
}
```

可变变量可以发生变化，进行类型转换将是不安全的。
然而，有时候尽管是可变的，类型转换也是有用的。
在这种情况下，开发人员必须使用 `mut` 关键字标记表达式，
以告诉编译器他们知道自己在做什么。

它的工作原理如下：

```v oksyntax
mut x := MySumType(MyStruct{123})
if mut x is MyStruct {
	// 即使是可变的，x 也会转为 MyStruct
	// 没有 mut 关键字就不会生效
	println(x)
}
// 与 match 相同
match mut x {
	MyStruct {
		// 即使是可变的，x 也会转为 MyStruct
		// 没有 mut 关键字就不会生效
		println(x)
	}
}
```

### Match

```v
os := 'windows'
print('V is running on ')
match os {
	'darwin' { println('macOS.') }
	'linux' { println('Linux.') }
	else { println(os) }
}
```

A `match`语句是一种更简洁的方式来编写一系列的`if - else`语句。当匹配到匹配分支时，将执行后续的语句块。当没有其他分支匹配时，将执行`else`分支。

```v
number := 2
s := match number {
	1 { 'one' }
	2 { 'two' }
	else { 'many' }
}
```

`match`语句还可以用作`if - else if - else`的替代形式：

```v
match true {
	2 > 4 { println('if') }
	3 == 4 { println('else if') }
	2 == 2 { println('else if2') }
	else { println('else') }
}
// 应该打印'else if2'
```

或作为`unless`的替代形式：[unless Ruby](https://www.tutorialspoint.com/ruby/ruby_if_else.htm)

```v
match false {
	2 > 4 { println('if') }
	3 == 4 { println('else if') }
	2 == 2 { println('else if2') }
	else { println('else') }
}
// 应该打印'if'
```

`match`表达式返回匹配分支的最终表达式的值。

```v
enum Color {
	red
	blue
	green
}

fn is_red_or_blue(c Color) bool {
	return match c {
		.red, .blue { true } // 逗号可以用于测试多个值
		.green { false }
	}
}
```

`match`语句还可以用于分支`enum`的变体，使用缩写的`.variant_here`语法。当所有分支都是详尽无遗时，不允许使用`else`分支。

```v
c := `v`
typ := match c {
	`0`...`9` { 'digit' }
	`A`...`Z` { 'uppercase' }
	`a`...`z` { 'lowercase' }
	else { 'other' }
}
println(typ)
// 'lowercase'
```

您还可以使用范围作为`match`模式。如果值落在分支范围内，将执行该分支。

请注意，范围使用`...`（三个点）而不是`..`（两个点）。这是因为范围*包含*最后一个元素，而不是排除（如`..`范围一样）。在`match`分支中使用`..`将引发错误。

```v
const start = 1

const end = 10

c := 2
num := match c {
	start...end {
		1000
	}
	else {
		0
	}
}
println(num)
// 1000
```

常量也可以在范围分支表达式中使用。

> **注意**
> 作为表达式的`match`在`for`循环和`if`语句中无法使用。

### In 操作符

`in`允许检查数组或映射是否包含元素。要执行相反的操作，请使用`!in`。

```v
nums := [1, 2, 3]
println(1 in nums) // true
println(4 !in nums) // true
```

> **注意**
> `in`检查映射是否包含键，而不是值。

```v
m := {
	'one': 1
	'two': 2
}

println('one' in m) // true
println('three' !in m) // true
```

它还用于编写更清晰和更紧凑的布尔表达式：

```v
enum Token {
	plus
	minus
	div
	mult
}

struct Parser {
	token Token
}

parser := Parser{}
if parser.token == .plus || parser.token == .minus || parser.token == .div || parser.token == .mult {
	// ...
}
if parser.token in [.plus, .minus, .div, .mult] {
	// ...
}
```

V会优化这种表达式，因此上面的两个`if`语句产生相同的机器代码，不会创建数组。

### For 循环

V只有一个循环关键字：`for`，有几种形式。

#### `for`/`in`

这是最常见的形式。您可以将其与数组、映射或数值范围一起使用。

##### 数组`for`

```v
numbers := [1, 2, 3, 4, 5]
for num in numbers {
	println(num)
}
names := ['Sam', 'Peter']
for i, name in names {
	println('${i}) ${name}')
	// 输出：0) Sam
	//         1) Peter
}
```

`for value in arr`形式用于遍历数组的元素。如果需要索引，可以使用另一种形式`for index, value in arr`。

请注意，该值是只读的。
如果需要在循环时修改数组，则需要将元素声明为可变的：

```v
mut numbers := [0, 1, 2]
for mut num in numbers {
	num++
}
println(numbers) // [1, 2, 3]
```

当标识符只是一个下划线时，它将被忽略。

##### 自定义迭代器

实现返回`Option`的`next`方法的类型可以使用`for`循环进行迭代。

```v
struct SquareIterator {
	arr []int
mut:
	idx int
}

fn (mut iter SquareIterator) next() ?int {
	if iter.idx >= iter.arr.len {
		return none
	}
	defer {
		iter.idx++
	}
	return iter.arr[iter.idx] * iter.arr[iter.idx]
}

nums := [1, 2, 3, 4, 5]
iter := SquareIterator{
	arr: nums
}
for squared in iter {
	println(squared)
}
```

上面的代码打印：

```
1
4
9
16
25
```

##### 遍历Map的 `for`

```v
m := {
	'one': 1
	'two': 2
}
for key, value in m {
	println('${key} -> ${value}')
	// 输出：one -> 1
	//         two -> 2
}
```

键或值可以使用单个下划线作为标识符来忽略。

```v


m := {
	'one': 1
	'two': 2
}
// 遍历键
for key, _ in m {
	println(key)
	// 输出：one
	//         two
}
// 遍历值
for _, value in m {
	println(value)
	// 输出：1
	//         2
}
```

##### 范围`for`

```v
// 打印'01234'
for i in 0 .. 5 {
	print(i)
}
```

`low..high`表示一个*独占*范围，表示从`low`到`high`之间的所有值，但*不包括*`high`。

#### 带有条件的`for`

```v
mut sum := 0
mut i := 0
for i <= 100 {
	sum += i
	i++
}
println(sum) // "5050"
```

这种形式的循环类似于其他语言中的`while`循环。一旦布尔条件评估为`false`，循环将停止迭代。再次强调，没有括号括住条件，括号始终是必需的。

#### 不带有条件的`for`

```v
mut num := 0
for {
	num += 2
	if num >= 10 {
		break
	}
}
println(num) // "10"
```

条件可以被省略，导致一个无限循环。

#### C风格的`for`

```v
for i := 0; i < 10; i += 2 {
	// 不要打印6
	if i == 6 {
		continue
	}
	println(i)
}
```

最后，还有传统的C样式`for`循环。与后者相比，它更安全，因为容易忘记更新计数器并陷入无限循环。

在这里，`i`不需要用`mut`声明，因为根据定义，它将始终是可变的。

#### 标记的break和continue

`break`和`continue`默认控制最内层的`for`循环。您还可以在`break`和`continue`后面加上一个标签名称，以引用外部的`for`循环：

```v
outer: for i := 4; true; i++ {
	println(i)
	for {
		if i < 7 {
			continue outer
		} else {
			break outer
		}
	}
}
```

标签必须紧随外部循环之前。
上面的代码会打印：

```
4
5
6
7
```

### defer

延迟执行语句将一组语句的执行推迟到包围函数返回之前。

```v
import os

fn read_log() {
	mut ok := false
	mut f := os.open('log.txt') or { panic(err) }
	defer {
		f.close()
	}
	// ...
	if !ok {
		// 在这里将调用延迟执行语句，文件将被关闭
		return
	}
	// ...
	// 在这里将调用延迟执行语句，文件将被关闭
}
```

如果函数返回一个值，则在评估返回表达式之后执行`defer`块：

```v
import os

enum State {
	normal
	write_log
	return_error
}

// 写日志文件并返回写入的字节数

fn write_log(s State) !int {
	mut f := os.create('log.txt')!
	defer {
		f.close()
	}
	if s == .write_log {
		// 在执行`f.write()`之后但在最终返回写入的字节数之前将调用`f.close()`
		return f.writeln('This is a log file')
	} else if s == .return_error {
		// 在`error()`函数返回后，文件将被关闭 - 因此错误消息仍将报告
		// 它为打开状态
		return error('nothing written; file open: ${f.is_opened}')
	}
	// 文件也将在这里关闭
	return 0
}

fn main() {
	n := write_log(.return_error) or {
		println('Error: ${err}')
		0
	}
	println('${n} bytes written')
}
```

要在`defer`块内访问函数的结果，可以使用`$res()`表达式。
当返回单个值时才使用`$res()`，而在多返回情况下使用`$res(idx)`是有参数的。

```v ignore
fn (mut app App) auth_middleware() bool {
	defer {
		if !$res() {
			app.response.status_code = 401
			app.response.body = 'Unauthorized'
		}
	}
	header := app.get_header('Authorization')
	if header == '' {
		return false
	}
	return true
}

fn (mut app App) auth_with_user_middleware() (bool, string) {
	defer {
		if !$res(0) {
			app.response.status_code = 401
			app.response.body = 'Unauthorized'
		} else {
			app.user = $res(1)
		}
	}
	header := app.get_header('Authorization')
	if header == '' {
		return false, ''
	}
	return true, 'TestUser'
}
```

### Goto

V允许使用`goto`无条件跳转到一个标签。标签名称必须包含在与`goto`语句相同的函数中。程序可以`goto`一个超出当前作用域或更深的标签。`goto`允许跳过变量初始化或返回到已经释放了内存的代码，因此它需要使用`unsafe`。

```v ignore
if x {
	// ...
	if y {
		unsafe {
			goto my_label
		}
	}
	// ...
}
my_label:
```

应该避免使用`goto`，特别是可以使用`for`时。
[标记的break/continue](#labelled-break--continue)可以用于跳出嵌套循环，这样就不会有违反内存安全性的风险。

## 结构体

```v
struct Point {
	x int
	y int
}

mut p := Point{
	x: 10
	y: 20
}
println(p.x) // 通过点运算符访问结构体字段
// 另一种字面量语法
p = Point{10, 20}
assert p.x == 10
```

### 堆上的结构体

结构体在堆栈上分配。要在堆上分配一个结构体并获得一个[引用](#references)，请使用 `&` 前缀：

```v
struct Point {
	x int
	y int
}

p := &Point{10, 10}
// 引用的字段访问具有相同的语法
println(p.x)
```

`p` 的类型是 `&Point`。它是对 `Point` 的[引用](#引用)。引用类似于 Go 中的指针和 C++ 中的引用。

```v
struct Foo {
mut:
	x int
}

fa := Foo{1}
mut a := fa
a.x = 2
assert fa.x == 1
assert a.x == 2

// fb := Foo{ 1 }
// mut b := &fb  // 错误：`fb` 是不可变的，不能有一个对它的可变引用
// b.x = 2

mut fc := Foo{1}
mut c := &fc
c.x = 2
assert fc.x == 2
assert c.x == 2
println(fc) // Foo{ x: 2 }
println(c) // &Foo{ x: 2 } // 注意前缀 `&`。
```

另见[栈和堆](#stack-and-heap)

### 默认字段值

```v
struct Foo {
	n   int    // 默认情况下，n 是 0
	s   string // 默认情况下，s 是 ''
	a   []int  // 默认情况下，a 是 `[]int{}` 
	pos int = -1 // 自定义默认值
}
```

在创建结构体时，默认情况下所有结构字段都将被清零。数组和映射字段将被分配空间。对于引用值，请参见[这里](#structs-with-reference-fields)。

也可以定义自定义默认值。

### 必填字段

```v
struct Foo {
	n int [required]
}
```

你可以用 `[required]` [属性](#attributes) 标记一个结构字段，告诉 V 在创建该结构体的实例时必须对该字段进行初始化。

下面的示例将无法编译，因为字段 `n` 没有明确初始化：

```v failcompile
_ = Foo{}
```

<a id='short-struct-initialization-syntax'></a>

### 简短的结构字面量语法

```v
struct Point {
	x int
	y int
}

mut p := Point{
	x: 10
	y: 20
}
p = Point{
	x: 30
	y: 4
}
assert p.y == 4
//
// 数组：第一个元素定义了数组的类型
points := [Point{10, 20}, Point{20, 30}, Point{40, 50}]
println(points) // [Point{x: 10, y: 20}, Point{x: 20, y: 30}, Point{x: 40,y: 50}]
```

省略结构体名称也适用于返回结构体字面量或将其作为函数参数传递。

### 结构体更新语法

V 使得返回对象的修改版本变得容易：

```v
struct User {
	name          string
	age           int
	is_registered bool
}

fn register(u User) User {
	return User{
		...u
		is_registered: true
	}
}

mut user := User{
	name: 'abc'
	age: 23
}
user = register(user)
println(user)
```

### 尾部结构字面量参数

V 不支持默认函数参数或命名参数，可以使用尾部结构字面量语法：

```v
[params]
struct ButtonConfig {
	text        string
	is_disabled bool
	width       int = 70
	height      int = 20
}

struct Button {
	text   string
	width  int
	height int
}

fn new_button(c ButtonConfig) &Button {
	return &Button{
		width: c.width
		height: c.height
		text: c.text
	}
}

button := new_button(text: 'Click me', width: 100)
// 高度未设置，因此它的默认值是 20
assert button.height == 20
```

如你所见，结构体名称和大括号都可以省略，而不是：

```v oksyntax nofmt
new_button(ButtonConfig{text:'Click me', width:100})
```

这仅适用于最后一个参数是结构体的函数。

> 注意 `[params]` 标签用于告诉 V，尾部结构参数可以被*完全*省略，因此你可以写成 `button := new_button()`。
> 否则，你必须*至少*指定一个字段名，即使它具有默认值，否则编译器会产生以下错误消息，当你在没有参数的情况下调用函数时：
> `error: 预期 1 个参数，但得到了 0 个`。

### 访问修饰符

默认情况下，结构体字段是私有且不可变的（这也使得结构体本身也是不可变的）。
它们的访问修饰符可以通过 `pub` 和 `mut` 进行更改。总共有 5 种可能的选项：

```v
struct Foo {
	a int // 默认情况下是私有且不可变的
mut:
	b int // 私有且可变的
	c int // (你可以列出多个具有相同访问修饰符的字段)
pub:
	d int // 公共和不可变的（只读）
pub mut:
	e int // 在父模块中可公开，但只能在父模块中进行修改
__global:
	//（不建议使用，这就是为什么“global”关键字以 __ 开头的原因）
	f int // 在父模块内外都是公共且可变的
}
```

私有字段仅在

同一[模块](#modules)内可用，任何直接尝试从另一个模块中访问它们都将在编译期间引发错误。公共不可变字段在任何地方都是只读的。

### 匿名结构体

V 支持匿名结构体：无需单独声明结构体名称。

```v
struct Book {
	author struct {
		name string
		age  int
	}

	title string
}

book := Book{
	author: struct {
		name: 'Samantha Black'
		age: 24
	}
}
assert book.author.name == 'Samantha Black'
assert book.author.age == 24
```

### 静态类型方法

V 现在支持静态类型方法，如 `User.new()`。可以通过 `fn [Type name].[function name]` 在结构体上定义这些方法，以便组织与结构体相关的所有函数：

```v oksyntax
struct User {}

fn User.new() User {
	return User{}
}

user := User.new()
```

这是工厂函数的替代方法，例如 `fn new_user() User {}`，应该使用它来代替。

请注意，这些不是构造函数，而是简单的函数。V 没有构造函数或类。

### `[noinit]` 结构体

V 支持 `[noinit]` 结构体，这些结构体不能在定义它们的模块之外进行初始化。它们要么用于内部使用，要么可以通过*工厂函数*在外部使用。

例如，考虑在名为 `sample` 的目录中的以下源代码：

```v oksyntax
module sample

[noinit]
pub struct Information {
pub:
	data string
}

pub fn new_information(data string) !Information {
	if data.len == 0 || data.len > 100 {
		return error('数据必须在 1 到 100 个字符之间')
	}
	return Information{
		data: data
	}
}
```

请注意，`new_information` 是一个*工厂*函数。现在，当我们想在模块外部使用这个结构体时：

```v okfmt
import sample

fn main() {
	// 当 [noinit] 属性存在时，这将无法工作：
	// info := sample.Information{
	// 	data: '示例信息。'
	// }

	// 使用这个代替：
	info := sample.new_information('示例信息。')!

	println(info)
}
```

### 方法

```v
struct User {
	age int
}

fn (u User) can_register() bool {
	return u.age > 16
}

user := User{
	age: 10
}
println(user.can_register()) // "false"
user2 := User{
	age: 20
}
println(user2.can_register()) // "true"
```

V 没有类，但你可以在类型上定义方法。方法是一个带有特殊接收器参数的函数。接收器出现在 `fn` 关键字和方法名称之间的自己的参数列表中。方法必须在接收器类型所在的模块中。

在此示例中，`can_register` 方法的接收器类型为 `User`，命名为 `u`。约定是不使用接收器名称如 `self` 或 `this`，而是使用一个简短的、最好是一个字母长的名称。

### 嵌入式结构体

V 支持嵌入式结构体。

```v
struct Size {
mut:
	width  int
	height int
}

fn (s &Size) area() int {
	return s.width * s.height
}

struct Button {
	Size
	title string
}
```

通过嵌入，结构体 `Button` 将自动获得来自结构体 `Size` 的所有字段和方法，这使得你可以这样做：

```v oksyntax
mut button := Button{
	title: '点击我'
	height: 2
}

button.width = 3
assert button.area() == 6
assert button.Size.area() == 6
print(button)
```

输出：

```
Button{
    Size: Size{
        width: 3
        height: 2
    }
    title: '点击我'
}
```

与继承不同，你不能在结构体和嵌套的结构体之间进行类型转换（嵌套的结构体也可以有自己的字段，它也可以嵌套多个结构体）。

如果需要直接访问嵌入的结构体，可以使用显式引用，如 `button.Size`。

从概念上讲，嵌入式结构体类似于面向对象编程中的[mixin](https://en.wikipedia.org/wiki/Mixin)，而不是基类。

你也可以初始化嵌入的结构体：

```v oksyntax
mut button := Button{
	Size: Size{
		width: 3
		height: 2
	}
}
```

或者分配值：

```v oksyntax
button.Size = Size{
	width: 4
	height: 5
}
```

如果多个嵌入式结构体具有相同的名称或如果在结构体中定义了具有相同名称的方法或字段，则可以像 `button.Size.area()` 这样调用嵌入式结构体中的方法或赋值给嵌入式结构体中的变量。当你没有指定嵌套的结构体名称时，将针对最外层的结构体的方法。

## 联合体

与结构体类似，联合体也支持嵌入。

```v
struct Rgba32_Component {
	r u8
	g u8
	b u8
	a u8
}

union Rgba32 {
	Rgba32_Component
	value u32
}

clr1 := Rgba32{
	value: 0x008811FF
}

clr2 := Rgba32{
	Rgba32_Component: Rgba32_Component{
		a: 128
	}
}

sz := sizeof(Rgba32)
unsafe {
	println('Size: ${sz}B,clr1.b: ${clr1.b},clr2.b: ${clr2.b}')
}
```

输出：`Size: 4B, clr1.b: 136, clr2.b: 0`

必须在 `unsafe` 块中执行联合体成员访问。

> **注意**
> 嵌入式结构的参数未必按照列出的顺序存储。

## 函数 2

### 默认情况下是不可变的函数参数

在 V 中，默认情况下，函数参数是不可变的，可变参数必须在调用时加上标记。

由于也没有全局变量，这意味着函数的返回值仅取决于它们的参数，并且它们的评估没有副作用（除非函数使用 I/O）。

即使传递了 [引用](#references)，函数参数在默认情况下也是不可变的。

> **注意**
> 然而，V 不是一种纯函数式的语言。

可以通过使用编译器标志启用全局变量(`-enable-globals`)，但这是为了低级应用程序如内核和驱动程序。

### 可变参数

通过使用关键字 `mut` 声明它们，可以修改函数参数：

```v
struct User {
	name string
mut:
	is_registered bool
}

fn (mut u User) register() {
	u.is_registered = true
}

mut user := User{}
println(user.is_registered) // "false"
user.register()
println(user.is_registered) // "true"
```

在这个例子中，接收者（即第一个参数）被明确标记为可变的，因此 `register()` 可以更改用户对象。对于非接收者参数，也同样适用：

```v
fn multiply_by_2(mut arr []int) {
	for i in 0 .. arr.len {
		arr[i] *= 2
	}
}

mut nums := [1, 2, 3]
multiply_by_2(mut nums)
println(nums)
// "[2, 4, 6]"
```

请注意，在调用此函数时，必须在 `nums` 前面加上 `mut`。这样做可以清楚地表明被调用的函数将修改该值。

最好返回值而不是修改参数，例如 `user = register(user)`（或 `user.register()`）而不是 `register(mut user)`。只应在应用程序的性能关键部分中修改参数，以减少分配和复制。

因此，V 不允许使用原始类型（例如整数）修改参数。只有诸如数组和映射之类的更复杂的类型才可以被修改。

### 可变数量的参数

V 支持接受任意数量的参数的函数，用 `...` 前缀表示。
下面，`a ...int` 表示将任意数量的参数收集到名为 `a` 的数组中。

```v
fn sum(a ...int) int {
	mut total := 0
	for x in a {
		total += x
	}
	return total
}

println(sum()) // 0
println(sum(1)) // 1
println(sum(2, 3)) // 5
// 使用数组解构
a := [2, 3, 4]
println(sum(...a)) // <-- 在这里使用前缀 ...。输出：9
b := [5, 6, 7]
println(sum(...b)) // 输出：18
```

### 匿名和高阶函数

```v
fn sqr(n int) int {
	return n * n
}

fn cube(n int) int {
	return n * n * n
}

fn run(value int, op fn (int) int) int {
	return op(value)
}

fn main() {
	// 函数可以传递给其他函数
	println(run(5, sqr)) // "25"
	// 可以在其他函数内部声明匿名函数：
	double_fn := fn (n int) int {
		return n + n
	}
	println(run(5, double_fn)) // "10"
	// 函数可以在不将它们分配给变量的情况下传递：
	res := run(5, fn (n int) int {
		return n + n
	})
	println(res) // "10"
	// 甚至可以拥有一个包含函数的数组/映射：
	fns := [sqr, cube]
	println(fns[0](10)) // "100"
	fns_map := {
		'sqr':  sqr
		'cube': cube
	}
	println(fns_map['cube'](2)) // "8"
}
```

### 闭包

V 也支持闭包。
这意味着匿名函数可以继承它们被创建的范围中的变量。它们必须通过列出所有要继承的变量来显式地执行此操作。

```v oksyntax
my_int := 1
my_closure := fn [my_int] () {
	println(my_int)
}
my_closure() // 输出 1
```

在创建匿名函数时，继承的变量会被复制。
这意味着如果在创建函数之后修改原始变量，则不会在函数中反映此修改。

```v oksyntax
mut i := 1
func := fn [i] () int {
	return i
}
println(func() == 1) // true
i = 123
println(func() == 1) // 仍然为 true
```

但是，在匿名函数内部可以修改变量。
这个变化不会在外部反映出来，但会在以后的函数调用中反映出来。

```v oksyntax
fn new_counter() fn () int {
	mut i := 0
	return fn [mut i] () int {
		i++
		return i
	}
}

c := new_counter()
println(c()) // 1
println(c()) // 2
println(c()) // 3
```

如果需要在函数外部修改值，请使用引用。

```v oksyntax
mut i := 0
mut ref := &i
print_counter := fn [ref] () {
	println(*ref)
}

print_counter() // 0
i = 10
print_counter() // 10
```

### 参数评估顺序

函数调用的参数的评估顺序 *不能* 保证。例如，考虑以下程序：

```v
fn f(a1 int, a2 int, a3 int) {
	dump(a1 + a2 + a3)
}

fn main() {
	f(dump(100), dump(200), dump(300))
}
```

V 当前不能保证它会按照 100、200、300 的顺序打印。唯一的保证是 600（来自`f` 的主体）将在所有它们之后打印。

这 *可能* 在 V 1.0 中发生变化。

## 引用

```v
struct Foo {}

fn (foo Foo) bar_method() {
	// ...
}

fn bar_function(foo Foo) {
	// ...
}
```

如果一个函数参数是不可变的（就像上面示例中的 `foo` 一样），V 可以通过值或引用传递它。编译器会决定，开发者不需要考虑这个问题。

您不再需要记住是应该按值传递结构体还是按引用传递。

您可以通过添加 `&` 来确保结构体始终以引用的方式传递：

```v
struct Foo {
	abc int
}

fn (foo &Foo) bar() {
	println(foo.abc)
}
```

`foo` 仍然是不可变的，不能被更改。为此，必须使用 `(mut foo Foo)`。

总的来说，V 的引用类似于 Go 的指针和 C++ 的引用。例如，通用树结构的定义看起来是这样的：

```v
struct Node[T] {
	val   T
	left  &Node[T]
	right &Node[T]
}
```

要取消引用，请使用 `*` 运算符，就像在 C 中一样。

## 常量

```v
const (
	pi    = 3.14
	world = '世界'
)

println(pi)
println(world)
```

常量是用 `const` 声明的。它们只能在模块级别（在函数外部）定义。
常量的值永远不能被更改。你也可以单独声明一个常量：

```v
const e = 2.71828
```

V 的常量比大多数语言更灵活。你可以赋予更复杂的值：

```v
struct Color {
	r int
	g int
	b int
}

fn rgb(r int, g int, b int) Color {
	return Color{
		r: r
		g: g
		b: b
	}
}

const (
	numbers = [1, 2, 3]
	red     = Color{
		r: 255
		g: 0
		b: 0
	}
	// 在编译时评估函数调用*
	blue = rgb(0, 0, 255)
)

println(numbers)
println(red)
println(blue)
```

\* WIP - 目前函数调用在程序启动时评估

通常情况下，全局变量是不允许的，所以这可能非常有用。

**模块**

可以使用 `pub const` 使常量公开：

```v oksyntax
module mymodule

pub const golden_ratio = 1.61803

fn calc() {
	println(mymodule.golden_ratio)
}
```

`pub` 关键字只允许在 `const` 关键字之前使用，不能在 `const ( )` 块内使用。

在模块外，所有常量都需要以模块名作为前缀。

### 需要模块前缀

在命名常量时，必须使用 `snake_case`。为了区分常量和局部变量，必须指定到常量的完整路径。例如，要访问 PI 常量，必须在 `math` 模块内外都使用完整的 `math.pi` 名称。只有在 `main` 模块（包含您的 `fn main()` 的模块）中才放松了这个规则，您可以使用在那里定义的常量的未限定名称，即 `numbers`，而不是 `main.numbers`。

vfmt 会处理这个规则，因此您可以在 `math` 模块内输入 `println(pi)`，vfmt 将自动将其更新为 `println(math.pi)`。

很多人更喜欢全大写的常量，比如 `TOP_CITIES`。但在V中，这种方式不是很合适，因为常量比其他语言中的常量更为强大。它们可以表示复杂的结构，而且由于没有全局变量，这种用法非常常见：

```v oksyntax
println('Top cities: ${top_cities.filter(.usa)}')
```

## 内建函数

V语言中包含一些内建函数，比如 `println`。以下是完整列表：

```v ignore
fn print(s string) // 将任何内容打印到stdout
fn println(s string) // 打印任何内容并在stdout上换行

fn eprint(s string) // 与print()相同，但使用stderr
fn eprintln(s string) // 与println()相同，但使用stderr

fn exit(code int) // 以自定义错误代码终止程序
fn panic(s string) // 在stderr上打印一条消息和回溯，并以错误代码1终止程序
fn print_backtrace() // 在stderr上打印回溯
```

> **注意**
> 虽然 `print` 函数接受一个字符串，但V还接受其他可打印类型。详情请见下文。

还有一个特殊的内建函数叫做 [`dump`](#在运行时候转储表达式)。

### println

`println` 是一个简单但功能强大的内建函数，可以打印任何东西：字符串、数字、数组、映射、结构体等。

```v
struct User {
	name string
	age  int
}

println(1) // "1"
println('hi') // "hi"
println([1, 2, 3]) // "[1, 2, 3]"
println(User{ name: 'Bob', age: 20 }) // "User{name:'Bob', age:20}"
```

另请参阅[数组方法](#数组方法)。

<a id='自定义类型的打印'></a>

### 打印自定义类型

如果你想为你的类型定义一个自定义的打印值，只需定义一个 `str() string` 方法：

```v
struct Color {
	r int
	g int
	b int
}

pub fn (c Color) str() string {
	return '{${c.r}, ${c.g}, ${c.b}}'
}

red := Color{
	r: 255
	g: 0
	b: 0
}
println(red)
```

### 在运行时候转储表达式

你可以使用 `dump(expr)` 来转储/跟踪任何V表达式的值。例如，将以下代码示例保存为 `factorial.v`，然后用 `v run factorial.v` 运行它：

```v
fn factorial(n u32) u32 {
	if dump(n <= 1) {
		return dump(1)
	}
	return dump(n * factorial(n - 1))
}

fn main() {
	println(factorial(5))
}
```

你会得到：

```
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: false
[factorial.v:2] n <= 1: true
[factorial.v:3] 1: 1
[factorial.v:5] n * factorial(n - 1): 2
[factorial.v:5] n * factorial(n - 1): 6
[factorial.v:5] n * factorial(n - 1): 24
[factorial.v:5] n * factorial(n - 1): 120
120
```

请注意，`dump(expr)` 将跟踪源位置、表达式本身以及表达式的值。

## 模块

每个位于文件夹根目录的文件都属于同一个模块。简单的程序不需要指定模块名称，默认为 'main'。

参见[符号可见性](#符号可见性)，[访问修饰符](#访问修饰符)。

### 创建模块

V是一门非常模块化的语言。鼓励创建可重用的模块，并且非常容易实现。
要创建一个新模块，创建一个包含你的模块名的目录，其中包含具有代码的.v文件：

```shell
cd ~/code/modules
mkdir mymodule
vim mymodule/myfile.v
```

```v failcompile
// myfile.v
module mymodule

// 要导出一个函数，我们必须使用 `pub`
pub fn say_hi() {
	println('hello from mymodule!')
}
```

模块内的所有项目都可以在模块的文件之间使用，无论是否以 `pub` 关键字为前缀。

```v failcompile
// myfile2.v
module mymodule

pub fn say_hi_and_bye() {
	say_hi() // 来自 myfile.v
	println('goodbye from mymodule')
}
```

现在你可以在你的代码中使用 `mymodule` 了：

```v failcompile
import mymodule

fn main() {
	mymodule.say_hi()
	mymodule.say_hi_and_bye()
}
```

* 模块名应该简短，不超过10个字符。
* 模块名必须使用 `snake_case`。
* 不允许循环导入。
* 你可以在一个模块中拥有任意数量的 .v 文件。
* 你可以在任何地方创建模块。
* 所有模块都会静态编译到一个单独的可执行文件中。

### `init` 函数

如果你希望模块在导入时自动调用一些设置/初始化代码，你可以使用一个模块 `init` 函数：

```v
fn init() {
	// 在这里放置你的初始化代码...
}
```

`init` 函数不能是公共（pub）的 - 它将自动调用。这个功能特别适用于初始化C库。

## 类型声明

### 类型别名

要将一个新类型 `NewType` 定义为 `ExistingType` 的别名，
请使用 `type NewType = ExistingType`。<br/>
这是[总和类型](#sum-types)声明的一种特殊情况。

### 枚举

```v
enum Color as u8 {
	red
	green
	blue
}

mut color := Color.red
// V 知道 `color` 是一个 `Color`。在这里没有必要使用 `color = Color.green`。
color = .green
println(color) // "green"
match color {
	.red { println('颜色是红色') }
	.green { println('颜色是绿色') }
	.blue { println('颜色是蓝色') }
}
```

枚举类型可以是任何整数类型，但如果是 `int` 的话可以省略：`enum Color {`。

枚举匹配必须是全面的，或者具有一个 `else` 分支。
这可以确保如果添加了一个新的枚举字段，它将在代码的所有地方进行处理。

枚举字段不能重用保留关键字。不过，保留关键字可以用 @ 符号转义：

```v
enum Color {
	@none
	red
	green
	blue
}

color := Color.@none
println(color)
```

整数可以赋给枚举字段：

```v
enum Grocery {
	apple
	orange = 5
	pear
}

g1 := int(Grocery.apple)
g2 := int(Grocery.orange)
g3 := int(Grocery.pear)
println('杂货 ID：${g1}，${g2}，${g3}')
```

输出：`杂货 ID：0，5，6`。

不允许在枚举变量上进行操作；它们必须显式转换为 `int`。

枚举可以像结构体一样拥有方法：

```v
enum Cycle {
	one
	two
	three
}

fn (c Cycle) next() Cycle {
	match c {
		.one {
			return .two
		}
		.two {
			return .three
		}
		.three {
			return .one
		}
	}
}

mut c := Cycle.one
for _ in 0 .. 10 {
	println(c)
	c = c.next()
}
```

输出：

```
one
two
three
one
two
three
one
two
three
one
```

### 函数类型

你可以使用类型别名来命名特定的函数签名，例如：

```v
type Filter = fn (string) string
```

这与任何其他类型一样工作 - 例如，一个函数可以接受一个函数类型的参数：

```v
type Filter = fn (string) string

fn filter(s string, f Filter) string {
	return f(s)
}
```

V 支持鸭子类型，因此函数不需要声明与函数类型的兼容性 - 它们只需要是兼容的：

```v
fn uppercase(s string) string {
	return s.to_upper()
}

// 现在 `uppercase` 可以在任何需要 `Filter` 的地方使用
```

兼容的函数也可以显式转换为函数类型：

```v oksyntax
my_filter := Filter(uppercase)
```

这里的转换纯粹是信息性的 - 再次强调，鸭子类型意味着结果类型与显式转换时的类型相同：

```v oksyntax
my_filter := uppercase
```

你可以将分配的函数作为参数传递：

```v oksyntax
println(filter('Hello world', my_filter)) // 输出 `HELLO WORLD`
```

当然，你也可以直接传递它，而不使用本地变量：

```v oksyntax
println(filter('Hello world', uppercase))
```

匿名函数也可以这样使用：

```v oksyntax
println(filter('Hello world', fn (s string) string {
	return s.to_upper()
}))
```

你可以在[这里](https://github.com/vlang/v/tree/master/examples/function_types.v)找到完整的示例。

### 接口

```v
// interface-example.1
struct Dog {
	breed string
}

fn (d Dog) speak() string {
	return '汪汪'
}

struct Cat {
	breed string
}

fn (c Cat) speak() string {
	return '喵喵'
}

// 不像 Go，但类似 TypeScript，V 的接口可以同时定义字段和方法。
interface Speaker {
	breed string
	speak() string
}

fn main() {
	dog := Dog{'莱昂贝格犬'}
	cat := Cat{'暹罗猫'}

	mut arr := []Speaker{}
	arr << dog
	arr << cat
	for item in arr {
		println('一只 ${item.breed} 说：${item.speak()}')
	}
}
```

#### 实现接口

类型通过实现其方法和字段来实现接口。
无需显式声明意图，也无需 "implements" 关键字。

接口可以有一个 `mut:` 部分。实现类型

将需要
具有接口 `mut:` 部分中声明的方法的 `mut` 接收器。

```v
// interface-example.2
module main

interface Foo {
	write(string) string
}

// => 实现接口 Foo 的类型的方法签名应该是：
// `fn (s Type) write(a string) string`

interface Bar {
mut:
	write(string) string
}

// => 实现接口 Bar 的类型的方法签名应该是：
// `fn (mut s Type) write(a string) string`

struct MyStruct {}

// MyStruct 实现接口 Foo，但 *不* 实现接口 Bar
fn (s MyStruct) write(a string) string {
	return a
}

fn main() {
	s1 := MyStruct{}
	fn1(s1)
	// fn2(s1) -> 编译错误，因为 MyStruct 没有实现 Bar
}

fn fn1(s Foo) {
	println(s.write('Foo'))
}

// fn fn2(s Bar) { // 不匹配
//      println(s.write('Foo'))
// }
```

#### 转换接口

我们可以使用动态类型转换运算符来测试接口的底层类型。

> **注意**
> 动态类型转换将变量 `s` 转换为指针，位于本示例中的 `if` 语句内部：

```v oksyntax
// interface-example.3 (从 interface-example.1 继续)
interface Something {}

fn announce(s Something) {
	if s is Dog {
		println('一只 ${s.breed} 狗') // `s` 自动转换为 `Dog` (智能转换)
	} else if s is Cat {
		println('一只猫说 ${s.speak()}')
	} else {
		println('其他东西')
	}
}

fn main() {
	dog := Dog{'莱昂贝格犬'}
	cat := Cat{'暹罗猫'}
	announce(dog)
	announce(cat)
}
```

```v
// interface-example.4
interface IFoo {
	foo()
}

interface IBar {
	bar()
}

// 仅实现 IFoo
struct SFoo {}

fn (sf SFoo) foo() {}

// 同时实现 IFoo 和 IBar
struct SFooBar {}

fn (sfb SFooBar) foo() {}

fn (sfb SFooBar) bar() {
	dump('这实现了 IBar')
}

fn main() {
	mut arr := []IFoo{}
	arr << SFoo{}
	arr << SFooBar{}

	for a in arr {
		dump(a)
		// 为了执行实现了 IBar 的实例。
		if a is IBar {
			a.bar()
		}
	}
}
```

有关更多信息，请参阅[动态类型转换](#dynamic-casts)。

#### 接口方法定义

也不像 Go，接口可以拥有自己的方法，类似于结构体可以拥有自己的方法。
这些 '接口方法' 不需要被实现，而是由实现该接口的结构体来实现。
它们只是一种便利的方式，可以写成 `i.some_function()`，而不是 `some_function(i)`，类似于结构体方法可以被看作是 `s.xyz()` 的一种便利方式，而不是 `xyz(s)`。

> **注意**
> 此功能不像 C# 中的 "默认实现"。

例如，如果一个结构体 `cat` 被包装在一个接口 `a` 中，该接口具有与结构体实现的方法同名的方法 `speak`，并且你调用 `a.speak()`，只会调用接口方法：

```v
interface Adoptable {}

fn (a Adoptable) speak() string {
	return '请收养我！'
}

struct Cat {}

fn (c Cat) speak() string {
	return '喵喵！'
}

struct Dog {}

fn main() {
	cat := Cat{}
	assert dump(cat.speak()) == '喵喵！'
	//
	a := Adoptable(cat)
	assert dump(a.speak()) == '请收养我！' // 调用 Adoptable 的 `speak`
	if a is Cat {
		// 但是，在这个 `if` 中，V 知道 `a` 不仅仅是一个 Adoptable，而是一个真正的 Cat，所以它将使用 Cat 的 `speak`，而不是 Adoptable 的 `speak`：
		dump(a.speak()) // 喵喵！
	}
	//
	b := Adoptable(Dog{})
	assert dump(b.speak()) == '请收养我！' // 调用 Adoptable 的 `speak`
	// if b is Dog {
	// 	dump(b.speak()) // 错误：未知的方法或字段：Dog.speak
	// }
}
```

#### 嵌入式接口

接口支持嵌入，就像结构体一样：

```v
pub interface Reader {
mut:
	read(mut buf []u8) ?int
}

pub interface Writer {
mut:
	write(buf []u8) ?int
}

// ReaderWriter 嵌入了 Reader 和 Writer。
// 效果与将 Reader 的所有方法/字段和 Writer 的所有方法/字段复制/粘贴到 ReaderWriter 中相同。
pub interface ReaderWriter {
	Reader
	Writer
}
```

### Sum Types (合成类型)

总和类型实例可以包含多种不同类型的值。使用 `type` 关键字声明总和类型：

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

sum := World(Moon{})
assert sum.type_name() == 'Moon'
println(sum)
```

内建方法 `type_name` 返回当前持有类型的名称。

利用总和类型，你可以构建递归结构，并在其上编写简洁而功能强大的代码。

```v
// V 的二叉树
struct Empty {}

struct Node {
	value f64
	left  Tree
	right Tree
}

type Tree = Empty | Node

// 对所有节点值求和

fn sum(tree Tree) f64 {
	return match tree {
		Empty { 0 }
		Node { tree.value + sum(tree.left) + sum(tree.right) }
	}
}

fn main() {
	left := Node{0.2, Empty{}, Empty{}}
	right := Node{0.3, Empty{}, Node{0.4, Empty{}, Empty{}}}
	tree := Node{0.5, left, right}
	println(sum(tree)) // 0.2 + 0.3 + 0.4 + 0.5 = 1.4
}
```

#### 动态类型转换

要检查总和类型实例是否持有特定类型，请使用 `sum is Type`。要将总和类型转换为其变体之一，可以使用 `sum as Type`：

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

fn (m Mars) dust_storm() bool {
	return true
}

fn main() {
	mut w := World(Moon{})
	assert w is Moon
	w = Mars{}
	// 使用 `as` 访问 Mars 实例
	mars := w as Mars
	if mars.dust_storm() {
		println('天气不好！')
	}
}
```

如果 `w` 不持有 `Mars` 实例，`as` 将抛出一个 panic。更安全的方法是使用智能转换。

#### 智能转换

```v oksyntax
if w is Mars {
	assert typeof(w).name == 'Mars'
	if w.dust_storm() {
		println('天气不好！')
	}
}
```

在 `if` 语句的代码块中，`w` 具有类型 `Mars`。这被称为*流感知类型*。
如果 `w` 是一个可变标识符，那么如果编译器智能转换它而没有警告，那将是不安全的。
这就是为什么在 `is` 表达式之前必须声明 `mut` 的原因：

```v ignore
if mut w is Mars {
	assert typeof(w).name == 'Mars'
	if w.dust_storm() {
		println('天气不好！')
	}
}
```

否则，`w` 会保留其原始类型。

> 这对于简单变量和像 `user.name` 这样的复杂表达式都适用。

#### 匹配总和类型

你也可以使用 `match` 来确定变体：

```v
struct Moon {}

struct Mars {}

struct Venus {}

type World = Mars | Moon | Venus

fn open_parachutes(n int) {
	println(n)
}

fn land(w World) {
	match w {
		Moon {} // 没有大气层
		Mars {
			// 轻微的大气层
			open_parachutes(3)
		}
		Venus {
			// 厚重的大气层
			open_parachutes(1)
		}
	}
}
```

`match` 必须对每个变体都有一个模式，或者有一个 `else` 分支。

```v ignore
struct Moon {}
struct Mars {}
struct Venus {}

type World = Moon | Mars | Venus

fn (m Moon) moon_walk() {}
fn (m Mars) shiver() {}
fn (v Venus) sweat() {}

fn pass_time(w World) {
    match w {
        // 使用被遮蔽的 match 变量，在这种情况下是 `w` (智能转换)
        Moon { w.moon_walk() }
        Mars { w.shiver() }
        else {}
    }
}
```

### Option/Result 类型和错误处理

Option 类型用于可能代表 `none` 的类型。Result 类型可以代表从函数返回的错误。

通过在类型名称前面添加 `?` 来声明 Option 类型：`?Type`。
Result 类型使用 `!`：`!Type`。

```v
struct User {
	id   int
	name string
}

struct Repo {
	users []User
}

fn (r Repo) find_user_by_id(id int) !User {
	for user in r.users {
		if user.id == id {
			// V 会自动将其包装成 result 或 option 类型
			return user
		}
	}
	return error('找不到用户 ${id}')
}

// 使用 option 版本的函数
fn (r Repo) find_user_by_id2(id int) ?User {
	for user in r.users {
		if user.id == id {
			return user
		}
	}
	return none
}

fn main() {
	repo := Repo{
		users: [User{1, 'Andrew'}, User{2, 'Bob'}, User{10, 'Charles'}]
	}
	user := repo.find_user_by_id(10) or { // option/result 类型必须在 `or` 块中处理
		println(err)
		return
	}
	println(user.id) // "10"
	println(user.name) // "Charles"

	user2 := repo.find_user_by_id2(10) or { return }
}
```

V 曾经将 `Option` 和 `Result` 结合成一个类型，现在它们是分开的。

将函数 "升级" 为 option/result 函数所需的工作量很小；
只需在返回类型前添加 `?` 或 `!`，并在发生错误时返回 `none` 或错误（分别）。

这是 V 中错误处理的主要机制。它们仍然是值，就像在 Go 中一样，
但优点是错误不能未经处理，并且处理它们要简洁得多。
与其他语言不同，V 不使用 `throw/try/catch` 块来处理异常。

`err` 在 `or` 块中定义，并被设置为传递给 `error()` 函数的字符串消息。



```v oksyntax
user := repo.find_user_by_id(7) or {
	println(err) // "找不到用户 7"
	return
}
```

#### 处理 option/result

有四种处理 option/result 的方法。第一种方法是传播错误：

```v
import net.http

fn f(url string) !string {
	resp := http.get(url)!
	return resp.body
}
```

`http.get` 返回 `!http.Response`。因为 `!` 跟在调用后面，错误将传播给 `f` 的调用者。
当在产生 option 的函数调用后使用 `?` 时，封闭函数必须返回一个 option。
如果在 `main()` 函数中使用错误传播，它将导致 `panic`，因为错误无法进一步传播。

`f` 的主体本质上是以下版本的精简版：

```v ignore
    resp := http.get(url) or { return err }
    return resp.body
```

---

第二种方法是早早地停止执行：

```v oksyntax
user := repo.find_user_by_id(7) or { return }
```

在这里，你可以调用 `panic()` 或 `exit()`，它将停止整个程序的执行，
或者使用控制流语句（`return`、`break`、`continue` 等）来中断当前块的执行。

> **注意**
> `break` 和 `continue` 只能在 `for` 循环内使用。

V 没有一种强制“展开” option 的方法（就像其他语言一样，
例如 Rust 的 `unwrap()` 或 Swift 的 `!`）。为此，请改用 `or { panic(err) }`。

---

第三种方法是在 `or` 块的末尾提供一个默认值。
在发生错误的情况下，该值将被分配，因此它必须与正在处理的 option 的内容具有相同的类型。

```v
fn do_something(s string) !string {
	if s == 'foo' {
		return 'foo'
	}
	return error('无效字符串')
}

a := do_something('foo') or { '默认值' } // a 将为 'foo'
b := do_something('bar') or { '默认值' } // b 将为 '默认值'
println(a)
println(b)
```

---

第四种方法是使用 `if` 展开：

```v
import net.http

if resp := http.get('https://google.com') {
	println(resp.body) // resp 是一个 http.Response，而不是 option
} else {
	println(err)
}
```

上面，`http.get` 返回一个 `!http.Response`。`resp` 仅在第一个
`if` 分支的作用域内。`err` 仅在 `else` 分支的作用域内。

### 自定义错误类型

V 允许你通过 `IError` 接口定义自定义错误类型。该接口要求实现两个方法：`msg() string` 和 `code() int`。任何实现了这些方法的类型都可以用作错误。

在定义自定义错误类型时，建议嵌入内建的 `Error` 默认实现。这为两个所需方法提供了一个空的默认实现，因此你只需要实现你真正需要的部分，并且可以在将来提供额外的实用函数。

```v
struct PathError {
	Error
	path string
}

fn (err PathError) msg() string {
	return 'Failed to open path: ${err.path}'
}

fn try_open(path string) ! {
	// V 会自动将其转换为 IError
	return PathError{
		path: path
	}
}

fn main() {
	try_open('/tmp') or { panic(err) }
}
```

### 泛型

```v wip
struct Repo[T] {
    db DB
}

struct User {
	id   int
	name string
}

struct Post {
	id   int
	user_id int
	title string
	body string
}

fn new_repo[T](db DB) Repo[T] {
    return Repo[T]{db: db}
}

// 这是一个泛型函数。V 将为其在使用时的每种类型生成相应的版本。
fn (r Repo[T]) find_by_id(id int) ?T {
    table_name := T.name // 在本例中，获取类型的名称可以得到表名
    return r.db.query_one[T]('select * from ${table_name} where id = ?', id)
}

db := new_db()
users_repo := new_repo[User](db) // 返回 Repo[User]
posts_repo := new_repo[Post](db) // 返回 Repo[Post]
user := users_repo.find_by_id(1)? // find_by_id[User]
post := posts_repo.find_by_id(1)? // find_by_id[Post]
```

目前，泛型函数定义必须声明其类型参数，但在将来，V 将从运行时参数类型的单字母类型名称中推断出泛型类型参数。这就是为什么 `find_by_id` 可以省略 `[T]`，因为接收器参数 `r` 使用了泛型类型 `T`。

另一个示例：

```v
fn compare[T](a T, b T) int {
	if a < b {
		return -1
	}
	if a > b {
		return 1
	}
	return 0
}

// compare[int]
println(compare(1, 0)) // 输出：1
println(compare(1, 1)) //          0
println(compare(1, 2)) //         -1
// compare[string]
println(compare('1', '0')) // 输出：1
println(compare('1', '1')) //          0
println(compare('1', '2')) //         -1
// compare[f64]
println(compare(1.1, 1.0)) // 输出：1
println(compare(1.1, 1.1)) //          0
println(compare(1.1, 1.2)) //         -1
```

## 并发

### 启动并发任务

V 的并发模型与 Go 非常相似。
目前，`spawn foo()` 会在不同线程中并发地运行 `foo()`：

```v
import math

fn p(a f64, b f64) { // 普通函数，无返回值
	c := math.sqrt(a * a + b * b)
	println(c)
}

fn main() {
	spawn p(3, 4)
	// p 将在并行线程中运行
	// 也可以写成以下形式
	// spawn fn (a f64, b f64) {
	// 	c := math.sqrt(a * a + b * b)
	// 	println(c)
	// }(3, 4)
}
```

> **注意**
> 线程依赖于计算机的 CPU（核心/线程数）。
> 请注意，使用 `spawn` 生成的 OS 线程在并发性方面有一些限制，
> 包括资源开销和可扩展性问题，可能会影响在高线程计数情况下的性能。

还有一个 `go` 关键字。目前，`go foo()` 会被 `vfmt` 自动重命名为 `spawn foo()`，并且将会有一种方法可以使用 `go` 启动一个协程（由运行时管理的轻量级线程）。

有时需要等待一个并行线程完成。这可以通过为启动的线程分配一个 *句柄*，然后稍后对该句柄调用 `wait()` 方法来实现：

```v
import math

fn p(a f64, b f64) { // 普通函数，无返回值
	c := math.sqrt(a * a + b * b)
	println(c) // 输出 `5`
}

fn main() {
	h := spawn p(3, 4)
	// p() 在并行线程中运行
	h.wait()
	// p() 一定已经完成
}
```

这种方法还可用于从在并行线程中运行的函数中获取返回值。无需修改函数本身即可调用它以实现并发调用。

```v
import math { sqrt }

fn get_hypot(a f64, b f64) f64 { // 返回值的普通函数
	c := sqrt(a * a + b * b)
	return c
}

fn main() {
	g := spawn get_hypot(54.06, 2.08) // 生成线程并获得其句柄
	h1 := get_hypot(2.32, 16.74) // 在此处执行其他计算
	h2 := g.wait() // 获取生成线程的结果
	println('结果：${h1}, ${h2}') // 输出 `结果：16.9, 54.1`
}
```

如果存在大量的任务，可能会更容易使用线程数组来管理它们：

```v
import time

fn task(id int, duration int) {
	println('任务 ${id} 开始')
	time.sleep(duration * time.millisecond)
	println('任务 ${id} 结束')
}

fn main() {
	mut threads := []thread{}
	threads << spawn task(1, 500)
	threads << spawn task(2, 900)
	threads << spawn task(3, 100)
	threads.wait()
	println('完成')
}

// 输出：
// 任务 1 开始
// 任务 2 开始
// 任务 3 开始
// 任务 3 结束
// 任务 1 结束
// 任务 2 结束
// 完成
```

另外，对于返回相同类型的线程，调用线程数组的 `wait()`
将返回所有计算出的值。

```v
fn expensive_computing(i int) int {
	return i * i
}

fn main() {
	mut threads := []thread int{}
	for i in 1 .. 10 {
		threads << spawn expensive_computing(i)
	}
	// Join all tasks
	r := threads.wait()
	println('所有作业完成：${r}')
}

// 输出：所有作业完成：[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### 通道

通道是线程之间进行通信的首选方式。V 的通道基本上与 Go 中的通道相似。你可以将对象推入通道的一端，并从另一端弹出对象。通道可以是有缓冲的或无缓冲的，并且可以从多个通道中进行 `select`。

#### 语法和用法

通道的类型为 `chan objtype`。可以在声明中指定一个可选的缓冲区长度作为 `cap` 字段：

```v
ch := chan int{} // 无缓冲 - “同步”
ch2 := chan f64{cap: 100} // 缓冲区长度为 100
```

通道不必声明为 `mut`。缓冲区长度不是类型的一部分，而是个体通道对象的字段。通道可以像普通变量一样传递给线程：

```v
fn f(ch chan int) {
	// ...
}

fn main() {
	ch := chan int{}
	spawn f(ch)
	// ...
}
```

可以使用箭头运算符将对象推入通道。该运算符也可以用于从另一端弹出对象：

```v
// 创建带有缓冲区的通道，以便在缓冲区有空间时推送不会阻塞
ch := chan int{cap: 1}
ch2 := chan f64{cap: 1}
n := 5
// 推送
ch <- n
ch2 <- 7.3
mut y := f64(0.0)
m := <-ch // 弹出并创建新变量
y = <-ch2 // 弹出到现有变量
```

可以关闭通道以表示不再能够推送任何对象。任何尝试这样做的企图都将导致运行时 panic（除非是 `select` 和 `try_push()` - 参见下文）。尝试弹出将立即返回，如果关联通道已关闭并且缓冲区为空。可以使用 `or {}` 块来处理这种情况（参见[处理选项/结果](#handling-options

results)）。

```v wip
ch := chan int{}
ch2 := chan f64{}
// ...
ch.close()
// ...
m := <-ch or {
    println('通道已关闭')
}

// 传播错误
y := <-ch2 ?
```

#### 通道选择

`select` 命令允许同时监视多个通道，而不会产生明显的 CPU 负载。它由一组可能的传输和相关的语句分支组成 - 类似于 [match](#match) 命令：

```v
import time

fn main() {
	ch := chan f64{}
	ch2 := chan f64{}
	ch3 := chan f64{}
	mut b := 0.0
	c := 1.0
	// ... 设置生成的线程，它们将在 ch/ch2 上发送
	spawn fn (the_channel chan f64) {
		time.sleep(5 * time.millisecond)
		the_channel <- 1.0
	}(ch)
	spawn fn (the_channel chan f64) {
		time.sleep(1 * time.millisecond)
		the_channel <- 1.0
	}(ch2)
	spawn fn (the_channel chan f64) {
		_ := <-the_channel
	}(ch3)

	select {
		a := <-ch {
			// 使用 `a` 做一些事情
			eprintln('> a: ${a}')
		}
		b = <-ch2 {
			// 使用预先声明的变量 `b` 做一些事情
			eprintln('> b: ${b}')
		}
		ch3 <- c {
			// 如果发送了 `c`，则做一些事情
			time.sleep(5 * time.millisecond)
			eprintln('> c: ${c} 已在通道 ch3 上发送')
		}
		500 * time.millisecond {
			// 如果在 0.5s 内没有通道就绪，则做一些事情
			eprintln('> 超过 0.5s 而没有通道准备就绪')
		}
	}
	eprintln('> 完成')
}
```

超时分支是可选的。如果不存在，`select` 将等待无限长的时间。还可以通过添加 `else { ... }` 分支，在调用 `select` 时立即进行处理，如果此时没有通道准备就绪。`else` 和 `<timeout>` 是互斥的。

`select` 命令可以用作类型为 `bool` 的 *表达式*，如果所有通道都关闭，则返回 `false`：

```v wip
if select {
    ch <- a {
        // ...
    }
} {
    // 通道已打开
} else {
    // 通道已关闭
}
```

#### 特殊通道功能

对于特殊目的，有一些内建字段和方法：

```v
struct Abc {
	x int
}

a := 2.13
ch := chan f64{}
res := ch.try_push(a) // 尝试执行 `ch <- a`
println(res)
l := ch.len // 队列中的元素数
c := ch.cap // 最大队列长度
is_closed := ch.closed // 布尔标志 - 通道是否已关闭
println(l)
println(c)
mut b := Abc{}
ch2 := chan Abc{}
res2 := ch2.try_pop(mut b) // 尝试执行 `b = <-ch2`
```

`try_push/pop()` 方法将立即返回以下结果之一 `.success`、`.not_ready` 或 `.closed` - 取决于是否已传输对象或无法传输的原因。不建议在生产中使用这些方法和字段 - 基于它们的算法经常受到竞态条件的影响。特别是 `.len` 和 `.closed` 不应用于做出决策。请改用 `or` 分支、错误传播或 `select`（请参见[语法和用法](#syntax-and-usage)和[通道选择](#channel-select)）。

### 共享对象

数据可以通过共享变量在线程和调用线程之间进行交换。
这样的变量应该被创建为 `shared`，并且也应该作为 `shared` 传递给线程。
底层的 `struct` 包含了一个隐藏的 *互斥锁*，它允许使用 `rlock` 进行只读访问，使用 `lock` 进行读/写访问。

```v
struct St {
mut:
	x int // 要共享的数据
}

fn (shared b St) g() {
	lock b {
		// 读取/修改/写入 b.x
	}
}

fn main() {
	shared a := St{
		x: 10
	}
	spawn a.g()
	// ...
	rlock a {
		// 读取 a.x
	}
}
```

共享变量必须是结构体、数组或映射。

## JSON

由于 JSON 的普及性质质，V 对其提供了直接支持。

V 生成了用于 JSON 编码和解码的代码。
它不使用运行时反射，这使得性能更好。

### 解析 JSON

```v
import json

struct Foo {
	x int
}

struct User {
	// 添加 [required] 属性将在输入中缺少该字段时导致解码失败。
	// 如果字段不是 [required]，但缺少了，那么它将被假定为具有默认值，如数字为 0，字符串为 ''，
	// 并且解码不会失败。
	name string [required]
	age  int
	// 使用 `skip` 属性来跳过某些字段
	foo Foo [skip]
	// 如果 JSON 中的字段名不同，可以指定它
	last_name string [json: lastName]
}

data := '{ "name": "Frodo", "lastName": "Baggins", "age": 25 }'
user := json.decode(User, data) or {
	eprintln('解码 JSON 失败，错误：${err}')
	return
}
println(user.name)
println(user.last_name)
println(user.age)
// 也可以解码 JSON 数组：
sfoos := '[{"x":123},{"x":456}]'
foos := json.decode([]Foo, sfoos)!
println(foos[0].x)
println(foos[1].x)
```

`json.decode` 函数接受两个参数：
第一个是要解码为的 JSON 值的类型，第二个是包含 JSON 数据的字符串。

### 编码 JSON

```v
import json

struct User {
	name  string
	score i64
}

mut data := map[string]int{}
user := &User{
	name: 'Pierre'
	score: 1024
}

data['x'] = 42
data['y'] = 360

println(json.encode(data)) // {"x":42,"y":360}
println(json.encode(user)) // {"name":"Pierre","score":1024}
```

json 模块还支持匿名结构字段，这对于具有许多层级的复杂 JSON API 很有帮助。

## 测试

### 断言

```v
fn foo(mut v []int) {
	v[0] = 1
}

mut v := [20]
foo(mut v)
assert v[0] < 4
```

`assert` 语句用于检查其表达式是否评估为 `true`。如果断言失败，程序通常会中止。断言应该只用于检测编程错误。当断言失败时，会将其报告给 *stderr*，并在可能时打印比较运算符（如 `<`、`==`）两侧的值。这对于快速找到意外的值非常有用。断言语句可以用在任何函数中，而不仅仅是测试函数，这在开发新功能时非常方便，可以保持你的不变性。

> **注意**
> 当使用 `-prod` 标志编译程序时，所有 `assert` 语句都会被 *移除*。

### 带额外消息的断言

这种形式的 `assert` 语句在失败时会打印额外的消息。请注意，你可以在那里使用任何字符串表达式 - 字符串字面值、返回字符串的函数、插值变量的字符串等。

```v
fn test_assertion_with_extra_message_failure() {
	for i in 0 .. 100 {
		assert i * 2 - 45 < 75 + 10, '断言失败，i 的值为：${i}'
	}
}
```

### 不中止程序的断言

当最初原型化功能和测试时，有时候希望断言不会停止程序，而只是打印失败消息。可以通过给包含断言的函数添加 `[assert_continues]` 标签来实现，例如运行以下程序：

```v
[assert_continues]
fn abc(ii int) {
	assert ii == 2
}

for i in 0 .. 4 {
	abc(i)
}
```

... 将产生以下输出：

```
assert_continues_example.v:3: FAIL: fn main.abc: 断言失败，ii 的值为 0
   左侧值: ii = 0
   右侧值: 2
assert_continues_example.v:3: FAIL: fn main.abc: 断言失败，ii 的值为 1
  左侧值: ii = 1
  右侧值: 2
assert_continues_example.v:3: FAIL: fn main.abc: 断言失败，ii 的值为 3
  左侧值: ii = 3
  右侧值: 2
```

> **注意**
> V 也支持一个命令行标志 `-assert continues`，它将全局改变所有断言的行为，就好像你给每个函数都打上了 `[assert_continues]` 标签。

### 测试文件

```v
// hello.v
module main

fn hello() string {
	return 'Hello world'
}

fn main() {
	println(hello())
}
```

```v failcompile
// hello_test.v
module main

fn test_hello() {
	assert hello() == 'Hello world'
}
```

要运行上面的测试文件，请使用 `v hello_test.v`。这将检查函数 `hello` 是否产生了正确的输出。V 将执行文件中的所有测试函数。

> **注意**
> 所有 `_test.v` 文件（内部和外部都是如此）都将编译为*独立的程序*。换句话说，你可以拥有尽可能多的 `_test.v` 文件和其中的测试，它们不会对正常的 `.v` 文件的编译产生任何影响，只有当你明确地运行 `v file_test.v` 或 `v test .` 时才会运行。

* 所有测试函数必须位于文件名以 `_test.v` 结尾的测试文件中。
* 测试函数的名称必须以 `test_` 开头以标记它们以供执行。
* 正常的函数也可以在测试文件中定义，并且应该手动调用。其他符号也可以在测试文件中定义，如类型。
* 有两种类型的测试：内部和外部。
* 内部测试必须像来自同一模块的所有其他 .v 文件一样*声明*它们的模块。内部测试甚至可以调用同一模块中的私有函数。
* 外部测试必须*导入*它们要测试的模块。它们无法访问模块的私有函数/类型。它们只能测试模块提供的外部/公共 API。

在上面的示例中，`test_hello` 是一个内部测试，可以调用私有函数 `hello()`，因为 `hello_test.v` 具有 `module main`，就像 `hello.v` 一样，即它们都是同一个模块的一部分。还要注意，由于 `module main` 就像其他所有模块一样，内部测试也可以用于测试主程序 .v 文件中的私有函数。

你还可以在测试文件中定义以下特殊的测试函数：

* `testsuite_begin`，它将在所有其他测试函数*之前*运行。
* `testsuite_end`，它将在所有其他测试函数*之后*运行。

如果测试函数具有错误返回类型，则传播的任何错误将使测试失败：

```v
import strconv

fn test_atoi() ! {
	assert strconv.atoi('1')! == 1
	assert strconv.atoi('one')! == 1 // 测试将失败
}
```

### 运行测试

要运行单个测试文件中的测试函数，请使用 `v foo_test.v`。

要测试整个模块，请使用 `v test mymodule`。你也可以使用 `v test .` 来测试当前文件夹（及其子文件夹）中的所有内容。你可以传递 `-stats` 选项以查看有关单个测试运行的更多详细信息。

你可以将其他测试数据放在一个名为 `testdata` 的文件夹中，该文件夹与你的 `_test.v` 文件紧邻。V 的测试框架将*忽略*这样的文件夹，同时在寻找要运行的测试时进行扫描。这很有用，如果你想将具有无效 V 源代码或其他测试的 .v 文件放在一起，包括已知的失败测试，这些测试应该由父级 `_test.v` 文件以特定的方式/选项运行。

> **注意**
> V 编译器的路径可通过 @VEXE 获取，因此 `_test.v` 文件可以像这样轻松地运行*其他*测试文件：

```v oksyntax
import os

fn test_subtest() {
	res := os.execute('${os.quoted_path(@VEXE)} other_test.v')
	assert res.exit_code == 1
	assert res.output.contains('other_test.v does not exist')
}
```

## 内存管理

V通过使用值类型、字符串缓冲区以及推崇简单、不含抽象的代码风格来避免不必要的分配。

在V中，有四种内存管理方式。

默认情况下，V使用一个精简且性能良好的追踪垃圾收集器（GC）。

第二种方式是自动释放（autofree），可以通过 `-autofree` 开启。它负责大部分对象（约90-100%）：编译期间会自动插入必要的释放调用。剩余的小部分对象通过GC释放。开发者不需要在代码中做任何更改。“它只管用”，就像Python、Go或Java一样，只是这里没有繁重的垃圾回收追踪一切或昂贵的引用计数。

对于愿意拥有更低层次控制的开发者，可以选择使用 `-gc none` 进行手动内存管理。

Arena分配可以通过 `v -prealloc` 实现。

### 控制

你可以利用V的自动释放引擎，在自定义数据类型上定义一个 `free()` 方法：

```v
struct MyType {}

[unsafe]
fn (data &MyType) free() {
	// ...
}
```

就像编译器为C数据类型释放内存一样，它会在每个变量的生命周期结束时静态地插入 `free()` 调用。

可以通过使用 `-autofree` 标志来启用自动释放。

对于愿意拥有更低层次控制的开发者，可以使用 `-manualfree` 来禁用自动释放，或者在想要手动管理内存的每个函数上添加 `[manualfree]` 标签（参见 [attributes](#attributes)）。

> **注意**
> 目前，Autofree仍然处于开发中。在它稳定下来并成为默认设置之前，请避免使用它。目前，分配由一个精简而性能良好的GC处理，直到V的自动释放引擎准备投入生产使用。

**示例**

```v
import strings

fn draw_text(s string, x int, y int) {
	// ...
}

fn draw_scene() {
	// ...
	name1 := 'abc'
	name2 := 'def ghi'
	draw_text('hello ${name1}', 10, 10)
	draw_text('hello ${name2}', 100, 10)
	draw_text(strings.repeat(`X`, 10000), 10, 50)
	// ...
}
```

这里的字符串没有在 `draw_text` 中逃逸，因此它们在函数退出时被清理。

实际上，使用 `-prealloc` 标志，前两个调用根本不会导致任何分配。这两个字符串很小，所以V将为它们使用一个预分配的缓冲区。

```v
struct User {
	name string
}

fn test() []int {
	number := 7 // 栈变量
	user := User{} // 分配在栈上的结构体
	numbers := [1, 2, 3] // 分配在堆上的数组，在函数退出时会被释放
	println(number)
	println(user)
	println(numbers)
	numbers2 := [4, 5, 6] // 被返回的数组，在这里不会被释放
	return numbers2
}
```

### 栈和堆

#### 栈和堆基础知识

与大多数其他编程语言一样，数据可以存储在两个位置：

* 栈允许快速分配，几乎没有管理开销。栈随着函数调用深度的增加和减少而增长和缩小 - 因此每个调用的函数都有其保持有效的栈段，直到函数返回。不需要释放，但这也意味着对栈对象的引用在函数返回时将变为无效。此外，栈空间受限（通常每个线程只有几兆字节）。
* 堆是一个由操作系统管理的大内存区域（通常几十亿字节）。堆对象是由特殊的函数调用分配和释放的，这些函数将管理任务委托给操作系统。这意味着它们可以在几个函数调用之间保持有效，但管理是昂贵的。

#### V的默认方法

出于性能考虑，V会尽可能将对象放在栈上，但在明显需要时会将它们分配在堆上。例如：

```v
struct MyStruct {
	n int
}

struct RefStruct {
	r &MyStruct
}

fn main() {
	q, w := f()
	println('q: ${q.r.n}, w: ${w.n}')
}

fn f() (RefStruct, &MyStruct) {
	a := MyStruct{
		n: 1
	}
	b := MyStruct{
		n: 2
	}
	c := MyStruct{
		n: 3
	}
	e := RefStruct{
		r: &b
	}
	x := a.n + c.n
	println('x: ${x}')
	return e, &c
}
```

在这里，`a` 存储在栈上，因为它的地址永远不会离开函数 `f()`。然而，对 `b` 的引用是作为返回值的一部分包含在 `e` 中的。同时对 `c` 的引用也是返回的一部分。因此 `b` 和 `c` 将被分配在堆上。

当将对象的引用作为函数参数传递时，情况变得不那么明显：

```v
struct MyStruct {
mut:
	n int
}

fn main() {
	mut q := MyStruct{
		n: 7
	}
	w := MyStruct{
		n: 13
	}
	x := q.f(&w) // 传递了 `q` 和 `w` 的引用
	println('q: ${q}\nx: ${x}')
}

fn (mut a

 MyStruct) f(b &MyStruct) int {
	a.n += b.n
	x := a.n * b.n
	return x
}
```

在这里，调用 `q.f(&w)` 传递了对 `q` 和 `w` 的引用，因为 `a` 是 `mut` 而 `f()` 的声明中 `b` 的类型是 `&MyStruct`，所以从技术上讲，这些引用是离开 `main()` 的。然而，这些引用的 *生命周期* 位于 `main()` 的作用域内，所以 `q` 和 `w` 是在栈上分配的。

#### 栈和堆的手动控制

在最后一个示例中，V编译器可以将 `q` 和 `w` 放在栈上，因为它假设在调用 `q.f(&w)` 中，这些引用仅被用于读取和修改引用的值 - 而不是传递引用本身。从某种程度上来说，`q` 和 `w` 对 `f()` 只是 *借用* 了这些引用。

如果 `f()` 自己处理引用，情况会有所不同：

```v
struct RefStruct {
mut:
	r &MyStruct
}

// 参见下面的讨论
[heap]
struct MyStruct {
	n int
}

fn main() {
	m := MyStruct{}
	mut r := RefStruct{
		r: &m
	}
	r.g()
	println('r: ${r}')
}

fn (mut r RefStruct) g() {
	s := MyStruct{
		n: 7
	}
	r.f(&s) // 引用 `s` 在 `r` 中被传递回 `main()`
}

fn (mut r RefStruct) f(s &MyStruct) {
	r.r = s // 在没有 `[heap]` 的情况下会触发错误
}
```

在这里，`f()` 看起来很无害，但它却在做恶心的事情 - 它将对 `s` 的引用插入到 `r` 中。这样做的问题在于 `s` 的生存期仅在 `g()` 执行期间，但 `r` 在 `g()` 后面的 `main()` 中使用。因此编译器会对 `f()` 中的赋值发出警告，因为 `s` *“可能指的是存储在栈上的对象”*。在 `g()` 中所做的假设是错误的。

解决这个问题的方法是在 `struct MyStruct` 的声明中使用 `[heap]` [attribute](#attributes)。它指示编译器 *始终* 在堆上分配 `MyStruct` 对象。这样，对 `s` 的引用在 `g()` 返回后仍然有效。编译器在检查 `f()` 时会考虑到 `MyStruct` 对象始终在堆上分配，因此允许将引用赋给 `r.r` 字段。

在其他编程语言中经常看到的一种模式是：

```v failcompile
fn (mut a MyStruct) f() &MyStruct {
	// 对 `a` 做一些事情
	return &a // 将返回借用对象的地址
}
```

在这里，`f()` 作为接收者传递了对 `a` 的引用，该引用在调用者处返回并同时作为结果返回。这样声明的意图是方法链式调用，如 `y = x.f().g()`。然而，使用这种方法的问题在于会创建对 `a` 的第二个引用 - 因此不仅是借用的，而且必须将 `MyStruct` 声明为 `[heap]`。

在V中，更好的做法是：

```v
struct MyStruct {
mut:
	n int
}

fn (mut a MyStruct) f() {
	// 对 `a` 做一些事情
}

fn (mut a MyStruct) g() {
	// 对 `a` 做一些其他事情
}

fn main() {
	x := MyStruct{} // 分配在栈上
	mut y := x
	y.f()
	y.g()
	// 而不是 `mut y := x.f().g()
}
```

这样就可以避免使用 `[heap]` 属性，从而提升性能。

然而，栈空间非常有限，正如上面提到的。因此，即使对于像上面提到的用例一样，也可能适合对非常大的结构使用 `[heap]` 属性。

还有一种在特定情况下手动控制分配的替代方法。尽管不建议使用这种方法，但出于完整性的考虑

，这里显示出来：

```v
struct MyStruct {
	n int
}

struct RefStruct {
mut:
	r &MyStruct
}

// 简单的函数 - 只是用来覆盖先前由 `g()` 使用的栈段

fn use_stack() {
	x := 7.5
	y := 3.25
	z := x + y
	println('${x} ${y} ${z}')
}

fn main() {
	m := MyStruct{}
	mut r := RefStruct{
		r: &m
	}
	r.g()
	use_stack() // 以擦除无效的栈内容
	println('r: ${r}')
}

fn (mut r RefStruct) g() {
	s := &MyStruct{ // `s` 明确引用堆对象
		n: 7
	}
	// 将上面的 `&MyStruct` 改成 `MyStruct` 并将下面的 `r.f(s)` 改成 `r.f(&s)`
	// 可以看到栈段中的数据被覆写
	r.f(s)
}

fn (mut r RefStruct) f(s &MyStruct) {
	r.r = unsafe { s } // 覆盖编译器的检查
}
```

在这里，使用 `unsafe` 块抑制了编译器检查。即使编译器可能不需要这一步，但如果不这样做，`r` 中的引用将变得无效（指向的内存区域将被 `use_stack()` 覆写），程序可能会崩溃（或者至少产生一个不可预测的最终输出）。这就是这种方法被称为 *不安全* 的原因，应该避免使用它！

## ORM

（ORM功能仍处于Alpha状态）

V拥有一个内置的ORM（对象关系映射），支持SQLite、MySQL和Postgres，但很快将支持MS SQL和Oracle。

V的ORM提供了许多优点：

- 通用的SQL方言语法。（在不同数据库之间迁移变得更容易。）
- 使用V的语法构建查询。（无需学习另一种语法。）
- 安全性。（所有查询都会自动进行清理，以防止SQL注入。）
- 编译时检查。（防止只能在运行时捕获的拼写错误。）
- 可读性和简洁性。（无需手动解析查询结果，然后手动从解析结果构建对象。）

```v
import db.sqlite

// 设置自定义表名。默认为结构体名称（区分大小写）
[table: 'customers']
struct Customer {
	id        int    [primary; sql: serial] // 整数类型的名为`id`的字段必须是第一个字段
	name      string [nonull]
	nr_orders int
	country   string [nonull]
}

db := sqlite.connect('customers.db')!

// 你可以创建表格：
// CREATE TABLE IF NOT EXISTS `Customer` (
//      `id` INTEGER PRIMARY KEY,
//      `name` TEXT NOT NULL,
//      `nr_orders` INTEGER,
//      `country` TEXT NOT NULL
// )
sql db {
	create table Customer
}!

// 从customers中选择计数(*)
nr_customers := sql db {
	select count from Customer
}!
println('所有客户的数量：${nr_customers}')

// 可以使用V语法构建查询
uk_customers := sql db {
	select from Customer where country == 'uk' && nr_orders > 0
}!
println(uk_customers.len)
for customer in uk_customers {
	println('${customer.id} - ${customer.name}')
}

// 插入一个新客户
new_customer := Customer{
	name: 'Bob'
	nr_orders: 10
}
sql db {
	insert new_customer into Customer
}!
```

更多示例和文档，请参阅[vlib/orm](https://github.com/vlang/v/tree/master/vlib/orm)。

## 撰写文档

其工作方式与Go非常相似。非常简单：不需要为代码单独编写文档，
vdoc将从源代码中的文档字符串生成它。

每个函数/类型/常量的文档必须放在声明的前面：

```v
// clearall清除数组中的所有位
fn clearall() {
}
```

注释必须以定义的名称开头。

有时候一行不足以解释一个函数的作用，在这种情况下，注释应该使用单行注释延伸到文档化的函数：

```v
// copy_all通过其值递归复制数组的所有元素，
// 如果`dupes`为false，则在过程中将消除所有重复的值。
fn copy_all(dupes bool) {
	// ...
}
```

按照惯例，建议以*现在时*编写注释。

模块的概述必须放在模块名称后面的第一个注释中。

要生成文档，请使用vdoc，例如 `v doc net.http`。

### 文档注释中的换行

跨越多行的注释将使用空格合并在一起，除非：

- 该行为空
- 该行以 `.` 结尾（句子结尾）
- 该行由至少3个 `-`、`= `、`_`、`*`、`~`（水平分隔线）组成
- 该行以至少一个 `#` 后跟一个空格开始（标题）
- 该行以 `|` 开头并以 `|` 结尾（表格）
- 该行以 `- ` 开头（列表）

## 工具

### v fmt

你不需要担心代码格式或设置样式指南。`v fmt`会为你搞定：

```shell
v fmt file.v
```

建议设置编辑器，以便在每次保存时运行 `v fmt -w`。vfmt运行通常很快（<30毫秒）。

在推送代码之前，始终运行 `v fmt -w file.v`。

#### 在本地禁用格式化

要在代码块中禁用格式化，请使用 `// vfmt off` 和 `// vfmt on` 注释将其包装起来。

```bash
// 不受fmt影响
// vfmt off

... 这里是你的代码 ...

// vfmt on

// 受fmt影响
... 这里是你的代码 ...
```

### v shader

你可以在V图形应用程序中使用GPU着色器。你可以使用[带有注释的GLSL方言](https://github.com/vlang/v/blob/1d8ece7/examples/sokol/02_cubes_glsl/cube_glsl.glsl)编写你的着色器，并使用 `v shader` 将其编译为所有受支持的目标平台。

```shell
v shader /path/to/project/dir/or/file.v
```

目前，你需要在代码中使用着色器之前，[包含一个头文件并声明一个粘合函数](https://github.com/vlang/v/blob/c14c324/examples/sokol/02_cubes_glsl/cube_glsl.v#L43-L46)。

### 性能分析

V对于对程序进行性能分析有很好的支持：`v -profile profile.txt run file.v`。这将产生一个profile.txt文件，你可以随后对其进行分析。

生成的profile.txt文件将具有带有4列的行：
a) 函数被调用的次数
b) 一个函数总共花费了多少时间（以毫秒为单位）
c) 平均调用一个函数花费了多少时间（以纳秒为单位）
d) v函数的名称

你可以使用以下命令按列3（每个函数的平均时间）进行排序：
`sort -n -k3 profile.txt|tail`

你也可以使用秒表来显式地测量你的代码的部分：

```v
import time

fn main() {
	sw := time.new_stopwatch()
	println('Hello world')
	println('问候全世界花费时间：${sw.elapsed().nanoseconds()}ns')
}
```

## 包管理

一个V *模块* 是一个包含.v文件的单个文件夹。一个V *包* 可以包含一个或多个V模块。一个V *包* 应该在其顶层文件夹中有一个`v.mod`文件，描述了包的内容。

V包通常安装在`~/.vmodules`文件夹中。可以通过设置环境变量`VMODULES`来覆盖该位置。

### 包命令

你可以使用V前端来执行包操作，就像你可以用它来编译代码、格式化代码、审查代码等一样。

```powershell
v [package_command] [param]
```

其中包命令可以是以下之一：

```
   install           从VPM安装包。
   remove            删除从VPM安装的包。
   search            从VPM搜索包。
   update            从VPM更新已安装的包。
   upgrade           升级所有过时的包。
   list              列出所有已安装的包。
   outdated          显示需要更新的已安装包。
```

你可以使用VPM安装已由其他人创建的包：

```powershell
v install [package]
```

**示例:**

```powershell
v install ui
```

包可以直接从git或mercurial仓库安装。

```powershell
v install [--once] [--git|--hg] [url]
```

**示例:**

```powershell
v install --git https://github.com/vlang/markdown
```

有时，你可能只想在未安装这些包时才安装依赖项：

```
v install --once [package]
```

使用v删除一个包：

```powershell
v remove [package]
```

**示例:**

```powershell
v remove ui
```

从[VPM](https://vpm.vlang.io/)更新已安装的包：

```powershell
v update [package]
```

**示例:**

```powershell
v update ui
```

或者你可以更新所有你的包：

```powershell
v update
```

要查看你已安装的所有包，你可以使用：

```powershell
v list
```

**示例:**

```powershell
> v list
已安装的包:
  markdown
  ui
```

要查看所有需要更新的包：

```powershell
v outdated
```

**示例:**

```powershell
> v outdated
包已是最新的。
```

### 发布包

1. 在你的包的顶层文件夹中放置一个`v.mod`文件（如果你用命令`v new mypackage`或`v init`创建了你的包，你已经有了一个`v.mod`文件）。

   ```sh
   v new mypackage
   输入你的项目描述: 我的优秀包。
   输入你的项目版本: (0.0.0) 0.0.1
   输入你的项目许可证: (MIT)
   初始化 ...
   完成!
   ````

   示例 `v.mod`：

   ```v ignore
   Module {
       name: 'mypackage'
       description: '我的优秀包。'
       version: '0.0.1'
       license: 'MIT'
       dependencies: []
   }
   ```

   最小的文件结构：

   ```
   v.mod
   mypackage.v
   ```

   你的包的名称应该与`mypackage.v`中的`module`指令一起使用。

2. 在带有`v.mod`文件的文件夹中创建一个git存储库（如果你使用了`v new`或`v init`，则不需要此步骤）：

   ```sh
   git init
   git add .
   git commit -m "INIT"
   ````

3. 在github.com上创建一个公共存储库。

4. 将本地存储库连接到远程存储库并推送更改。

5. 将你的包添加到公共V包注册表VPM：
   https://vpm.vlang.io/new

   你需要使用你的Github账号登录才能注册包。
   **警告：** _目前无法在提交后编辑你的条目。请仔细检查你的包名和github url，因为你以后无法更改它们。_

6. 最终包名是你的github账号和你提供的包名的组合，例如`mygithubname.mypackage`。

**可选的：** 在github.com上使用 `vlang` 和 `vlang-package` 标记你的V包，以提供更好的搜索体验。

# 高级主题（Advanced Topics）

## 属性

V语言具有几个属性，可以修改函数和结构体的行为。

属性是指定在函数/结构体/枚举声明之前的`[]`内的编译器指令，仅适用于后续的声明。

```v
// [flag] 启用枚举类型作为位字段使用

[flag]
enum BitField {
	read
	write
	other
}

fn main() {
	assert 1 == int(BitField.read)
	assert 2 == int(BitField.write)
	mut bf := BitField.read
	assert bf.has(.read | .other) // 测试是否设置了*至少一个*标志
	assert !bf.all(.read | .other) // 测试是否所有标志都已设置
	bf.set(.write | .other)
	assert bf.has(.read | .write | .other)
	assert bf.all(.read | .write | .other)
	bf.toggle(.other)
	assert bf == BitField.read | .write
	assert bf.all(.read | .write)
	assert !bf.has(.other)
}
```

结构体字段的弃用：

```v oksyntax
module abc

// 请注意，仅在*其他模块*中对Xyz.d的*直接*访问，将产生弃用通知/警告：
pub struct Xyz {
pub mut:
	a int
	d int [deprecated: '请使用Xyz.a代替'; deprecated_after: '2999-03-01']
	// 上述标签，将产生一个通知，因为弃用日期在遥远的未来
}
```

函数/方法的弃用：

```v
// 调用此函数将导致弃用警告

[deprecated]
fn old_function() {
}

// 还可以显示自定义的弃用消息

[deprecated: '请使用new_function()代替']
fn legacy_function() {}

// 你还可以指定一个日期，在此日期之后，将视该函数为已弃用。在此日期之前，对函数的调用将是编译器通知 - 你会看到它们，但不会影响编译。在此日期之后，调用将成为警告，因此使用普通编译仍将正常工作，但使用 -prod 编译将不会（所有警告都像错误一样处理）。
// 弃用日期后的6个月，调用将成为严格的编译器错误。

[deprecated: '请使用new_function2()代替']
[deprecated_after: '2021-05-27']
fn legacy_function2() {}
```

```v nofmt
// 此函数的调用将被内联。
[inline]
fn inlined_function() {
}

// 此函数的调用将不会被内联。
[noinline]
fn function() {
}

// 此函数将不会返回给其调用者。
// 这样的函数可以在代码块的末尾使用，就像 exit/1 或 panic/1 一样。此类函数不能具有返回类型，并且应该以 for{} 结束，或者通过调用其他 `[noreturn]` 函数来结束。
[noreturn]
fn forever() {
	for {}
}

// 必须在 `unsafe {}` 块中调用以下函数。
// 请注意，`risky_business()` 中的代码仍将被检查，除非你也将其包装在 `unsafe {}` 块中。
// 这在你想要在某些不安全操作之前/之后具有检查的 `[unsafe]` 函数时非常有用，但仍将受益于V的安全功能。

[unsafe]
fn risky_business() {
	// 将要检查的代码，也许检查前提条件
	unsafe {
		// 不会被检查的代码，例如指针算术，访问联合字段，调用其他 `[unsafe]` 函数等...
		通常情况下，将代码包装在 `unsafe{}` 中是一个很好的做法。
		另请参见 [Memory-unsafe code](#memory-unsafe-code)。
	}
	// 将要检查的代码，也许检查后提条件和/或保持不变量
}

// V的自动释放引擎将不会在此函数中处理内存管理。
// 你将负责在此函数中手动释放内存。
[manualfree]
fn custom_allocations() {
}

// 仅用于C互操作，告诉V以下结构体在C中用 `typedef struct` 定义
[typedef]
struct C.Foo {
}

// 用于向函数添加自定义调用约定，可用调用约定：stdcall、fastcall 和 cdecl。
// 此列表也适用于类型别名（见下文）。
[callconv: "stdcall"]
fn C.DefWindowProc(hwnd int, msg int, lparam int, wparam int)

// 用于向函数类型别名添加自定义调用约定。
[callconv: "fastcall"]
type FastFn = fn (int) bool

// 仅在Windows上：
// 如果没有此属性，所有图形应用程序在Windows上都将具有以下行为：
// 如果从控制台或终端运行；保持终端打开以便查看所有 (e)println 语句。
// 如果从Explorer等启动；打开应用程序，但不会打开终端，也不会看到 (e)println 输出。
// 用于强制打开一个终端以查看输出

，即使是从Explorer启动的应用程序也是如此。
// 仅在 main() 之前有效。
[console]
fn main() {
}
```

## 条件编译

### 编译时伪变量

V还为您的代码提供了一组伪字符串变量，它们在编译时替换为实际的值：

- `@FN` => 替换为当前V函数的名称
- `@METHOD` => 替换为ReceiverType.MethodName
- `@MOD` => 替换为当前V模块的名称
- `@STRUCT` => 替换为当前V结构体的名称
- `@FILE` => 替换为V源文件的绝对路径
- `@LINE` => 替换为出现它的V行号（作为字符串）。
- `@FILE_LINE` => 像 `@FILE:@LINE` 一样，但文件部分是相对路径
- `@COLUMN` => 替换为出现它的列号（作为字符串）。
- `@VEXE` => 替换为V编译器的路径
- `@VEXEROOT`  => 将被替换为包含V可执行文件的*文件夹*（作为字符串）。
- `@VHASH`  => 替换为V编译器的缩短提交哈希（作为字符串）。
- `@VMOD_FILE` => 替换为最近的v.mod文件的内容（作为字符串）。
- `@VMODROOT` => 将被替换为最近的v.mod文件所在的*文件夹*（作为字符串）。

这允许你在调试/记录/跟踪代码时执行以下示例：

```v
eprintln('file: ' + @FILE + ' | line: ' + @LINE + ' | fn: ' + @MOD + '.' + @FN)
```

另一个例子是，如果你想将v.mod中的版本/名称嵌入到你的可执行文件中：

```v ignore
import v.vmod
vm := vmod.decode( @VMOD_FILE ) or { panic(err) }
eprintln('${vm.name} ${vm.version}\n ${vm.description}')
```

### 编译时反射

`$` 用作编译时（也称为“comptime”）操作的前缀。

内置JSON支持非常好，但V还允许你为任何数据格式创建高效的序列化程序。V具有编译时的 `if` 和 `for` 结构：

```v
struct User {
	name string
	age  int
}

fn main() {
	$for field in User.fields {
		$if field.typ is string {
			println('${field.name} 是字符串类型')
		}
	}
}

// 输出：
// name 是字符串类型
```

有关更完整的示例，请参阅[`examples/compiletime/reflection.v`](/examples/compiletime/reflection.v)。

#### `$if` 条件

```v
fn main() {
	// 支持在一个分支中有多个条件
	$if ios || android {
		println('在移动设备上运行！')
	}
	$if linux && x64 {
		println('64位 Linux。')
	}
	// 用作表达式的用法
	os := $if windows { 'Windows' } $else { 'UNIX' }
	println('使用 ${os}')
	// $else-$if 分支
	$if tinyc {
		println('tinyc')
	} $else $if clang {
		println('clang')
	} $else $if gcc {
		println('gcc')
	} $else {
		println('不同的编译器')
	}
	$if test {
		println('测试中')
	}
	// v -cg ...
	$if debug {
		println('调试中')
	}
	// v -prod ...
	$if prod {
		println('生产构建')
	}
	// v -d 选项 ...
	$if option ? {
		println('自定义选项')
	}
}
```

如果要在编译时评估`if`条件，必须在前面加上`$`符号。
目前它可以用于检测操作系统、编译器、平台或编译选项。
`$if debug`是一个特殊选项，就像`$if windows`或`$if x32`一样，它在程序使用`v -g`或`v -cg`编译时启用。
如果你使用了自定义的`#ifdef`，那么你确实需要`$if option ? {}`，并使用`v -d option`进行编译。
内置选项的完整列表如下：

| 操作系统                       | 编译器           | 平台                          | 其他                                  |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------- |
| `windows`, `linux`, `macos`    | `gcc`, `tinyc`   | `amd64`, `arm64`, `aarch64`   | `debug`, `prod`, `test`               |
| `mac`, `darwin`, `ios`,        | `clang`, `mingw` | `i386`, `arm32`               | `js`, `glibc`, `prealloc`             |
| `android`, `mach`, `dragonfly` | `msvc`           | `x64`, `x32`                  | `no_bounds_checking`, `freestanding`  |
| `gnu`, `hpux`, `haiku`, `qnx`  | `cplusplus`      | `little_endian`, `big_endian` | `no_segfault_handler`, `no_backtrace` |
| `solaris`, `termux`            |                  |                               | `no_main`                             |

#### `$embed_file`

```v ignore
import os
fn main() {
	embedded_file := $embed_file('v.png')
	os.write_file('exported.png', embedded_file.to_string())!
}
```

V可以使用`$embed_file(<path>)`编译时调用将任意文件嵌入可执行文件中。路径可以是相对于源文件的绝对路径或相对路径。

当你不使用`-prod`时，文件将不会被嵌入。相反，它将在程序首次在运行时调用`embedded_file.data()`时在运行时加载，这样你就可以更容易地在外部编辑器中进行更改，而无需重新编译可执行文件。

当你使用`-prod`编译时，文件将*被嵌入到*可执行文件中，增加了二进制文件的大小，但使其更自包含，因此更容易分发。在这种情况下，`embedded_file.data()`将不会进行*任何IO*，它将始终返回相同的数据。

`$embed_file`在使用`-prod`编译时支持对嵌入文件进行压缩。目前仅支持一种压缩类型：`zlib`。

```v ignore
import os
fn main() {
	embedded_file := $embed_file('v.png', .zlib) // 使用zlib压缩
	os.write_file('exported.png', embedded_file.to_string())!
}
```

`$embed_file`返回一个名为[EmbedFileData](https://modules.vlang.io/v.embed_file.html#EmbedFileData)的对象，可以用于以`string`或`[]u8`的形式获取文件内容。

#### `$tmpl` 用于嵌入和解析V模板文件

V拥有一个简单的模板语言，可以用于文本和HTML模板，并且可以通过`$tmpl('path/to/template.txt')`轻松地进行嵌入：

```v ignore
fn build() string {
	name := 'Peter'
	age := 25
	numbers := [1, 2, 3]
	return $tmpl('1.txt')
}

fn main() {
	println(build())
}
```

1.txt:

```
name: @name

age: @age

numbers: @numbers

@for number in numbers
  @number
@end
```

输出:

```
name: Peter

age: 25

numbers: [1, 2, 3]

1
2
3
```

了解更多详细信息 [details](https://github.com/vlang/v/blob/master/vlib/v/TEMPLATES.md)

#### `$env`

```v
module main

fn main() {
	compile_time_env := $env('ENV_VAR')
	println(compile_time_env)
}
```

V可以从环境变量中在编译时获取值。
`$env('ENV_VAR')`也可以用于顶层的`#flag`和`#include`语句：
`#flag linux -I $env('JAVA_HOME')/include`。

#### `$compile_error` 和 `$compile_warn`

这两个编译时函数在编译时显示自定义错误/警告非

常有用。

两者的唯一参数都是包含要显示的消息的字符串文字：

```v failcompile nofmt
// x.v
module main

$if linux {
    $compile_error('Linux is not supported')
}

fn main() {
}

$ v run x.v
x.v:4:5: error: Linux is not supported
    2 |
    3 | $if linux {
    4 |     $compile_error('Linux is not supported')
      |     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    5 | }
    6 |
```

### 编译时类型

编译时类型将多个类型组合成一个更高级的通用类型。这在具有通用参数的函数中很有用，其中输入类型必须具有特定属性，例如数组中的`.len`属性。

V支持以下编译时类型：

- `$alias` => 匹配[类型别名](#类型别名)。
- `$array` => 匹配[数组](#数组)和[固定大小数组](#固定大小数组)。
- `$enum` => 匹配[枚举](#枚举)。
- `$float` => 匹配`f32`、`f64`和浮点字面值。
- `$function` => 匹配[函数类型](#函数类型)。
- `$int` => 匹配`int`、`i8`、`i16`、`i32`、`i64`、`u8`、`u16`、`u32`、`u64`、`isize`、`usize`和整数字面值。
- `$interface` => 匹配[接口](#接口)。
- `$map` => 匹配[映射](#映射)。
- `$option` => 匹配[Option类型](#optionresult类型和错误处理)。
- `$struct` => 匹配[结构体](#结构体)。
- `$sumtype` => 匹配[求和类型](#求和类型)。

### 特定环境的文件

如果文件具有特定于环境的后缀，它将仅在该环境中进行编译。

- `.js.v` => 仅由JS后端使用。这些文件可以包含JS代码。
- `.c.v` => 仅由C后端使用。这些文件可以包含C代码。
- `.native.v` => 仅由V的本机后端使用。
- `_nix.c.v` => 仅在Unix系统（非Windows）上使用。
- `_${os}.c.v` => 仅在特定`os`系统上使用。例如，`_windows.c.v`仅在Windows上编译时使用，或者使用`-os windows`。
- `_default.c.v` => 仅当没有更特定的平台文件时使用。例如，如果同时存在`file_linux.c.v`和`file_default.c.v`，并且你正在为linux编译，那么只会使用`file_linux.c.v`，并且将忽略`file_default.c.v`。

以下是一个更完整的示例：
main.v:

```v ignore
module main
fn main() { println(message) }
```

main_default.c.v:

```v ignore
module main
const ( message = 'Hello world' )
```

main_linux.c.v:

```v ignore
module main
const ( message = 'Hello linux' )
```

main_windows.c.v:

```v ignore
module main
const ( message = 'Hello windows' )
```

在上面的示例中：

- 当你为Windows编译时，你将得到'Hello windows'

- 当你为linux编译时，你将得到'Hello linux'

- 当你为任何其他平台编译时，你将得到不特定的'Hello world'消息。

- `_d_customflag.v` => 仅当你向V传递`-d customflag`时才会使用。这对应于`$if customflag ? {}`，但适用于整个文件，而不仅仅是一个单独的块。`customflag`应该是一个蛇形命名的标识符，不能包含任意字符（只能是小写拉丁字母+数字+`_`）。

  > **注意**

> 组合 `_d_customflag_linux.c.v` 后缀将不起作用。
> 如果你确实需要一个包含平台相关代码的自定义标志文件，请使用后缀 `_d_customflag.v`，然后在其中使用平台相关的编译时条件块，例如 `$if linux {}` 等。

- `_notd_customflag.v` => 类似于 _d_customflag.v，但仅在你未传递 `-d customflag` 给 V 时使用。

另请参阅 [交叉编译](#交叉编译)。

## 内存不安全的代码

有时为了效率，您可能希望编写可能会损坏内存或容易受到安全漏洞影响的底层代码。V 支持编写此类代码，但默认情况下不允许。

V 要求将任何可能不安全的内存操作标记为有意的。将它们标记也会向阅读代码的任何人指出，如果出现错误，可能会存在内存安全性问题。

可能不安全的操作示例包括：

- 指针算术
- 指针索引
- 从不兼容类型转换为指针
- 调用某些 C 函数，例如 `free`、`strlen` 和 `strncmp`。

要标记可能不安全的操作，请将它们放在 `unsafe` 块中：

```v
// 分配 2 个未初始化的字节并返回对它们的引用
mut p := unsafe { malloc(2) }
p[0] = `h` // 错误：只允许在 `unsafe` 块中进行指针索引
unsafe {
    p[0] = `h` // 正确
    p[1] = `i`
}
p++ // 错误：只允许在 `unsafe` 块中进行指针算术
unsafe {
    p++ // 正确
}
assert *p == `i`
```

最佳实践是避免将内存安全表达式放在 `unsafe` 块内，以便尽可能清晰地说明使用 `unsafe` 的原因。通常，任何您认为是内存安全的代码都不应该在 `unsafe` 块内，以便编译器可以验证它。

如果您怀疑程序违反了内存安全性，您可以提前找到原因：查看 `unsafe` 块（以及它们与周围代码的交互方式）。

> **注意**
> 这是一个正在进行的工作。

## 具有引用字段的结构体

具有引用的结构体需要显式将初始值设置为引用值，除非结构体已经定义了自己的初始值。

零值引用，或者说空指针，在未来将**不会**得到支持，目前依然可以使用值 `0` 的数据结构，例如依赖于引用字段的链表或二叉树，但需要了解它是不安全的，并且可能会导致 panic。

```v
struct Node {
	a &Node
	b &Node = unsafe { nil } // 自动初始化为 nil，谨慎使用！
}

// 引用字段必须初始化，除非声明了初始值。
// 零值 (0) 是可以的，但是要谨慎使用，它是一个空指针。
foo := Node{
	a: 0
}
bar := Node{
	a: &foo
}
baz := Node{
	a: 0
	b: 0
}
qux := Node{
	a: &foo
	b: &bar
}
println(baz)
println(qux)
```

## sizeof 和 __offsetof

- `sizeof(Type)` 给出了类型的字节大小。
- `__offsetof(Struct, field_name)` 给出了结构体字段的偏移量（以字节为单位）。

```v
struct Foo {
	a int
	b int
}

assert sizeof(Foo) == 8
assert __offsetof(Foo, a) == 0
assert __offsetof(Foo, b) == 4
```

## 有限的运算符重载

运算符重载定义了某些类型的特定二元运算符的行为。

```v
struct Vec {
	x int
	y int
}

fn (a Vec) str() string {
	return '{${a.x}, ${a.y}}'
}

fn (a Vec) + (b Vec) Vec {
	return Vec{a.x + b.x, a.y + b.y}
}

fn (a Vec) - (b Vec) Vec {
	return Vec{a.x - b.x, a.y - b.y}
}

fn main() {
	a := Vec{2, 3}
	b := Vec{4, 5}
	mut c := Vec{1, 2}

	println(a + b) // "{6, 8}"
	println(a - b) // "{-2, -2}"
	c += a
	//^^ 自动生成自 + 重载
	println(c) // "{3, 5}"
}
```

> 运算符重载违反了 V 的简单和可预测性的哲学。
> 但由于科学和图形应用是 V 的领域之一，
> 运算符重载是一个重要的功能，以提高可读性：
>
> `a.add(b).add(c.mul(d))` 比 `a + b + c * d` 难以阅读得多。

可以对以下二元运算符进行运算符重载：`+，-，*，/，%，<，==`。

### 隐式生成的重载

- `==` 由编译器自动生成，但可以被覆盖。

- `!=`，`>`，`<=` 和 `>=` 在定义了 `==` 和 `<` 时会自动生成。
  它们不能被显式覆盖。
- 赋值运算符 (`*=`, `+=`, `/=`, 等) 在相应的运算符被定义且操作数具有相同类型时会自动生成。
  它们不能被显式覆盖。

### 限制

为了提高安全性和可维护性，运算符重载受到限制。

#### 类型限制

- 在覆盖 `<` 和 `==` 时，返回类型必须严格为 `bool`。
- 两个参数必须具有相同的类型（就像在 V 的所有运算符中一样）。

#### 其他限制

- 不允许在重载中更改参数。
- 在运算符函数内部调用其他函数是不允许的（**计划中**）。

## 性能调优



生成的 C 代码通常在使用 `-prod` 编译您的代码时足够快。然而，在某些情况下，您可能希望向编译器提供额外的提示，以便它可以进一步优化某些代码块。

> **注意**
> 这些通常是 *很少* 需要的，并且除非您*分析您的代码*，然后看到对它们存在重大好处，否则不应使用它们。
> 正如 gcc 的文档所说：“程序员在预测他们的程序实际执行时通常做得很糟糕”。

`[inline]` - 您可以将函数标记为 `[inline]`，以便 C 编译器尝试内联它们，这在某些情况下可能对性能有利，但可能会影响可执行文件的大小。

`[direct_array_access]` - 在标记为 `[direct_array_access]` 的函数中，编译器将直接将数组操作转换为 C 数组操作 - 省略边界检查。这可能会在函数中节省大量时间，但代价是使函数变得不安全 - 除非用户将检查边界。

`if _likely_(bool expression) {` 这向 C 编译器暗示传递的布尔表达式非常可能为 true，因此它可以生成具有较低的分支预测错误机会的汇编代码。在 JS 后端中，这什么也不做。

`if _unlikely_(bool expression) {` 类似于 `_likely_(x)`，但它暗示布尔表达式非常不可能为真。在 JS 后端中，这也什么也不做。

### 通过代码生成进行反射

### 内存使用优化

V 提供了与内存使用相关的以下属性，可应用于结构类型：`[packed]` 和 `[minify]`。这些属性会影响结构的内存布局，从而可能减少缓存/内存的使用，并提高性能。

#### `[packed]`

可以向结构添加 `[packed]` 属性，以创建一个不对齐的内存布局，从而减小结构的整体内存占用。

> **注意**
> 在某些 CPU 架构上，使用 [packed] 属性可能会对性能产生负面影响，甚至可能会受到禁止。
> 仅当最小化内存使用对您的程序至关重要并且您愿意牺牲性能时才使用此属性。

#### `[minify]`

可以向结构添加 `[minify]` 属性，允许编译器重新排列字段，以最小化内部间隔，同时保持对齐。

> **注意**
> 使用 `[minify]` 属性可能会导致二进制序列化或反射方面出现问题。
> 在使用此属性时，请注意这些潜在的副作用。

## 原子操作（Atomics）

V 没有对原子操作提供特殊的支持，但可以通过在 V 中调用 C 函数来将变量视为原子操作。
通常情况下，C11 标准的原子操作函数（如 `atomic_store()`）通常是使用宏和 C 编译器技巧来定义的，以提供一种*重载的 C 函数*。

由于 V 故意不支持函数重载，因此在名为 `atomic.h` 的 C 头文件中定义了这些包装函数，它们是 V 编译器基础设施的一部分。

针对所有无符号整数类型和指针都有专用的包装器。（在 Windows 上不完全支持 `u8`）- 函数名称包括类型名称作为后缀，例如 `C.atomic_load_ptr()` 或 `C.atomic_fetch_add_u64()`。

要使用这些函数，必须包含所使用操作系统的 C 头文件，并声明打算使用的函数。例如：

```v
$if windows {
	#include "@VEXEROOT/thirdparty/stdatomic/win/atomic.h"
} $else {
	#include "@VEXEROOT/thirdparty/stdatomic/nix/atomic.h"
}

// 声明我们想要使用的函数 - V 不解析 C 头文件
fn C.atomic_store_u32(&u32, u32)
fn C.atomic_load_u32(&u32) u32
fn C.atomic_compare_exchange_weak_u32(&u32, &u32, u32) bool
fn C.atomic_compare_exchange_strong_u32(&u32, &u32, u32) bool

const num_iterations = 10000000

// 请参见下面的“全局变量”部分
__global (
	atom u32 // 普通变量但用作原子变量
)

fn change() int {
	mut races_won_by_change := 0
	for {
		mut cmp := u32(17) // 可寻址的值，用于比较和存储找到的值
		// `if atom == 17 { atom = 23 races_won_by_change++ } else { cmp = atom }` 的原子版本
		if C.atomic_compare_exchange_strong_u32(&atom, &cmp, 23) {
			races_won_by_change++
		} else {
			if cmp == 31 {
				break
			}
			cmp = 17 // 重新分配，因为被 atom 的值覆盖了
		}
	}
	return races_won_by_change
}

fn main() {
	C.atomic_store_u32(&atom, 17)
	t := spawn change()
	mut races_won_by_main := 0
	mut cmp17 := u32(17)
	mut cmp23 := u32(23)
	for i in 0 .. num_iterations {
		// `if atom == 17 { atom = 23 races_won_by_main++ }` 的原子版本
		if C.atomic_compare_exchange_strong_u32(&atom, &cmp17, 23) {
			races_won_by_main++
		} else {
			cmp17 = 17
		}
		desir := if i == num_iterations - 1 { u32(31) } else { u32(17) }
		// `for atom != 23 {} atom = desir` 的原子版本
		for !C.atomic_compare_exchange_weak_u32(&atom, &cmp23, desir) {
			cmp23 = 23
		}
	}
	races_won_by_change := t.wait()
	atom_new := C.atomic_load_u32(&atom)
	println('atom: ${atom_new}, #exchanges: ${races_won_by_main + races_won_by_change}')
	// 打印 `atom: 31, #exchanges: 10000000`)
	println('races won by\n- `main()`: ${races_won_by_main}\n- `change()`: ${races_won_by_change}')
}
```

在此示例中，`main()` 和生成的线程 `change()` 都尝试用值 `17` 替换全局 `atom` 中的值为 `23`。反方向的替换也会做 10000000 次。最后一次替换将使用 `31` 完成，从而使生成的线程结束。

无法预测哪个线程会发生多少次替换，但总和将始终为 10000000。（使用注释中的非原子命令，该值将更高或程序将挂起 - 取决于所使用的编译器优化。）

## 全局变量

默认情况下，V 不允许全局变量。然而，在低级应用程序中，它们是有用的，因此可以通过编译器标志 `-enable-globals` 启用它们的使用。全局变量的声明必须用 `__global ( ... )` 包围，就像上面的例子中所示。

全局变量的初始化器必须明确转换为所需的目标类型。如果没有提供初始化器，则会执行默认初始化。某些对象（如信号量和互斥锁）需要在 *现场* 明确初始化，即不使用从函数调用返回的值，而是通过引用调用方法进行初始化。可以使用一个单独的 `init()` 函数来实现此目的 - 它将在 `main()` 之前调用：

```v
import sync

__global (
	sem   sync.Semaphore // 需要在 `init()` 中初始化
	mtx   sync.RwMutex   // 需要在 `init()` 中初始化
	f1    = f64(34.0625)  // 显式初始化
	shmap shared map[string]f64  // 作为空的 `shared` map 初始化
	f2    f64             // 初始化为 `0.0`
)

fn init() {
	sem.init(0)
	mtx.init()
}
```

请注意，在多线程应用程序中，对全局变量的访问受到竞态条件的影响。有几种方法可以处理这些问题：

- 对于变量声明，请使用 `shared` 类型并对访问使用 `lock` 块。对于较大的对象（如结构体、数组或映射）这是最合适的方法。
- 使用特殊的 C 函数（参见[上文](#原子)）将原始数据类型处理为“原子”。
- 使用显式同步原语（如互斥锁）来控制访问。在这种情况下，编译器无法真正帮助，因此你必须知道你在做什么。
- 不在乎 —— 这种方法是可能的，但仅在全局变量的确切值并不真的重要时才有意义。例如，`rand` 模块中就可以找到一个例子，其中全局变量用于生成（非密码学）伪随机数。在这种情况下，数据竞争导致不同线程中的随机数在某种程度上相互关联，考虑到使用同步原语会带来的性能惩罚，这是可以接受的。

## 交叉编译（Cross Compilation）

要进行交叉编译项目，只需运行以下命令：

```shell
v -os windows .
```

或者

```shell
v -os linux .
```

> **注意**
> 在Linux机器上进行交叉编译Windows二进制文件需要先安装用于MinGW-w64（面向Win64）的GNU C编译器。

对于基于Ubuntu/Debian的发行版：

```shell
sudo apt-get install gcc-mingw-w64-x86-64
```

对于基于Arch的发行版：

```shell
sudo pacman -S mingw-w64-gcc
```

（暂时无法进行macOS的交叉编译。）

如果你没有任何C依赖项，那么这就是你需要做的一切。这甚至适用于使用`ui`模块编译GUI应用程序或使用`gg`编译图形应用程序的情况。

你将需要安装Clang、LLD链接器，并下载一个包含Windows和Linux库文件以及包含文件的zip文件。V会提供给你一个链接。

## 调试（Debugging）

### C 后端二进制（默认）

要调试生成的二进制文件（标志：`-b c`），你可以传递以下标志：

- `-g` - 生成一个带有更多调试信息的优化程度较低的可执行文件。V会在panic时产生的堆栈跟踪中强制执行来自.v文件的行号。通常最好传递`-g`，除非你正在编写底层代码，此时请使用下一个选项`-cg`。
- `-cg` - 生成一个带有更多调试信息的优化程度较低的可执行文件。在这种情况下，可执行文件将使用C源代码的行号。它通常与`-keepc`一起使用，这样你可以在panic时检查生成的C程序，或者使你的调试器（`gdb`、`lldb`等）能够显示生成的C源代码。
- `-showcc` - 打印用于构建程序的C命令。
- `-show-c-output` - 打印在编译程序时你的C编译器产生的输出。
- `-keepc` - 在成功编译后不要删除生成的C源代码文件。也保持使用相同的文件路径，这样更稳定，更容易在编辑器/IDE中保持打开。

如果你正在为现有的C库编写一个底层的包装器，为了获得最佳的调试体验，你可以同时传递这些标志：`v -keepc -cg -showcc yourprogram.v`，然后只需在生成的可执行文件`yourprogram`上运行调试器（gdb/lldb）或IDE。

如果你只想检查生成的C代码，而不进行进一步的编译，你也可以使用`-o`标志（例如`-o file.c`）。这将使V生成`file.c`然后停止。

如果你想查看仅针对单个C函数（例如`main`）生成的C源代码，你可以使用：`-printfn main -o file.c`。

要调试V可执行文件本身，你需要从src中进行编译，使用 `./v -g -o v cmd/v`。

你可以使用例如 `v -g -keepc prog_test.v` 来调试测试。需要使用 `-keepc` 标志，以便在创建并运行可执行文件后，它不会被删除。

要查看V支持的所有标志的详细列表，请使用 `v help`，`v help build` 和 `v help build-c`。

**命令行调试**

1. 使用调试信息编译二进制文件 `v -g hello.v`
2. 使用 [lldb](https://lldb.llvm.org) 或 [GDB](https://www.gnu.org/software/gdb/) 进行调试，例如 `lldb hello`

[在GDB中调试由V创建的可执行文件时的故障排除（调试）](https://github.com/vlang/v/wiki/Troubleshooting-(debugging)-executables-created-with-V-in-GDB)

**可视化调试设置:**

* [Visual Studio Code](vscode.md)

### 本地后端二进制

目前，对于由本地后端生成的二进制文件（标志：`-b native`），不提供调试支持。

### JavaScript 后端

要调试生成的 JavaScript 输出，你可以激活源映射：
`v -b js -sourcemap hello.v -o hello.js`

查看所有支持的选项，请查看最新的帮助：
`v help build-js`

## V and C

### 从V调用C

**示例**

```v
#flag -lsqlite3
#include "sqlite3.h"
// 参见 https://www.sqlite.org/quickstart.html 中的示例
struct C.sqlite3 {
}

struct C.sqlite3_stmt {
}

type FnSqlite3Callback = fn (voidptr, int, &&char, &&char) int

fn C.sqlite3_open(&char, &&C.sqlite3) int

fn C.sqlite3_close(&C.sqlite3) int

fn C.sqlite3_column_int(stmt &C.sqlite3_stmt, n int) int

// ... 你也可以只定义参数的类型而省略C.前缀

fn C.sqlite3_prepare_v2(&C.sqlite3, &char, int, &&C.sqlite3_stmt, &&char) int

fn C.sqlite3_step(&C.sqlite3_stmt)

fn C.sqlite3_finalize(&C.sqlite3_stmt)

fn C.sqlite3_exec(db &C.sqlite3, sql &char, cb FnSqlite3Callback, cb_arg voidptr, emsg &&char) int

fn C.sqlite3_free(voidptr)

fn my_callback(arg voidptr, howmany int, cvalues &&char, cnames &&char) int {
	unsafe {
		for i in 0 .. howmany {
			print('| ${cstring_to_vstring(cnames[i])}: ${cstring_to_vstring(cvalues[i]):20} ')
		}
	}
	println('|')
	return 0
}

fn main() {
	db := &C.sqlite3(unsafe { nil }) // 这表示 `sqlite3* db = 0`
	// 将字符串文字传递给C函数调用将得到C字符串，而不是V字符串
	C.sqlite3_open(c'users.db', &db)
	// C.sqlite3_open(db_path.str, &db)
	query := 'select count(*) from users'
	stmt := &C.sqlite3_stmt(unsafe { nil })
	// 注意：你也可以使用V字符串的`.str`字段，
	// 以获取其C风格的零终止表示
	C.sqlite3_prepare_v2(db, &char(query.str), -1, &stmt, 0)
	C.sqlite3_step(stmt)
	nr_users := C.sqlite3_column_int(stmt, 0)
	C.sqlite3_finalize(stmt)
	println('数据库中有 ${nr_users} 个用户。')
	//
	error_msg := &char(0)
	query_all_users := 'select * from users'
	rc := C.sqlite3_exec(db, &char(query_all_users.str), my_callback, voidptr(7), &error_msg)
	if rc != C.SQLITE_OK {
		eprintln(unsafe { cstring_to_vstring(error_msg) })
		C.sqlite3_free(error_msg)
	}
	C.sqlite3_close(db)
}
```

### 从C调用V

由于V可以编译为C，所以调用V代码从C中非常容易，一旦你知道了如何做。

使用 `v -o file.c your_file.v` 生成一个对应于V代码的C文件。

更多详情参见 [call_v_from_c example](../examples/call_v_from_c)。

### 传递C编译flag

在V文件的顶部添加 `#flag` 指令以提供C编译标志，如：

- `-I` 用于添加C包含文件搜索路径
- `-l` 用于添加要链接的C库名称
- `-L` 用于添加C库文件搜索路径
- `-D` 用于设置编译时变量

你可以（可选地）为不同的目标使用不同的标志。
目前支持 `linux`, `darwin`, `freebsd`, 和 `windows` 标志。

> **注意**
> 每个标志必须单独占一行（暂时如此）

```v oksyntax
#flag linux -lsdl2
#flag linux -Ivig
#flag linux -DCIMGUI_DEFINE_ENUMS_AND_STRUCTS=1
#flag linux -DIMGUI_DISABLE_OBSOLETE_FUNCTIONS=1
#flag linux -DIMGUI_IMPL_API=
```

在控制台构建命令中，你可以使用：

- `-cc` 来更改默认的C后端编译器。
- `-cflags` 传递自定义标志给后端C编译器（在其他C选项之前传递）。
- `-ldflags` 传递自定义标志给后端C链接器（在其他C选项之后传递）。
- 例如：`-cc gcc-9 -cflags -fsanitize=thread`。

你可以在终端中定义一个 `VFLAGS` 环境变量来存储你的 `-cc` 和 `-cflags` 设置，而不是每次都在构建命令中包含它们。

### #pkgconfig

添加 `#pkgconfig` 指令用于告诉编译器应该使用哪些模块来进行编译和链接，使用相应依赖关系提供的 pkg-config 文件。

由于在 `#flag` 中不能使用反引号，并且出于安全和可移植性原因不希望生成进程，V使用了自己的pkgconfig库，它与标准的freedesktop库兼容。

如果没有传递标志，它将向 pkgconfig 添加 `--cflags` 和 `--libs` （而不是V）。
换句话说，下面的两行代码做的是一样的：

```v oksyntax
#pkgconfig r_core
#pkgconfig --cflags --libs r_core
```

会在一个硬编码的默认pkg-config路径列表中查找 `.pc` 文件，用户可以通过使用 `PKG_CONFIG_PATH` 环境变量添加额外的路径。可以传递多个模块。

要检查pkg-config是否存在，可以将 `$pkgconfig('pkg')` 作为一个编译时的“if”条件来使用，以检查pkg-config是否存在。如果存在，将创建分支。可以使用 `$else` 或 `$else $if` 来处理其他情况。

```v ignore
$if $pkgconfig('mysqlclient') {
	#pkgconfig mysqlclient
} $else $if $pkgconfig('mariadb') {
	#pkgconfig mariadb
}
```

### 包含C代码

你也可以直接在你的V模块中包含C代码。
例如，假设你的C代码位于模块文件夹内名为 'c' 的文件夹中。然后：

- 在你的模块顶层文件夹中

放置一个名为 `v.mod` 的文件（如果你用 `v new` 创建了你的模块，你已经有了 `v.mod` 文件）。例如：

```v ignore
Module {
	name: 'mymodule',
	description: '我的模块封装了一个简单的C库。',
	version: '0.0.1'
	dependencies: []
}
```

- 在你的模块顶部添加以下行：

```v oksyntax
#flag -I @VMODROOT/c
#flag @VMODROOT/c/implementation.o
#include "header.h"
```

> **注意**
> @VMODROOT 将被V替换为*最近的父文件夹，其中有一个 v.mod 文件*。
> 任何与v.mod文件所在的文件夹相邻或在其下面的.v文件，都可以使用 `#flag @VMODROOT/abc` 来引用此文件夹。
> @VMODROOT 文件夹也会被*添加到模块查找路径的前面*，因此你可以通过只命名它们来*导入*@VMODROOT下的其他模块。

以上的指令会让V在你的模块文件夹中查找一个已编译的 .o 文件。
如果V找到了它，那么该 .o 文件将会链接到使用该模块的主可执行文件中。
如果没有找到，V将假设存在一个 `@VMODROOT/c/implementation.c` 文件，并尝试将其编译成 .o 文件，然后将使用它。

这允许你在V模块中包含C代码，以便更容易地进行分发。
你可以在这里查看一个完整的使用C代码的V包装模块的最小示例：
[project_with_c_code](https://github.com/vlang/v/tree/master/vlib/v/tests/project_with_c_code)。
另一个示例演示了如何在C和V之间传递结构体：
[interoperate between C to V to C](https://github.com/vlang/v/tree/master/vlib/v/tests/project_with_c_code_2)。

### C类型

普通的零终止C字符串可以通过 `unsafe { &char(cstring).vstring() }` 或者如果你已经知道它们的长度可以用 `unsafe { &char(cstring).vstring_with_len(len) }` 转换为V字符串。

> **注意**
> `.vstring()` 和 `.vstring_with_len()` 方法并不会创建 `cstring` 的副本，所以在调用完 `.vstring()` 方法后不应该释放它。
> 如果你需要复制C字符串（一些libc API（如 `getenv`）几乎要求如此，因为它们返回指向内部libc内存的指针），可以使用 `cstring_to_vstring(cstring)`。

在Windows上，C API通常返回所谓的`wide`字符串（utf16编码）。可以使用 `string_from_wide(&u16(cwidestring))` 将其转换为V字符串。

V拥有以下类型，以便与C更轻松地进行交互：

- `voidptr` 用于C的 `void*`，
- `&u8` 用于C的 `byte*`，
- `&char` 用于C的 `char*`，
- `&&char` 用于C的 `char**`。

要将 `voidptr` 转换为V引用，请使用 `user := &User(user_void_ptr)`。

`voidptr` 也可以通过类型转换解引用为V结构体：`user := User(user_void_ptr)`。

[一个从V调用C代码的模块的示例](https://github.com/vlang/v/blob/master/vlib/v/tests/project_with_c_code/mod1/wrapper.v)

### C声明

C标识符可以通过与模块特定标识符类似的方式访问，函数必须在使用之前在V中重新声明。可以在C的 `C` 前缀后面使用任何C类型，但是必须在V中重新声明类型才能访问类型成员。

要重新声明复杂类型，例如以下C代码：

```c
struct SomeCStruct {
	uint8_t implTraits;
	uint16_t memPoolData;
	union {
		struct {
			void* data;
			size_t size;
		};

		DataView view;
	};
};
```

子数据结构的成员可以直接在包含结构中声明，如下所示：

```v
struct C.SomeCStruct {
	implTraits  u8
	memPoolData u16
	// 这些成员属于当前无法在V中完全表示的子数据结构。
	// 直接像这样声明它们就足以访问。
	// union {
	// struct {
	data voidptr
	size usize
	// }
	view C.DataView
	// }
}
```

数据成员的存在对V是已知的，可以在不重新创建原始结构的情况下使用它们。

或者，你可以[嵌入](#嵌入结构)子数据结构以保持并行代码结构。

### 导出到共享库

默认情况下，所有V函数在C中的命名方案如下：`[模块名]__[函数名]`。

例如，模块`bar`中的 `fn foo() {}` 将导致 `bar__foo()`。

要使用自定义导出名称，请使用 `[export]` 属性：

```v
[export: 'my_custom_c_name']
fn foo() {
}
```

### 将C转换为V

V可以将您的C代码转换为可读的V代码，并在C库之上生成V包装器。

C2V当前使用Clang的AST来生成V代码，因此要将C文件转换为V，你需要在你的机器上安装Clang。

让我们首先创建一个简单的程序 `test.c`：

```c
#include "stdio.h"

int main() {
	for (int i = 0; i < 10; i++) {
		printf("hello world\n");
	}
        return 0;
}
```

运行 `v translate test.c`，V将会生成 `test.v`：

```v
fn main() {
	for i := 0; i < 10; i++ {
		println('hello world')
	}
}
```

要在C库之上生成一个包装器，请使用以下命令：

```bash
v translate wrapper c_code/libsodium/src/libsodium
```

这将生成一个名为 `libsodium` 的目录，其中包含一个V模块。

一个由C2V生成的libsodium包装器的示例：

[https://github.com/vlang/libsodium](https://github.com/vlang/libsodium)

<br>

何时应该将C代码转换为V，何时应该只是从V调用C代码？

如果你有一个编写良好、经过良好测试的C代码，
那么当然你可以随时从V中调用这段C代码。

将其转换为V会给你带来几个优点：

- 如果你计划开发该代码库，现在你拥有了一个语言中的所有内容，这比C更安全且更容易开发。
- 交叉编译变得更容易。你完全不必担心它。
- 也不再需要构建标志和包含文件。

### 解决C问题

在某些情况下，C互操作可能非常困难。
其中之一是当头文件相互冲突时。
例如，V需要包含Windows头文件库，以便您的V二进制文件在所有平台上都能无缝地工作。

然而，由于Windows头文件库使用非常通用的名称（如`Rectangle`），
如果你希望使用C代码，而C代码也定义了一个名为`Rectangle`的名称，这将导致冲突。

对于这种非常特定的情况，我们有 `#preinclude`。

这将允许在V添加其内置库之前对事物进行配置。

示例用法：

```v ignore
// 这将在使用内置库之前包含。
#preinclude "pre_include.h"
// 这将在使用内置库后包含。
#include "include.h"
```

可能会包含在 `pre_include.h` 中的示例
可以在[这里找到](https://github.com/irish

greencitrus/raylib.v/blob/main/include/pre.h)。

这是一个高级功能，除非在C互操作的非常特定情况下，否则不会必要，
这可能会引起更多的问题而不是解决问题。

请将其视为最后的手段！

## V其它的功能

### 内联汇编

<!-- ignore because it doesn't pass fmt test (why?) -->

```v ignore
a := 100
b := 20
mut c := 0
asm amd64 {
    mov eax, a
    add eax, b
    mov c, eax
    ; =r (c) as c // 输出
    ; r (a) as a // 输入
      r (b) as b
}
println('a: ${a}') // 100
println('b: ${b}') // 20
println('c: ${c}') // 120
```

要获取更多示例，请参阅 [vlib/v/slow_tests/assembly/asm_test.amd64.v](https://github.com/vlang/v/tree/master/vlib/v/slow_tests/assembly/asm_test.amd64.v)。

### 代码热重载

```v live
module main

import time

[live]
fn print_message() {
	println('Hello! Modify this message while the program is running.')
}

fn main() {
	for {
		print_message()
		time.sleep(500 * time.millisecond)
	}
}
```

使用 `v -live message.v` 构建此示例。

您还可以使用 `v -live run message.v` 运行此示例。确保在命令中使用V的文件路径，**而不是**文件夹路径（如 `v -live run .`） - 在这种情况下，您需要修改文件夹的内容（例如添加新文件），因为对 *message.v* 的更改将不会产生任何效果。

您希望重新加载的函数必须在其定义之前带有 `[live]` 属性。

目前不能在程序运行时修改类型。

更多示例，包括一个图形应用程序：
[github.com/vlang/v/tree/master/examples/hot_reload](https://github.com/vlang/v/tree/master/examples/hot_reload)。

### 在V中编写跨平台Shell脚本

V可以用作编写部署脚本、构建脚本等的Bash的替代方案。

使用V进行这种操作的优势在于语言的简单性和可预测性，以及跨平台支持。 "V脚本" 可在类Unix系统以及Windows上运行。

要使用V的脚本模式，请将源文件保存为带有 `.vsh` 文件扩展名。这将使 `os` 模块中的所有函数成为全局函数（因此您可以使用 `mkdir()` 而不是 `os.mkdir()`，例如）。

V还知道立即编译并运行 `.vsh` 文件，因此您不需要单独的步骤来编译它们。V还会重新编译由 `.vsh` 文件生成的可执行文件，*仅当它比 .vsh 源文件旧时*，即第一次运行后，将更快，因为不需要重新编译未更改的脚本。

示例 `deploy.vsh`：

```v oksyntax
#!/usr/bin/env -S v

// 注意：上面的 shebang 行将 .vsh 文件与Unix类系统关联起来，
// 因此可以通过指定 .vsh 文件的路径来运行它，一旦将其设置为可执行（使用 `chmod +x deploy.vsh`），
// 就可以像这样输入其名称/路径： `./deploy.vsh`

// 打印命令然后执行它
fn sh(cmd string) {
	println('❯ ${cmd}')
	print(execute_or_exit(cmd).output)
}

// 如果 build/ 存在，则将其删除，如果不存在，则忽略任何错误
rmdir_all('build') or {}

// 创建 build/，由于 build/ 不存在，永远不会失败
mkdir('build')!

// 将 *.v 文件移动到 build/
result := execute('mv *.v build/')
if result.exit_code != 0 {
	println(result.output)
}

sh('ls')

// 类似于：
// files := ls('.')!
// mut count := 0
// if files.len > 0 {
//     for file in files {
//         if file.ends_with('.v') {
//              mv(file, 'build/') or {
//                  println('err: ${err}')
//                  return
//              }
//         }
//         count++
//     }
// }
// if count == 0 {
//     println('No files')
// }
```

现在，您可以像编译普通的V程序一样编译它，并获得一个可以在任何地方部署和运行的可执行文件：
`v deploy.vsh && ./deploy`

或者只是像传统的Bash脚本一样运行它：
`v run deploy.vsh`

在类Unix平台上，可以直接运行该文件，方法是使其可执行（使用 `chmod +x`）：
`./deploy.vsh`

### 没有扩展名的Vsh脚本

虽然V通常不允许没有指定文件扩展名的vsh脚本，但有一种方法可以绕过此规则并拥有具有完全自定义名称和shebang的文件。尽管存在此功能，但只建议用于特定用例，如将脚本放在路径中，并且不应用于诸如构建或部署脚本之类的情况。要访问此功能，请以 `#!/usr/bin/env -S v -raw-vsh-tmp-prefix tmp` 开头，其中 `tmp` 是内置可执行文件的前缀。这将以 crun 模式运行，因此仅在对脚本进行更改后才会重新构建

，并将二进制文件保留为 `tmp.<scriptfilename>`。**注意**：如果此文件名已存在，则将覆盖该文件。如果每次都要重新构建，而不是保留此二进制文件，请改用 `#!/usr/bin/env -S v -raw-vsh-tmp-prefix tmp run`。

# 附录

## 附录一：关键字

V语言有44个保留关键字（其中3个是字面量）：

```v ignore
as
asm
assert
atomic
break
const
continue
defer
else
enum
false
fn
for
go
goto
if
import
in
interface
is
isreftype
lock
match
module
mut
none
or
pub
return
rlock
select
shared
sizeof
spawn
static
struct
true
type
typeof
union
unsafe
volatile
__global
__offsetof
```

请参阅 [V 类型](#V 类型)。

## 附录二：运算符

这里只列出了针对[基本类型](#基本类型)的运算符。

```v ignore
+    sum                    integers, floats, strings
-    difference             integers, floats
*    product                integers, floats
/    quotient               integers, floats
%    remainder              integers

~    bitwise NOT            integers
&    bitwise AND            integers
|    bitwise OR             integers
^    bitwise XOR            integers

!    logical NOT            bools
&&   logical AND            bools
||   logical OR             bools
!=   logical XOR            bools

<<   left shift             integer << unsigned integer
>>   right shift            integer >> unsigned integer
>>>  unsigned right shift   integer >> unsigned integer


Precedence    Operator
    5            *  /  %  <<  >> >>> &
    4            +  -  |  ^
    3            ==  !=  <  <=  >  >=
    2            &&
    1            ||


Assignment Operators
+=   -=   *=   /=   %=
&=   |=   ^=
>>=  <<=  >>>=
```