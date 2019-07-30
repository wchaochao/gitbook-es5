# RegExp对象

标签（空格分隔）： ES5

---

类型为`RegExp`的对象

## 构造函数

```
语法：function RegExp(pattern[, flag]) {...}
解释：创建一个正则对象
参数：pattern - 模式字符串，默认为空字符串
        空字符串对应/(?:)/
        字符串对应/pattern/, 字符串中要用\\对应pattern中的\
     flag - 标志字符串，只能为提供的标志，可包含多个标志，默认无标志
返回值：返回创建的正则对象

RegExp(pattern[, flag])等同于new RegExp(pattern[, flag])
```

### 静态属性

* `length`:`2`, 可接受的参数个数
* `prototype`: `RegExp`实例对象的原型对象，是个`Object`对象
* `__proto__`: `Function.prototype`, 原型，非标准属性

## 原型对象

```
RegExp.prototype
regexp.__proto__
regexp.constructor.prototype
Object.getPrototypeOf(regexp)
```

### 原型属性

* `constructor`: `RegExp`, 构造函数
* `__proto__`: `Object.prototype`, 原型，非标准属性

### 原型方法

**转换方法**

#### Regexp.prototype.toString()

```
语法：Regexp.prototype.toString()
解释：返回当前正则的字符串表示
返回值：返回"/pattern/flags"
```

**匹配方法**

#### RegExp.prototype.test()

```
语法：RegExp.prototype.test(str)
解释：判断是否匹配
     非全局模式 - 从0开始匹配，当前正则的lastIndex属性不变
     全局模式 - 从lastIndex开始匹配
        有匹配，lastIndex设置为紧随最近一次成功匹配的下一个位置
        无匹配，lastIndex设置为0
参数：str - 要匹配的字符串
返回值：有匹配，返回true
       无匹配，返回false
```

示例

```javascript
// 非全局模式
/cat/.test('cats and dogs') // true

// 全局模式
var r = /x/g;
var s = '_x_x';

r.lastIndex // 0
r.test(s) // true

r.lastIndex // 2
r.test(s) // true

r.lastIndex // 4
r.test(s) // false
```

#### RegExp.prototype.exec()

```
语法：RegExp.prototype.exec(str)
解释：获取匹配信息
     非全局模式 - 从0开始匹配，当前正则的lastIndex属性不变
     全局模式 - 从lastIndex开始匹配
        有匹配，lastIndex设置为紧随最近一次成功匹配的下一个位置
        无匹配，lastIndex设置为0
参数：str - 要匹配的字符串
返回值：有匹配，返回[匹配子串，...捕获组的匹配项]且arr.index=匹配子串的索引，arr.input=原始字符串
       无匹配，返回null
```

示例

```javascript
// 循环匹配
var str = "cat, bat, fat, sat";
var regexp = /.at/g;
var match = regexp.exec(str);

while (match !== null) {
  console.log(match[0]);
  match = regexp.exec(str);
}
```

## 实例对象

### 创建

```javascript
// 字面量法
var regExp=/pattern/flags;

// 构造函数法
var regExp=new RegExp(pattern[,flags]);
var regExp=RegExp(pattern[,flags]);

// ES3中正则表达式字面量始终会共享一个RegExp实例对象
// ES5中已修改为使用正则表达式字面量都会创建一个新的RegExp实例对象
```

### 实例属性

* `__proto__`: `RegExp.prototype`, 原型，非标准属性
* `global`: 是否设置了`g`标志，只读
* `ignoreCase`: 是否设置了`i`标志，只读
* `multiline`: 是否设置了`m`标志，只读
* `lastIndex`: 下次匹配的起始索引, 从0开始，可写
* `source`: 模式字符串，即`"pattern"`，只读
