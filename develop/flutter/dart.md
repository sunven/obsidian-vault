# dart

**late**

- 声明一个不可为 null 的变量，该变量在声明后进行初始化。
- 延迟初始化变量

```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

用途，场景：
- 该变量可能不需要，并且初始化它的成本很高。
- 您正在初始化一个实例变量，并且其初始值设定项需要访问`this`

```dart
// This is the program's only call to readThermometer().
// 如果`temperature`从未使用该变量，则`readThermometer()`永远不会调用昂贵的函数
late String temperature = readThermometer(); // Lazily initialized.
```

**final const**

- 最终变量只能设置一次
- const 变量是编译时常量
- 常量变量是隐式最终变量

实例变量可以是final但不是const
```dart
class P {
  // const c = 'c'; ❌
  final b = 1;
  static const String a = 'a';
}
```

不同：
- const 编译时确定值
- final 运行时确定值
- 使用范围
	- const 声明常量变量。创建常量值，以及声明创建常量值的构造函数
		- 常量构造函数：创建一个不变对象，所有成员变量都是 `final` 的
	- final 声明常量变量

```dart
var p1 = const Point(1, 2, p);
const p2 = Point(1, 2, p);
```

p1 p2 指向同一个对象

identical ==

== 操作符在比较对象时，会检查对象的 equals 方法（可以被重载），用于确定对象的"相等性"。
而 identical 仅仅检查对象引用的"同一性"。它只关心对象的引用