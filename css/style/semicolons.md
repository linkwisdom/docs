#从google codestyle中看看分号的重要性
分号在JS中使用非常敏感，所以最好在变量赋值语句后加上分号

以下为使用分号的几种危险用法

* 函数变量赋值后无分号，如果后面紧跟括号可能被执行

:

	MyClass.prototype.myMethod = function() {
		return 42;
	}  // No semicolon here.

	(function() {
		// Some initialization code wrapped in a function to create a scope for locals.
	})();


那会发生什么呢？
第二个匿名函数被当作参数传递给了第一个函数!

* 变量赋值后无分号，后面紧跟属性选择

:

    var x = {
       'i': 1,
       'j': 2
    }
    
    [att].pop();

代码实际执行变成

    x[att].pop()

* 意外的语法错误

:

    var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]
    -1 == resultOfOperation() || die();