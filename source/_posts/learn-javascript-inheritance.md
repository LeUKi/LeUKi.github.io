---
title: 'JavaScript 类的继承'
date: 2021-11-02 21:26:18
tags: [JavaScript]
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
> 更好的代码复用、扩展，你需要类的继承

# ES5

总的来说，ES5 类的继承需要结合对象冒充继承和原型链继承两个方案，下面一一举例。

想搞继承，首先得有个父类，这里有这么一个构造函数：

```javascript
function Person(name, age) {
    this.name = name; //实例属性
    this.age = age; //实例属性
    this.run = function () { //实例方法
        console.log(this.name + ' is running');
    }
}
```

在类描述外部添加了原型方法和静态方法：

```javascript
Person.prototype.swim = function () { //类上添加原型方法
    console.log(`${this.name} is swiming`);
}

Person.work = function () { //类上添加静态方法
    console.log(`${this.name} is working`);
}
```

## 对象冒充继承

这里通过 call 方法继承父类，第一个参数传入子类。

```javascript
function Student(name, age, grade) {
    Person.call(this, name, age); //对象冒充继承
    this.grade = grade; //实例属性
}
```

实例化一个对象，发现能继承父类的实例属性和方法，但不能继承原型属性和方法。静态方法也不能被继承。

```javascript
let student1 = new Student('张三', 18, '一年级'); //实例化对象

//继承父类的实例方法
student1.run(); //张三 is running
//不可继承父类的原型方法
//student1.swim(); //TypeError: student1.swim is not a function
//不可继承父类的静态方法
//Student.work(); //TypeError: Student.work is not a function
```

## 原型链继承

首先建一个空的子类，将父类的实例赋给子类的 prototype 属性。

```javascript
function Teacher(name, age, subject) {}

Teacher.prototype = new Person(); //原型链继承
```

实例化一个对象，发现可以使用父类的实例方法和原型方法，但 new 实例化传参不可用，需要手动修改实例属性。同时静态方法也不能被继承。

```javascript
let teacher1 = new Teacher('李四', 30, '语文');//实例化对象

//实例属性存在但是没有初始化
teacher1.run(); //undefined is running
teacher1.swim(); //undefined is swiming
//修改实例属性
teacher1.name = "王五"; 
teacher1.run(); //王五 is running
teacher1.swim(); //王五 is swiming

//不可继承父类的静态方法
//Teacher.work(); //TypeError: Teacher.work is not a function
```

## 对象冒充+原型链继承

新建一个子类，通过结合两者实现继承。

```javascript
function Programmer(name, age, language) {
    Person.call(this, name, age); //对象冒充继承
    this.language = language; //实例属性
    this.introduce = function () { //实例方法
        console.log(`${this.name} is a ${this.language} developer`);
    }
}

Programmer.prototype = new Person(); //原型链继承
```

实例化一个对象，发现可以使用父类的实例方法和原型方法，子类也能向父类传参。但同时静态方法仍然不能被继承。

```javascript
let programmer1 = new Programmer('赵六', 35, 'JavaScript');//实例化对象

//继承父类的实例方法
programmer1.run(); //赵六 is running
//子类方法使用父类的实例属性
programmer1.introduce(); //赵六 is a JavaScript developer
//继承父类的原型方法
programmer1.swim(); //赵六 is swiming

//不可继承父类的静态方法
Programmer.work(); //TypeError: Programmer.work is not a function
```

# ES6

ES6 为类的继承提供了好用的语法糖。

在 class 内，使用 constructor 创建实例属性，用函数创建实例方法，还可以用 static 表示其是静态属性或方法。

```javascript
class Animal {
    constructor(name, age) { //实例属性创建
        this.name = name;
        this.age = age;
    }
    speak() { //实例方法
        console.log(this.name + ' makes a noise.');
    }
    static words = 'All animals eat food.'; //静态属性
}
```

此时在类描述外部添加了原型方法和静态方法：

```javascript
Animal.prototype.run = function () { //类上添加原型方法
    console.log(this.name + ' is running.');
}

Animal.eat = function () { //类上添加静态方法
    console.log(this.words);
}
```

建一个子类，通过 extends 关键词继承父类，在 constructor 中的 super 方法类似 ES5 的 call，传入给父类的实例属性。

```javascript
class Dog extends Animal {
    constructor(name, age, color) {
        super(name, age);
        this.color = color;
    }
    colorIs() {
        console.log(this.name + ' is ' + this.color);
    }
}
```

实例化一个对象，发现可以使用父类的实例方法和原型方法，子类也能向父类传参。重点是，静态方法在 ES6 上是能被继承的！

```javascript
let dog1 = new Dog('Teddy', 2, 'white'); //实例化

//继承父类的实例方法
dog1.speak(); //Teddy makes a noise.
//子类方法使用父类的实例属性
dog1.colorIs(); //Teddy is white
//继承父类的原型方法
dog1.run(); //Teddy is running.

//继承父类的静态方法
Dog.eat(); //All animals eat food.
```

# 最后

ES6 与 ES5 在类继承上对于父类的静态方法处理有很大不同。

是时候深入底层，走进原型链，探探JavaScript底下的世界。

