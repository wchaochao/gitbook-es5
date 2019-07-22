# Boolean构造器

标签（空格分隔）： ES5

---

## 构造函数

### Boolean(value)

作为函数使用，转换为Boolean类型

```javascript
/**
 * value转换为Boolean类型
 */
```

示例

```javascript
Boolean() // false
Boolean(undefined) // false
Boolean(null) // false
Boolean(NaN) // false
Boolean(0) // false
Boolean('') // false
Boolean({}) // true
```

### new Boolean(value)

作为构造器使用，创建Boolean对象

```javascript
/**
 * 创建Boolean对象
 * [[Class]]属性为'Boolean'
 * [[Prototype]]属性为Boolean.prototype
 * [[Extensible]]属性为true
 * [[PrimitiveValue]]属性为ToBoolean(value)
 */
```

示例

```javascript
new Boolean() // Boolean{false}
new Boolean(undefined) // Boolean{false}
new Boolean(null) // Boolean{false}
new Boolean(NaN) // Boolean{false}
new Boolean(0) // Boolean{false}
new Boolean('') // Boolean{false}
new Boolean({}) // Boolean{true}
```

### 静态属性

```javascript
Boolean.[[Class]] = 'Function'
Boolean.[[Prototype]] = Function.Prototype
Boolean.[[Extensible]] = true

Boolean.[[DefineOwnProperty]]('length', {
  [[Value]]: 1,
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
Boolean.[[DefineOwnProperty]]('prototype', {
  [[Value]]: {constructor: Boolean,...},
  [[Writable]]: false,
  [[Enumerable]]: false,
  [[Configurable]]: false
}, false)
```

## 原型对象

Boolean对象的原型

```
Boolean.prototype
boo.__proto__
boo.constructor.prototype
Object.getPrototypeOf(boo)
```

### 原型属性

```javascript
Boolean.prototype.[[Class]] = 'Boolean'
Boolean.prototype.[[Prototype]] = Object.prototype
Boolean.prototype.[[Extensible]] = true
Boolean.prototype.[[Primitive]] = fasle

Boolean.prototype.constructor = Boolean
```

### 原型方法

* this不为Boolean类型或Boolean对象，抛出TypeError

#### Boolean.prototype.toString( )

获取Boolean对象的字符串表示

```javascript
/**
 * 将[[PrimitiveValue]]值转换为String类型并返回
 */
```

示例

```javascript
Boolean.prototype.toString.call(1) // 抛出TypeError
true.toString() // 'true'
```

#### Boolean.prototype.valueOf( )

获取Boolean对象的值表示

```javascript
/**
 * 返回[[PrimitiveValue]]值
 */
```

示例

```javascript
Boolean.prototype.valueOf.call(1) // 抛出TypeError
true.valueOf() // true
```

## 实例对象

[[Class]]为Boolean的对象

```javascript
// 通过构造器Boolean创建
new Boolean(1)

// 通过构造器Object创建
new Object(true)
```

### 实例属性

```javascript
B.[[Class]] = 'Boolean'
B.[[Prototype]] = Boolean.prototype
B.[[Extensible]] = true
B.[[PrimitiveValue]] = boo
```
