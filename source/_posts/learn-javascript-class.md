---
title: 'JavaScript 类'
date: 2021-11-02 18:47:43
tags: [JavaScript]
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
> 最近项目中用到了类的概念，其实更早的时候已经接触到了，现在捡起来过一遍，还不晚

# ES5

## 实现

ES5 可以通过构造函数进行类的实现。

 ```javascript
function Person(name, age) {
    this.name = name; //实例属性
    this.age = age; //实例属性
    this.run = function () { //实例方法
        console.log(this.name + ' is running');
    }
}
 ```

构造函数实际就是一个普通函数，但我们可以通过 new 关键词进行实例化。在构造函数中声明实例属性和方法，实例上就能读取调用。

```javascript
let person1 = new Person('张三', 18); //实例化
let person2 = new Person('李四', 20); //实例化

//读取实例属性
console.log(person1.name); //张三 
console.log(person2.age); //20
//调用实例方法
person1.run(); //张三 is running
person2.run(); //李四 is running
```

## 静态属性和方法

可以在类上添加静态属性和方法，我们能通过类名访问到它们。实例对象不能直接调用类的静态属性方法。

```javascript
Person.words = 'I am a person'; //类上添加静态属性
Person.say = function () { //类上添加静态方法
    console.log(`Person saying: \"${Person.words}\"`); 
}

//在类上读取静态属性
console.log(Person.words); //Person say: I am a person
//在类上调用静态方法
Person.say(); //Person saying: "I am a person"

//不可在实例上读取静态属性 
//console.log(person1.words); //undefined
//不可在实例上调用静态方法 
//person1.say(); //TypeError: person1.say is not a function
```

## 原型属性和方法

可以在类上添加原型属性和方法，我们能通过实例对象访问它们。类不能直接调用原型属性方法。

```javascript
Person.prototype.weight = 60; //类上添加原型属性
Person.prototype.lostWeight = function () { //类上添加原型方法
    this.weight--;
    console.log(`${this.name}\'s weight is ${this.weight} now!`);
}

//在实例上读取原型属性
console.log(person1.weight); //60
//在实例上调用原型方法
person1.lostWeight(); //张三 is saying

//不可在类上读取原型属性 
//console.log(Person.weight); //undefined
//不可在类上调用原型方法
//Person.lostWeight(); //TypeError: Person.lostWeight is not a function
```

# ES6

## 实现

在 ES6 中，类由 class 关键词实现。

```javascript
class Animal {
  constructor(name, age) { //实例属性创建
    this.name = name;
    this.age = age;
  }
  speak() { //实例方法
    console.log(this.name + ' makes a noise.');
  }

  static eat() { //静态方法
    console.log(this.words);
  }
  static words = 'All animals eat food.'; //静态属性
}
```

调用方法与 ES5 无异。

```javascript
//调用静态方法
Animal.eat(); //All animals eat food.

let dog1 = new Animal('Teddy', 2); //实例化
//调用实例方法
dog1.speak(); //Teddy makes a noise.
```

## 静态属性和方法

与 ES5 无异。

```javascript
//类上添加静态方法
Animal.sleep = function () {
  console.log('All animals sleep.');
}
//在类上调用静态方法
Animal.sleep(); //All animals sleep.
```

## 原型属性和方法

与 ES5 无异。

```javascript
Animal.prototype.run = function () { //类上添加原型方法
  console.log(this.name + ' is running.');
}
//在实例上调用原型方法
dog1.run(); //Teddy is running.
```

# 最后

静态属性和方法服务于类本身，原型函数在类上添加但服务于实例。ES6 的 class 关键词是 ES5 构造函数的语法糖，创建有别使用无异。要搞明白后面类的继承还得从构造函数入手。