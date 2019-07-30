# Console对象

标签（空格分隔）： ES5

---

输出信息到控制台

## console.log()

```
语法：console.log(...value)
      console.log(...msg)
      console.log('String: %s, Int: %d, Float: %f, Object: %o, CssStyle: %c', str, ints, floats, obj, CssStyle)
解释：输出信息，自带换行符
```

示例

```javascript
// 值
console.log({foo: 'bar'}) // Object {foo: "bar"}

// 字符串
console.log('a', 'b', 'c') // a b c

// 格式字符串
console.log('%d %s balloons', 99, 'red'); // 99 red balloons
console.log('%cThis text is styled!', 'color: red; background: yellow; font-size: 24px;') // 黄底红字的This text is styled

// 混合
console.log(' %s + %s ', 1, 1, '= 2', true) // 1 + 1  = 2, true
```

## console.info()

同console.log, 有信息图标

## console.warn()

同console.log, 有警告图标

## console.error()

同console.log, 有错误图标并显示错误堆栈

## console.dir()

```
语法：console.dir(object: Object)
解释：以树的形式输出对象
```

## console.dirxml()

```
语法：console.dirxml(object: Object)
解释：以树的形式输出DOM对象
```

## console.table()

```
语法：console.table(data: Array | Object [, columns: Array<String>])
解释：使用表格显示数据
参数：data - 数组或对象数据
      columns - 要显示的列名数组
```

示例

```javascript
// 数组
console.table(["apples", "oranges", "bananas"]);

var languages = [
  { name: "JavaScript", fileExtension: ".js" },
  { name: "TypeScript", fileExtension: ".ts" },
  { name: "CoffeeScript", fileExtension: ".coffee" }
];

console.table(languages);

// 对象
console.table({firstName: "John", lastName: "Smith"});

var languages = {
  csharp: { name: "C#", paradigm: "object-oriented" },
  fsharp: { name: "F#", paradigm: "functional" }
};

console.table(languages);
console.table(languages, ["name"])
```

## console.count()

```
语法：console.count([label: String])
解释：按标签输出调用次数
参数：label - 标签字符串
```

示例

```javascript
// 无标签
function greet(user) {
  console.count();
  return 'hi ' + user;
}

greet('bob')
//  : 1
// "hi bob"

greet('alice')
//  : 2
// "hi alice"

greet('bob')
//  : 3
// "hi bob"

// 有标签
function greet(user) {
  console.count(user);
  return "hi " + user;
}

greet('bob')
// bob: 1
// "hi bob"

greet('alice')
// alice: 1
// "hi alice"

greet('bob')
// bob: 2
// "hi bob"
```

## console.assert()

```
语法：console.assert(assertion, ...value: any)
      console.assert(assertion, ...msg: String)
解释：断言失败时，显示错误信息
参数：assertion - 断言表达式
      ...value, ...msg - 错误信息
```

示例

```javascript
console.assert(false, '判断条件不成立')
// Assertion failed: 判断条件不成立
```

## console.time()

```
语法：console.time(timerName: String)
解释：开始计时
参数：timerName - 计时器名称
```

## console.timeEnd()

```
语法：console.timeEnd(timerName: String)
解释：结束计时
参数：timerName - 计时器名称
```

示例

```javascript
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```

## console.group

```
语法：console.group(groupName: String)
解释：分组输出信息，默认展开
参数：groupName - 组名
```

## console.groupCollapsed

```
语法：console.groupCollapsed(groupName: String)
解释：分组输出信息，默认折叠
参数：groupName - 组名
```

## console.groupEnd

```
语法：console.groupEnd()
解释：结束分组
```

示例

```javscript
console.group('一级分组');
console.log('一级分组的内容');

console.group('二级分组');
console.log('二级分组的内容');

console.groupEnd(); // 二级分组结束
console.groupEnd(); // 一级分组结束
```

## console.clear()

```
语法：console.clear()
解释：清空输出信息
```
