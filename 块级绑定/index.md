# var 声明与变量提升

**var**关键字声明的变量无论声明在什么位置，都会视为声明在函数或者全局作用域的顶端，在判断语句中也是如此.
```js
 console.log(a);
 if (false) {
    var a = 1;
  }
```
上面代码会被编译为
```js
var a 
console.log(a); //undefined
if(false) {
    a = 1;
}

```
# var声明和函数声明式

两种声明都可以导致变量被提升到顶层，区别是var声明 不会同时进行赋值，函数声明会赋值.


在同一个作用域中使用var和函数声明式，个人理解函数会在var之后被提升
```js
>1
console.log(a); // ƒ a() {}
var a;
function a() {}

>2
console.log(a); // ƒ a() {}
function a() {}
var a;

``` 
无论变量声明的位置变化，最后被声明的都是**function a**

# 在代码块中无法同时使用var 和函数声明式
```js
{
        var a //Uncaught SyntaxError: Identifier 'a' has already been declared 
        function a() {}
}
```




# let声明
let 声明的语法与 var 的语法一致。你基本上可以用 let 来代替 var 进行变量声明.

由于 let 声明并不会被提升到当前代码块的顶部，因此你需要手动将 let 声明放置到顶部，以便让变量在整个代码块内部可用.

1. let不会进行变量提升
```js
 console.log(a); // ReferenceError: Cannot access 'a' before initializationat
    let a
```

2. 禁止重复声明

如果一个标识符已经在代码块内部被定义，那么在此代码块内使用同一个标识符进行 let 声
明就会导致抛出错误.
```js
var count = 30;
// 语法错误
let count = 40;
```

3. 块级作用域

在代码块中声明的变量只能在**代码块中访问**
```js
 {
      let x = 0
  }
 console.log(x); //x is not defined

```

# const声明
在 ES6 中里也可以使用 const 语法进行声明。

1. 使用 const 声明的变量会被认为是常量（constant ），意味着它们的值在被设置完成后就不能再被改变
```js
const name; // Missing initializer in const declaration

//无法重新赋值
const test
test =2 //Assignment to constant variable.

//可以对常量对象成员进行修改
const obj = { a: 1 };
      obj.a = 2;
      console.log(obj); //{a: 2}

```

2. 和let 一样无法重复声明


3. 暂时性死区
   
述 let 或 const 声明的变量为何在声明处之前无法被访问，被称为**暂时性死区（ temporal dead zone ， TDZ ）的**.

甚至会影响**typeof**.


```js
//访问一个从未声明的变量，会报错
  console.log(a); // a is not defined

//使用typeof 访问一个从未声明的变量则会返回undefined
 console.log(typeof a); //undefined

 //如果在暂时性死区使用typeof 访问变量会报错
   console.log(typeof a); //Cannot access 'a' before initialization at 
     let a 

```



