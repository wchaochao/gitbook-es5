# Function构造器

标签（空格分隔）： ES5

---

## 构造函数

### Function(p1, p2, … , pn, body)

作为函数使用，等同于作为构造器使用

### new Function(p1, p2, … , pn, body)

作为构造器使用，创建函数对象

```javascript
/**
 * 前n个参数转换为String类型，解析成FormalParameterList
 * 最后一个参数转换为String类型，解析成FunctionBody
 * 创建函数对象，形参为FormalParameterList，函数体为FunctionBody，作用域为全局作用域，严格模式为strict
 */
```

示例

```javascript
new Function() // FunctionBody = ''
new Function('return 1') // FunctionBody = 'return 1'
new Function('a', 'b', 'c', 'return a + b + c') // FormalParameterList = List{'a', 'b', 'c'}, FunctionBody = 'return a + b + c'
new Function('a, b, c', 'return a + b + c') // FormalParameterList = List{'a', 'b', 'c'}, FunctionBody = 'return a + b + c'
new Function('a, b', 'c', 'return a + b + c') // FormalParameterList = List{'a', 'b', 'c'}, FunctionBody = 'return a + b + c'
```

### 静态属性

```javascript
Function.[[Class]] = 'Function'
Function.[[Prototype]] = Function.Prototype
Function.[[Extensible]] = true

Function.[[DefineOwnProperty]]('length', {
  [[Value]]: 1,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
Function.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: Function,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

## 原型对象

Function对象的原型

```javascript
Function.prototype
fn.__proto__
fn.constructor.prototype
Object.getPrototypeOf(fn)
```

### 原型属性

```javascript
Function.prototype.[[Class]] = 'Function'
Function.prototype.[[Prototype]] = Object.prototype
Function.prototype.[[Extensible]] = true

Function.prototype.constructor = Function
Function.prototype.length = 0
```

### 原型方法

**转换方法**

#### Function.prototype.toString()

获取函数的字符串表示

```javascript
/**
 * this不为函数，抛出TypeError
 * this为函数，返回函数的源代码（与实现有关）
 */
if (!IsCallable(this)) {
  throw TypeError
} else {
  return this.SourceCode
}
```

示例

```javascript
Function.prototype.toString.call(undefined) // 抛出TypeError

function foo () {}
foo.toString() // 'function foo () {}'
```

**绑定方法**

#### Function.prototype.call(thisArg[ , arg1 [ , arg2, … ] ])

执行函数，并指定this和实参

```javascript
/**
 * this不为函数，抛出TypeError
 * this为函数，调用[[Call]]方法，thisArg为thisArg参数，argList为thisArg后面的参数
 */
```

示例

```javascript
Function.prototype.call.length // 1

Object.prototype.toString.call(undefined) // '[object Undefined]'
Array.prototype.slice.call('abc', 1) // ['b', 'c']
```

#### Function.prototype.apply(thisArg, argArray)

执行函数，并指定this和实参数组

```javascript
/**
 * this不为函数，抛出TypeError
 * this为函数，调用[[Call]]方法，thisArg为thisArg参数，argList由argArray决定
 *     argArray为undefined或null, argList为空List
 *     argArray不为Object类型, 抛出TypeError
 *     argArray为Object类型，argList由ToUint32(argArray.length)内的元素组成
 */
```

示例

```javascript
Function.prototype.apply.length // 2

Object.prototype.toString.apply(undefined) // '[object Undefined]'
Array.prototype.slice.apply('abc', 1) // 抛出TypeError
Array.prototype.slice.apply('abc', [1]) // ['b', 'c']
Array.prototype.slice.apply('abc', {0: 1, length: 1}) // ['b', 'c']

// 找出数组的最大元素，最小元素
let arr = [10, 2, 4, 15, 9]

let min = Math.min.apply(Math, arr)
let max = Math.max.apply(Math, arr)

// 将类数组对象转换为叔祖对象
function foo() {
  console.log(Array.prototype.slice.apply(arguments))
}
```

#### Function.prototype.bind(thisArg[, arg1 [, arg2, …]])

基于原函数指定this和实参，生成一个新函数

```javascript
/**
 * 创建新函数
 * [[Class]]属性为'Function'
 * [[Prototype]]属性为Function.prototype
 * [[Extensible]]属性为true
 * [[Target]]属性为原函数this，非函数抛出TypeError
 * [[BoundThis]]属性为thisArg参数
 * [[BoundArgs]]属性为thisArg后面的参数
 * length属性为Target的形参个数减已指定的实参个数，不小于0
 * 访问caller、arguments属性抛出TypeError
 * 调用[[Call]]方法相当于调用Target的[[Call]]方法，thisArg为BoundThis，argList为BoundArgs拼接传入的参数
 * 调用[[Constructor]]方法相当于调用Target的[[Constructor]]方法，argList为BoundArgs拼接传入的参数
 * 调用[[HasInstance]]方法相当于调用Target的[[HasInstance]]方法
 */
```

示例

```javascript
Function.prototype.bind.length // 1

function foo (a, b) {
  this.a = a
  this.b = b
  return a + b
}
let o = {}
let bar = foo.bind(o, 10)

// bar对象
{
  [[Class]]: 'Function',
  [[Prototype]]: Function.prototype,
  [[Extensible]]: true,
  [[Target]]: foo
  [[BoundThis]]: o,
  [[BoundArgs]]: List{10},
  length: 1,
  caller: thrower,
  arguments: thrower
}

bar(2) // 12
let b = new bar(2) // {a: 10, b: 2}
b instanceOf bar // true

// 与call结合
var slice = Function.prototype.call.bind(Array.prototype.slice);
slice([1, 2, 3], 0, 1); // [1]

function f() {
  console.log(this.v);
}

var o = { v: 123 };
var bind = Function.prototype.call.bind(Function.prototype.bind);
bind(f, o)(); // 123
```

示例

```javascript
// 与call结合
var slice = Function.prototype.call.bind(Array.prototype.slice);
slice([1, 2, 3], 0, 1); // [1]

function f() {
  console.log(this.v);
}

var o = { v: 123 };
var bind = Function.prototype.call.bind(Function.prototype.bind);
bind(f, o)(); // 123
```

## 实例对象

[[Class]]为Function的对象

```javascript
// 通过函数声明创建
function foo () {}

// 通过函数表达式创建
let foo = function foo () {}

// 通过构造器Function创建
new Function('a, b', 'return a + b')

// 通过Function.prototype.bind()创建
let bar = foo.bind({a: 1})
```

### 实例属性

```javascript
func.[[Class]] = 'Function'
func.[[Prototype]] = Function.prototype
func.[[Extensible]] = true

func.[[FormalParameters]] // 形参列表
func.[[Code]] // 函数体
func.[[Scope]] // 作用域

func.[[Target]] // 绑定的函数
func.[[BoundThis]] // 绑定的this值
func.[[BoundArgs]] // 绑定的实参

func.length // 形参个数
func.prototype // 原型对象
```

### 实例方法

```javascript
func.[[Call]] // 调用方法
func.[[Constructor]] // 构造方法
func.[[HasInstance]] // 判断实例
```
