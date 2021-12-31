---
title: TypeScrip-特性
layout: post
index_img: https://cdn.bazijun.top/img/origin-cat.jpg
banner_img: https://cdn.bazijun.top/img/origin-cat.jpg
sticky: 100
hide: false
categories:
  - null
tags:
  - null
date: 2021-12-31 14:00:21
---
<!--  toc -->
[TOC]
# typeScript 中 js不具有的特性


> **tip** 
>  1. `赋值`不可以使用类型检查，`定义`类和接口还有函数时使用。
>  2.  ts的思维就是面向对象的思维，用类的视角去思考业务场景。
### class中的super
* ts中： 子类的构造函数中，必须在调用 `super(父类的属性)`把父类的构造方法也执行了,不然继承无效。类似java的写法了。

> 抽象类无法被实例化，就是用来被继承的，一个超级类。一个真正的爸爸类。

关键字 `abstract`
``` typeScript
  abstract class Animal {
    name: string;
    constructor(name: string) {
      this.name = name
    }
    abstract sayHello():void
  }
```

* 抽象类中可以定义**抽象方法**，并且继承抽象类的类必须重写抽象方法，不然会报错。

### 接口
* 普通的类型描述
  
``` typeScript
  type myTpe = {
    name: string,
    age: number
  }
```

* 接口用来定义一个类的结构，用来定义一个类中应该包含哪些属性和方法，同时接口也可以当作类型声明去使用。
* **接口可以重名**，并且实际使用时，为所有名为myInterface接口的merge版本。
* **接口中的属性都不能有实际的值**，类似抽象类，但接口中所有属性方法都是抽象的，而抽象类可以有实际的属性方法。
* `就是接口中只要定义的属性方法，就必须被引用(重写)`
* 接口就是一种对类的规范和限制。

关键字 `interface`

``` typeScript
  interface myInterface{
    name: string;
    age: number;
    sayHello(): void
  }
```
#### 使用接口
class 中使用关键字 `implements`
``` typeScript
class myClass implements myInterface {
  name: string;
  age: number;
  constructor(name:string, age:number){
    this.name = name
    this.age = age
  }
  sayHello() {
    console.log('你好呀！')
  }
}
```
函数使用的方式就和普通类型一样
``` typeScript
  function myFn(config: myInterface):myInterface{
    return config
  }
```
### 属性修饰符
> 下面就越来越像 java 了

* `readonly` 只读属性
* `public` 默认值 修饰的属性可以在任意位置访问(修改) 
  * 在构造函数的传参中，用`public`定义参数，就可以省略在外面的属性定义。
* `protected` 受保护的属性，只能在当前类和当前子类中访问，不能实例中访问。
* `private` 私有属性，私有属性只能在该类内部进行访问 (修改) => **但可以通过该类中方法来操作这些私有属性** `或使用get set修饰的属性来控制。`
  * *属性存储器 get set*
  ``` typeScript
  class test {
    private _name: string
    constructor(name:string) {
      this._name = name
    }
    get name() {
      return this._name
    }
    set name(value:string){
      this._name = value
    }
  }
  ```

### 泛型

>在定义函数和类时，如果遇到不明确的类型，就可以使用泛型。

定义具有泛型的函数，并且参数和返回值的类型都使用该泛型。他的类型未知，只有调用时才知道
* 泛型可以多个
* 函数和类都可以用
* 泛型可以继承类和接口
* **泛型可以理解为代替类型的一个变量**
``` typeScript
  function fn<T>(a: T):T{
    return a
  }
```
调用具有泛型的函数，推荐指定泛型，这样才规范。
``` typeScript
  fn(10) // 直接调用，ts引擎会根据你的参数判断泛型的类型
  fn<string>('hello') // 指定泛型
```
多个泛型
``` typeScript
  function fn<T, K>(a: T, b: K):T{
    return a + b
  }
  // 调用
  fn(100,200) // 直接调用
  fn<number，string>(23, '你好') // 指定泛型
```
泛型继承
`泛型T必须是Inter的实现类(子类)`
``` typeScript
  interface Inter{
    length: number
  }
  function fn<T extends Inter>(a: T):number{
    return a.length
  }
  // 调用时传的参数就必须符合接口Inter了
  fn({length: 500})
```
类使用泛型
``` typeScript
  class Myclass<T>{
    name: T;
    constructor(name: T) {
      this.name = name
    }
  }
  const mc = new Myclass<string>('把子君')
```

