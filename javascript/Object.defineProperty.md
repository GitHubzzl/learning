# Object.defineProperty



## “=” 与 Object.defineProperty

为JavaScript对象新增或者修改属性，有两种不同方式：直接使用=赋值或者使用Object.defineProperty()定义。如下：

```javascript
// 示例1
var obj = {};
// 直接使用=赋值
obj.a = 1;

// 使用Object.defineProperty定义
Object.defineProperty(obj, "b",
{
    value: 2
});

console.log(obj) // 打印"{a: 1, b: 2}"

```

这样看两者似乎没有区别，对吧？但是，如果使用Object.getOwnPropertyDescriptor()查看obj.a与obj.b的属性的描述描述符(property descriptor)时，会发现=与Object.defineProperty并不一样：

```javascript
// 示例2
var obj = {};
obj.a = 1;
Object.defineProperty(obj, "b",
{
    value: 2
});
console.log(Object.getOwnPropertyDescriptor(obj, "a")); 
// 打印"{value: 1, writable: true, enumerable: true, configurable: true}"
console.log(Object.getOwnPropertyDescriptor(obj, "b")); 
// 打印"{value: 2, writable: false, enumerable: false, configurable: false}"

```

可知，使用=赋值时，属性的属性描述符value是可以修改的，而writable、enumerable和configurable都为true。

而使用Object.defineProperty()定义的属性的属性描述符writable、enumerable和configurable默认值为false，但是**都可以修改。**

使用Object.defineProperty()定义时，同时将writable、enumerable和configurable设为true，等价于使用=赋值，代码示例3和4是等价的：

```javascript
// 示例3
var obj = {};

obj.name = "Fundebug";
console.log(Object.getOwnPropertyDescriptor(obj, "name")); 
// 打印{value: "Fundebug", writable: true, enumerable: true, configurable: true}

```

```javascript
// 示例4
var obj = {};

Object.defineProperty(obj, "name",
{
    value: "Fundebug",
    writable: true,
    enumerable: true,
    configurable: true
});
console.log(Object.getOwnPropertyDescriptor(obj, "name")); 
// 打印{value: "Fundebug", writable: true, enumerable: true, configurable: true}
```

> 由于writable、enumerable和configurable都是false，导致obj.name属性不能赋值、不能遍历而且不能删除

> 当writable与enumerable同时为false时，属性不能重新使用Object.defineProperty()定义