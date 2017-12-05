
## 原型链

当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。

在原型链上查找属性比较耗时，对性能有副作用，这在性能要求苛刻的情况下很重要。另外，试图访问不存在的属性时会遍历整个原型链。

![](./img/prototype.png)
基本的原型链 蓝色

``` js
Person.prototype == person.__proto__ 
Person.prototype.constructor == Person
Object.getPrototypeOf(person) === Person.prototype
Object.prototype.__proto__ === null

person.constructor === Person.prototype.constructor // 注意
```

```__proto__ ```，绝大部分浏览器都支持这个非标准的方法访问原型，然而它并不存在于 Person.prototype 中，实际上，它是来自于 Object.prototype ，与其说是一个属性，不如说是一个 getter/setter，当使用 obj.__proto__ 时，可以理解成返回了 Object.getPrototypeOf(obj)。

---

判断某个原型对象是不是某个实例的原型:**isPrototypeOf()**
```
Cat.prototype.isPrototypeOf(cat1)
```

---

判断某一个属性到底是本地属性，还是继承自原型对象的属性:**hasOwnProperty()**

检查属性是否undefined还不够。该属性可能存在，但其值恰好设置为undefined

hasOwnProperty 是Object.prototype的自身属性。
```
cat1.hasOwnProperty("name")
```


## 其他

尽量不要扩展原生对象的原型
扩展内置原型的唯一理由是支持JavaScript 引擎的新特性，如Array.forEach。