# Global对象

标签（空格分隔）： ES5

---

全局对象，内置全局属性和全局方法

## 全局属性

### 值属性

* `undefined`: 特殊值`undefined`
* `NaN`: 特殊值`NaN`
* `Infinity`: 特殊值`Infinity`

### 构造器属性

* `Object`: Object构造器
* `Function`: Function构造器
* `Array`: Array构造器
* `String`：String构造器
* `Boolean`：Boolean构造器
* `Number`: Number构造器
* `Date`: Date构造器
* `RegExp`: RegExp构造器
* `Error`: Error构造器
* `EvalError`: EvalError构造器
* `RangeError`: RangeError构造器
* `ReferenceError`: ReferenceError构造器
* `SyntaxError`: SyntaxError构造器
* `TypeError`: TypeError构造器
* `URIError`: URIError构造器

### 单体对象属性

* `Math`: Math对象
* `JSON`: JSON对象

## 全局方法

### eval方法

```javascript
eval(x)

/**
 * x不为字符串，直接返回
 * x为字符串，解析为程序
 *    解析失败，抛出SyntaxError
 *    解析成功，创建eval上下文，执行程序、返回结果，最后退出eval上下文
 */
```

示例

```javascript
eval(2) // 2
eval('let a = 1') // undefined
eval('1 + 1') // 2
eval('throw new Error('error')') // error
```

### 数字方法

#### isNaN(number)

转换为Number类型后判断是否是NaN

```javascript
/**
 * 将number转换为Number类型
 *     是NaN，返回true
 *     不是NaN，返回false
 */
```

示例

```javascript
isNaN(undefined) // true
isNaN(null) // false
isNaN(true) // false
isNaN(1) // false
isNaN(NaN) // true
isNaN('123') // false
isNaN('123ab') // true
isNaN({}) // true
```

#### isFinite(number)

转换为Number类型后判断是否是有限数字

```javascript
/**
 * 将number转换为Number类型
 *     是NaN、Infinity、-Infinity，返回false
 *     其他情况，返回true
 */
```

示例

```javascript
isFinite(undefined) // false
isFinite(null) // true
isFinite(true) // true
isFinite(1) // true
isFinite(NaN) // false
isFinite(Infinity) // false
isFinite('123') // true
isFinite('123ab') // false
isFinite({}) // false
```

### 字符串方法

#### parseInt(string, radix)

将字符串解析为整数

```javascript
/**
 * string转换为String类型并去除前置空格，radix转换为Int32类型
 * 确定符号位
 *     string以-开头，符号为负
 *     string以+或其他开头，符号为正
 * 确定进制数
 *    radix为0，string以0x或0X开头，按16进制解析，其他按10进制解析
 *    radix为16，string不管是否以0x或0X开头，都按16进制解析
 *    radix在[2, 36]之内，按radix进制解析
 *    radix在[2, 36]之外，直接返回NaN
 * 确定string中匹配radix进制的最长前缀
 *    无匹配，返回NaN
 *    有匹配，按radix进制解析为数字 * 符号
 */
```

示例

```javascript
parseInt(undefined) // NaN
parseInt('   123') // 123
parseInt('\t\v\r123\n ') // 123
parseInt('-123') // -123
parseInt('0x123') // 291
parseInt('0x123', 16) // 291
parseInt('123', 16) // 291
parseInt('0x123', 10) // 0
parseInt('123', 1) // NaN
parseInt('') // NaN
parseInt('123.45') // 123
parseInt('123e-2') // 123

// 自动转换为科学计数法的数字
parseInt(1000000000000000000000.5) // 1
// 等同于
parseInt('1e+21') // 1

parseInt(0.0000008) // 8
// 等同于
parseInt('8e-7') // 8
```

#### parseFloat(string)

将字符串解析为十进制数字

```javascript
/**
 * string转换为String类型并去除前置空格
 * 确定string中匹配数字字符串的最长前缀
 *    无匹配，返回NaN
 *    有匹配，转换为Number类型
 */
```

示例

```javascript
parseFloat(undefined) // NaN
parseFloat('   123') // 123
parseFloat('') // NaN
parseFloat('123.45abc') // 123.45
parseFloat('0x12abc') // 18
parseFloat('Infinity') // Infinity
parseFloat('1e2') // 100
```

### URI方法

#### URI组成

```javascript
uri :::
  uriCharacters(opt) // URI字符

uriCharacters ::: // URI字符
  uriCharacter uriCharacters(opt)

uriCharacter ::: // 单个URI字符
  uriReserved // URI保留字符
  uriUnescaped // URI非转义字符
  uriEscaped // URI转义字符

uriReserved ::: one of // URI保留字符
  ; / ? : @ & = + $ ,

uriUnescaped :::  // URI非转义字符
  uriAlpha // URI字母
  DecimalDigit // 十进制数字
  uriMark // URI标记

uriAlpha ::: one of // URI字母
  a b c d e f g h i j k l m n o p q r s t u v w x y z
  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

uriMark ::: one of // URI标记
  - _ . ! ~ * ' ( )
  
uriEscaped ::: // URI转义字符
  % HexDigit HexDigit
```

非URI字符都需转义：使用UTF-8编码，再用%xx%xx表示

```
'字'转码：%E5%AD%97
```

#### encodeURI(uri)

编码URI

```javascript
/**
 * uri转换为String类型
 * uriUnescaped + uriReserved + '#'不编码，其他都编码
 */
```

示例

```javascript
encodeURI('http://www.w3school.com.cn/My first/') // http://www.w3school.com.cn/My%20first/
```

#### encodeURIComponent(uriComponent)

编码URI组件

```javascript
/**
 * uriComponent转换为String类型
 * uriUnescaped不编码，其他都编码
 */
```

示例

```javascript
encodeURIComponent('http://www.w3school.com.cn/p 1/') // http%3A%2F%2Fwww.w3school.com.cn%2Fp%201%2F
```

#### decodeURI(encodeURI)

解码URI

```javascript
/**
 * encodeURI转换为String类型
 * uriReserved + '#'的编码不解码，其他的都解码
 */
```

示例

```javascript
decodeURI('http://www.w3school.com.cn/My%20first/') // http://www.w3school.com.cn/My first/

decodeURI('http%3A%2F%2Fwww.w3school.com.cn%2Fp%201%2F') // http%3A%2F%2Fwww.w3school.com.cn%2Fp 1%2F
```

#### decodeURIComponent(encodedURIComponent)

解码URI组件

```javascript
/**
 * encodedURIComponent转换为String类型
 * 全都进行解码
 */
```

示例

```javascript
decodeURIComponent('http://www.w3school.com.cn/My%20first/') // http://www.w3school.com.cn/My first/

decodeURIComponent('http%3A%2F%2Fwww.w3school.com.cn%2Fp%201%2F') // http://www.w3school.com.cn/p 1/ 
```
