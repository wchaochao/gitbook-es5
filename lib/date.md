# Date构造器

标签（空格分隔）： ES5

---

类型为`Date`的对象

## 构造函数

```
语法：function Date() {...}
     function Date(value) {...}
     function Date(dateString: Number) {...}
     function Date(year: Number, month: Number[, day: Number[, hour: Number[, minute: Number[, second: Number[, millisecond: Number]]]]]) {...}
解释：创建一个Date对象
参数：为空时会依据系统设置的当前时间创建一个Date对象
     value - 自1970年1月1日00:00:00(UTC时间)过去的毫秒数，自动转换为整数，可为负，NaN返回Invalid Date
     dateString - date字符串，同Date.Parse()中的参数
     时间参数 - 同Date.UTC()中的参数，不过为本地时间参数
返回值：返回创建的Date对象，不能创建时返回Invalid Date

Date(args)返回Date对象的字符串表示，与new Date(args)不同
```

### 静态属性

* `length`:`7`, 可接受的参数个数
* `prototype`: `Date`实例对象的原型对象，是个`Object`对象
* `__proto__`: `Function.prototype`, 原型，非标准属性

### 静态方法

#### Date.parse()

```
语法：Date.parse(dateString)
解释：解析date字符串
参数：dateString - date字符串，格式如下
        M/D/YYYY - 本地时间
        MMMM D, YYYY - 本地时间
        ddd MMMM D YYYY HH:mm:ss - 本地时间
        ddd MMMM D YYYY HH:mm:ss Z - UTC时间
        YYYY-MM-DD - UTC时间
        YYYY-MM-DDTHH:mm:ss.sss - 本地时间
        YYYY-MM-DDTHH:mm:ss.sssZ - UTC时间
返回值：可以解析，返回对应的毫秒数
       无法解析，返回NaN
```

#### Date.UTC()

```
语法：Date.UTC(year: Number, month: Number[, day: Number[, hour: Number[, minute: Number[, second: Number[, millisecond: Number]]]]])
解释：解析UTC时间参数
参数：时间参数 - 为UTC时间，自动转换为整数，为NaN时无法解析
        year - 年份，最好指定4位年份，0~99之间的整数加1900
        month - 月份，0~11之间，超出范围自动进位或借位
        day - 天数，0~31之间，超出范围自动进位或借位，为空时当作1
        hour - 小时数，0~23之间，超出范围自动进位或借位，为空时当作0
        minute - 分钟数，0~59之间，超出范围自动进位或借位，为空时当作0
        second - 秒数，0~59之间，超出范围自动进位或借位，为空时当作0
        millisecond - 毫秒数，0~999之间，超出范围自动进位或借位，为空时当作0
返回值：可以解析，返回对应的毫秒数
       无法解析，返回NaN
```

#### Date.now()

```
语法：Date.now()
解释：返回当前时间对应的毫秒数
```

polyfill

```
if (typeof Date.now !== "function") {
  Date.now = function () {
    return new Date().getTime();
  }
}
```

## 原型对象

```
Date.prototype
date.__proto__
date.constructor.prototype
Object.getPrototypeOf(date)
```

### 原型属性

* `constructor`: `Date`, 构造函数
* `__proto__`: `Object.prototype`, 原型，非标准属性

### 原型方法

**格式化方法**

#### Date.prototype.valueOf()

```
语法：Date.prototype.valueOf()
解释：返回当前Date对象的值表示
返回值：返回从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数，Invalid Date返回NaN
```

#### Date.prototype.toString()

```
语法：Date.prototype.toString()
解释：返回当前Date对象的字符串表示，通常为ddd MMM D YYYY HH:mm:ss GMT+时区格式，Invalid Date返回"Invalid Date"
```

#### Date.prototype.toDateString()

```
语法：Date.prototype.toDateString()
解释：返回当前Date对象的日期字符串，通常为ddd MMM D YYYY格式，Invalid Date返回"Invalid Date"
```

#### Date.prototype.toTimeString()

```
语法：Date.prototype.toTimeString()
解释：返回当前Date对象的时间字符串，通常为HH:mm:ss GMT+时区格式，Invalid Date返回"Invalid Date"
```

#### Date.prototype.toLocaleString()

```
语法：Date.prototype.toLocaleString([locales: String | Array<String> [, options: Object]])
解释：返回当前Date对象的本地字符串表示，Invalid Date返回"Invalid Date"
参数：locales - 区域
     options - 可选配置
```

#### Date.prototype.toLocaleDateString()

```
语法：Date.prototype.toLocaleDateString([locales: String | Array<String> [, options: Object]])
解释：返回当前Date对象的本地日期字符串表示，Invalid Date返回"Invalid Date"
参数：locales - 区域
     options - 可选配置
```

#### Date.prototype.toLocaleTimeString()

```
语法：Date.prototype.toLocaleTimeString([locales: String | Array<String> [, options: Object]])
解释：返回当前Date对象的本地时间字符串表示，Invalid Date返回"Invalid Date"
参数：locales - 区域
     options - 可选配置
```

#### Date.prototype.toUTCString()

```
语法：Date.prototype.toUTCString()
解释：返回当前Date对象的UTC时间字符串，通常为ddd, D MMM YYYY HH:mm:ss GMT格式，Invalid Date返回"Invalid Date"
```

#### Date.prototype.toISOString()

```
语法：Date.prototype.toISOString()
解释：返回当前Date对象的UTC时间ISO格式字符串，通常为YYYY-MM-DDTHH:mm:ss.sssZ格式，Invalid Date抛出RangeError
```

#### Date.prototype.toJSON()

```
语法：Date.prototype.toJSON()
解释：返回当前Date对象的JSON格式字符串，通常为YYYY-MM-DDTHH:mm:ss.sssZ格式，Invalid Date返回null
```

**获取方法**

`Invalid Date`返回`NaN`

#### Date.prototype.getTime()

```
语法：Date.prototype.getTime()
解释：返回从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.getFullYear()

```
语法：Date.prototype.getFullYear()
解释：根据本地时间返回当前Date对象的年份
```

#### Date.prototype.getMonth()

```
语法：Date.prototype.getMonth()
解释：根据本地时间返回当前Date对象的月份(0~11)
```

#### Date.prototype.getDate()

```
语法：Date.prototype.getDate()
解释：根据本地时间返回当前Date对象的天数(1~31)
```

#### Date.prototype.getDay()

```
语法：Date.prototype.getDay()
解释：根据本地时间返回当前Date对象的星期中的第几天，0(星期天)到6(星期六)
```

#### Date.prototype.getHours()

```
语法：Date.prototype.getHours()
解释：根据本地时间返回当前Date对象的小时数(0~23)
```

#### Date.prototype.getMinutes()

```
语法：Date.prototype.getMinutes()
解释：根据本地时间返回当前Date对象的分钟数(0~59)
```

#### Date.prototype.getSeconds()

```
语法：Date.prototype.getSeconds()
解释：根据本地时间返回当前Date对象的秒数(0~59)
```

#### Date.prototype.getMilliseconds()

```
语法：Date.prototype.getMilliseconds()
解释：根据本地时间返回当前Date对象的毫秒数(0~999)
```

#### Date.prototype.getTimezoneOffset()

```
语法：Date.prototype.getTimezoneOffset()
解释：返回当前时区的偏移分钟数
```

#### Date.prototype.getUTCFullYear()

```
语法：Date.prototype.getUTCFullYear()
解释：根据UTC时间返回当前Date对象的年份
```

#### Date.prototype.getUTCMonth()

```
语法：Date.prototype.getUTCMonth()
解释：根据UTC时间返回当前Date对象的月份(0~11)
```

#### Date.prototype.getUTCDate()

```
语法：Date.prototype.getUTCDate()
解释：根据UTC时间返回当前Date对象的天数(1~31)
```

#### Date.prototype.getUTCDay()

```
语法：Date.prototype.getUTCDay()
解释：根据UTC时间返回当前Date对象的星期中的第几天，0(星期天)到6(星期六)
```

#### Date.prototype.getUTCHours()

```
语法：Date.prototype.getUTCHours()
解释：根据UTC时间返回当前Date对象的小时数(0~23)
```

#### Date.prototype.getUTCMinutes()

```
语法：Date.prototype.getUTCMinutes()
解释：根据UTC时间返回当前Date对象的分钟数(0~59)
```

#### Date.prototype.getUTCSeconds()

```
语法：Date.prototype.getUTCSeconds()
解释：根据UTC时间返回当前Date对象的秒数(0~59)
```

#### Date.prototype.getUTCMilliseconds()

```
语法：Date.prototype.getUTCMilliseconds()
解释：根据UTC时间返回当前Date对象的毫秒数(0~999)
```

**设置方法**

设置后日期为`Invalid Date`则返回`NaN`

#### Date.prototype.setTime()

```
语法：Date.prototype.setTime(value: Number)
解释：设置当前Date对象的总毫秒数
参数：value - 自1970年1月1日00:00:00(UTC时间)过去的毫秒数，自动转换为整数，可为负
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setFullYear()

```
语法：Date.prototype.setFullYear(year: Number[, month: Number[, day: Number]])
解释：根据本地时间设置当前Date对象的年份
参数：year - 年份，自动转换为整数
     month - 月份，自动转换为整数，0~11之间，超出范围自动进位或借位
     day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setMonth()

```
语法：Date.prototype.setMonth(month: Number[, day: Number])
解释：根据本地时间设置当前Date对象的月份
参数：month - 月份，自动转换为整数，0~11之间，超出范围自动进位或借位
     day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setDate()

```
语法：Date.prototype.setDate(day: Number)
解释：根据本地时间设置当前Date对象的天数
参数：day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setHours()

```
语法：Date.prototype.setHours(hour: Number[, minute: Number[, second: Number[, millisecond: Number]]])
解释：根据本地时间设置当前Date对象的小时数
参数：hour - 小时数，自动转换为整数，0~23之间，超出范围自动进位或借位
     minute - 分钟数，自动转换为整数，0~59之间，超出范围自动进位或借位
     second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setMinutes()

```
语法：Date.prototype.setMinutes(minute: Number[, second: Number[, millisecond: Number]])
解释：根据本地时间设置当前Date对象的分钟数
参数：minute - 分钟数，自动转换为整数，0~59之间，超出范围自动进位或借位
     second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond, 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setSeconds()

```
语法：Date.prototype.setSeconds(second: Number[, millisecond: Number])
解释：根据本地时间设置当前Date对象的秒数
参数：second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setMilliseconds()

```
语法：Date.prototype.setMilliseconds(millisecond)
解释：根据本地时间设置当前Date对象的豪秒数
参数：millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCFullYear()

```
语法：Date.prototype.setUTCFullYear(year: Number[, month: Number[, day: Number]])
解释：根据UTC时间设置当前Date对象的年份
参数：year - 年份，自动转换为整数
     month - 月份，自动转换为整数，0~11之间，超出范围自动进位或借位
     day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCMonth()

```
语法：Date.prototype.setUTCMonth(month: Number[, day: Number])
解释：根据UTC时间设置当前Date对象的月份
参数：month - 月份，自动转换为整数，0~11之间，超出范围自动进位或借位
     day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCDate()

```
语法：Date.prototype.setUTCDate(day: Number)
解释：根据UTC时间设置当前Date对象的天数
参数：day - 天数，自动转换为整数，0~31之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCHours()

```
语法：Date.prototype.setUTCHours(hour: Number[, minute: Number[, second: Number[, millisecond: Number]]])
解释：根据UTC时间设置当前Date对象的小时数
参数：hour - 小时数，自动转换为整数，0~23之间，超出范围自动进位或借位
     minute - 分钟数，自动转换为整数，0~59之间，超出范围自动进位或借位
     second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCMinutes()

```
语法：Date.prototype.setUTCMinutes(minute: Number[, second: Number[, millisecond: Number]])
解释：根据UTC时间设置当前Date对象的分钟数
参数：minute - 分钟数，自动转换为整数，0~59之间，超出范围自动进位或借位
     second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCSeconds()

```
语法：Date.prototype.setUTCSeconds(second: Number[, millisecond: Number])
解释：根据UTC时间设置当前Date对象的秒数
参数：second - 秒数，自动转换为整数，0~59之间，超出范围自动进位或借位
     millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

#### Date.prototype.setUTCMilliseconds()

```
语法：Date.prototype.setUTCMilliseconds(millisecond: Number)
解释：根据UTC时间设置当前Date对象的豪秒数
参数：millisecond - 毫秒数，自动转换为整数，0~999之间，超出范围自动进位或借位
返回：返回设置后从1970年1月1日00:00:00(UTC时间)到该日期的毫秒数
```

## 实例对象

### 创建

```javascript
// 构造函数法
var date = new Date(args);
```

### 实例属性

* `__proto__`: `Date.prototype`, 原型，非标准属性
