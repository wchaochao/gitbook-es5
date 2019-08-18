# JSON对象

标签（空格分隔）： ES5

---

## 属性

```javascript
JSON.[[Class]] = 'JSON'
JSON.[[Prototype]] = 'Object.prototype'
JSON.[[Extensible]] = true
```

## 方法

### JSON.parse(text [ , reviver ])

将JSON格式的字符串转换为JavaScript值

```javascript
/**
 * text转换为String类型
 *   不符合JSON格式时，抛出SyntaxError
 *   符合JSON格式时，解析成JavaScript值unfiltered
 * reviver不为函数时，直接返回unfiltered
 * reviver为函数时，使用递归函数Walk对unfiltered进行过滤转换，Walk接收对象和属性两个参数，初始参数为{'': unfiltered}和''
 *   使用对象和属性获取属性值
 *   该属性值为数组时，先对每个元素进行Walk处理，参数为数组和索引
 *      返回值为undefined时，删除该元素
 *      返回值为其他时，修改该元素为返回值
 *   该属性值为对象时，对每个可枚举属性进行Walk处理，参数为对象和属性
 *      返回值为undefined时，删除该元素
 *      返回值为其他时，修改该元素为返回值
 *   最后调用reviver函数，this为对象，参数为属性和属性值，返回返回值
 */
```

示例

```javascript
// 无reviver
JSON.parse('undefined') // 抛出SyntaxError
JSON.parse('null') // null
JSON.parse('true') // true
JSON.parse('12.3') // 12.3
JSON.parse('"abc"') // 'abc'
JSON.parse('{"a": 1}') // {a: 1}
JSON.parse('["a"]') // ['a']

// 有reviver
function reviver (key, val) {
 console.log('[' + key + ']: ' + val)
  return val
}

JSON.parse('123', reviver)
// []: 123

JSON.parse('{"a":1,"b":[1,2,3],"c":{"d":[4,5,6]}}', reviver)
// [a]: 1
// [0]: 1
// [1]: 2
// [2]: 3
// [b]: [1, 2, 3]
// [0]: 4
// [1]: 5
// [2]: 6
// [d]: 4,5,6
// [c]: {d: [4, 5, 6]}
// []: {a: 1, b: [1, 2, 3], c: {d:[4, 5, 6]}}

JSON.parse('{"a": 1, "b": [1, 2, 3]}', (key, value) => {
  if (key === 'a' || key === '1') {
    return undefined
  } else {
    return value
  }
}) // {b: [1, empty, 3]}
```

### stringify(value [ , replacer [ , space ] ])

将JavaScript值转换为JSON格式的字符串

```javascript
/**
 * value包装成{'': value}对象
 * replacer为函数时，replacerFunction为replacer
 * replacer为数组时，挑选为Number类型、Number对象、String类型、String对象的元素转换为String类型，push进PropertyList
 * space为Number类型或Number对象时，转换为Number类型，限制在[0, 10]内，gap为space个空格
 * space为String类型或String对象时，gap为space前10个字符
 * space为其他时，gap为空字符串
 * 调用Str函数，接收对象和属性两个参数，初始参数为{'': value}和''，返回返回值
 *   使用对象和属性获取属性值
 *   属性值为对象且有toJSON方法时，调用toJSON方法，属性值置为返回值
 *   replacerFunction函数存在时，调用replacerFunction方法，this为对象，参数为属性名和属性值，属性值置为返回值
 *   属性值为Number对象时，转换为Number类型
 *   属性值为String对象时，转换为String类型
 *   属性值为Boolean对象时，属性值置为[[PrimitiveValue]]值
 *   属性值为Null或Boolean类型时，转换为String类型并返回
 *   属性值为Number类型时
 *      属性值为有限值，转换为String类型并返回
 *      属性值不为有限值，返回'null'
 *   属性值为String类型时，进行Quate处理
 *      使用双引号包裹
 *      "、\、\b、\f、\n、\r、\r加\
 *      \u0020前的字符改为\\u
 *   属性值为数组时，进行JA处理
 *      将元素处理为Str(holder, index)形式
 *         Str函数返回值为undefined时置为'null'
 *      无gap时返回'[' + properties + ']'，属性分隔符为','
 *      有gap时返回'[' + sparator + properties + '\n' + lastIndent + ']'，属性分隔符为',\n' + indent
 *   属性值为对象且不为函数时，进行JO处理
 *      将白名单属性或可枚举属性处理为"key":Str(holder, key)形式
 *         Str函数返回值为undefined时忽略
 *         有gap时:后有空格
 *      无gap时返回'{' + properties + '}'，属性分隔符为','
 *      有gap时返回'{' + sparator + properties + '\n' + lastIndent + '}'，属性分隔符为',\n' + indent
 *   属性值为其他值，返回undefined
 */
```

示例

```javascript
// 原始值
JSON.stringify(undefined) // undefined
JSON.stringify(null) // 'null'
JSON.stringify(true) // 'true'
JSON.stringify(12) // '12'
JSON.stringify('a') // '"a"'
JSON.stringify('"') // '"\\""'
JSON.stringify('\u0000') // '"\\u0000"'

// 特殊对象
JSON.stringify(new Number(12)) // '12'
JSON.stringify(function () {}) // undefined
JSON.stringify(new Date()) // '"2019-08-15T08:32:28.452Z"'

// 对象
let o = {a: 1, b: {c: 2}}
JSON.stringify(o) // '{"a":1,"b":{"c":2}}'

JSON.stringify(o, null, 2)
// '{
//   "a": 1,
//   "b": {
//     "c": 2
//   }
// }'
JSON.stringify(o, null, '|-')
// '{
// |-"a": 1,
// |-"b": {
// |-|-"c": 2
// |-}
// }'

function replacer (key, val) {
 console.log('[' + key + ']: ' + val)
  return val
}
JSON.stringify(o, replacer)
// []: [object Object]
// [a]: 1
// [b]: [object Object]
// [c]: 2
// '{"a":1,"b":{"c":2}}'

let whiteList = ['a', 'c']
JSON.stringify(o, whiteList) // '{"a":1}'

// 数组
let arr = [undefined, 1, {a: 2}]
JSON.stringify(arr) // '[null,1,{"a":2}]'
JSON.stringify(arr, [1, 2]) // '[null,1,{}]'
JSON.stringify(arr, null, 2)
// '[
//   null,
//   1,
//   {
//     "a": 2
//   }
//  ]'

// 循环引用
let a = []
a[0] = a
JSON.stringify(a) // 抛出TypeError
```
