# JSON对象

标签（空格分隔）： ES5

---

用于解析和转换JSON字符串

## JSON

JavaScript对象表示法(`JavaScript Object Notation`), 一种基于文本、独立于语言的轻量级数据交换格式

### JSON格式值

值的类型和格式

* `null`
* 数值: 十进制数值
  * 小数点后要有数字
  * 禁止前导`0`
  * 不能使用八进制和十六进制
  * 不能使用`NaN, Infinity, -Infinity`
* 字符串：必须使用双引号
* 布尔值：`true, false`
* 数组
  * 元素必须是JSON格式值
  * 最后一个元素后不能有逗号
* 对象
  * 属性名必须放在双引号中
  * 属性值必须是JSON格式值
  * 最后一个属性后不能有逗号

```
JSON = null
    or true or false
    or JSONNumber
    or JSONString
    or JSONObject
    or JSONArray

JSONNumber = - PositiveNumber
          or PositiveNumber
PositiveNumber = DecimalNumber
              or DecimalNumber . Digits
              or DecimalNumber . Digits ExponentPart
              or DecimalNumber ExponentPart
DecimalNumber = 0
             or OneToNine Digits
ExponentPart = e Exponent
            or E Exponent
Exponent = Digits
        or + Digits
        or - Digits
Digits = Digit
      or Digits Digit
Digit = 0 through 9
OneToNine = 1 through 9

JSONString = ""
          or " StringCharacters "
StringCharacters = StringCharacter
                or StringCharacters StringCharacter
StringCharacter = any character
                  except " or \ or U+0000 through U+001F
               or EscapeSequence
EscapeSequence = \" or \/ or \\ or \b or \f or \n or \r or \t
              or \u HexDigit HexDigit HexDigit HexDigit
HexDigit = 0 through 9
        or A through F
        or a through f

JSONObject = { }
          or { Members }
Members = JSONString : JSON
       or Members , JSONString : JSON

JSONArray = [ ]
         or [ ArrayElements ]
ArrayElements = JSON
             or ArrayElements , JSON
```

## 静态方法

### JSON.parse()

```
语法：JSON.parse(JSONstr: String[, reviver: (key, value) => any])
解释：将JSON字符串解析为JavaScript值
参数：JSONstr - JSON字符串，不符合JSON格式时抛出SyntaxError
     reviver - 变换函数，对解析后的JavaScript值进行变换，不是Function类型时不变换
        解析后的JavaScript值为数组或对象时，需要先变换里面的元素或属性值，再变换外层的值
        参数：key, 变换里层时为索引或属性名，变换最外层时为空字符串
             value, 变换里层时为元素或属性值，变换最外层时为整个值
        返回值：返回undefined, 变换里层时删除元素或属性值，变换最外层时返回undefined
               返回其他值, 变换里层时修改元素或属性值，变换最外层时返回其他值
返回值：返回解析变换后的JavaScript值
```

示例

```javascript
JSON.parse('{}') // {}
JSON.parse('true') // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse('null') // null

var o = JSON.parse('{"name": "张三"}');
o.name // 张三

var JSONStr = '{"a":1,"b":[1,2,3],"c":{"d":[4,5,6]}}';
var reviver = function (key, value) {
  console.log("[" + key + "]: " + value);
  if (key !== "") {
    return value;
  }
}

console.log(JSON.parse(JSONStr, reviver));
// "[a]: 1"
// "[0]: 1"
// "[1]: 2"
// "[2]: 3"
// "[b]: 1,2,3"
// "[0]: 4"
// "[1]: 5"
// "[2]: 6"
// "[d]: 4,5,6"
// "[c]: {"d":[4,5,6]}"
// "[]: {"a":1,"b":[1,2,3],"c":{"d":[4,5,6]}}"
// {"a":1,"b":[1,2,3],"c":{"d":[4,5,6]}}
```

### JSON.stringify()

```
语法：JSON.stringify(value: any[, replacer: Array<String> | (key, value) => any [, space: String]])
解释：将JavaScript值转换为JSON字符串
参数：value - 要转换为JSON字符串的值
        Number、String、Boolean等包装对象会转换为相应的原始值
        Undefined、函数为数组元素时转化为null, 不为数组元素时忽略
        对象存在toJSON方法时，调用toJSON(), 如Date对象
        其他对象忽略不可枚举的属性，如RegExp对象、Error对象、Math对象、JSON对象相当于{}
     replacer
        为函数时，先对value进行变换（从外往里，从前往后）
          返回值为对象或数组时，继续对返回值的属性值或元素进行变换
          返回值为undefined时，忽略该属性
          返回值为其他值时，停止往里变换
        为数组且value为对象时，数组元素代表能被序列化成JSON字符串的属性名
        其他值，忽略
     space - 缩进，用于增加返回的 JSON 字符串的可读性，最多10个字符长度
        为数字，每一级别会比上一级别缩进多这个数字值的空格
        为字符串，每一级别会比上一级别多缩进用该字符串
        其他值，不缩进
返回值：返回转换后为JSON字符串，不能转换时返回undefined
```

polyfill

```javascript
if (!JSON) {
  JSON = {
    parse: function (sJSON) {
      return eval('(' + sJSON + ')');
    },
    stringify: (function () {
      var toString = Object.prototype.toString;
      var isArray = Array.isArray || function (a) {
        return toString.call(a) === '[object Array]';
      };
      var escMap = {
        '"': '\\"',
        '\\': '\\\\',
        '\b': '\\b',
        '\f': '\\f',
        '\n': '\\n',
        '\r': '\\r',
        '\t': '\\t'
      };
      var escFunc = function (m) {
        return escMap[m] || '\\u' + (m.charCodeAt(0) + 0x10000).toString(16).substr(1);
      };
      var escRE = /[\\"\u0000-\u001F\u2028\u2029]/g;
      return function stringify(value) {
        if (value == null) {
          return 'null';
        } else if (typeof value === 'number') {
          return isFinite(value) ? value.toString() : 'null';
        } else if (typeof value === 'boolean') {
          return value.toString();
        } else if (typeof value === 'object') {
          if (typeof value.toJSON === 'function') {
            return stringify(value.toJSON());
          } else if (isArray(value)) {
            var res = '[';
            for (var i = 0; i < value.length; i++)
              res += (i ? ', ' : '') + stringify(value[i]);
            return res + ']';
          } else if (toString.call(value) === '[object Object]') {
            var tmp = [];
            for (var k in value) {
              if (value.hasOwnProperty(k))
                tmp.push(stringify(k) + ': ' + stringify(value[k]));
            }
            return '{' + tmp.join(', ') + '}';
          }
        }
        return '"' + value.toString().replace(escRE, escFunc) + '"';
      };
    })()
  };
}
```

示例

```javascript
// 字符串转换
JSON.stringify(false) // "false"
JSON.stringify('false') // "\"false\""

// 数组转换
var arr = [undefined, function () {}];
JSON.stringify(arr) // "[null,null]"

// 对象转换
var obj = {
  a: undefined,
  b: function () {}
};

JSON.stringify(obj) // "{}"

// 正则转换
JSON.stringify(/foo/) // "{}"

// 不可枚举属性
var obj = {};
Object.defineProperties(obj, {
  'foo': {
    value: 1,
    enumerable: true
  },
  'bar': {
    value: 2,
    enumerable: false
  }
});

JSON.stringify(obj); // "{"foo":1}"

// toJSON方法
var date = new Date('2015-01-01');
date.toJSON() // "2015-01-01T00:00:00.000Z"
JSON.stringify(date) // ""2015-01-01T00:00:00.000Z""
```

replacer示例

```javascript
// 指定属性
var obj = {
  'prop1': 'value1',
  'prop2': 'value2',
  'prop3': 'value3'
};

var selectedProperties = ['prop1', 'prop2'];

JSON.stringify(obj, selectedProperties) // "{"prop1":"value1","prop2":"value2"}"

// 函数变换
var o = {a: {b: 1}};

function f(key, value) {
  console.log("["+ key +"]:" + value);
  return value;
}

JSON.stringify(o, f)
// []:{a: {b: 1}}
// [a]:{b: 1}
// [b]:1
// '{"a":{"b":1}}'

// 返回对象
var o = {a: 1};

function f(key, value) {
  if (typeof value === 'object') {
    return {b: 2};
  }
  return value * 2;
}

JSON.stringify(o, f) // "{"b": 4}"

// 返回undefined
function f(key, value) {
  if (typeof(value) === "string") {
    return undefined;
  }
  return value;
}

JSON.stringify({ a: "abc", b: 123 }, f) // '{"b": 123}'
```

space示例

```javascript
// 空格缩进
JSON.stringify({ p1: 1, p2: 2 }, null, 2);
/*
"{
  "p1": 1,
  "p2": 2
}"
*/

// 字符串缩进
JSON.stringify({ p1:1, p2:2 }, null, '|-');
/*
"{
|-"p1": 1,
|-"p2": 2
}"
*/
```
