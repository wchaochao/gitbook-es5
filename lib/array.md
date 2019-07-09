# Array构造器

标签（空格分隔）： ES5

---

## 构造函数

### Array([item0 [ , item1 [ , … ] ] ] )

作为函数使用，等同于作为构造器使用

### new Array([item0 [ , item1 [ , … ] ] ] )

作为构造器使用，创建数组对象

```javascript
/**
 * 创建数组对象
 * [[Class]]属性为'Array'
 * [[Prototype]]属性为Array.prototype
 * [[Extensible]]属性为true
 * 参数只有一个且为Number类型
 *     参数为UInt32类型，length属性为该参数
 *     参数不为UInt32类型，抛出RangError
 * 其他情况，length属性为参数个数，元素为对应参数
 */
```

示例

```javascript
// 无参数
new Array() // []

// 单个UInt类型参数
new Array(8) // [empty × 8]

// 单个非UInt类型数字参数
new Array(3.2) // RangeError: Invalid array length
new Array(-3) // RangeError: Invalid array length

// 单个非数字参数
new Array('abc') // ['abc']
new Array([1]) // [Array[1]]

// 多参数
new Array(1, 2) // [1, 2]
new Array('a', 'b', 'c') // ['a', 'b', 'c']
```

### 静态属性

```javascript
Array.[[Class]] = 'Function'
Array.[[Prototype]] = Function.Prototype
Array.[[Extensible]] = true

Array.[[DefineOwnProperty]]('length', {
  [[Value]]: 1,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
Array.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: Array,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

### 静态方法

#### Array.isArray(arg)

判断arg是否是数组

```javascript
/**
 * [[Class]]为Array，返回true
 * [[Class]]不为Array，返回false
 */
```

polyfill

```javascript
if (typeof Array.isArray !== "function") {
  Array.isArray = function (value) {
    return Object.prototype.toString.call(value) === "[object Array]";
  }
}
```

示例

```javascript
Array.isArray(1) // false
Array.isArray({}) // false
Array.isArray([]) // true
```

## 原型对象

Array对象的原型

```
Array.prototype
arr.__proto__
arr.constructor.prototype
Object.getPrototypeOf(arr)
```

### 原型属性

```javascript
Array.prototype.[[Class]] = 'Array'
Array.prototype.[[Prototype]] = Object.prototype
Array.prototype.[[Extensible]] = true

Array.prototype.constructor = Array
Array.prototype.length = 0
```

### 原型方法

* this转换为Object类型O
* length属性转换为UInt32类型len

**转换方法**

#### Array.prototype.toString()

获取数组的字符串表示

```javascript
/**
 * 有join方法，调用join方法
 * 无join方法，调用Object.prototype.toString方法
 */
```

示例

```javascript
Array.prototype.toString.call(undefined) // 抛出TypeError

let arr = []
arr.toString() // ''

let arr = [1, 2, 3]
arr.toString() // '1,2,3'

let o = {a: 1}
Array.prototype.toString.call(o) // '[object Object]'

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.toString.call(o) // '[object Object]'
Array.prototype.toString.call('abc') // '[object String]'
```

#### Array.prototype.toLocaleString()

获取数组的本地字符串表示

```javascript
/**
 * 遍历索引值
 *     索引值为undefined或null，转换为''
 *     索引值不为undefined或null，调用toLocaleString方法
 * 用逗号将各索引值拼接起来
 */
```

示例

```javascript
Array.prototype.toLocaleString.call(undefined) // 抛出TypeError

let arr = []
arr.toLocaleString() // ''

let arr = [1, undefined, 3]
arr.toLocaleString() // '1,,3'

let o = {a: 1}
Array.prototype.toLocaleString.call(o) // ''

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.toLocaleString.call(o) // '0,1'
Array.prototype.toLocaleString.call('abc') // 'a,b,c'
```

#### Array.prototype.join(separator)

以指定分隔符连接数组元素

```javascript
/**
 * separator转换为String类型，默认为','
 * 遍历索引值
 *     索引值为undefined或null，转换为''
 *     索引值不为undefined或null，转换为String类型
 * 用分隔符将各索引值拼接起来
 */
```

示例

```javascript
Array.prototype.join.length // 1

Array.prototype.join.call(undefined) // 抛出TypeError

let arr = []
arr.join() // ''

let arr = [1, undefined, 3]
arr.join() // '1,,3'

let o = {a: 1}
Array.prototype.join.call(o) // ''

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.join.call(o) // '0,1'
Array.prototype.join.call('abc', '-') // 'a-b-c'
```

**栈方法**

#### Array.prototype.push([item1 [ , item2 [ , … ] ] ] )

将元素追加到数组末尾并返回数组长度

```javascript
/**
 * 参数追加到索引末尾，length随之变化
 * 返回新length
 */
```

示例

```javascript
Array.prototype.push.length // 1

Array.prototype.push.call(undefined) // 抛出TypeError

let arr = []
arr.push(1, 2) // 2, arr为[1, 2]

let arr = [1, 2]
arr.push(3) // 3, arr为[1, 2, 3]

let o = {a: 1}
Array.prototype.push.call(o) // 0, o为{a: 1, length: 0}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.push.call(o, 2) // 3, o为{0: 0, 1: 1, 2: 2, length: 3}
Array.prototype.push.call('abc', 1, 2) // Uncaught TypeError: Cannot assign to read only property 'length' of object '[object String]'
```

#### Array.prototype.pop()

移除最后一个元素

```javascript
/**
 * 移除最后一个索引，length随之变化
 * 返回移除索引对应的元素
 */
```

示例

```javascript
Array.prototype.pop.call(undefined) // 抛出TypeError

let arr = []
arr.pop() // undefined, arr为[]

let arr = [1, 2, 3]
arr.pop() // 3, arr为[1, 2]

let o = {a: 1}
Array.prototype.pop.call(o) // undefined, o为{a: 1, length: 0}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.pop.call(o) // 1, o为{0: 0, length: 1}
Array.prototype.pop.call('abc') // Uncaught TypeError: Cannot delete property '2' of [object String]
```

**队列方法**

#### Array.prototype.unshift([item1 [ , item2 [ , … ] ] ] )

将元素追加到数组开头并返回数组长度

```javascript
/**
 * 参数追加到索引开头，其他索引和length随之变化
 * 返回新length
 */
```

示例

```javascript
Array.prototype.unshift.length // 1

Array.prototype.unshift.call(undefined) // 抛出TypeError

let arr = []
arr.unshift(1, 2) // 2, arr为[1, 2]

let arr = [1, 2]
arr.unshift(3) // 3, arr为[3, 1, 2]

let o = {a: 1}
Array.prototype.unshift.call(o) // 0, o为{a: 1, length: 0}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.unshift.call(o, 2) // 3, o为{0: 2, 1: 0, 2: 1, length: 3}
Array.prototype.unshift.call('abc', 1, 2) // Uncaught TypeError: Cannot assign to read only property '2' of object '[object String]'
```

#### Array.prototype.shift()

移除第一个元素并返回该元素

```javascript
/**
 * 移除第一个索引，其他索引和length随之变化
 * 返回移除索引对应的元素
 */
```

示例

```javascript
Array.prototype.shift.call(undefined) // 抛出TypeError

let arr = []
arr.shift() // undefined, arr为[]

let arr = [1, 2, 3]
arr.shift() // 1, arr为[2, 3]

let o = {a: 1}
Array.prototype.shift.call(o) // undefined, o为{a: 1, length: 0}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.shift.call(o) // 1, o为{0: 1, length: 1}
Array.prototype.shift.call('abc') // Uncaught TypeError: Cannot assign to read only property '0' of object '[object String]'
```

**重排序方法**

#### Array.prototype.reverse()

数组倒序排列

```javascript
/**
 * 索引倒序排列
 */
```

示例

```javascript
Array.prototype.reverse.call(undefined) // 抛出TypeError

let arr = []
arr.reverse() // []

let arr = [1, 2, 3]
arr.reverse() // [3, 2, 1]

let o = {a: 1}
Array.prototype.reverse.call(o) // {a: 1}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.reverse.call(o) // {0: 1, 1: 0, length: 2}
Array.prototype.reverse.call('abc') // Uncaught TypeError: Cannot assign to read only property '0' of object '[object String]'
```

#### Array.prototype.sort(comparefn)

数组按comparefn排序

```javascript
/**
 * 对任意两个索引j、k进行排序
 *     空位 > undefined > 其他值
 *     comparefn为undefined，索引值转换为String类型比较
 *     comparefn不为undefined
 *         不为函数，抛出TypeError
 *         为函数，参数为两索引值
 *             comparefn(a, b) < 0, 则a < b
 *             comparefn(a, b) = 0, 则a = b
 *             comparefn(a, b) > 0, 则a = b
 */
```

示例

```javascript
Array.prototype.reverse.sort(undefined) // 抛出TypeError

let arr = []
arr.sort() // []

let arr = [1, , 3, undefined, null]
arr.sort() // [1, 3, null, undefined, empty]

let arr = [1, , 3, undefined, null]
arr.sort(2) // TypeError

let arr = [1, , 3, undefined, null]
arr.sort((a, b) => a - b) // [null, 1, 3, undefined, empty]

let o = {a: 1}
Array.prototype.sort.call(o) // {a: 1}

let o = {
  0: 1,
  2: 3,
  3: undefined,
  4: null,
  length: 5
}
Array.prototype.sort.call(o) // {0: 1, 1: 3, 2: null, 3: undefined, length: 5}
Array.prototype.sort('abc') // Uncaught TypeError: Cannot assign to read only property '0' of object '[object String]'
```

**操作方法**

#### Array.prototype.concat([item1 [ , item2 [ , … ] ] ] )

数组拼接

```javascript
/**
 * 遍历O与参数组成的列表列表
 *     列表值不为数组，设置新数组元素为列表值
 *     列表值为数组，设置新数组元素为数组元素
 */
```

示例

```javascript
Array.prototype.concat.length // 1

Array.prototype.concat.call(undefined) // 抛出TypeError

let arr = [1,,2]
arr.concat() // [1, empty, 2]

let arr = [1,,2]
arr.concat(3, undefined, [4,,5]) // [1, empty, 2, 3, undefined, 4, empty, 5]

let o = {a: 1}
Array.prototype.concat.call(o) // [{a: 1}]

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.concat.call(o) // [{0: 0, 1: 1, length: 2}]
Array.prototype.concat.call('abc', [1, 2]) // [String{'abc'}, 1, 2]
```

#### Array.prototype.slice(start, end)

数组截取

```javascript
/**
 * start转换为整数，为负数时加len
 *      小于0时置为0，大于len时置为len，落在[0, len]之间
 * end为undefined时，置为len
 * end不为undefined时，与start同样处理
 * 截取[start, end)的索引值组成新数组
 */
```

示例

```javascript
Array.prototype.slice.length // 2

Array.prototype.slice.call(undefined) // 抛出TypeError

let arr = [1,,2]
arr.slice() // [1, empty, 2]

let arr = [1,,2]
arr.slice(1, -1) // [empty]
arr.slice(2, 1) // []

let o = {a: 1}
Array.prototype.slice.call(o, 1, -1) // []

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.slice.call(o, 0, -1) // [0]
Array.prototype.slice.call('abc', 1, -1) // ['b']
```

#### Array.prototype.splice(start, deleteCount [ , item1 [ , item2 [ , … ] ] ] )

数组替换

```javascript
/**
 * start转换为整数，为负数时加len
 *      小于0时置为0，大于len时置为len，落在[0, len]之间
 * deleteCount转换为整数
 *      小于0时置为0，大于len - start时置为len - start，落在[0, len - start]之间
 * 在start位置删除deleteCount个索引，插入参数，其他索引和length随之变化
 * 返回删除索引值组成的新数组
 */
```

示例

```javascript
Array.prototype.splice.length // 2

Array.prototype.splice.call(undefined) // 抛出TypeError

let arr = [1,,2]
arr.splice() // [], arr为[1, empty, 2]

let arr = [1,,2]
arr.splice(0, 0, 1) // [], arr为[1, 1, empty, 2]
arr.splice(-2, 2, 2) // [empty, 2], arr为[1, 2]
arr.splice(4, 5, 6, 7)  // [], arr为[1, empty, 2, 6, 7]

let o = {a: 1}
Array.prototype.splice.call(o, 1, -1) // [], o为{a: 1, length: 0}

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.splice.call(o, 0, 1, 2) // [0], o为{0: 2, 1: 1, length: 2}
Array.prototype.splice.call('abc', 1, 1) // Uncaught TypeError: Cannot assign to read only property '1' of object '[object String]'
```

**位置方法**

#### Array.prototype.indexOf(searchElement [ , fromIndex ] )

按索引升序从指定索引开始查找元素

```javascript
/**
 * fromIndex未提供，置为0
 * fromIndex已提供
 *      转换为整数，为负数时加len，小于0时置为0
 * 从fromIndex开始升序查找searchElement（严格相等）
 *     查找到，则返回对应的索引
 *     查找不到，则返回-1
 */
```

示例

```javascript
Array.prototype.indexOf.length // 1

Array.prototype.indexOf.call(undefined) // 抛出TypeError

let arr = [1,,2,undefined,1,NaN]
arr.indexOf() // 3
arr.indexOf(1) // 0
arr.indexOf(1, 2) // 4
arr.indexOf('1') // -1
arr.indexOf(NaN) // -1

let o = {a: 1}
Array.prototype.indexOf.call(o, 1) // -1

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.indexOf.call(o, 0) // 0
Array.prototype.indexOf.call('abcba', 'b', 2) // 3
```

#### Array.prototype.lastIndexOf(searchElement [ , fromIndex ] )

按索引降序从指定索引开始查找元素

```javascript
/**
 * fromIndex未提供，置为len - 1
 * fromIndex已提供
 *      转换为整数，为负数时加len，大于len - 1时置为len - 1
 * 从fromIndex开始降序查找searchElement（严格相等）
 *     查找到，则返回对应的索引
 *     查找不到，则返回-1
 */
```

示例

```javascript
Array.prototype.lastIndexOf.length // 1

Array.prototype.lastIndexOf.call(undefined) // 抛出TypeError

let arr = [1,,2]
arr.lastIndexOf() // -1

let arr = [1,,2,undefined,1,NaN]
arr.lastIndexOf() // 3
arr.lastIndexOf(1) // 4
arr.lastIndexOf(1, 2) // 0
arr.lastIndexOf('1') // undefined
arr.lastIndexOf(NaN) // undefined

let o = {a: 1}
Array.prototype.lastIndexOf.call(o, 1) // -1

let o = {
  0: 0,
  1: 1,
  length: 2
}
Array.prototype.lastIndexOf.call(o, 0) // 0
Array.prototype.lastIndexOf.call('abcba', 'b', 2) // 1
```

**遍历方法**

在使用遍历方法时最好不要修改数组

* 新添加的元素不会被遍历
* 未被遍历的元素被修改，遍历时值为修改后的元素
* 未被遍历的元素被delete删除，遍历时会跳过该元素
* 元素被数组方法移除时，length和index将受到影响

#### Array.prototype.forEach(callbackfn [ , thisArg ] )

数组遍历

```javascript
/**
 * callbackfn不为函数抛出TypeError, thisArg未提供为undefined
 * 遍历索引值，对非空位的索引值调用callbackfn，this为thisArg，参数为(索引值，索引，O)
 * 返回undefined
 */
```

示例

```javascript
Array.prototype.forEach.length // 1

Array.prototype.forEach.call(undefined) // 抛出TypeError

let arr = []
arr.forEach(1) // 抛出TypeError

let arr = []
arr.forEach(x => console.log(x))

let arr = [1,,2]
arr.forEach(x => console.log(x))
// 1
// 2

let arr = [1,,2]
arr.forEach((ele, index, arr) => {
  console.log(ele + this.x)
}, {x: 1})
// 2
// 3

let o = {a: 1}
Array.prototype.forEach.call(o, x => console.log(x))

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.forEach.call(o, x => console.log(x))
// 0
// 2

Array.prototype.forEach.call('abc', x => console.log(x))
// 'a'
// 'b'
// 'c'
```

#### Array.prototype.map(callbackfn [ , thisArg ] )

数组映射

```javascript
/**
 * callbackfn不为函数抛出TypeError, thisArg未提供为undefined
 * 遍历索引值，对非空位的索引值调用callbackfn，this为thisArg，参数为(索引值，索引，O)
 *      callbackfn返回值映射到新数组中
 * 返回新数组
 */
```

示例

```javascript
Array.prototype.map.length // 1

Array.prototype.map.call(undefined) // 抛出TypeError

let arr = []
arr.map(1) // 抛出TypeError

let arr = []
arr.map(x => x + 1) // []

let arr = [1,,2]
arr.map(x => x + 1) // [2, empty, 3]

let arr = [1,,2]
arr.map((ele, index, arr) => {
  return ele + this.x
}, {x: 1}) // [2, empty, 3]

let o = {a: 1}
Array.prototype.map.call(o, x => x + 1) // []

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.map.call(o, x => x + 1) // [1, empty, 3]
Array.prototype.map.call('abc', x => x + 1) // ['a1', 'b1', 'c1']
```

#### Array.prototype.filter(callbackfn [ , thisArg ] )

数组过滤

```javascript
/**
 * callbackfn不为函数抛出TypeError, thisArg未提供为undefined
 * 遍历索引值，对非空位的索引值调用callbackfn，this为thisArg，参数为(索引值，索引，O)
 *     若callbackfn返回值转换为true，则将索引值添加到新数组中
 * 返回新数组
 */
```

示例

```javascript
Array.prototype.filter.length // 1

Array.prototype.filter.call(undefined) // 抛出TypeError

let arr = []
arr.filter(1) // 抛出TypeError

let arr = []
arr.filter(x => x > 0) // []

let arr = [1,,2]
arr.filter(x => x > 0) // [1, 2]

let arr = [1,,2]
arr.filter(function (ele, index, arr) {
  return ele > this.x
}, {x: 1}) // [1, 2]

let o = {a: 1}
Array.prototype.filter.call(o, x => x > 0) // []

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.filter.call(o, x => x > 0) // [2]
Array.prototype.filter.call('abc', x => x < 'd') // ['a', 'b', 'c']
```

#### Array.prototype.every(callbackfn [ , thisArg ] )

判断数组是否所有元素符合条件

```javascript
/**
 * callbackfn不为函数抛出TypeError, thisArg未提供为undefined
 * 遍历索引值，对非空位的索引值调用callbackfn，this为thisArg，参数为(索引值，索引，O)
 *     若有callbackfn返回值转换为false，则返回false
 *     若所有callbackfn的返回值都转换为true，则返回true
 */
```

示例

```javascript
Array.prototype.every.length // 1

Array.prototype.every.call(undefined) // 抛出TypeError

let arr = []
arr.every(1) // 抛出TypeError

let arr = []
arr.every(x => x > 0) // true

let arr = [1,,2]
arr.every(x => x > 0) // true

let arr = [1,,2]
arr.every(function (ele, index, arr) {
  return ele > this.x
}, {x: 1}) // false

let o = {a: 1}
Array.prototype.every.call(o, x => x > 0) // true

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.every.call(o, x => x > 0) // false
Array.prototype.every.call('abc', x => x < 'd') // true
```

#### Array.prototype.some(callbackfn [ , thisArg ] )

判断数组是否有元素符合条件

```javascript
/**
 * callbackfn不为函数抛出TypeError, thisArg未提供为undefined
 * 遍历索引值，对非空位的索引值调用callbackfn，this为thisArg，参数为(索引值，索引，O)
 *     若有callbackfn返回值转换为true，则返回true
 *     若所有callbackfn的返回值都转换为false，则返回false
 */
```

示例

```javascript
Array.prototype.some.length // 1

Array.prototype.some.call(undefined) // 抛出TypeError

let arr = []
arr.some(1) // 抛出TypeError

let arr = []
arr.some(x => x > 0) // false

let arr = [1,,2]
arr.some(x => x > 0) // true

let arr = [1,,2]
arr.some(function (ele, index, arr) {
  return ele > this.x
}, {x: 1}) // true

let o = {a: 1}
Array.prototype.some.call(o, x => x > 0) // false

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.some.call(o, x => x > 0) // true
Array.prototype.some.call('abc', x => x < 'd') // true
```

**累计方法**

依次处理数组中的每个元素，最终累计为一个值

#### Array.prototype.reduce(callbackfn [ , initialValue ] )

按索引升序对数组进行累计

```javascript
/**
 * callbackfn不为函数抛出TypeError
 * initialValue提供时，accumulator为initialValue，start为0
 * initialValue未提供时，accumulator为第一个非空位索引值，start为索引 + 1
 *      无非空位索引值时，抛出TypeError
 * 从start开始升序遍历索引值，对非空位的索引值调用callbackfn，this为undefined，参数为(accumulator, 索引值，索引，O)，返回值赋给accumulator
 * 返回accumulator
 */
```

示例

```javascript
Array.prototype.reduce.length // 1

Array.prototype.reduce.call(undefined) // 抛出TypeError

let arr = []
arr.reduce(1) // 抛出TypeError

let arr = []
arr.reduce((pre, next) => pre + next) // 抛出TypeError

let arr = [,,,]
arr.reduce((pre, next) => pre + next) // 抛出TypeError

let arr = [,1,,2]
arr.reduce((pre, next) => pre + next) // 3

let arr = [,1,,2]
arr.reduce((pre, next) => pre + next, 3) // 6

let o = {a: 1}
Array.prototype.reduce.call(o, (pre, next) => pre + next) // 抛出TypeError

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.reduce.call(o, (pre, next) => pre + next) // 2
Array.prototype.reduce.call('abc', (pre, next) => pre + next) // 'abc'
```

#### Array.prototype.reduceRight(callbackfn [ , initialValue ] )

按索引降序对数组进行累计

```javascript
/**
 * callbackfn不为函数抛出TypeError
 * initialValue提供时，accumulator为initialValue，start为len - 1
 * initialValue未提供时，accumulator为倒数第一个非空位索引值，start为索引 - 1
 *      无非空位索引值时，抛出TypeError
 * 从start开始降序遍历索引值，对非空位的索引值调用callbackfn，this为undefined，参数为(accumulator, 索引值，索引，O)，返回值赋给accumulator
 * 返回accumulator
 */
```

示例

```javascript
Array.prototype.reduceRight.length // 1

Array.prototype.reduceRight.call(undefined) // 抛出TypeError

let arr = []
arr.reduceRight(1) // 抛出TypeError

let arr = []
arr.reduceRight((pre, next) => pre + next) // 抛出TypeError

let arr = [,,,]
arr.reduceRight((pre, next) => pre + next) // 抛出TypeError

let arr = [,1,,2]
arr.reduceRight((pre, next) => pre + next) // 3

let arr = [,1,,2]
arr.reduceRight((pre, next) => pre + next, 3) // 6

let o = {a: 1}
Array.prototype.reduceRight.call(o, (pre, next) => pre + next) // 抛出TypeError

let o = {
  0: 0,
  2: 2,
  length: 3
}
Array.prototype.reduceRight.call(o, (pre, next) => pre + next) // 2
Array.prototype.reduceRight.call('abc', (pre, next) => pre + next) // 'cba'
```

## 实例对象

[[Class]]为Array的对象

```javascript
// 通过数组直接量创建
[1]

// 通过构造器Array创建
new Array('a', 'b')
```

### 实例属性

```javascript
arr.[[Class]] = 'Array'
arr.[[Prototype]] = Array.prototype
arr.[[Extensible]] = true

arr.[[DefineOwnProperty]]('length', {
  [[Value]]: length,
  [[Writable]]: true,
  [[Enumerable]]: false,
  [[Configurable]]: false
})
```

### 设置数组属性

```javascript
/**
 * P为length属性，设置length值
 *    newLen不为UInt32类型，抛出RangeError
 *    newLen >= oldLen, 设置length属性为newLen
 *    newLen < oldLen, 设置length属性为新值并删除所有索引大于newLen - 1的属性
 *        删除失败时，设置length属性为失败时的索引 + 1
 * P为索引属性，设置元素值
 *    P <= len - 1，设置P对应的元素
 *    P > len - 1，设置P对象的元素值，并设置length为索引 + 1
 * P为普通属性，设置属性值
 */
```

示例

```javascript
// 非法length
let arr = [1, 2, 3]

arr.length = -1 // 抛出RangeError
arr.length = Math.pow(2, 32) // 抛出RangeError
arr.length = 2.3 // 抛出RangeError
arr.length = 'abc' // 抛出RangeError

// 增长length
let arr = [1, 2, 3]
arr.length = 10 // arr为[1, 2, 3, empty × 7]

// 减少length
let arr = [1, 2, 3]
arr.length = 2 // arr为[1, 2]

// 修改元素
let arr = [1, 2, 3]
arr[1] = 0 // arr为[1, 0, 3]

// 添加元素
let arr = [1, 2, 3]
arr[9] = 0 // arr为[1, 2, 3, empty × 6, 0]

// 设置属性
arr[-1] = 'a'
```
