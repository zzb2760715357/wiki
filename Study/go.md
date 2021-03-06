=Learning Go=

==介绍==
这本书主要介绍go这个革新(innovative)的语言。不是教你怎么去编程，而是教你怎样使用go。

学习最好的途径就是写自己的程序。

go语言是一门年轻的语言，特性还一直在添加，甚至被删除。

==获得GO==
# 首先安装mercurial
# export GOROOT=~/go
# hg clone -r release https:/go.googlecode.com/hg/ $GOROOT

```
    其实到googlecode下载tar包就好了。
```
===设置环境===
```
    ### go env ###
    export GOROOT=~/go	#set the GOROOT environment variable
    export GOOS=linux	#linux,darwin,freebad
    export GOARCH=amd64	#386,amd64
    export GOBIN=~/bin
    export PATH=$PATH:~/bin
```

==起源==
go可以追溯到plan9.plan9被认为是Unix的继任者。Unix的核心思想是：一切皆是文件，但是网络和图形设备不行。在Plan9中这个思想被升级而且真正实现一切皆是文件。Plan9中还包含一个语言叫做Limbo。

像Limdo一样，go可以很好的支持交叉编译和channels。

==hello world==
```
    package main
    import "fmt"
    func main() {
    	fmt.Printf("Hello, wordld!\n")
    }
```
* 首行是必须的。所有的go文件以package <something>开头，对于独立运行的执行文件必须是package main；
* 学要将fmt包加入main。不是main的其他包都被称为库。
* package main必须首先出现，紧跟着是import。在go中，package总是首先出现，然后是import，然后是其他所有内容。当go程序在执行的时候，首先调用的函数main.main()，这是从C中继承而来。

==变量==
go同其他语言不同的地方在于变量的类型在变量名的后面。不是int a，而是a int。声明和赋值是两过程，但是可以连在一起。
```
    var a int	|	a := 15
    var b bool	|	b := false
    a = 15	|
    b = false	|
```

右边的代码使用了:=使得在一步内完成了声明和赋值（这一形式只可用在函数内）。多个var声明可以成组：
```
    var (
    	x int
    	b bool
    )
    a, b := 20, 16
```

一个特殊的变量名是_，任何赋给它的值都被丢弃。将35赋给b，同时丢弃34。
```
    _, b := 34, 35
```

int型在32位机上32位的，在64位上是64的。所以这里：
```
    package main
    func main() {
     	var a int
    	var b int32
    	b = a + a
    }
```
b = a + a是违法的。

==常量==
常量在Go中，也就是constant。他们在编译时被创建，只能是数字、字符串或布尔值；const x = 42生成x这个常量。可以使用iota生成枚举值。
``` 
    const （
    	a = iota
    	b = iota
    )
```
第一个iota表示为0，因此a等于0，当iota再次在新的一行食用时，它的值增加了1，因此b的值是1。

也可以像下面这样省略Go重复iota：
```
    const （
    	a = iota
    	b	<--- implicitly b = iota
    )
```
