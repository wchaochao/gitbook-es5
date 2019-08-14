# RegExp构造器

标签（空格分隔）： ES5

---

类型为`RegExp`的对象

## 构造函数

### RegExp(pattern, flags)

作为函数使用，返回RegExp对象

```javascript
/**
 * pattern为RegExp对象且flags为undefined，直接返回pattern
 * 其他情况，调用new RegExp生成RegExp对象
 */
```

示例

```javascript
RegExp(/a/) // /a/
RegExp(/a/, undefined) // /a/
RegExp(/a/, 'i') // /a/i
```

### new RegExp(pattern, flags)

作为构造器使用，创建RegExp对象

```javascript
/**
 * 参数处理
 * pattern为RegExp对象时，置为该对象的Pattern
 * pattern为undefined时，置为空字符串
 * pattern为其他时，转换为字符串
 * flags为undefined时，置为空字符串
 * flags为其他时，转换为字符串
 * flags含'g', 'i', 'm'之外的字符或含多个'g', 'i', 'm'时，抛出SyntaxError
 * 
 * 创建RegExp对象
 * [[Class]]属性为'RegExp'
 * [[Prototype]]属性为RegExp.prototype
 * [[Extensible]]属性为true
 * [[Match]]方法为执行pattern获取的字符串匹配函数
 * source属性为pattern转义后的字符串（对/, 空字符串转义）
 * global属性为flags是否含'g'
 * ignorecase属性为flags是否含'i'
 * multiline属性为flags是否含'm'
 * lastIndex属性为0
 */
```

示例

```javascript
new RegExp(/a/) // /a/
new RegExp() // /(?:)/
new RegExp('a') // /a/
new RegExp(/a/, 'i') // /a/i
new RegExp('a', 'a') // 抛出SyntaxError
new RegExp('a', 'gg') // 抛出SyntaxError

new RegExp('/', 'gim')
// {
//   source: '\/',
//   global: true,
//   ignorecase: true,
//   multiline: true,
//   lastIndex: 0
// }
```

### 静态属性

```javascript
RegExp.[[Class]] = 'Function'
RegExp.[[Prototype]] = Function.Prototype
RegExp.[[Extensible]] = true

RegExp.[[DefineOwnProperty]]('length', {
  [[Value]]: 2,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
RegExp.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: RegExp,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

## 原型对象

RegExp对象的原型

```javascript
RegExp.prototype
regexp.__proto__
regexp.constructor.prototype
Object.getPrototypeOf(regexp)
```

### 原型属性

```javascript
RegExp.prototype.[[Class]] = 'RegExp'
RegExp.prototype.[[Prototype]] = Object.prototype
RegExp.prototype.[[Extensible]] = true
RegExp.prototype.[[Match]] = evaluate('')

RegExp.prototype.constructor = RegExp
RegExp.prototype.source = '(?:)'
RegExp.prototype.global = false
RegExp.prototype.ignorecase = false
RegExp.prototype.multiline = false
RegExp.prototype.lastIndex = 0
```

### 原型方法

* this不为RegExp对象时，抛出TypeError

**转换方法**

#### RegExp.prototype.toString()

获取RegExp对象的字符串表示

```javascript
/**
 * 返回/source/flags形式的字符串，flags的顺序为'gim'
 */
```

示例

```javascript
RegExp.prototype.toString.call(undefined) // 抛出TypeError

new RegExp('', 'img') // /(?:)/gim
new RegExp('a', 'ig') // /a/gi
```

**匹配方法**

#### RegExp.prototype.exec(string)

获取匹配信息

```javascript
/**
 * string转换为String类型
 * 非全局匹配，从0开始匹配，lastIndex属性不变
 * 全局匹配，从lastIndex开始匹配（lastIndex转换为整数）
 *    匹配成功时，将lastIndex属性置为endIndex
 *    匹配不成功时，将lastIndex属性置为0
 * 能匹配到，返回一个包含匹配信息的数组
 *    第一个元素为匹配字符串，其他元素为捕获组匹配
 *    Input属性为string
 *    Index属性为匹配成功的位置
 * 不能匹配到，返回null
 */
```

示例

```javascript
RegExp.prototype.exec.call(undefined) // 抛出TypeError

// 非全局匹配
/(.)at/.exec('at') // null
/(.)at/.exec('cat') // ['cat', 'c', index: 0, input: 'cat']

// 全局匹配
let reg = /(.)at/g

reg.exec('cat') // ['cat', 'c', index: 0, input: 'cat']
reg.lastIndex // 3

reg.exec('cat') // null
reg.lastIndex // 0
```

#### RegExp.prototype.test(string)

```javascript
/**
 * 调用RegExp.prototype.exec方法
 *    结果为null, 返回false
 *    结果不为null, 返回true
 */
```

示例

```javascript
RegExp.prototype.test.call(undefined) // 抛出TypeError

// 非全局匹配
/(.)at/.test('at') // false
/(.)at/.test('cat') // true

// 全局匹配
let reg = /(.)at/g

reg.test('cat') // true
reg.lastIndex // 3

reg.test('cat') // false
reg.lastIndex // 0
```

## 实例对象

[[Class]]为RegExp的对象

```javascript
// 通过正则直接量创建
/a/

// 通过构造器RegExp创建
new RegExp('a', 'i')
```

### 实例属性

```javascript
regexp.[[Class]] = 'RegExp'
regexp.[[Prototype]] = RegExp.prototype
regexp.[[Extensible]] = true
regexp.[[Match]] = evaluate(pattern)
```

#### source

pattern转义字符串

```javascript
regexp.[[DefineOwnProperty]]('source', {
  [[Value]]: source,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```

#### global

是否是全局匹配

```javascript
regexp.[[DefineOwnProperty]]('global', {
  [[Value]]: global,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```

#### ignorecase

是否忽略大小写

```javascript
regexp.[[DefineOwnProperty]]('ignorecase', {
  [[Value]]: ignorecase,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```

#### multiline

是否为多行匹配

```javascript
regexp.[[DefineOwnProperty]]('multiline', {
  [[Value]]: multiline,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```

#### lastIndex

下次匹配开始的位置

```javascript
regexp.[[DefineOwnProperty]]('lastIndex', {
  [[Value]]: lastIndex,
  [[Writable]]: true,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```
