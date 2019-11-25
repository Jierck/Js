## 一、基本类型和引用类型的值
* 首先js中包含两种不同的数据类型的值：基本类型和引用类型。
基本类型指的是简单的数据段
* 引用类型指的是可能由多个值构成的对象这些值是保存在内存中的。
但是js不能直接操作对象的内存的空间。
* 1、动态的属性
    - 基本类型的值是不可以添加属性。只能给引用类型值动态的添加属性。
```JavaScript
    // 基本类型
    var name = "ck";
    name.age = 27;
    console.log(name.age); //undefined
    // 引用类型
    var person = new Object();
    person.age = 27;
    console.log(person.age); //27
```
* 2、复制变量值
    * 分两种分别为复制基本类型值和复制引用类型值。
        * 复制基本变量值后两个值是可以进行操作的所以是不会互相影响的。
而复制引用类型的时候是互相影响的。复制后的是变量值其实类似指针一样，它们访问的是同一个对象。看下面的列子：
            ```JavaScript
            var name1 = new Object();
            var name2 = name1;
            name1.age = 27;
            console.log(name1.age); //27
            name2.age = 28;
            console.log(name1.age); //28
            ```
* 3、传递参数
    * JS中所有函数的参数只能按值传递。其实就是把值从一个变量复制到另外一个变量一样。
    * 在向传递基本类型的值时，被传递的值会被复制给一个局部变量（其实就是命名参数或者说时arguments对象的一个元素），并且函数内部的变化不会影响函数外部的变化 。列子：
        ```JavaScript
        function add(num){
                num += 10;
                return num;
        }
        var sz  = 20;
        console.log(sz); // 20
        console.log(add(sz));  //30
        ```





