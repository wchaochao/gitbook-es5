# Error对象

标签（空格分隔）： ES5

---

类型为`Error`的对象

## 构造函数

```
语法：function Error(message: String[, fileName: String[, lineNumber: Number]]) {...}
解释：创建一个错误对象
参数：message - 错误信息，默认为空字符串
     fileName - 错误所在的文件名称，非标准
     lineNumber - 错误所在的文件行号，非标准
返回值：返回创建的错误对象

Error(message)等同于new Error(message)
```

### 子类

#### SyntaxError

语法错误

```javascript
// 变量名错误
var 1a; // Uncaught SyntaxError: Invalid or unexpected token

// 缺少括号
console.log 'hello'); // Uncaught SyntaxError: Unexpected string
```

#### ReferenceError

引用错误

```javascript
// 使用一个不存在的变量
unknownVariable // Uncaught ReferenceError: unknownVariable is not defined

// this 对象不能手动赋值
this = 1 // ReferenceError: Invalid left-hand side in assignment
```

#### RangeError

超出有效范围

```javascript
// 数组长度不得为负数
new Array(-1) // Uncaught RangeError: Invalid array length
```

#### TypeError

类型错误

```javascript
new 123 // Uncaught TypeError: number is not a function

var obj = {};
obj.unknownMethod() // Uncaught TypeError: obj.unknownMethod is not a function
```

#### URIError

URI函数错误

```javascript
decodeURI('%2') // URIError: URI malformed
```

#### EvalError

eval函数错误

#### 自定义错误类型

```javascript
function UserError(message) {
  this.message = message || '默认信息';
  this.name = 'UserError';
}

UserError.prototype = new Error();
UserError.prototype.constructor = UserError;

new UserError('这是自定义的错误！');
```

### 静态属性

* `length`:`1`, 可接受的参数个数
* `prototype`: `Error`实例对象的原型对象，是个`Object`对象
* `__proto__`: `Function.prototype`, 原型，非标准属性

## 原型对象

```
Error.prototype
err.__proto__
err.constructor.prototype
Object.getPrototypeOf(err)
```

### 原型属性

* `constructor`: `Error`, 构造函数
* `__proto__`: `Object.prototype`, 原型，非标准属性

### 原型方法

#### Error.prototype.toString()

```
语法：Error.prototype.toString()
解释：返回当前Error对象的字符串表示
返回值：一般返回this.name + ": " + this.message
```

profill

```javascript
Error.prototype.toString = function () {
  "use strict";

  var name = this.name;
  name = (name === undefined) ? "Error" : String(name);

  var msg = this.message;
  msg = (msg === undefined) ? "" : String(msg);

  return name + (name !== "" && msg !== "" ? ": " : "") + msg;
}
```

## 实例对象

### 创建

```javascript
// 构造函数法
var arr = new Error(message[, fileName[, lineNumber]]);
var arr = Error(message[, fileName[, lineNumber]]);
```

### 实例属性

* `__proto__`: `Error.prototype`, 原型，非标准属性
* `message`: 错误信息
* `name`: 错误名称, 非标准属性
* `stack`: 错误堆栈, 非标准属性
* `fileName`: 错误所在的文件名称, 非标准属性
* `lineNumber`: 错误所在的文件行号, 非标准属性
* `columnNumber`: 错误所在的文件列号, 非标准属性
