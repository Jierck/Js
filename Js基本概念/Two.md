## 一、变量
* 1、ECMAScript的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据。也就是说每个变量仅仅是一个用于保存值的占位符而已。在JS中定义变量时要使用var 操作符 如下：
```JavaScript
    var message;
```
<font color="#ff0000">注意：var 是一个关键字，后跟变量名（即一个标识符）</font>。

* 2、上面的一行代码定义了一个名为message的变量，该变量可以用来保存任何值。同时像这样未经过初始化的变量，会保存一个特殊的值——undefined。同时JS也支持直接初始化变量，所以可以在定义变量的同时就可以设置变量的值。如下：

```JavaScript
    var message = "hi";
```

* 3、上面的代码虽然保存了一个字符串"hi"，但是这样的初始化变量并不会把它标记为字符串类型；初始化的过程其实就是给变量赋值，所以修改变量值的时候可以同时修改值的类型。但是不建议这么做，即使这种操作在JS中是有效的。

* 4、需要注意的是，用var操作符定义的变量将成为定义该变量的作用域中的局部变量。也就是说，如果在函数中使用var定义的一个变量，那么这个变量在函数退出后就会被销毁。例如：
```JavaScript
    function test() {
        var message = "hi"; //局部变量
    }
    test();
    console.log(message);//报错未找到到该变量
```

<font color=#008000 >_PS：我一直认为加var是定义全局变量。不加var是定义局部变量。_</font>

* 5、相反的在上面的代码中如果想创建的变量可以被函数外读取，我们省略var操作符，变量message既可以变成一个全局变量。
注意：虽然省略var操作符可以定义全局变量，但这也不是推荐的做法。因为在局部作用域中定义全局变量会变得很难维护。同时也会导致不必要的混乱。在未经声明的变量赋值在严格模式下会导致抛出ReferenceError错误。 

* 6、同时推荐使用一条语句定义多个变量，因为JS是松散类型的，所以使用不同类型初始化变量的操作是可以用一条语句完成，这样可以提高可读性。如下所示：
```JavaScript
    var message = "hi", //字符串
    found = false, //布尔
    age = 29 ; // 整形
```
<font color="#ff0000">注意：在严格模式下，不能定义名为eval或argument 的变量，否则会导致语法错误。</font>

## 二、数据类型

* 1、JS中有5种简单数据类型（也可以称为基本数据类型）分别为：Undefined、Null、Boolean、Number和String。有一种复杂数据类型——Object，Object本质上是由一组无序的名值对组成的。
JS不支持任何创建自定义类型的机制，所以所有的值最终都将是上述6种数据类型之一。

* 2、typeof操作符：因为ECMAScript是松散类型的，因此需要有一种手段来检测给定变量的数据类型，typeof就是负责提供这方面信息的操作符。对一个值使用typeof操作符可能返回下列某个字符串：
    - "Undefined"——如果值未定义;
    - "boolean"——如果值是布尔值;
    - "string"——如果值是字符串;
    - "number"——如果值是数值;
    - "object"——如果值是对象或Null;
    - "function"——如果值是函数

    - 1、使用typeof的例子：
```JavaScript
    var message = "hi", //字符串
        found = false, //布尔
        age = 29; // 整形
    console.log(typeof message) //String
    console.log(typeof （message）) //String
    console.log(typeof found) //boolean
    console.log(typeof age) //number
    console.log(typeof 29) //number
```
<font color=#008000 >上面的例子说明，typeof操作符的操作可以是变量，也可以是数值字面量，需要注意的是typeof是一个操作符而不是一个函数，所以例子中的括号虽然可以使用，但这不是必须的。

在某些情况下，typeof操作符是会返回一些难以理解但是从技术角度上来讲是正确的值，比如调用typeof null会返回"object",因为特殊值null会被认为是一个空的对象引用。在Safari5及之前的版本,Chrome7及之前版本在对正则表达式调用typeof操作符时会返回"function",其他浏览器在这种情况上会返回"object"。

PS:在技术角度上讲，函数在JS中时对象，不是一种数据类型.然而，函数也确实有些特殊的属性，因此通过typeof操作符来区分函数和其他对象是有必要的。</font>

* 3、Undefined类型只有一个值，即特殊的undefined。.所以在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined。例如：

```JavaScript
    // 形式一
    var message;
    console.log(message == undefined) //true
    // 形式二
    var message = undefined;
    console.log(message == undefined) //true

    //以上两种形式的写法是等价只是区别是第二种是用undefined值显式的初始化变量message，但是没有必要因为默认未经过初始化的值为undefined。当然引入undefined值主要是为了区别空指针对象和未初始化变量。
```

* 3.1、未初始化的变量和未声明的变量还是有区别的，未定义的变量浏览器会报错，为初始化的变量浏览器会显出undefined。

<font color="#ff0000">注意：在使用typeof操作符的时候，未初始化和未定义的变量都是显示undefined，所以最好还是将变量显式的初始化undefined，这样就可以知道变量是未声明的，而不是尚未初始化。</font>

* 4、NULL类型，NULL类型和undefined一样也是只有一个值类型的数据类型，这个特殊值是	null。从逻辑上来讲，NULL表示的是一个空指针，这也是为什么使用typeof操作符检测NULL值时返回的值会返回“object”的原因。如下
```JavaScript
    var car = null;
    consloe.log( typeof car) //  "object"
```

+ 2、如果定义的变量准备在将来用于保存对象，那么最好将改变量初始化为NULL而不是其余值。这样一来，只要直接检查null值就可以知道相应的变量是否已经保存了一个对象的引用。

<font color=#008000 >_PS：var ob = null 和 var ob = “” 这两个声明变量的方式是不一样的  NULL 是一个特殊的类型，从逻辑上讲是一个空指针 ，也可以理解为一个空对象 ，但是“  ”这样的写法只是定义了一个字符串。_</font>

如下
```JavaScript
    if(car != null){
    //对car对象执行某些操作
    }
```

* 4.3、实际上undefined是派生自null值的，所以根据规定它们在相等性测试上是返回的true。

conloe.log(undefined == unll) //true

<font color="#ff0000">注意，在上面的列子中使用的 相等操作符 所以返回ture 这种操作符是转换字符类型的 如果使用强调相等操作符（===） 是不可能返回ture的。

所以尽管undefined和null有这样的关系，但用途完全不同，无论什么情况下都没有必要将变量的值显式的设置为undefined，但是对于null它是用来声明一个空对象的，没有保存的对象的变量就应该明确的让变量保存为null。</font>

* 5、Boolean类型（布尔类型）布尔类型有两个字面值true和false。需要注意的是这两个值与数字值没有关系。同时这两个值是区分大小写的。
在js中所有类型的值都与布尔值有关 可以用转型函数Boolean()进行转换。
    - string 类型的值非空为true 空值为false
    - Number 非零数字包括无穷大为true 0和NaN为fals
    - Object 任何对象为true null 为false
    - Undefined 只有false

* 6、Number类型
    + 1、整数类型 十进制 正常写法 八进制 0开头范围0~7 超过无效 八进制在严格模式下无效 会抛出错误，十六进制前两位必须是0x开头。
    + 2、浮点数值数值中必须包含小数点。
    + 3、数值范围 最小数值Number.MIN_VALUE 最大数值Number.MAX_VALUE
    + 4、NaN，非数值 可以利用isNaN()函数来判断是否可以转化为数值。而且NaN与任何值都相等 包括自己本身。注意一下因为布尔值是可以转换成0和1的所以布尔值判断为false
    + 5、数值转换，有三个函数可以把非数值转化为数值：Number(),parseInt(),和parseFloat()。
        - number()转换规则：
            - 布尔值转换成1（true）和 0 （false）
            - 数字值简单的传入和返回
            - null返回0.
            - undefined返回NaN
            - 字符串如果只是整形数字转换为数字会省略前面的0、浮点格式转换为对应的浮点值同样也会忽略前面的0，十六进制时转换为相同大小的十进制整数值，空字符串转化为0，其他为NaN。
            - 对象，调用对象的valueof()方法然后依照前面的规则转换返回值，如果转换结果为NaN则调用对象的toString()方法，再依次按照前面的规则进行转换返回字符串。
            - 一般情况下Number()函数在转换字符串的时候比较复杂且不够合理，所以我们在处理整数的时候更多用的是parseInt()函数。parseInt()函数转换字符串的时候更多的是看其是否符合数值模式，会忽略前面的空格指导找到第一个非空字符。如果第一个字符不是数字或者负号会返回NaN，所以这个函数在转换空字符的时候返回NaN而Number返回的是0.如果第一个是数字它会继续解析第二个字符，直到不是数字或者没有为止。所以例如“1234hhh”这样的字符串会转化为1234 ，“hhh”会完全忽略，同时 "12.1"这样的字符串由于"."不是有效字符会被转化为12.在解析八进制这样的字面量es3和es5会产生分歧
            如var num = parseInt("070");
            - 在es3是56也就是8进制转换成10进制后的值在es5中是70忽略前面的0；这样的情况下es5通过声明转换进制类型解决var num = parseInt("070",8)；当你声明了16进制的时候可以不需要写0x而且也可以保证获得正确的结果
            - parseFloat和parseInt类似。遇到第一个小数点是有效的但是遇到第二个小数点是无效的同时它会忽略前导的0而且只解析十进制 所以在解析16进制的时候始终会将其转换成0；并且如果字符串是个整数它也是会转换成整数的。

* 7、String类型即字符串可以用双引号或者单引号标识两者没有区别。
   +  1、转义字符又称转义序列或者叫字符字面量，用于表示非打印字符，或者具有其他用途的字符。
    常用的有\n(换行)，\t(制表),\b（退格），\r(回车)，\f(进纸)，\\（斜杠），\' \"(单双引号)
   +  2、字符串是不可变的也就是说一旦创建值就不能改变，要改变原来的字符串就必须要先销毁原来的字符串然后再填充该变量。
   +  3、转换成字符串两种一个是toString（）一个是String()方法
        - toString()方法是几乎每个值都有的但是null和undefind值是没有这个方法的除此之外包括字符串都是有这个方法的。需要注意的是默认情况下以十进制的格式标识，如果需要通过二进制或者八进制、16进制表示的话是可以通过指定基数来表示的。如：

        ```javaScript
            var num = 10;
            alert(num.toString(16)) //a
        ``` 
        - String()方法和toString方法不同的是如果不知道转换值是否为null或者undefinde可以用该方法规则为。
        - 如果值有toString的方法则按照toString()的方法来如果是null则转换成null如果是undefined转换成undefined.

* 8、Object类型就是一组数据和功能的集合。对象可以通过执行new操作符来创建注意大小写

如：
```javaScript
var o = new bject();
```
有下列属性和方法：
- constructor:保存着用于创建当前对象的函数。
- hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中（不是实例的原型中）是否存在其中作为参数的属性名必须是以字符串形式指定。
- isPrototype(object):用于检查传入的对象是否是当前对象的原型。
- propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in语句来枚举，同样参数的属性名必须以字符串形式指定。
- toLocaleString():返回对象的字符串表示，该字符串与执行环境的地区对应。
- toString():返回对象的字符串表示。
- valueOf():返回对象的字符串、数值或者布尔值。通常和toString()方法返回值相同。
## 四、语句
* for-in：用来遍历（枚举）对象的属性
```JavaScript
    var o = new Object();
        o={
            name:"ck",
            age:23,
            year:"Mon Feb 19 2018 04:42:32 GMT+0800 (中国标准时间)"
        }
        for(var ck in o){
            document.write(ck+);
}
```
* lable语句在代码中添加标签可以配合break或continue语句来引用
```JavaScript
    var num = 0;
        var count = 10;
        start: for(var i = 0  ; i<count ; i++){
            for (var j = 0; j < count; j++) {
                if (i==5 && j == 5) {
                    continue start;
                }
                num++
            }
        }
        alert(num) //95
``` 
* width语句主要目的是将代码的作用域设置到一个特定的对象中
```JavaScript
    with(o){
            var name = name;
            var age = age;
            var year = year;
        }
        //等价与
        var name = o.name;
        var age = o.age;
        var year = o.year;

```
## 五，函数
* 结构：function name(){}

    可以function one(){} 也可以 var num = function(){}

```JavaScript
    function hello (message1,message2){
            return message1+message2;
            alert(message1+message2);//不会执行
        }
        console.log(hello("hello","world"))
```
* 函数在return语句后执行完会立即退出。
* return 函数可以不带任何返回值返回后的值为undefined。

* 函数的参数：
    - 首先js的参数是没有限制的我们命名参数只是为了方便我们知道传了什么参数，原因是js的参数在内部是一个数组我们可以通过argument对象来访问它同时它也可以和命名参数一起使用。
    - 第二参数是不在乎数据类型的。
```javaScript
    function hello (){
                return arguments[0]+arguments[1];
            }
    console.log(hello("hello","world"))
```
## 六，没有重载
* 不能像Java一样将一个函数编写两个定义。如果有多个定义会按照最后一个定义来。