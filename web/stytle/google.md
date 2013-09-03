1. 变量声明用var
* 变量声明务必用var

2. 常量定义
* 使用大写字母和下划线_
* 注释用@const

3. 分号使用
* 在赋值函数变量，数组，关联数组后不使用分号结束会引起许多问题
* 赋值，函数调用，返回值后务必用分号结束

4. 函数嵌套
* 函数嵌套很有用，但是要灵活掌握

5. 在非函数的块元素里面定义函数

    if (x) {
      function foo() {}
    }

6. 异常
* 谨慎在代码中屏蔽错误，避免调试发现不到问题
* 组件中的异常处理最好封装处理
* 编写必要的自定义异常

7. 使用兼容性好的标准特性
8. 使用基本类型，避免使用封装类
9. 避免使用多层原型，尽量使用属性拷贝的继承方式
10. 为对象添加属性
    为对象添加属性可以在在对象定义的构造函数里面添加，或者通过原型对象添加属性。
    动态的为对象添加属性会降低JS的性能


    Foo.prototype.bar = function() {
      /* ... */
    };
    
    /** @constructor */
    function Foo() {
      this.bar = value;
    }


11. 删除属性delete
   通过delete删除对象的属性效率要低于直接把属性赋为空,除非是真正想改变对象的keyList


	obj.foo = null;

12. 闭包
* 闭包在JS中非常有用
* 避免闭包中绑定DOM事件

<pre>
    function foo(element, a, b) {
      element.onclick = function() { /* uses a and b */ };
    }
</pre>

在闭包中引入dom元素非常容易造成嵌套引用，从而导致内存泄漏问题

the function closure keeps a reference to element, a, and b even if it never uses element. Since element also keeps a reference to the closure, we have a cycle that won't be cleaned up by garbage collection. In these situations, the code can be structured as follows:

<pre>
    function foo(element, a, b) {
      element.onclick = bar(a, b);
    }
    
    function bar(a, b) {
      return function() { /* uses a and b */ }
    }
</pre>

1 3. eval
* 建议只用于反序列化数据或RPC解析中使用
* eval用户的输入内容是危险的

1 4. with
:不要使用
:with能够立即改变代码的上下文
:如果with包含的对象使用了 setter变量，可能会执行很多其它代码

:

    with (foo) {
      var x = 3;
      return x;
    }

Answer: anything. The local variable x could be clobbered by a property of foo and perhaps it even has a setter, in which case assigning 3 could cause lots of other code to execute. Don't use with.

1 5. this
* Only in object constructors, methods, and in setting up closures
* this在很多情况下指向的是全局根对象(eval, 闭包内函数,DOM事件绑定，全局代码)
* apply和call能够改变this的指向

因为this很容易用错，因此在下面的场合中避免使用this

* in constructors
* in methods of objects (including in the creation of closures)

1 6. for-in 遍历
* for-in遍历常常被错误用来遍历一个数组
* for-in遍历的是对象的属性，包括原型链中的值，但不包括数组中索引

*

    function printArray(arr) {
      for (var key in arr) {
        print(arr[key]);
      }
    }
    
    printArray([0,1,2,3]);  // This works.
    
    var a = new Array(10);
    printArray(a);  // This is wrong.
    
    a = document.getElementsByTagName('*');
    printArray(a);  // This is wrong.
    
    a = [0,1,2,3];
    a.buhu = 'wine';
    printArray(a);  // This is wrong again.
    
    a = new Array;
    a[3] = 3;
    printArray(a);  // This is wrong again.

1 7. 关联数组 Associate Array

* 不要用Array对象作为Map/Hash对象

1 8. 多行字符串文本
* 使用+连接字符串或者使用数组组织过长的字符串
* 不要使用\组织多行，对JS的压缩后有不可控制的风险

:

    var myString = 'A rather long string of English text, an error message \
                    actually that just keeps going and going -- an error \
                    message to make the Energizer bunny blush (right through \
                    those Schwarzenegger shades)! Where was I? Oh yes, \
                    you\'ve got an error and all the extraneous whitespace is \
                    just gravy.  Have a nice day.';



1 9. Use Array and Object literals instead of Array and Object constructors.

使用Array和Object列表形式创建对象，避免用构造函数创建对象。

Array对象的构造函数的参数列表有歧义, 容易产生误用

:
	// Length is 3.
	var a1 = new Array(x1, x2, x3);

	// Length is 2.
	var a2 = new Array(x1, x2);

	// If x1 is a number and it is a natural number the length will be x1.
	// If x1 is a number but not a natural number this will throw an exception.
	// Otherwise the array will have one element with x1 as its value.
	var a3 = new Array(x1);

	// Length is 0.
	var a4 = new Array();

因此，参数个数为1时，容易出现问题；但是在参数个数为2时能够正常的创建列表

为了避免参数变为1个时候的奇怪问题，创建数组时用列表方式更为可靠

	var a = [x1, x2, x3];
	var a2 = [x1, x2];
	var a3 = [x1];
	var a4 = [];


对象的构造函数没有相同的问题，但是从可读性和性能等因素出发，用列表定义关联数组更为可靠

:

	var o = new Object();
	var o2 = new Object();
	o2.a = 0;
	o2.b = 1;
	o2.c = 2;
	o2['strange key'] = 3;
	Should be written as:

	var o = {};

	var o2 = {
	  a: 0,
	  b: 1,
	  c: 2,
	  'strange key': 3
	};

2 0. 禁止修改内置对象的原型

Modifying builtins like `Object.prototype` and `Array.prototype` are strictly forbidden. Modifying other builtins like `Function.prototype` is less dangerous but still leads to hard to debug issues in production and should be avoided.


2 1. 禁止用IE下的条件注释

Don't do this:

    var f = function () {
        /*@cc_on if (@_jscript) { return 2* @*/  3; /*@ } @*/
    };

