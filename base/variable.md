变量提升
===========
 思考
-----
```javascript
      console.log(test); // undefined
      var test = true;
      console.log(test); // true
```
##### 相当于

```javascript
    var test;
    console.log(test); // undefined
    test = true;
    console.log(test); // true
```

原因
-----
变量提升的根本原因是**变量声明**与**赋值的分离**，
如例子 var test = true; 这个代码是分两步进行的。首先是 var test 这一部分的变量声明，
**这个过程是在代码编译时进行的。**
然后是 test = 2; 这一部分的变量赋值，**这个过程是在代码执行时进行的**。