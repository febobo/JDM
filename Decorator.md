# 装饰者模式
在传统的面向对象语言中，给对象添加功能常常使用继承的方式，但是继承的方式并不灵活，下面我们列举两条
- 会导致超类与子类存在强耦合性，当超类改变时，子类也会随之改变
- 超类的内部细节对子类是可见的，继承常常被认为破坏了封装性

# 生活中装饰者
比如我们现在有4中型号的自行车，我们为每种自选车都定义了一单独的类，现在要给每种自行车都装上前灯，后灯，铃铛，如果使用继承的方式来给每种自行车创建子类，则需要4*3=12个子类，但是如果把前灯，后灯，铃铛动态组合到自行车上面，则只需要额外增加3个类
这种给对象动态的增加职责的方式称为装饰者（decorator）模式,装饰者模式能够在不改变对象自身的基础上，在程序运行期间给对象动态添加职责，跟继承想比，装饰者是一种更轻便灵活的做法

# 装饰函数
在javascript中，几乎一切对象，其中函数被称为一等对象，在平时开发式作中， 大部分时间都在和函数打交道，在javascript中可以很方便的某个对象扩展属性和方法，但却很难在不改动某个函数源代码的情况下，给该函数添加一些额外的功能，在代码的运行期间我们很难切入某个函数的运行环境

要想为函数添加一些功能，最简单的方式就是直接改写该函数，但这也是最差的方法，直接违反了开放－封闭原则
```
var a = function(){
  console.log(1)
}

// 改写成
var a = function(){
  console.log(1)
  console.log(2)
}
```
很多时间我们不想去改变原函数，因为我们不清楚自己的改动会为原函数带来什么样的后果，所以我们需要一个即不改变原函数，又能动态给函数添加职责的方法
```
var a = function(){
  console.log(1)
}
var _a = a;
a = function(){
  _a();
  console.log(2)
}
a()
```
我们保存原引用的方式就可以改写某个函数，这其实是开发中很常见的一种方式， 比如我们想很window.onload 添加一个事件，但是我们又不确定别人是否也绑定onload ，所以为了避免覆盖掉其它人写的，我们一般会先保存onload 的引用，把它放入到新的onload 里执行

这样的代码显示是符合开放－封闭原则的，但是这种方式还是有其它问题，如
- 必须维护中间变量（如上面的_a），虽然看起来不太起眼，但如果函数的装饰链较长，或者需要装饰的函数较多，这些中间变量也会越来越多
- this 莫名丢失