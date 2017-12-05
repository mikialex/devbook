# js对象相关内容

## 对象创建方法以及其原型链

### 对象字面量
```js
var o = {a: 1};

// o这个对象继承了Object.prototype上面的所有属性
// 所以可以这样使用 o.hasOwnProperty('a').
// hasOwnProperty 是Object.prototype的自身属性。
// Object.prototype的原型为null。
// 原型链如下:
// o ---> Object.prototype ---> null

var a = ["yo", "whadup", "?"];

// 数组都继承于Array.prototype 
// (indexOf, forEach等方法都是从它继承而来).
// 原型链如下:
// a ---> Array.prototype ---> Object.prototype ---> null

function f(){
  return 2;
}

// 函数都继承于Function.prototype
// (call, bind等方法都是从它继承而来):
// f ---> Function.prototype ---> Object.prototype ---> null
```

### 构造器
构造器其实就是一个普通的函数。当使用 new 操作符 来作用这个函数时，它就可以被称为构造方法（构造函数）
```js
function Graph() {
  this.vertices = [];
  this.edges = [];
}

Graph.prototype = {
  addVertex: function(v){
    this.vertices.push(v);
  }
};

var g = new Graph();
// g是生成的对象,他的自身属性有'vertices'和'edges'.
// 在g被实例化时,g.__proto__指向了Graph.prototype.
```

### Object.create
新对象的原型就是调用 create 方法时传入的第一个参数：
```js
var a = {a: 1}; 
// a ---> Object.prototype ---> null

var b = Object.create(a);
// b ---> a ---> Object.prototype ---> null
console.log(b.a); // 1 (继承而来)

var c = Object.create(b);
// c ---> b ---> a ---> Object.prototype ---> null

var d = Object.create(null);
// d ---> null
console.log(d.hasOwnProperty); // undefined, 因为d没有继承Object.prototype
```


## 对象修改方法

### 修改值
**Object.assign()**

将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

注意：1名字相同会覆盖，2继承属性和不可枚举属性是不能拷贝的，3**值为undefined或null会被跳过**, 4只拷贝值，**没有深拷贝**

---


### 修改定义
