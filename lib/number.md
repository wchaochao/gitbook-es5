# Number构造器

标签（空格分隔）： ES5

---

## 构造函数

### Number([ value ])

作为函数使用，转换为Number类型

```javascript
/**
 * value未提供，返回+0
 * value已提供，转换为Boolean类型
 */
```

示例

```javascript
Number() // +0
Number(undefined) // NaN
Number(null) // +0
Number(true) // 1
Number(false) // +0
Number(' \n ') // 0
Number(' 0123.45 ') // 123.45
Number(' 0x12 ') // 18
Number({}) // NaN
Number([1]) // 1
```

### new Number([ value ])

作为构造器使用，创建Boolean对象

```javascript
/**
 * 创建Number对象
 * [[Class]]属性为'Number'
 * [[Prototype]]属性为Number.prototype
 * [[Extensible]]属性为true
 * [[PrimitiveValue]]属性为Number([value])
 */
```

示例

```javascript
new Number() // Number{+0}
new Number(undefined) // Number{NaN}
new Number(null) // Number{+0}
new Number(true) // Number{1}
new Number(false) // Number{+0}
new Number(' \n ') // Number{0}
new Number(' 0123.45 ') // Number{123.45}
new Number(' 0x12 ') // Number{18}
new Number({}) // Number{NaN}
new Number([1]) // Number{1}
```

### 静态属性

```javascript
Number.[[Class]] = 'Function'
Number.[[Prototype]] = Function.Prototype
Number.[[Extensible]] = true

Number.[[DefineOwnProperty]]('length', {
  [[Value]]: 1,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
Number.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: String,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

* `EPSILON`: 数字间的最小间隔
* `MAX_SAFE_INTEGER`: 2^53-1, 能够精确表示的最大整数
* `MIN_SAFE_INTEGER`: -2^53-1, 能够精确表示的最小整数
* `MAX_VALUE`: 能表示的最大的正数
* `MIN_VALUE`: 能表示的最小的正数
* `NAN`: 非数字
* `POSITIVE_INFINITY`: 正无穷大，大于`MAX_VALUE`的值会被转换为`POSITIVE_INFINITY`
* `NEGATIVE_INFINITY`: 负无穷大，小于`-MAX_VALUE`的值会被转换为`NEGATIVE_INFINITY`

## 原型对象

Number对象的原型

```
Number.prototype
num.__proto__
num.constructor.prototype
Object.getPrototypeOf(num)
```

### 原型属性

```javascript
Number.prototype.[[Class]] = 'Number'
Number.prototype.[[Prototype]] = Object.prototype
Number.prototype.[[Extensible]] = true
Number.prototype.[[Primitive]] = +0

Number.prototype.constructor = Number
```

### 原型方法

* this不为Boolean类型或Boolean对象，抛出TypeError

**转换方法**

#### Number.prototype.toString([radix])

获取Number对象的字符串表示

```javascript
/**
 * radix为undefined，置为10
 * radix不为undefined，转换为整数
 *    不在[2, 36]之内，抛出TypeError
 *    在[2, 36]之内，返回数字的radix进制字符串
 */
```

示例

```javascript
Number.prototype.toString.call(true) // 抛出TypeError

(123).toString() // '123'
(123).toString('abc') // 抛出RangeError
(123).toString(10) // '123'
(123).toString(16.2) // '7b'
```

#### Number.prototype.toLocaleString()

获取Number对象的本地字符串表示

```javascript
/**
 * 返回数字的本地字符串
 */
```

示例

```javascript
Number.prototype.toLocaleString.call(true) // 抛出TypeError

(123).toLocaleString() // '123'
```

#### Number.prototype.valueOf()

获取Number对象的值表示

```javascript
/**
 * 返回[[PrimitiveValue]]值
 */
```

示例

```javascript
Number.prototype.valueOf.call(true) // 抛出TypeError

(123).valueOf() // 123
```

**格式化方法**

#### Number.prototype.toFixed(fractionDigits)

格式化为十进制表示并保留指定位数小数的字符串

```javascript
/**
 * fractionDigits转换为整数f
 *    f不在[0, 20]之内，抛出RangeError（允许具体实现保留超过20位小数，如chome允许保留[0, 100]个小数）
 * this转换为Number类型x
 *    x为NaN，返回'NaN'
 *    x为负数，符号为负，其他按正数处理
 *    x >= 10^21，x直接转换为String类型
 *    x < 10^21，x保留f位小数并转换为String类型
 */
```

示例

```javascript
Number.prototype.toFixed.length // 1

Number.prototype.toFixed.call(true) // 抛出TypeError

(123.456).toFixed(-1) // 抛出RangeError
(NaN).toFixed(2) // 'NaN'
(Math.pow(10, 21) + 123.456).toFixed(2) // '1e+21'
(-Infinity).toFixed(2) // '-Infinity'
(123.456).toFixed(0) // '123'
(123.456).toFixed(1) // '123.4'
(123.456).toFixed(2) // '123.46'
(-123.456).toFixed(2) // '-123.46'
(0.0456).toFixed(0) // '0'
(0.0456).toFixed(1) // '0.0'
(0.0456).toFixed(2) // '0.05'
```

#### Number.prototype.toExponential(fractionDigits)

格式化为科学计数法表示并保留指定位数小数的字符串

```javascript
/**
 * this转换为Number类型x
 *    x为NaN，返回'NaN'
 *    x为负数，符号为负，其他按正数处理
 *    x为无穷大，返回s + 'Infinity'
 *    fractionDigits不为undefined时转换为整数f
 *       f不在[0, 20]之内，抛出RangeError（允许具体实现保留超过20位小数，如chome允许保留[0, 100]个小数）
 *    x为有限数，用科学计数法m * 10^e表示
 *       f不为undefined时，m保留f位小数
 *       e使用+d或-d表示
 *       返回s + m + 'e' + e
 */
```

示例

```javascript
Number.prototype.toExponential.length // 1

Number.prototype.toExponential.call(true) // 抛出TypeError

(NaN).toExponential(-1) // 'NaN'
(-Infinity).toExponential(-1) // '-Infinity'
(123.456).toExponential(-1) // 抛出RangeError
(Math.pow(10, 21) + 123.456).toExponential() // '1e+21'
(Math.pow(10, 21) + 123.456).toExponential(2) // '1.00e+21'
(123.456).toExponential() // '1.23456e+2'
(123.456).toExponential(3) // '1.235e+2'
(-123.456).toExponential(2) // '-1.23e+2'
(0.0456).toExponential() // '4.56e-2'
(0.0456).toExponential(1) // '4.6e-2'
```

#### Number.prototype.toPrecision(precision)

格式化为合适形式表示（十进制或科学计数法）并保留指定位数有效数字的字符串

```javascript
/**
 * precision为undefined时，返回ToString(this)
 * this转换为Number类型x
 *    x为NaN，返回'NaN'
 *    x为负数，符号为负，其他按正数处理
 *    x为无穷大，返回s + 'Infinity'
 *    precision转换为整数p
 *       p不在[1, 21]之内，抛出RangeError（允许具体实现保留超过21位有效数字，如chome允许保留[1, 100]个有效数字）
 *    x为有限数，用科学计数法m * 10^e表示
 *       e < -6或 e >= p，返回科学计数法表示并保留p位有效数字（p - 1位小数）的字符串
 *       e为其他， 返回十进制表示并保留p位有效数字（p - 1 - e位小数）的字符串
 */
```

示例

```javascript
Number.prototype.toPrecision.length // 1

Number.prototype.toPrecision.call(true) // 抛出TypeError

(123).toPrecision() // '123'
(Math.pow(10, 21) + 123.456).toPrecision() // '1e+21'
(NaN).toPrecision(-1) // 'NaN'
(-Infinity).toPrecision(-1) // '-Infinity'
(123.456).toPrecision(2) // '1.2e+2'
(123.456).toPrecision(3) // '123'
(123.456).toPrecision(4) // '123.5'
(0.0456).toPrecision(2) // '0.046'
(0.000000456).toPrecision(2) // '4.6e-7'
```

## 实例对象

[[Class]]为Number的对象

```javascript
// 通过构造器Number创建
new Number(true)

// 通过构造器Object创建
new Object(1)
```

### 实例属性

```javascript
N.[[Class]] = 'Number'
N.[[Prototype]] = Number.prototype
N.[[Extensible]] = true
N.[[PrimitiveValue]] = num
```
