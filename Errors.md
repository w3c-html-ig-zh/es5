错误 
-----

实现必须在相关的ECMAScript语言结构被解释执行时报告大部分错误。**早期错误**是一个在程序中的任何结构被解释执行之前所包含的可检测且可报告的错误。实现必须在程序首次解释执行之前报告**早期错误**。**eval** 代码中的**早期错误**在 **eval** 被调用时报告，但这是在　**eval** 代码中的结构被解释执行之前做的。**早期错误**之外的任何错误都是运行时错误。

实现必须将下面的错误类型作为早期错误来处理：

-   任何语法错误
-   试图在定义一个 *[ObjectLiteral](ES5/expressions#ObjectLiteral "wikilink")* 时，将多个 **get** 或 **set** 访问器属性分配到同一个名字上。
-   试图在定义一个 *[ObjectLiteral](ES5/expressions#ObjectLiteral "wikilink")* 时，同时将数据属性和访问器属性（**get** 或 **set**）分配到同一个名字上。
-   正则表达式字面量中因缺少实现定义的语法扩展而产生的错误。
-   试图在[严格模式代码中定义一个](ES5/execution#strict-mode-code "wikilink") *[ObjectLiteral](ES5/expressions#ObjectLiteral "wikilink")* 时，将多个数据属性分配到同一个名字上。
-   *[WithStatement](ES5/statements#WithStatement "wikilink")* 出现在[严格模式代码中](ES5/execution#strict-mode-code "wikilink")。
-   在[严格模式代码中定义的](ES5/execution#strict-mode-code "wikilink") [FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink") 和 [FunctionExpression](ES5/functions#FunctionExpression "wikilink")，它们的 *[FormalParameterList](ES5/functions#FormalParameterList "wikilink")* 中多次出现同一个 *[Identifier](ES5/lexical#Identifier "wikilink")*。
-   **return**、**break**、**continue** 使用不当。
-   试图在早期已经确定为非[引用类型的任意值上调用](ES5/types#Reference "wikilink") [PutValue](ES5/types#PutValue "wikilink")（例如，执行赋值语句 3 = 4）。

即使编译器可以证实一个结构会在任何情况下都无法无误地执行，实现也不该将其它种类的错误当做**早期错误**来对待。在这种情况下实现可以发出一个早期警告，直到相关的结构被真正地解释执行到后再报错。

实现应报出所有指定的错误，但以下情况除外：

-   实现可以扩展程序的语法和正则表达式的 pattern 或 flags 语法。当程序的语法或正则表达式的 pattern 或 flags 语法遇到一个实现了程序语法定义扩展或正则表达式语法扩展时，所有允许抛出 [SyntaxError](ES5/builtins#SyntaxError "wikilink") 的操作（例如调用 [eval](ES5/builtins#x15.1.2 "wikilink")、使用正则表达式字面量、使用 [Function](ES5/builtins#x15.3 "wikilink") 或 [RegExp](ES5/builtins#x15.10 "wikilink") 构造器）都允许使用实现定义的行为来替代 [SyntaxError](ES5/builtins#SyntaxError "wikilink") 的抛出。
-   实现可以提供超出这份规范描述的额外类型、值、对象、属性、函数。这可能导致结构（例如访问一个全局变量）得到实现定义的行为，从而取代原有的错误（比如 [ReferenceError](ES5/builtins#ReferenceError "wikilink")）的抛出。
-   当 <var>fractionDigits</var> 或 <var>precision</var> 参数超出了指定的范围，实现可以为 [toFixed](ES5/builtins#x15.7.4.5 "wikilink")、[toExponential](ES5/builtins#x15.7.4.6 "wikilink")、[toPrecision](ES5/builtins#x15.7.4.7 "wikilink")，这几个函数定义抛出 [RangeError](ES5/builtins#RangeError "wikilink") 之外的行为。

