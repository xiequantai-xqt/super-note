# 基础概念

## 数据类型

### 一、JavaScript有哪些数据类型，它们的区别？

JavaScript的数据类型可以分为两大类，基本数据类型和引用数据类型。

基本数据类型：

1. Number: 表示数字，可以是整数或浮点数，包括Infinity、-Infinity和NaN（非数字）。
2. String: 表示文本，由零个或多个字符组成，使用单引号(' ')或双引号(" ")包围。
3. Boolean: 只有两个值：true 和 false，用于逻辑判断。
4. Null: 表示一个刻意的空值，只有一个值null，用来表示一个变量被赋值为空对象指针。
5. Undefined: 表示变量已被声明但未被赋值，只有一个值undefined。
6. BigInt: 用于存储超过常规Number类型安全整数范围的大整数。
7. Symbol: ES6引入的新类型，表示独一无二的值，常用于对象的唯一属性键。

引用数据类型：

1. Object: 包括普通对象、数组(Array)、函数(Function)等，存储在堆内存中，变量实际存储的是指向这些数据的引用（地址）。

数据类型的区别：

1. 存储方式：基本数据类型直接存储值，存储在栈内存中；引用数据类型在栈中存储的是引用地址，数据本身存储在堆内存中。
2. 复制行为：基本数据类型的变量复制给另一个变量时，会创建一个新的值，两者互不影响。而引用数据类型复制时，复制的是引用，因此改变其中一个变量的值可能会影响到另一个。
3. 值的比较：基本数据类型使用==或===比较时，直接比较值或者类型是否相等。引用数据类型使用==比较可能会发生类型转换，使用===则要求类型和值都相等。
4. 内存占用：基本数据类型占用的内存相对固定且较小。引用数据类型根据数据的实际大小动态分配内存，可能占用更多内存空间。

### 二、数据类型检测的方式有哪些？

1. typeof：返回一个表示变量数据类型的字符串。对于基本类型值（不包括null和undefined）和函数非常准确。
2. instanceof：用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上，以此判断该对象是否是这个构造函数的实例。

```javascript
variable instanceof Constructor // 语法
[] instanceof Array  // true
```

3. constructor：每个对象都有一个内置的constructor属性，指向创建该对象的构造函数。但这个属性可以被修改，所以不是完全可靠。

```javascript
variable.constructor === Constructor // 语法
(new Date()).constructor === Date  // true
```

4. Object.prototype.toString.call()：是最准确的数据类型检测方法之一，可以区分所有基本类型和引用类型，包括null和undefined。

```javascript
Object.prototype.toString.call(variable)  // 语法
Object.prototype.toString.call([])  // "[object Array]"
```

### 三、判断数组的方式有哪些？

1. Array.isArray()

   - 用途：ES5引入的标准方法，专门用来判断一个值是否为数组。

   - 语法：Array.isArray(variable)

   - 例子：Array.isArray([]) 返回 true。

2. instanceof

   - 用途：检查一个对象是否是某个构造函数的实例。

   - 语法：variable instanceof Array

   - 例子：[] instanceof Array 返回 true。

3. 对象的constructor属性

   - 用途：检查对象的constructor属性是否指向Array构造函数。

   - 语法：variable.constructor === Array

   - 注意：此方法可能因constructor被重写而不准确。

4. 检查`__proto__`

   - 用途：检查对象的`__proto__`属性是否等于Array.prototype。

   - 语法：`variable.__proto__ === Array.prototype`

   - 注意：`__proto__`属性在某些旧的或不兼容的环境中可能不存在。

5. toString()方法

   - 用途：调用对象的toString()方法，返回"[object Array]"表示是数组。

   - 语法：Object.prototype.toString.call(variable) === "[object Array]"

   - 优点：这种方法比较通用，适用于各种情况，包括跨环境。

在实际开发中，Array.isArray()通常是首选方法，因为它是最安全和最标准的。其他方法在某些特定情况下可能不可靠，尤其是当涉及到对象的原型链被篡改时。

### 四、null和undefined区别？

1. 类型差异：

   - undefined是一种基本数据类型，其类型本身即为undefined。

   - null也是一种基本数据类型，但有趣的是，使用typeof操作符检查null时，会返回"object"，这是一个历史遗留问题，实际上它并不是对象类型。

2. 含义差异：

   - undefined通常表示变量已声明但尚未被赋值，或者声明前使用变量，再或者函数没有返回值的情况。

   - null则常常被用作一个故意设置的空值，表示某个变量意在指向一个对象，但现在没有指向任何对象。

3. 逻辑比较：

   - 在宽松相等(==)比较中，null和undefined被认为是相等的，因为它们都代表“无值”。

   - 使用严格相等(===)时，它们不相等，因为它们是两种不同的数据类型。

4. 转换行为：

   - 在转换为布尔值时，两者都会被转换为false。

   - 在转换为数值时，undefined转换为NaN，而null转换为0。

### 五、map和Object的区别？

1. 键的类型：Map的键类型可以是任意类型，Object的键类型只能是string或者Symbol。
2. 遍历顺序：遍历Map对象时，会按照插入的顺序返回键值对。Object的遍历顺序在不同的JS引擎下可能是不同的。
3. 获取属性值：Map通过get方法获取指定键的值，Object通过 点语法 或者 方括号 的语法访问属性值。
4. 使用场景：当需要频繁操作数据，同时键的类型比较复杂时，可以选择Map。

### 六、map和weakMap的区别？

1. 键的类型：Map的键类型可以是任意类型，WeakMap的键类型只能是对象。
2. 内存管理：Map中的键值对只要没有被显式删除，就会一直存在于内存中，会阻止垃圾回收器回收作为键的对象，即使在代码的其他地方不再使用这个对象。当一个对象作为键被添加到  WeakMap  后，如果在  WeakMap  之外没有对这个对象的其他引用，垃圾回收器可以在适当的时候回收这个对象及其相关的键值对。这有助于防止内存泄漏，特别是在处理对象缓存等场景时非常有用。
3. 可枚举性：Map对象是可枚举的，可以通过entries()获取迭代器。WeakMap是不可枚举的，因为  WeakMap  的键是弱引用，其内容随时会因为垃圾回收而改变，所以不适合提供遍历机制。

### 七、其他值到字符串的转换规则？

1. Null 和 Undefined 类型 ，null 转换为 "null"，undefined 转换为 "undefined"，
2. Boolean 类型，true 转换为 "true"，false 转换为 "false"。
3. Number 类型的值直接转换，不过那些极小和极大的数字会使用指数形式。
4. Symbol 类型的值直接转换，但是只允许显式强制类型转换，使用隐式强制类型转换会产生错误。
5. 对普通对象来说，除非自行定义 toString() 方法，否则会调用 toString()（Object.prototype.toString()）来返回内部属性 [[Class]] 的值，如"[object Object]"。如果对象有自己的 toString() 方法，字符串化时就会调用该方法并使用其返回值。

### 八、其他值到数字值的转换规则？

1. Undefined 类型的值转换为 NaN。
2. Null 类型的值转换为 0。
3. Boolean 类型的值，true 转换为 1，false 转换为 0。
4. String 类型的值转换如同使用 Number() 函数进行转换，如果包含非数字值则转换为 NaN，空字符串为 0。
5. Symbol 类型的值不能转换为数字，会报错。
6. 对象（包括数组）会首先被转换为相应的基本类型值，如果返回的是非数字的基本类型值，则再遵循以上规则将其强制转换为数字。

### 九、其他值到布尔类型的值的转换规则？

以下这些是假值：

1. undefined
2. null
3. false
4. +0、-0
5. NaN
6. ""

假值的布尔强制类型转换结果为 false。从逻辑上说，假值列表以外的都应该是真值。

### 十、substring和substr函数的区别是什么？

从兼容性方面来说，substring 是 JavaScript 标准方法，在各种新旧浏览器中兼容性良好，自 ECMAScript 1 起就被支持。substr 虽被广泛支持，但已被标记为非标准方法，在未来的 JavaScript 版本或严格环境中可能被废弃或修改，不过目前主流浏览器如 Chrome、Firefox、Safari 等仍支持它。

在实际应用场景中，substring 更适用于依据明确的索引位置范围提取子字符串，比如从文件路径中提取文件名。而 substr 侧重于从指定起始位置提取固定长度的字符串，例如从固定格式的短信内容里提取特定长度的验证码等。

## 变量声明

### 一、let、const、var的区别？

1. 作用域：

   - var: 在函数作用域或全局作用域中声明变量。在函数外部声明的 var 变量会成为全局变量。在函数内部，var 会被提升至函数作用域的顶部。

   - let 和 const: 引入了块级作用域的概念。这意味着它们声明的变量仅在其所在的代码块（如 if 语句、for 循环或其他大括号包裹的任意代码块）内有效。let 和 const 不会被提升至块级作用域的顶部。

2. 变量重新赋值

   - var和let: 允许变量被重新赋值。

   - const: 声明的是常量，一旦赋值就不能再次更改，如果试图重新赋值给 const 变量会导致错误。如果是引用数据类型，虽然不能重新赋值整个变量，但可以修改其内部属性或元素。

3. 变量提升

   - var: 存在变量提升现象，可以在声明之前访问变量，此时值为 undefined。

   - let 和 const: 没有变量提升到作用域顶部的现象，如果在声明前访问，会引发 ReferenceError。

4. 暂时性死区
   - let 和 const: 在它们声明之前的区域被称为暂时性死区，在这个区域内访问这些变量会报错。

### 二、const对象的属性可以修改吗？

在JS中，当使用const关键字声明并且初始化一个对象，这个变量实际上保存的是指向那个对象的一个引用地址。这个地址是固定的，引用地址指向的内存是可以修改的。

## 运算符

### 一、typeof null 的结果是什么，为什么？

typeof null 的结果是 "object"。原因是JavaScript最初实现的时候，所有值都被设计为可以存储在一个32位的单元中，其中包含一个类型标签来指示值的类型。null 值的二进制表示是全0，这在当时的类型标记系统中恰好与对象类型的标记相匹配。因此，当对 null 应用 typeof 操作符时，它会错误地被识别为 "object"。尽管这一行为被认为是一个错误，由于修正它会导致大量依赖现有行为的代码出现问题，因此这一特征就被保留了下来。

### 二、intanceof 操作符的实现原理?

instanceof 操作符用于判断一个对象是否是另一个对象的实例，或者是否在其原型链上存在另一个对象的构造函数。它的实现原理基于JavaScript的原型链机制。

### 三、typeof 与 instanceof 区别？

1. 作用不同：typeof 主要用于检测基本数据类型，而 instanceof 用于检查对象是否属于特定类或构造函数的实例。
2. 适用范围不同：typeof 对于原始值和函数非常有效，但对于所有对象（包括数组和 null）都返回 "object"。instanceof 则主要用于对象，特别是当需要区分不同类型的对象时。
3. 实现原理不同：typeof 是基于值的类型直接判断，而 instanceof 是通过原型链来判断一个对象是否是某个构造函数的实例。

## 浮点数

### 一、为什么0.1+0.2 ! == 0.3，如何让其相等？

这个现象出现是因为浮点数的表示和计算存在精度问题。

1. 使用容差比较：定义一个很小的正数作为容差，然后比较两个浮点数之差的绝对值是否小于这个容差。

```javascript
   function isEqualWithPrecision(a, b, precision = 1e-15) {
     return Math.abs(a - b) < precision;
   }
   console.log(isEqualWithPrecision(0.1 + 0.2, 0.3)); // 输出：true
```

2. 使用toFixed方法：将浮点数转换为字符串，指定小数点后的位数，然后再转回数字进行比较。但这种方法也有其局限性，特别是当涉及较大或较小的数值时，可能会有信息丢失。

```javascript
   console.log((0.1 + 0.2).toFixed(10) === '0.3'); // 注意：这种方法在特定情况下可能不准确
```

## 深拷贝&浅拷贝

### 一、object.assign和扩展运算法是深拷贝还是浅拷贝，两者区别？

两者都是浅拷贝的方式。

区别：

- Object.assign() 方法可以将所有可枚举的属性的值从一个或多个源对象复制到目标对象，返回值是目标对象。
- 扩展运算符与 Object.assign() 类似，也是用来创建一个新的实例，但它通常用于函数调用或字面量表达式中。

## ES6+特性

### 一、ES6引入了哪些特性？

