# Date构造器

标签（空格分隔）： ES5

---

## 构造函数

### Date([year [, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ] ] ] )

作为函数使用，返回当前时间的字符串表示（当前时间为计算机的时间）

```javascript
/**
 * 返回当前时间的字符串表示
 */
```

### new Date()

无参数，作为构造器使用，创建Date对象，时间为当前时间

```javascript
/**
 * 创建Date对象
 * [[Class]]属性为'Date'
 * [[Prototype]]属性为Date.prototype
 * [[Extensible]]属性为true
 * [[PrimitiveValue]]属性为当前时间对应的UTC毫秒数
 */
```

### new Date(value)

1个参数，作为构造器使用，创建Date对象，指定UTC毫秒数或时间字符串

```javascript
/**
 * 创建Date对象
 * [[Class]]属性为'Date'
 * [[Prototype]]属性为Date.prototype
 * [[Extensible]]属性为true
 * [[PrimitiveValue]]属性为指定的UTC毫秒数或时间字符串对应的UTC毫秒数，限制为前后一亿天内的毫秒数
 *   value转换为Primitive类型
 *      value为字符串时，调用Date.parse获取UTC毫秒数
 *      value为其他，转换为Number类型
 */
```

示例

```javascript
new Date(undefined) // Invalid Date
new Date(0) // Thu Jan 01 1970 08:00:00 GMT+0800 (中国标准时间)
new Date('2010') // Fri Jan 01 2010 08:00:00 GMT+0800 (中国标准时间)
new Date('2010-01-01') // Fri Jan 01 2010 08:00:00 GMT+0800 (中国标准时间)
new Date('2010-01-01T01:01') // Fri Jan 01 2010 01:01:00 GMT+0800 (中国标准时间)
new Date('2010-01-01T01:01Z') // Fri Jan 01 2010 09:01:00 GMT+0800 (中国标准时间)
new Date('2/3/2010') // Wed Feb 03 2010 00:00:00 GMT+0800 (中国标准时间)
new Date('Febraury 3, 2010') // Wed Feb 03 2010 00:00:00 GMT+0800 (中国标准时间)
```

### new Date(year, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ] )

至少2个参数，作为构造器使用，创建Date对象，指定本地时间元素

```javascript
/**
 * 创建Date对象
 * [[Class]]属性为'Date'
 * [[Prototype]]属性为Date.prototype
 * [[Extensible]]属性为true
 * [[PrimitiveValue]]属性为本地时间元素对应的UTC毫秒数，限制前后一亿天内
 *   year转换为Number类型
 *      year转换为整数在[0, 99]之内时，将year置为1900 + ToInteger(year)
 *   month转换为Number类型
 *   date转换为Number类型，默认为1
 *   hours转换为Number类型，默认为0
 *   minutes转换为Number类型，默认为0
 *   seconds转换为Number类型，默认为0
 *   ms转换为Number类型，默认为0
 */
```

示例

```javascript
new Date(2101, undefined) // Invalid Date
new Date(2010, 1) // Mon Feb 01 2010 00:00:00 GMT+0800 (中国标准时间)
new Date(10, 3) // Fri Apr 01 1910 00:00:00 GMT+0800 (中国标准时间)
new Date(2000, 4, 5, 6, 7, 8, 9) // Fri May 05 2000 06:07:08 GMT+0800 (中国标准时间)
new Date(2002, 16, 32, 25, 26, 80) // Mon Jun 02 2003 01:27:20 GMT+0800 (中国标准时间)
```

### 静态属性

```javascript
Date.[[Class]] = 'Function'
Date.[[Prototype]] = Function.Prototype
Date.[[Extensible]] = true

Date.[[DefineOwnProperty]]('length', {
  [[Value]]: 7,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
Date.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: Date,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

### 静态方法

#### Date.now()

获取当前时间对应的UTC毫秒数

```javascript
/**
 * 返回当前时间对应的UTC毫秒数
 */
```

#### Date.parse(string)

将时间字符串解析为UTC毫秒数

```javascript
/**
 * string转换为String类型，再解析为UTC毫秒数
 *   YYYY - UTC时间
 *   YYYY-MM - UTC时间
 *   YYYY-MM-DD - UTC时间
 *   YYYY-MM-DDTHH:mm - 本地时间
 *   YYYY-MM-DDTHH:mm:ss - 本地时间
 *   YYYY-MM-DDTHH:mm:ss.sss - 本地时间
 *   YYYY-MM-DDTHH:mm:ss.sssZ - 时区时间
 *   M/D/YYYY - 本地时间
 *   MMMM D, YYYY - 本地时间
 *   ddd MMMM D YYYY HH:mm:ss - 本地时间
 *   ddd MMMM D YYYY HH:mm:ss Z - UTC时间
 */
let s = ToString(s)
return parse(s)
```

#### Date.UTC(year, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ] )

将UTC时间元素转换为UTC毫秒数

```javascript
/**
 * 将UTC时间元素转换为对应的UTC毫秒数，限制前后一亿天内
 *   year转换为Number类型
 *      year转换为整数在[0, 99]之内时，将year置为1900 + ToInteger(year)
 *   month转换为Number类型
 *   date转换为Number类型，默认为1
 *   hours转换为Number类型，默认为0
 *   minutes转换为Number类型，默认为0
 *   seconds转换为Number类型，默认为0
 *   ms转换为Number类型，默认为0
 */
```

## 原型对象

Date对象的原型

```javascript
Date.prototype
date.__proto__
date.constructor.prototype
Object.getPrototypeOf(date)
```

### 原型属性

```javascript
Date.prototype.[[Class]] = 'Date'
Date.prototype.[[Prototype]] = Object.prototype
Date.prototype.[[Extensible]] = true
Date.prototype.[[PrimitiveValue]] = NaN

Date.prototype.constructor = Date
```

### 原型方法

* this不为Date对象，抛出TypeError（toJSON方法除外）

**转换方法**

#### Date.prototype.toString( )

获取Date对象的字符串表示

```javascript
/**
 * 返回Date对象的字符串表示
 *   通常为ddd MMM D YYYY HH:mm:ss GMT+时区格式
 *   非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toString.call(undefined) // 抛出TypeError

(new Date(undefined)).toString() // 'Invalid Date'
(new Date('2010-01-01')).toString() // 'Fri Jan 01 2010 08:00:00 GMT+0800 (中国标准时间)'
```

#### Date.prototype.toDateString( )

获取Date对象的日期字符串表示

```javascript
/**
 * 返回Date对象的日期字符串表示
 *   通常为ddd MMM D YYYY格式
 *   非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toDateString.call(undefined) // 抛出TypeError

(new Date(undefined)).toDateString() // 'Invalid Date'
(new Date('2010-01-01')).toDateString() // 'Fri Jan 01 2010'
```

#### Date.prototype.toTimeString( )

获取Date对象的时间字符串表示

```javascript
/**
 * 返回Date对象的时间字符串表示
 *   通常为HH:mm:ss GMT+时区格式
 *   非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toTimeString.call(undefined) // 抛出TypeError

(new Date(undefined)).toTimeString() // 'Invalid Date'
(new Date('2010-01-01')).toTimeString() // '08:00:00 GMT+0800 (中国标准时间)'
```

#### Date.prototype.toLocaleString( )

获取Date对象的本地字符串表示

```javascript
/**
 * 返回Date对象的本地字符串表示
 * 非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toLocaleString.call(undefined) // 抛出TypeError

(new Date(undefined)).toLocaleString() // 'Invalid Date'
(new Date('2010-01-01')).toLocaleString() // '2010/1/1 上午8:00:00'
```
#### Date.prototype.toLocaleDateString( )

获取Date对象的本地日期字符串表示

```javascript
/**
 * 返回Date对象的本地日期字符串表示
 * 非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toLocaleDateString.call(undefined) // 抛出TypeError

(new Date(undefined)).toLocaleDateString() // 'Invalid Date'
(new Date('2010-01-01')).toLocaleDateString() // '2010/1/1'
```

#### Date.prototype.toLocaleTimeString( )

获取Date对象的本地时间字符串表示

```javascript
/**
 * 返回Date对象的本地时间字符串表示
 * 非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toLocaleTimeString.call(undefined) // 抛出TypeError

(new Date(undefined)).toLocaleTimeString() // 'Invalid Date'
(new Date('2010-01-01')).toLocaleTimeString() // '上午8:00:00'
```

#### Date.prototype.toUTCString( )

获取Date对象的UTC时间字符串表示

```javascript
/**
 * 返回Date对象的UTC时间字符串表示
 *   通常为ddd, DD MMM YYYY HH:mm:ss GMT格式
 *   非法Date返回'Invalid Date'
 */
```

示例

```javascript
Date.prototype.toUTCString.call(undefined) // 抛出TypeError

(new Date(undefined)).toUTCString() // 'Invalid Date'
(new Date('2010-01-01')).toUTCString() // 'Fri, 01 Jan 2010 00:00:00 GMT'
```

#### Date.prototype.toISOString( )

获取Date对象的ISO时间字符串表示

```javascript
/**
 * 返回Date对象的ISO时间字符串表示
 *   通常为YYYY-MM-DDTHH:mm:ss.sssZ格式
 *   非法Date抛出RangeError
 */
```

示例

```javascript
Date.prototype.toISOString.call(undefined) // 抛出TypeError

(new Date(undefined)).toISOString() // 抛出RangeError
(new Date('2010-01-01')).toISOString() // '2010-01-01T00:00:00.000Z'
```

#### Date.prototype.toJSON()

获取Date对象的JSON字符串表示

```javascript
/**
 * this转换为Object对象O，再转换为原始值类型t，偏向Number
 * t为Number类型且不为有限数字，返回null
 * t为其他，调用O的toISOString方法，返回返回值
 *   toISOString方法不存在时，抛出TypeError
 */
```

示例

```javascript
Date.prototype.toJSON.call(undefined) // 抛出TypeError
Date.prototype.toJSON.call(NaN) // null
Date.prototype.toJSON.call(1) // 抛出TypeError

(new Date(undefined)).toJSON() // null
(new Date('2010-01-01')).toJSON() // '2010-01-01T00:00:00.000Z'
```

#### Date.prototype.valueOf( )

获取Date对象的值表示

```javascript
/**
 * 返回[[PrimitiveValue]]值
 */
```

示例

```javascript
Date.prototype.valueOf.call(undefined) // 抛出TypeError

(new Date(undefined)).valueOf() // NaN
(new Date('2010-01-01')).valueOf() // 1262304000000
```

**获取方法**

* Invalid Date返回NaN

#### Date.prototype.getTime( )

获取Date对象的时间值

```javascript
/**
 * 返回[[PrimitiveValue]]值
 */
```

示例

```javascript
Date.prototype.getTime.call(undefined) // 抛出TypeError

(new Date(undefined)).getTime() // NaN
(new Date('2010-01-01')).getTime() // 1262304000000
```

#### Date.prototype.getFullYear( )

获取Date对象的本地年

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的年
 */
```

示例

```javascript
Date.prototype.getFullYear.call(undefined) // 抛出TypeError

(new Date(undefined)).getFullYear() // NaN
(new Date('2010-01-01T00:00:00')).getFullYear() // 2010
```

#### Date.prototype.getUTCFullYear( )

获取Date对象的UTC年

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的年
 */
```

示例

```javascript
Date.prototype.getUTCFullYear.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCFullYear() // NaN
(new Date('2010-01-01T00:00')).getUTCFullYear() // 2009
```

#### Date.prototype.getMonth( )

获取Date对象的本地月，[0, 11]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的月
 */
```

示例

```javascript
Date.prototype.getMonth.call(undefined) // 抛出TypeError

(new Date(undefined)).getMonth() // NaN
(new Date('2010-01-01T00:00:00')).getMonth() // 0
```

#### Date.prototype.getUTCMonth( )

获取Date对象的UTC月，[0, 11]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的月
 */
```

示例

```javascript
Date.prototype.getUTCMonth.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCMonth() // NaN
(new Date('2010-01-01T00:00:00')).getUTCMonth() // 11
```

#### Date.prototype.getDate( )

获取Date对象的本地日，[1, 31]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的日
 */
```

示例

```javascript
Date.prototype.getDate.call(undefined) // 抛出TypeError

(new Date(undefined)).getDate() // NaN
(new Date('2010-01-01T00:00:00')).getDate() // 1
```

#### Date.prototype.getUTCDate( )

获取Date对象的UTC日，[1, 31]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的日
 */
```

示例

```javascript
Date.prototype.getUTCDate.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCDate() // NaN
(new Date('2010-01-01T00:00:00')).getUTCDate() // 31
```

#### Date.prototype.getDay( )

获取Date对象的本地星期，[0, 6]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的星期
 */
```

示例

```javascript
Date.prototype.getDay.call(undefined) // 抛出TypeError

(new Date(undefined)).getDay() // NaN
(new Date('2010-01-01T00:00:00')).getDay() // 5
```

#### Date.prototype.getUTCDay( )

获取Date对象的UTC星期，[0, 6]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的星期
 */
```

示例

```javascript
Date.prototype.getUTCDay.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCDay() // NaN
(new Date('2010-01-01T00:00:00')).getUTCDay() // 4
```

#### Date.prototype.getHours( )

获取Date对象的本地时，[0, 23]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的时
 */
```

示例

```javascript
Date.prototype.getHours.call(undefined) // 抛出TypeError

(new Date(undefined)).getHours() // NaN
(new Date('2010-01-01T00:00:00')).getHours() // 0
```

#### Date.prototype.getUTCHours( )

获取Date对象的UTC时，[0, 23]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的时
 */
```

示例

```javascript
Date.prototype.getUTCHours.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCHours() // NaN
(new Date('2010-01-01T00:00:00')).getUTCHours() // 16
```

#### Date.prototype.getMinutes( )

获取Date对象的本地分，[0, 59]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的分
 */
```

示例

```javascript
Date.prototype.getMinutes.call(undefined) // 抛出TypeError

(new Date(undefined)).getMinutes() // NaN
(new Date('2010-01-01T00:00:00')).getMinutes() // 0
```

#### Date.prototype.getUTCMinutes( )

获取Date对象的UTC分，[0, 59]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的分
 */
```

示例

```javascript
Date.prototype.getUTCMinutes.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCMinutes() // NaN
(new Date('2010-01-01T00:00:00')).getUTCMinutes() // 0
```

#### Date.prototype.getUTCSeconds( )

获取Date对象的UTC秒，[0, 59]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的秒
 */
```

示例

```javascript
Date.prototype.getUTCSeconds.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCSeconds() // NaN
(new Date('2010-01-01T00:00:00')).getUTCSeconds() // 0
```

#### Date.prototype.getMilliseconds( )

获取Date对象的本地毫秒，[0, 999]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，转换为本地时间值，返回对应的毫秒
 */
```

示例

```javascript
Date.prototype.getMilliseconds.call(undefined) // 抛出TypeError

(new Date(undefined)).getMilliseconds() // NaN
(new Date('2010-01-01T00:00:00')).getMilliseconds() // 0
```

#### Date.prototype.getUTCMilliseconds( )

获取Date对象的UTC毫秒，[0, 59]的整数

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回对应的毫秒
 */
```

示例

```javascript
Date.prototype.getUTCMilliseconds.call(undefined) // 抛出TypeError

(new Date(undefined)).getUTCMilliseconds() // NaN
(new Date('2010-01-01T00:00:00')).getUTCMilliseconds() // 0
```

#### Date.prototype.getTimezoneOffset( )

获取UTC时间和本地时间的分钟差

```javascript
/**
 * 时间值为NaN，返回NaN
 * 时间值不为NaN，返回UTC时间和本地时间的分钟差
 */
```

示例

```javascript
Date.prototype.getTimezoneOffset.call(undefined) // 抛出TypeError

(new Date(undefined)).getTimezoneOffset() // NaN
(new Date('2010-01-01T00:00:00')).getTimezoneOffset() // -480
```

**设置方法**

* 设置后日期为`Invalid Date`则返回`NaN`

#### Date.prototype.setTime(time)

设置Date对象的时间值

```javascript
/**
 * time转换为Number类型，限制为前后一亿天内的毫秒数
 * 设置[[PrimitiveValue]]属性为time，并返回
 */
```

示例

```javascript
Date.prototype.setTime.call(undefined) // 抛出TypeError

(new Date()).setTime(NaN) // NaN
(new Date(undefined)).setTime(0) // 0
(new Date('2010-01-01T00:00:00')).setTime(0) // 0
```

#### Date.prototype.setMilliseconds(ms)

设置Date对象的本地毫秒

```javascript
/**
 * ms转换为Number类型，设置本地毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setMilliseconds.call(undefined) // 抛出TypeError

(new Date()).setMilliseconds(NaN) // NaN
(new Date(undefined)).setMilliseconds(0) // NaN
(new Date('2010-01-01T00:00:00')).setMilliseconds(100) // 1262275200100
(new Date('2010-01-01T00:00:00')).setMilliseconds(2000) // 1262275202000
```

#### Date.prototype.setUTCMilliseconds(ms)

设置Date对象的UTC毫秒

```javascript
/**
 * this不为Date对象，抛出TypeError
 * ms转换为Number类型，设置UTC毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
if (Object.prototype.toString.call(this) !== '[object Date]') {
  throw TypeError
}
let t = this.[[PrimitiveValue]]
let time = MakeTime(HourFromTime(t), MinFromTime(t), SecFromTime(t), ToNumber(ms))
let v = TimeClip(MakeDate(Day(t), time))
this.[[PrimitiveValue]] = v
return v
```

示例

```javascript
Date.prototype.setUTCMilliseconds.call(undefined) // 抛出TypeError

(new Date()).setUTCMilliseconds(NaN) // NaN
(new Date(undefined)).setUTCMilliseconds(0) // NaN
(new Date('2010-01-01T00:00:00')).setUTCMilliseconds(100) // 1262275200100
(new Date('2010-01-01T00:00:00')).setUTCMilliseconds(2000) // 1262275202000
```

#### Date.prototype.setSeconds(sec [, ms ])

设置Date对象的本地秒

```javascript
/**
 * sec转换为Number类型，设置本地秒为sec
 * ms提供时转换为Number类型，设置本地毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setSeconds.length // 2 

Date.prototype.setSeconds.call(undefined) // 抛出TypeError

(new Date()).setSeconds(NaN) // NaN
(new Date(undefined)).setSeconds(0) // NaN
(new Date('2010-01-01T00:00:00')).setSeconds(1) // 1262275201000
(new Date('2010-01-01T00:00:00')).setSeconds(1, 100) // 1262275201100
(new Date('2010-01-01T00:00:00')).setSeconds(100, 2000) // 1262275302000
```

#### Date.prototype.setUTCSeconds(sec [, ms ])

设置Date对象的UTC秒

```javascript
/**
 * sec转换为Number类型，设置UTC秒为sec
 * ms提供时转换为Number类型，设置UTC毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCSeconds.length // 2 

Date.prototype.setUTCSeconds.call(undefined) // 抛出TypeError

(new Date()).setUTCSeconds(NaN) // NaN
(new Date(undefined)).setUTCSeconds(0) // NaN
(new Date('2010-01-01T00:00:00')).setUTCSeconds(1) // 1262275201000
(new Date('2010-01-01T00:00:00')).setUTCSeconds(1, 100) // 1262275201100
(new Date('2010-01-01T00:00:00')).setUTCSeconds(100, 2000) // 1262275302000
```

#### Date.prototype.setMinutes(min [, sec [, ms ] ] )

设置Date对象的本地分

```javascript
/**
 * min转换为Number类型，设置本地分为min
 * sec提供时转换为Number类型，设置本地秒为sec
 * ms提供时转换为Number类型，设置本地毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setMinutes.length // 3

Date.prototype.setMinutes.call(undefined) // 抛出TypeError

(new Date()).setMinutes(NaN) // NaN
(new Date(undefined)).setMinutes(0) // NaN
(new Date('2010-01-01T00:00:00')).setMinutes(1) // 1262275260000
(new Date('2010-01-01T00:00:00')).setMinutes(1, 1) // 1262275261000
(new Date('2010-01-01T00:00:00')).setMinutes(1, 1, 100) // 126227561100
(new Date('2010-01-01T00:00:00')).setMinutes(100, 100, 2000) // 1262281302000
```

#### Date.prototype.setUTCMinutes(min [, sec [, ms ] ] )

设置Date对象的UTC分

```javascript
/**
 * min转换为Number类型，设置UTC分为min
 * sec提供时转换为Number类型，设置UTC秒为sec
 * ms提供时转换为Number类型，设置UTC毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCMinutes.length // 3

Date.prototype.setUTCMinutes.call(undefined) // 抛出TypeError

(new Date()).setUTCMinutes(NaN) // NaN
(new Date(undefined)).setUTCMinutes(0) // NaN
(new Date('2010-01-01T00:00:00')).setUTCMinutes(1) // 1262275260000
(new Date('2010-01-01T00:00:00')).setUTCMinutes(1, 1) // 1262275261000
(new Date('2010-01-01T00:00:00')).setUTCMinutes(1, 1, 100) // 126227561100
(new Date('2010-01-01T00:00:00')).setUTCMinutes(100, 100, 2000) // 1262281302000
```

#### Date.prototype.setHours(hour [, min [, sec [, ms ] ] ])

设置Date对象的本地时

```javascript
/**
 * hour转换为Number类型，设置本地时为hour
 * min提供时转换为Number类型，设置本地秒为min
 * sec提供时转换为Number类型，设置本地秒为sec
 * ms提供时转换为Number类型，设置本地毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setHours.length // 4

Date.prototype.setHours.call(undefined) // 抛出TypeError

(new Date()).setHours(NaN) // NaN
(new Date(undefined)).setHours(0) // NaN
(new Date('2010-01-01T00:00:00')).setHours(1) // 1262278800000
(new Date('2010-01-01T00:00:00')).setHours(1, 1) // 1262278860000
(new Date('2010-01-01T00:00:00')).setHours(1, 1, 1) // 1262278861000
(new Date('2010-01-01T00:00:00')).setHours(1, 1, 1, 100) // 1262278861100
(new Date('2010-01-01T00:00:00')).setHours(100, 100, 100, 2000) // 1262641302000
```

#### Date.prototype.setUTCHours(hour [, min [, sec [, ms ] ] ])

设置Date对象的UTC时

```javascript
/**
 * hour转换为Number类型，设置UTC时为hour
 * min提供时转换为Number类型，设置UTC秒为min
 * sec提供时转换为Number类型，设置UTC秒为sec
 * ms提供时转换为Number类型，设置UTC毫秒为ms
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCHours.length // 4

Date.prototype.setUTCHours.call(undefined) // 抛出TypeError

(new Date()).setUTCHours(NaN) // NaN
(new Date(undefined)).setUTCHours(0) // NaN
(new Date('2010-01-01T00:00:00')).setUTCHours(1) // 1262221200000
(new Date('2010-01-01T00:00:00')).setUTCHours(1, 1) // 1262221260000
(new Date('2010-01-01T00:00:00')).setUTCHours(1, 1, 1) // 1262221261000
(new Date('2010-01-01T00:00:00')).setUTCHours(1, 1, 1, 100) // 1262221261100
(new Date('2010-01-01T00:00:00')).setUTCHours(100, 100, 100, 2000) // 1262583702000
```

#### Date.prototype.setDate(date)

设置Date对象的本地日

```javascript
/**
 * date转换为Number类型，设置本地日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setDate.call(undefined) // 抛出TypeError

(new Date()).setDate(NaN) // NaN
(new Date(undefined)).setDate(0)  // NaN
(new Date('2010-01-01T00:00:00')).setDate(10) // 1263052800000
(new Date('2010-01-01T00:00:00')).setDate(100) // 1270828800000
```

#### Date.prototype.setUTCDate(date)

设置Date对象的UTC日

```javascript
/**
 * date转换为Number类型，设置UTC日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCDate.call(undefined) // 抛出TypeError

(new Date()).setUTCDate(NaN) // NaN
(new Date(undefined)).setUTCDate(0)  // NaN
(new Date('2010-01-01T00:00:00')).setUTCDate(10) // 1260460800000
(new Date('2010-01-01T00:00:00')).setUTCDate(100) // 1268236800000
```

#### Date.prototype.setMonth(month [, date ] )

设置Date对象的本地月

```javascript
/**
 * month转换为Number类型，设置本地月为month
 * date提供时转换为Number类型，设置本地日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setMonth.length // 2 

Date.prototype.setMonth.call(undefined) // 抛出TypeError

(new Date()).setMonth(NaN) // NaN
(new Date(undefined)).setMonth(0) // NaN
(new Date('2010-01-01T00:00:00')).setMonth(10) // 1288540800000
(new Date('2010-01-01T00:00:00')).setMonth(10, 10) // 1289318400000
(new Date('2010-01-01T00:00:00')).setMonth(100, 100) // 1533657600000
```

#### Date.prototype.setUTCMonth(month [, date ] )

设置Date对象的UTC月

```javascript
/**
 * month转换为Number类型，设置UTC月为month
 * date提供时转换为Number类型，设置UTC日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCMonth.length // 2 

Date.prototype.setUTCMonth.call(undefined) // 抛出TypeError

(new Date()).setUTCMonth(NaN) // NaN
(new Date(undefined)).setUTCMonth(0) // NaN
(new Date('2010-01-01T00:00:00')).setUTCMonth(10) // 1259683200000
(new Date('2010-01-01T00:00:00')).setUTCMonth(10, 10) // 1257868800000
(new Date('2010-01-01T00:00:00')).setUTCMonth(100, 100) // 1502208000000
```

#### Date.prototype.setFullYear(year [, month [, date ] ] )

设置Date对象的本地年

```javascript
/**
 * 时间值为NaN时，本地时间值置为+0
 * year转换为Number类型，设置本地年为year
 * month提供时转换为Number类型，设置本地月为month
 * date提供时转换为Number类型，设置本地日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setFullYear.length // 3

Date.prototype.setFullYear.call(undefined) // 抛出TypeError

(new Date()).setFullYear(NaN) // NaN
(new Date(undefined)).setFullYear(2010) // 1262275200000
(new Date('2010-01-01T00:00:00')).setFullYear(2012) // 1325347200000
(new Date('2010-01-01T00:00:00')).setFullYear(2012, 10, 10) // 1352476800000
(new Date('2010-01-01T00:00:00')).setFullYear(2010, 100, 100) // 1533657600000
```

#### Date.prototype.setUTCFullYear(year [, month [, date ] ] )

设置Date对象的UTC年

```javascript
/**
 * 时间值为NaN时，UTC时间值置为+0
 * year转换为Number类型，设置UTC年为year
 * month提供时转换为Number类型，设置UTC月为month
 * date提供时转换为Number类型，设置UTC日为date
 * 重新计算时间值赋给[[PrimitiveValue]]属性并返回
 */
```

示例

```javascript
Date.prototype.setUTCFullYear.length // 3

Date.prototype.setUTCFullYear.call(undefined) // 抛出TypeError

(new Date()).setUTCFullYear(NaN) // NaN
(new Date(undefined)).setUTCFullYear(2010) // 1262304000000
(new Date('2010-01-01T00:00:00')).setUTCFullYear(2012) // 1356969600000
(new Date('2010-01-01T00:00:00')).setUTCFullYear(2012, 10, 10) // 1352563200000
(new Date('2010-01-01T00:00:00')).setUTCFullYear(2010, 100, 100) // 1533744000000
```

## 实例对象

[[Class]]为Date的对象

```javascript
// 通过构造器Date创建
new Date()
new Date(0)
new Date('2010-01-01')
new Date(2010, 0)
```

### 实例属性

```javascript
date.[[Class]] = 'Date'
date.[[Prototype]] = Date.prototype
date.[[Extensible]] = true
date.[[PrimitiveValue]] = timeValue
```
