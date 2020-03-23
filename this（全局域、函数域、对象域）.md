# this的原理

### 一、什么时候会用到 this
```javascript
var obj = {
	foo:function(){console.log(this.bar)},
	bar:1
}
var foo = obj.foo;
var bar = 2;

obj.foo() // 1
foo() // 2
```
为什么都是调用的`foo()`函数，但结果却不相同。因为`this`的指向不同，`this`指的是函数运行时所在的环境。对于`obj.foo()`，`foo`运行在`obj`环境，所以`this`指向`obj`；对于`foo()`来说，`foo()`运行在全局环境，所以`this`指向全局环境。
**函数的运行环境是如何决定的？**

### 二、内存的数据结构
```
var obj = {foo:5};
```
将对象赋值给变量`obj`，先生成一个对象`{foo:5}`，然后将对象的地址赋值给变量`obj`，因此变量`obj`是一个地址，而对象是以字典结构保存，每一个属性名对应一个属性描述对象。
![image.png](https://i.loli.net/2020/03/23/D13YochCTqZOu6A.png)

### 三、函数
而当对象中属性的值是一个函数时：
```javascript
var obj = { foo: function (){} };
```
这样的话，会单独将函数保存在内存中，然后再将函数的地址赋给`foo`属性的`value`属性。
![image.png](https://i.loli.net/2020/03/23/lIctj4Q5baGexMr.png)
由于函数是单独存储在内存中的，所有可以在不同的环境中执行。

### 四、环境变量
javascript 允许在函数体内部，引用当前环境的其他变量。
```javascript
var f = function(){
	console.log(x);
}
```
函数体中的变量`x`由运行环境提供。由于函数可以在不同的运行环境执行，`this`能够在函数体内部获得当前的运行环境（context），在函数体内部，指代函数当前的运行环境。
```javascript
var f = function () {
  console.log(this.x);
}

var x = 1;
var obj = {
  f: f,
  x: 2,
};

// 单独执行
f() // 1

// obj 环境执行
obj.f() // 2
```