函数提升
===========
函数分为： **函数声明、函数表达式、匿名函数**。

这里主要讨论函数声明和函数表达式。

关于函数表达式提升
---------

~~~javascript
console.log(fn);
var fn = function() {
    console.log('this fn.');
};
console.log(fn);
~~~
此时的结果：undefined ，fn的函数
<br/><br/>
如果这么写:
~~~javascript
fn(); // Uncaught TypeError: fn is not a function
var fn = function() {
    console.log('this fn.');
};
fn();
~~~
**原因**：fn本来就是undefined， 如果当成函数执行，那肯定是不可以的。
在这里，函数表达式的提升和变量提升是一样的，在代码编译时进行变量声明，在执行期，在原位置进行赋值，此时
函数表达式特殊在所赋的值是个函数罢了。

关于函数声明提升
---------
~~~javascript
console.log(fn);
function fn() {
    console.log('this fn.');
}
console.log(fn);
~~~
此时的结果：fn的函数 ，fn的函数,
及时这么写：
~~~javascript
fn();
function fn() {
    console.log('this fn.');
}
fn();
~~~
结果： this fn. 和 this fn.

原因：函数声明方式提升会将函数体一起提升上去,抽空原来位置，
<br/>
<br/>
**注意：**
<br/>
(1)函数声明和变量声明都会被提升。但是函数会首先被提升，然后才是变量。
<br/>
(2)函数声明比变量优先级要高，并且定义过程不会被变量覆盖，除非是赋值。

高级
---------
```javascript

function fn(a){
    console.log(a); // 20
    var a = 10;
}
fn(20);
```
~~~javascript

function fn(a){
    var a;
    function a(){}
    console.log(a); // fn a() {}
}
fn(20);
~~~
~~~javascript

function fn(a){
    var a = 10;
    function a(){}
    console.log(a); // 10
}
fn(20);
~~~
相当于
~~~javascript

function fn(a){
    function a(){}
    var a = 10;
    console.log(a); // 10
}
fn(20);
~~~
~~~javascript

function fn(a){
    console.log(a); // fn a() {}
    var a = 10;
    function a(){}
}
fn(20);
~~~
####了解：
在创建过程中，如果发现已经存在相同名称的属性，则不会影响已经存在的属性, 除非是已赋值。
<br/>
EC（执行上下文）创建的过程是由先后顺序的：参数声明 > 函数声明 > 变量声明