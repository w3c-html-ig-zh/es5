主值表达式
----------

`   `*<b id="PrimaryExpression">`PrimaryExpression`</b>*` :`
`       `**`this`**` `
`       `*[`Identifier`](ES5/lexical#Identifier "wikilink")*
`       `*[`Literal`](ES5/lexical#Literal "wikilink")*
`       `**
`       `**
`       `**`(`**` `**` `**`)`**

### this关键字

**this** 关键字执行为当前执行环境的 [this 绑定](ES5/execution#ThisBinding "wikilink")。

### 标识符引用 

*[Identifier](ES5/lexical#Identifier "wikilink")* 的执行遵循 [10.3.1](ES5/execution#identifier-resolution "wikilink") 所规定的标识符查找。标识符执行的结果总是一个 [Reference](ES5/types#Reference "wikilink") 类型的值。

### 字面量引用  

*[Literal](ES5/lexical#Literal "wikilink")* 按照 [7.8](ES5/lexical#literals "wikilink") 所描述的方式执行。

### 数组初始化 

数组初始化是一个以字面量的形式书写的描述数组对象的初始化的表达式。它是一个零个或者多个表达式的序列，其中每一个表示一个[数组元素](ES5/builtins#array-element "wikilink")，并且用方括号括起来。元素并不一定要是字面量，每次数组初始化执行时它们都会被执行一次。

[数组元素可能在元素列表的开始](ES5/builtins#array-element "wikilink")、结束，或者中间位置以逗号取代。当元素列表中的一个逗号的前面没有 **（如，一个逗号在另一个逗号之前。）的情况下，缺失的[数组元素仍然会对数组长度有贡献](ES5/builtins#array-element "wikilink")，并且增加后续元素的索引值。以逗号省略的数组元素是 **undefined**。假如元素在数组末尾被省略，那么元素不会贡献数组长度。

`   `*<b id="ArrayLiteral">`ArrayLiteral`</b>*` :`
`       `**`[`**` `**` `**`]`**
`       `**`[`**` `**` `**`]`**
`       `**`[`**` `**` `**`,`**` `**` `**`]`**

`   `*<b id="ElementList">`ElementList`</b>*` :`
`       `**` `**
`       `**` `**`,`**` `**` `**

`   `*<b id="Elision">`Elision`</b>*` :`
`       `**`,`**
`       `**` `**`,`**

产生式 ** **:** **[** **<sub>opt</sub> **]** 按照下面的过程执行 :

1.  令 <var>array</var> 为以表达式 **new Array()** 完全一致的方式创建一个新对象的结果，其中 [Array](ES5/builtins#x15.4 "wikilink") 是一个标准的内置构造器。
2.  令 <var>pad</var> 为解释执行 ** 的结果；如果不存在的话，使用数值 **0**。
3.  以参数 **"length"**、<var>pad</var> 和 **false** 调用 <var>array</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内置方法
4.  返回 <var>array</var>。

产生式 ** **:** **[** ** **]** 按照下面的过程执行 :

1.  返回解释执行 ** 的结果。

产生式 ** **:** **[** ** **,** **<sub>opt</sub> **]** 按照下面的过程执行：

1.  令 <var>array</var> 为解释执行 ** 的结果。
2.  令 <var>pad</var> 为解释执行 ** 的结果；如果不存在的话，使用数值 **0**。
3.  令 <var>len</var> 为以参数 **"length"** 调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内置方法的结果。
4.  以参数 **"length"**、[ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>pad</var>+<var>len</var>) 和 **false** 调用 <var>array</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内置方法。
5.  返回 <var>array</var>。

产生式 ** **:** **<sub>opt</sub> ** 按照下面的过程执行 :

1.  令 <var>array</var> 为以表达式 **new Array()** 完全一致的方式创建一个新对象的结果，其中 [Array](ES5/builtins#x15.4 "wikilink") 是一个标准的内置构造器。
2.  令 <var>firstIndex</var> 为解释执行 ** 的结果；如果不存在的话，使用数值 **0**。
3.  令 <var>initResult</var> 为解释执行 ** 的结果。
4.  令 <var>initValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>initResult</var>)。
5.  以参数 [ToString](ES5/conversion#to-string "wikilink")(<var>firstIndex</var>)、属性描述对象 { [[Value]]: <var>initValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 调用 <var>array</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内置方法。
6.  返回 <var>array</var>。

产生式 ** **:** ** **,** **<sub>opt</sub> ** 按照下面的过程执行 :

1.  令 <var>array</var> 为解释执行 ** 的结果。
2.  令 <var>pad</var> 为解释执行 ** 的结果；如果不存在的话，使用数值 **0**。
3.  令 <var>initResult</var> 为解释执行 ** 的结果。
4.  令 <var>initValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>initResult</var>)。
5.  令 <var>len</var> 为以参数 **"length"** 调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内置方法的结果。
6.  以参数 [ToString](ES5/conversion#to-string "wikilink")([ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>pad</var>+<var>len</var>)) 和属性描述对象 { [[Value]]: <var>initValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 调用 <var>array</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内置方法。
7.  返回 <var>array</var>。

产生式 ** **:** **,** 按照下面的过程执行 :

1.  返回数值 **1**。

产生式 ** **:** ** **,** 按照下面的过程执行 :

1.  令 <var>preceding</var> 为解释执行 ** 的结果。
2.  返回 <var>preceding</var>+**1**。

### 对象初始化 

对象初始化是一个以直接量的方式描述对象的初始化过程的表达式。它是用花括号括起来的由零或者多对属性名 / 关联值组成的列表，值不需要是直接量，每次对象初始化被执行到时他们会执行一次。

`   `*<b id="ObjectLiteral">`ObjectLiteral`</b>*` :`
`       `**`{` `}`**` `
`       `**`{`**` `**` `**`}`**
`       `**`{`**` `**` `**`,` `}`**

`   `*<b id="PropertyNameAndValueList'">`PropertyNameAndValueList`</b>*` :`
`       `**
`       `**` `**`,`**` `**

`   `*<b id="PropertyAssignment">`PropertyAssignment`</b>*` :`
`       `**` `**`:`**` `**
`       `**`get`**` `**` `**`(` `)` `{`**` `*[`FunctionBody`](ES5/functions#FunctionBody "wikilink")*` `**`}`**
`       `**`set`**` `**` `**`(`**` `**` `**`)` `{`**` `*[`FunctionBody`](ES5/functions#FunctionBody "wikilink")*` `**`}`**

`   `*<b id="PropertyName">`PropertyName`</b>*` :`
`       `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*
`       `*[`StringLiteral`](ES5/lexical#StringLiteral "wikilink")*
`       `*[`NumericLiteral`](ES5/lexical#NumericLiteral "wikilink")*

`   `*<b id="PropertySetParameterList">`PropertySetParameterList`</b>*` :`
`       `*[`Identifier`](ES5/lexical#Identifier "wikilink")*

产生式 ** **:** **{** **}** 按照下面的过程执行 :

1.  如同以表达式 **new Object()** 创建新对象，其中 [Object](ES5/builtins#x15.2 "wikilink") 是标准的内置构造器。

产生式 s ** **:** **{** ** **}** 以及 ** **:** **{** ** ,**}** 按照下面的过程执行 :

1.  返回解释执行 ** 的结果。

产生式 ** **:** ** 按照下面的过程执行 :

1.  令 <var>obj</var> 为以表达式 **new Object()** 完全一致的方式创建一个新对象的结果，其中 [Object](ES5/builtins#x15.2 "wikilink") 是一个标准的内置构造器。
2.  令 <var>propId</var> 为解释执行 ** 的结果。
3.  以参数 <var>propId</var>.**name**、<var>propId</var>.**descriptor** 和 **false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内置方法。
4.  返回 <var>obj</var>。

产生式 ** **:** ** **,** ** 按照下面的过程执行 :

1.  令 <var>obj</var> 为解释执行 ** 的结果。
2.  令 <var>propId</var> 为解释执行 ** 的结果。
3.  令 <var>previous</var> 为以参数 <var>propId</var>.**name** 调用 <var>obj</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内置方法的结果。
4.  如果 <var>previous</var> 不是 **undefined**，且当以下任意一个条件为 **true** 时，则抛出一个 **SyntaxError** 异常：
    -   产生式包含在[严格模式下并且](ES5/execution#strict-mode-code "wikilink") [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(<var>previous</var>) 为 **true** 并且 [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(<var>propId</var>.**descriptor**) 为 **true**。
    -   [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(<var>previous</var>) 为 **true** 并且 [IsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>propId</var>.**descriptor**) 为 **true**。
    -   [IsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>previous</var>) 为 **true** 并且 [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(<var>propId</var>.**descriptor**) 为 **true**。
    -   [IsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>previous</var>) 为 **true** 并且 [IsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>propId</var>.**descriptor**) 为 **true** 并且 <var>previous</var> 和 <var>propId</var>.**descriptor** 都有 [[[Get]]](ES5/types#descriptor-Get "wikilink") 字段或者 <var>previous</var> 和 <var>propId</var>.**descriptor** 都有 [[[Set]]](ES5/types#descriptor-Set "wikilink") 字段。

如果以上步骤抛出一个 **SyntaxError**，那么实现应该把这个错误视为[早期错误](ES5/errors#early-error "wikilink")。

产生式 ** **:** ** **:** ** 按照下面的过程执行 :

1.  令 <var>propName</var> 为解释执行 ** 的结果。
2.  令 <var>exprValue</var> 为解释执行 ** 的结果。
3.  令 <var>propValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>exprValue</var>)。
4.  令 <var>desc</var> 为[属性描述对象](ES5/types#property-descriptor "wikilink") {[[Value]]: <var>propValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}。
5.  返回 [属性标识符](ES5/types#property-identifier "wikilink") (<var>propName</var>, <var>desc</var>)。

产生式 ** **:** **get** ** **( ) {** *[FunctionBody](ES5/functions#FunctionBody "wikilink")* **}** 按照下面的过程执行：

1.  令 <var>propName</var> 为解释执行 ** 的结果。
2.  令 <var>closure</var> 为根据 [13.2](ES5/functions#creating-function-objects "wikilink") 的定义，以空参数列表和 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 函数体创建的一个新的函数对象。传入当前执行中的执行环境的 [LexicalEnvironment](ES5/execution#LexicalEnvironment "wikilink") 作为 **Scope**。假如 ** 包含在[严格模式代码中或者](ES5/execution#strict-mode-code "wikilink") *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，传入 **true** 为严格模式标志。
3.  令 <var>desc</var> 为[属性描述对象](ES5/types#property-descriptor "wikilink") {[[Get]]: <var>closure</var>, [[Enumerable]]: **true**, [[Configurable]]: **true**}。
4.  返回 [属性标识符](ES5/types#property-identifier "wikilink") (<var>propName</var>, <var>desc</var>)。

产生式 ** **:** **set** ** '''( ''' ''**'' )** **{** *[FunctionBody](ES5/functions#FunctionBody "wikilink")* **}** 按照下面的过程执行：

1.  令 <var>propName</var> 为解释执行 ** 的结果。
2.  令 <var>closure</var> 为按照 [13.2](ES5/functions#creating-function-objects "wikilink") 规定，以 ** 作为参数列表和 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 函数体创建的一个新的函数对象。传入当前执行中的执行环境的 [LexicalEnvironment](ES5/execution#LexicalEnvironment "wikilink") 作为 **Scope**。假如 ** 包含在[严格模式代码中或者](ES5/execution#strict-mode-code "wikilink") *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，传入 **true** 为严格模式标志。
3.  令 <var>desc</var> 为[属性描述对象](ES5/types#property-descriptor "wikilink") {[[Set]]: <var>closure</var>, [[Enumerable]]: **true**, [[Configurable]]: **true**}。
4.  返回[属性标识符](ES5/types#property-identifier "wikilink") (<var>propName</var>, <var>desc</var>)。

假如 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 是[严格模式或者被包含在](ES5/execution#strict-mode-code "wikilink")[严格模式代码内](ES5/execution#strict-mode-code "wikilink")，** 中的 **，**"eval"** 或者 **"arguments"** 作为标识符将会是一个语法错误。

产生式 ** ''': ''' *[IdentifierName](ES5/lexical#IdentifierName "wikilink")* 按照下面的过程执行：

1.  返回一个包含跟 *[IdentifierName](ES5/lexical#IdentifierName "wikilink")* 完全相同的字符序列的字符串值。

产生式 ** ''': ''' *[StringLiteral](ES5/lexical#StringLiteral "wikilink")* 按照下面的过程执行：

1.  返回 *[StringLiteral](ES5/lexical#StringLiteral "wikilink")* 的字符串值。

产生式 ** **:** *[NumericLiteral](ES5/lexical#NumericLiteral "wikilink")* 按照下面的过程执行：

1.  令 <var>nbr</var> 为求 *[NumericLiteral](ES5/lexical#NumericLiteral "wikilink")* 值的结果。
2.  返回 [ToString](ES5/conversion#to-string "wikilink")(<var>nbr</var>)。

### 群组运算符 

产生式 ** **:** **(** ** **)** 按照下面的过程执行：

1.  返回执行 ** 的结果。这可能是一个 [Reference](ES5/types#Reference "wikilink")。

左值表达式
----------

`   `*<b id="MemberExpression">`MemberExpression`</b>*` :`
`       `**
`       `*[`FunctionExpression`](ES5/functions#FunctionExpression "wikilink")*
`       `**` `**`[`**` `**` `**`]`**
`       `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*
`       `**`new`**` `**` `**

`   `*<b id="NewExpression">`NewExpression`</b>*` :`
`       `**
`       `**`new`**` `**

`   `*<b id="CallExpression">`CallExpression`</b>*` :`
`       `**` `**
`       `**` `**
`       `**` `**`[`**` `**` `**`]`**
`       `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*

`   `*<b id="Arguments">`Arguments`</b>*` :`
`       `**`(` `)`**
`       `**`(`**` `**` `**`)`**

`   `*<b id="ArgumentList">`ArgumentList`</b>*` :`
`       `**
`       `**` `**`,`**` `**

`   `*<b id="LeftHandSideExpression">`LeftHandSideExpression`</b>*` :`
`       `**
`       `**

### 属性访问 

属性是通过 name 来访问的，可以使用点表示法访问

`   `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*
`   `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*

或者括号表示法访问

`   `**` `**`[`**` `**` `**`]`**` `
`   `**` `**`[`**` `**` `**`]`**

点表示法是根据以下的语法转换解释

`   `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*

这会等同于下面这个行为

`   `**` `**`[`**` `*<identifier-name-string>*` `**`]`**

类似地，

`   `**` `**`.`**` `*[`IdentifierName`](ES5/lexical#IdentifierName "wikilink")*

是等同于下面的行为

`   `**` `**`[`**` `*<identifier-name-string>*` `**`]`**

*<identifier-name-string>* 是一个字符串字面量，它与 Unicode 编码后的 *[IdentifierName](ES5/lexical#IdentifierName "wikilink")* 包含相同的字符序列。

产生式 ** **:** ** **[** ** **]** 按照下面的过程执行：

1.  令 <var>baseReference</var> 为解释执行 ** 的结果。
2.  令 <var>baseValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>baseReference</var>)。
3.  令 <var>propertyNameReference</var> 为解释执行 ** 的结果。
4.  令 <var>propertyNameValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>propertyNameReference</var>)。
5.  调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")(<var>baseValue</var>)。
6.  令 <var>propertyNameString</var> 为 [ToString](ES5/conversion#to-string "wikilink")(<var>propertyNameValue</var>)。
7.  如果正在执行中的语法产生式包含在[严格模式代码当中](ES5/execution#strict-mode-code "wikilink")，令 <var>strict</var> 为 **true**，否则令 <var>strict</var> 为 **false**。
8.  返回一个值类型的[引用](ES5/types#Reference "wikilink")，其基值为 <var>baseValue</var> 且其引用名为 <var>propertyNameString</var>，严格模式标记为 <var>strict</var>。

产生** **:** ** **[** ** **]**的执行方式与以上执行过程完全一样，除非**在步骤1已经执行过。

### new 运算符 

产生式 ** **:** **new** ** 按照下面的过程执行：

1.  令 <var>ref</var> 为解释执行 ** 的结果。
2.  令 <var>constructor</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>ref</var>)。
3.  如果 [Type](ES5/types#Type "wikilink")(<var>constructor</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
4.  如果 <var>constructor</var> 没有实现 [[[Construct]]](ES5/types#Construct "wikilink") 内置方法，抛出一个 **TypeError** 异常。
5.  返回调用 <var>constructor</var> 的 [[[Construct]]](ES5/types#Construct "wikilink") 内置方法的结果，传入按无参数传入参数列表（就是一个空的参数列表）。

产生式 ** **:** **new** ** ** 按照下面的过程执行 :

1.  令 <var>ref</var> 为解释执行 ** 的结果。
2.  令 <var>constructor</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>ref</var>)。
3.  令 <var>argList</var> 为解释执行 ** 的结果，是一个参数值的内部列表（[11.2.4](#argument-lists "wikilink")）。
4.  如果 [Type](ES5/types#Type "wikilink")(<var>constructor</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
5.  如果 <var>constructor</var> 没有实现 [[[Construct]]](ES5/types#Construct "wikilink") 内置方法，抛出一个 **TypeError** 异常。
6.  返回以 <var>argList</var> 为参数调用 <var>constructor</var> 的 [[[Construct]]](ES5/types#Construct "wikilink") 内置方法的结果。

### 函数调用 

产生式 ** **:** ** ** 按照下面的过程执行 :

1.  令 <var>ref</var> 为解释执行 ** 的结果。
2.  令 <var>func</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>ref</var>)。
3.  令 <var>argList</var> 为解释执行 ** 的结果，产生参数值们的内部列表（参见 [11.2.4](#argument-lists "wikilink")）。
4.  如果 [Type](ES5/types#Type "wikilink")(<var>func</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
5.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>func</var>) 为 **false**，抛出一个 **TypeError** 异常。
6.  如果 [Type](ES5/types#Type "wikilink")(<var>ref</var>) 为 [Reference](ES5/types#Reference "wikilink")，那么
    1.  如果 [IsPropertyReference](ES5/types#IsPropertyReference "wikilink")(<var>ref</var>) 为 **true**，那么
        1.  令 <var>thisValue</var> 为 [GetBase](ES5/types#GetBase "wikilink")(<var>ref</var>)。

    2.  否则，<var>ref</var> 的基值是一个[环境记录项](ES5/execution#environment-record "wikilink")。
        1.  令 <var>thisValue</var> 为调用 [GetBase](ES5/types#GetBase "wikilink")(<var>ref</var>) 的 [ImplicitThisValue](ES5/execution#ImplicitThisValue "wikilink") 具体方法的结果。

7.  否则，[Type](ES5/types#Type "wikilink")(<var>ref</var>) 不是 [Reference](ES5/types#Reference "wikilink")。
    1.  令 <var>thisValue</var> 为 **undefined**。

8.  返回调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内置方法的结果，传入 <var>thisValue</var> 作为 **this** 值和列表 <var>argList</var> 作为参数列表。

### 参数列表 

产生式 ** **:** **( )** 按照下面的过程执行：

1.  返回一个空[列表](ES5/types#List "wikilink")。

产生式 ** **:** '''( ''' ** **)** 按照下面的过程执行：

1.  返回解释执行 ** 的结果。

产生式 ** **:** ** 按照下面的过程执行：

1.  令 <var>ref</var> 为解释执行 ** 的结果。
2.  令 <var>arg</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>ref</var>)。
3.  返回唯一的项目是 <var>arg</var> 的[列表](ES5/types#List "wikilink")。

产生式 ** **:** ** **,** ** 按照下面的过程执行 :

1.  令 <var>precedingArgs</var> 为解释执行 ** 的结果。
2.  令 <var>ref</var> 为解释执行 ** 的结果。
3.  令 <var>arg</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>ref</var>)。
4.  返回一个[列表](ES5/types#List "wikilink")，长度比 <var>precedingArgs</var> 大 1 且它的项目为 <var>precedingArgs</var> 的项目按顺序在后面接 <var>arg</var>，<var>arg</var> 就是这个新的列表的最后一个项目。

### 函数表达式 

产生式 ** **:** *[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 按照下面的过程执行 :

1.  返回解释执行 *[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 的结果。

后缀表达式 
-----------

`   `*<b id="PostfixExpression">`PostfixExpression`</b>*` :`
`       `**
`       `**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`++`**` `
`       `**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`--`**

### 后缀自增运算符

产生式 <var>PostfixExpression</var> **:** ** [[no *LineTerminator* here](ES5/notation#restricted-production "wikilink")] **++** 按照下面的过程执行：

1.  令 <var>lhs</var> 为解释执行 ** 的结果。
2.  假如以下所有条件都为真，抛出一个 **SyntaxError** 异常：
    -   [Type](ES5/types#Type "wikilink")(<var>lhs</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>lhs</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>lhs</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>lhs</var>) 为 **"eval"** 或 **"arguments"**

3.  令 <var>oldValue</var> 为 [ToNumer](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>lhs</var>))。
4.  令 <var>newValue</var> 为 **1** 加上 <var>oldValue</var> 的结果，使用与 **+** 运算符 相同的规则（参见 [11.6.3](#additive-operators "wikilink")）。
5.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lhs</var>, <var>newValue</var>)。
6.  返回 <var>oldValue</var>。

### 后缀自减运算符

产生式 <var>PostfixExpression</var> **:** ** [[no *LineTerminator* here](ES5/notation#restricted-production "wikilink")] '''-- ''' 按照下面的过程执行：

1.  令 <var>lhs</var> 为解释执行 ** 的结果。
2.  假如以下所有条件都为真，抛出一个 **SyntaxError** 异常：
    -   [Type](ES5/types#Type "wikilink")(<var>lhs</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>lhs</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>lhs</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>lhs</var>) 为 **"eval"** 或 **"arguments"**

3.  令 <var>oldValue</var> 为 [ToNumer](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>lhs</var>))。
4.  令 <var>newValue</var> 为从 <var>oldValue</var> 减掉 **1** 的结果，使用与 **-** 运算符 相同的规则（参见 [11.6.3](#additive-operators "wikilink")）。
5.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lhs</var>, <var>newValue</var>)。
6.  返回 <var>oldValue</var>。

一元运算符 
-----------

`   `*<b id="UnaryExpression">`UnaryExpression`</b>*` :`
`       `**
`       `**`delete`**` `**
`       `**`void`**` `**
`       `**`typeof`**` `**
`       `**`++`**` `**
`       `**`--`**` `**
`       `**`+`**` `**
`       `**`-`**` `**
`       `**`~`**` `**
`       `**`!`**` `**

### delete 运算符 

产生式 ** **:** **delete** ** 按照下面的过程执行 :

1.  令 <var>ref</var> 为解释执行 ** 的结果。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>ref</var>) 不是 [Reference](ES5/types#Reference "wikilink")，返回 **true**。
3.  若 [IsUnresolvableReference](ES5/types#IsUnresolvableReference "wikilink")(<var>ref</var>) 则
    1.  如果 [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>ref</var>) 为 **true**，抛出一个 **SyntaxError** 异常。
    2.  否则，返回 **true**。

4.  如果 [IsPropertyReference](ES5/types#IsPropertyReference "wikilink")(<var>ref</var>) 为 **true** 则：
    1.  返回以 [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>ref</var>) 和 [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>ref</var>) 做为参数调用 [ToObject](ES5/conversion#to-object "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>ref</var>)) 的 [[[Delete]]](ES5/types#Delete "wikilink") 内置方法的结果。

5.  否则，<var>ref</var> 是到[环境记录项绑定的](ES5/execution#environment-record "wikilink") [Reference](ES5/types#Reference "wikilink")，所以：
    1.  如果 [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>ref</var>) 为 **true**，抛出一个 **SyntaxError** 异常。
    2.  令 <var>bindings</var> 为 [GetBase](ES5/types#GetBase "wikilink")(<var>ref</var>)。
    3.  返回以 [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>ref</var>) 为参数调用 <var>bindings</var> 的 [DeleteBinding](ES5/execution#DeleteBinding "wikilink") 具体方法的结果。

### void 运算符

产生式 ** **:** **void** ** 按照下面的过程执行 :

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  调用 [GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>)。
3.  返回 **undefined**。

### typeof 运算符 

产生式 ** **:** **typeof** ** 按照下面的过程执行 :

1.  令 <var>val</var> 为解释执行 ** 的结果。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>val</var>) 为 [Reference](ES5/types#Reference "wikilink")，则：
    1.  如果 [IsUnresolvableReference](ES5/types#IsUnresolvableReference "wikilink")(<var>val</var>) 为 **true**，返回 **"undefined"**。
    2.  令 <var>val</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>val</var>)。

3.  返回根据 **表20** 由 [Type](ES5/types#Type "wikilink")(<var>val</var>) 决定的字符串。

|---|---|
|val 类型|结果|
|Undefined|**"undefined"**|
|Null|**"object"**|
|Boolean|**"boolean"**|
|Number|**"number"**|
|String|**"string"**|
|Object（原生，且没有实现 [[[Call]]](ES5/types#Call "wikilink")）|**"object"**|
|Object（原生或者宿主且实现了 [[[Call]]](ES5/types#Call "wikilink")）|**"function"**|
|Object（宿主且没实现 [[[Call]]](ES5/types#Call "wikilink")）|由实现定义，但不能是 **"undefined"**、**"boolean"**、**"number"** 或 **"string"**。|

### 前自增运算符 

产生式 ** **:** **++** ** 按照下面的过程执行：

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  假如以下所有条件都为真，抛出一个 **SyntaxError** 异常：
    -   [Type](ES5/types#Type "wikilink")(<var>expr</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>expr</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>expr</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>expr</var>) 为 **"eval"** 或 **"arguments"**

3.  令 <var>oldValue</var> 为 [ToNumer](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。
4.  令 <var>newValue</var> 为 **1** 加上 <var>oldValue</var> 的结果，使用与 **+** 运算符 相同的规则（参见 [11.6.3](#additive-operators "wikilink")）。
5.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>expr</var>, <var>newValue</var>)。
6.  返回 <var>newValue</var>。

### 前自减运算符 

产生式 ** **:** '''-- ''' ** 按照下面的过程执行：

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  假如以下所有条件都为真，抛出一个 **SyntaxError** 异常：
    -   [Type](ES5/types#Type "wikilink")(<var>expr</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>expr</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>expr</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>expr</var>) 为 **"eval"** 或 **"arguments"**

3.  令 <var>oldValue</var> 为 [ToNumer](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。
4.  令 <var>newValue</var> 为从 <var>oldValue</var> 减掉 **1** 的结果，使用与 **-** 运算符 相同的规则（参见 [11.6.3](#additive-operators "wikilink")）。
5.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>expr</var>, <var>newValue</var>)。
6.  返回 <var>newValue</var>。

### 一元 + 运算符 

产生式 ** **:** **+** ** 按照下面的过程执行 :

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  返回 [ToNumber](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。

### 一元 - 运算符 

产生式 ** **:** **-** ** 按照下面的过程执行：

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  令 <var>oldValue</var> 为 [ToNumber](ES5/conversion#to-number "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。
3.  如果 <var>oldValue</var> 为 **NaN**，返回 **NaN**。
4.  返回 <var>oldValue</var> 取负（即，算出一个数字相同但是符号相反的值）的结果。

### 按位非运算符 

产生式 ** **:** **\~** ** 按照下面的过程执行：

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  令 <var>oldValue</var> 为 [ToInt32](ES5/conversion#to-int32 "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。
3.  返回 <var>oldValue</var> 按位取反的结果。结果为 32位 有符号整数。

### 逻辑非运算符 

产生式 ** **:** **!** ** 按照下面的过程执行 :

1.  令 <var>expr</var> 为解释执行 ** 的结果。
2.  令 <var>oldValue</var> 为 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>expr</var>))。
3.  如果 <var>oldValue</var> 为 **true**，返回 **false**。
4.  返回 **true**。

乘法运算符
----------

`   `*<b id="MultiplicativeExpression">`MultiplicativeExpression`</b>*` :`
`       `**
`       `**` `**`*`**` `**
`       `**` `**`/`**` `**
`       `**` `**`%`**` `**

产生式 ** **:** ** *@* **，其中 @ 表示上面定义的运算符其一，按照下面的过程执行：

1.  令 <var>left</var> 为解释执行 ** 的结果。
2.  令 <var>leftValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>left</var>)。
3.  令 <var>right</var> 为解释执行 ** 的结果。
4.  令 <var>rightValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>right</var>)。
5.  令 <var>leftNum</var> 为 [ToNumber](ES5/conversion#to-number "wikilink")(<var>leftValue</var>)。
6.  令 <var>rightNum</var> 为 [ToNumber](ES5/conversion#to-number "wikilink")(<var>rightValue</var>)。
7.  返回将特定运算符 (**\***, **/** 或 **%**) 作用于 <var>leftNum</var> 和 <var>rightNum</var> 的结果。参见 [11.5.1](#times-operator "wikilink")、[11.5.2](#divide-operator "wikilink")、[11.5.3](#mod-operator "wikilink") 后的注解。

### 使用 \* 运算符 

**\*** 运算符表示乘法，产生操作数的乘积。乘法运算满足交换律。因为精度问题，乘法不总是满足结合律。

浮点数的乘法遵循 IEEE 754 二进制双精度幅度浮点算法规则：

-   若两个操作数之一为 **NaN**，结果为 **NaN**。
-   假如两个操作数的正负号相同，结果就是正的，如果不同就是负的。
-   无穷大被零乘结果是 **NaN**。
-   无穷大被无穷大乘结果就是无穷大。符号按照前面说过的规则决定。
-   无穷大被有穷的非零值乘结果是带正负号的无穷大。符号仍然按照前面说过的规则决定。
-   其它情况下，既没有无穷大也没有 **NaN** 参与运算，结果计算出来后会按照 [IEEE 754 round-to-nearest](http://en.wikipedia.org/wiki/IEEE_floating_point#Roundings_to_nearest) 取到最接近的能表示的数。如果值过大不能表示，则结果为相应的正负无穷大。如果值过小不能表示，则结果为相应的正负零。ECMAScript 要求支持 IEEE 754 规定的渐进下溢。

### 使用 / 运算符 

**/** 运算符表示除法，产生操作数的商。左操作数是被除数，右操作数是除数。ECMAScript 不支持整数除法。所有除法运算的操作数和结果都是双精度浮点数。浮点数的除法遵循 IEEE 754 二进制双精度幅度浮点算法规则：

-   若两个操作数之一为 **NaN**，结果为 **NaN**。
-   假如两个操作数的正负号相同，结果就是正的，如果不同就是负的。
-   无穷大被无穷大除结果是 **NaN**。
-   无穷大被零除结果是无穷大。符号按照前面说过的规则决定。
-   无穷大被非零有穷的值除结果是有正负号的无穷大。符号按照前面说过的规则决定。
-   有穷的非零值被无穷大除结果是零。符号按照前面说过的规则决定。
-   零被零除结果是 **NaN**；零被其它有穷数除结果是零，符号按照前面说过的规则决定。
-   有穷的非零值被零除结果是有正负号的无穷大。符号按照前面说过的规则决定。
-   其它情况下，既没有无穷大也没有 **NaN** 参与运算，结果计算出来后会按照 [IEEE 754 round-to-nearest](http://en.wikipedia.org/wiki/IEEE_floating_point#Roundings_to_nearest) 取到最接近的能表示的数。如果值过大不能表示，则结果为相应的正负无穷大。如果值过小不能表示，则结果为相应的正负零。ECMAScript 要求支持 IEEE 754 规定的渐进下溢。

### 使用 % 运算符 

**%** 运算符产生其运算符在除法中的余数。左操作数是被除数，右操作数是除数。

浮点数使用 **%** 运算符的余数运算与 IEEE 754 所定义的 “remainder” 运算不完全相同。IEEE 754 “remainder” 运算做邻近取整除法的余数计算，而不是舍尾除法，这样它的行为跟通常意义上的整数余数运算符行为不一致。而 ECMAScript 语言定义浮点操作 **%** 为与 Java 取余运算符一致；可以参照 C 库中的函数 fmod。

ECMAScript 浮点数的取余法遵循 IEEE 754 二进制双精度幅度浮点算法规则：

-   若两个操作数之一为 **NaN**，结果为 **NaN**。
-   结果的符号等于被除数。
-   若被除数是无穷大或者除数是零，或者两者皆是，结果就是 **NaN**。
-   若被除数有穷而除数为无穷大，结果为被除数。
-   若被除数为零且除数非零且有穷，结果与被除数相同。
-   其它情况下，既没有零或无穷大，也没有 **NaN** 参与运算，从被除数 <var>n</var> 和除数 <var>d</var> 得到浮点数余数 <var>r</var> 以数学关系式 <var>r</var> = <var>n</var> ? (<var>d</var> × <var>q</var>) 定义，其中 <var>q</var> 是个整数，在 <var>n</var> / <var>d</var> 为负时为负，在 <var>n</var> / <var>d</var> 为正时为正，它应该在不超过 <var>n</var> 和 <var>d</var> 的商的前提下尽可能大。结果计算出来后会按照 [IEEE 754 round-to-nearest](http://en.wikipedia.org/wiki/IEEE_floating_point#Roundings_to_nearest) 取到最接近的能表示的数。

加法运算符
----------

`   `*<b id="AdditiveExpression">`AdditiveExpression`</b>*` :`
`       `**
`       `**` `**`+`**` `**
`       `**` `**`-`**` `**

### 加法运算符（+） 

加法运算符启动字符串相接或是数值相加。

产生式 ** **:** ** **+** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lprim</var> 为 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>lval</var>)。
6.  令 <var>rprim</var> 为 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>rval</var>)。
7.  如果 [Type](ES5/types#Type "wikilink")(<var>lprim</var>) 为 **String** 或者 [Type](ES5/types#Type "wikilink")(<var>rprim</var>) 为 String，则：
    1.  返回由 [ToString](ES5/conversion#to-string "wikilink")(<var>lprim</var>) 和 [ToString](ES5/conversion#to-string "wikilink")(<var>rprim</var>) 连接而成的字符串。

8.  返回将加法运算作用于 [ToNumber](ES5/conversion#to-number "wikilink")(<var>lprim</var>) 和 [ToNumber](ES5/conversion#to-number "wikilink")(<var>rprim</var>) 的结果。参见 [11.6.3](#additive-operators "wikilink") 后的注解。

### 减法运算符（-） 

产生式 ** **:** ** **-** ** 按照下面的过程执行 :

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lnum</var> 为 [ToNumber](ES5/conversion#to-number "wikilink")(<var>lval</var>)。
6.  令 <var>rnum</var> 为 [ToNumber](ES5/conversion#to-number "wikilink")(<var>rval</var>)。
7.  返回返回将减法运算作用于 <var>lnum</var> 和 <var>rnum</var> 的结果。参见 [11.6.3](#additive-operators "wikilink") 后的注解。

### 加法作用于数字 

**+** 运算符作用于两个数字类型的操作数时表示加法，产生两个操作数之和。**-** 运算符表示剑法，产生两个数字之差。

加法是满足交换律的运算，但是不总满足结合律。

加法遵循 IEEE 754 二进制双精度幅度浮点算法规则：

-   若两个操作数之一为 **NaN**，结果为 **NaN**。
-   两个正负号相反的无穷之和为 **NaN**。
-   两个正负号相同的无穷大之和是具有相同正负的无穷大。
-   无穷大和有穷值之和等于操作数中的无穷大。
-   两个负零之和为 **-0**。
-   两个正零，或者两个正负号相反的零之和为 **+0**。
-   零与非零有穷值之和等于非零的那个操作数。
-   两个大小相等，符号相反的非零有穷值之和为 **+0**。
-   其它情况下，既没有无穷大也没有 **NaN** 或者零参与运算，并且操作数要么大小不等，要么符号相同，结果计算出来后会按照 [IEEE 754 round-to-nearest](http://en.wikipedia.org/wiki/IEEE_floating_point#Roundings_to_nearest) 取到最接近的能表示的数。如果值过大不能表示，则结果为相应的正负无穷大。如果值过小不能表示，则结果为相应的正负零。ECMAScript 要求支持 IEEE 754 规定的渐进下溢。

**-** 运算符作用于两个数字类型时表示减法，产生两个操作数之差。左边操作数是被减数右边是减数。给定操作数 <var>a</var> 和 <var>b</var>，总是有 <var>a</var>–<var>b</var> 产生与 <var>a</var> + (-<var>b</var>) 产生相同结果。

移位运算符
----------

`   `*<b id="ShiftExpression">`ShiftExpression`</b>*` :`
`       `**
`       `**` `**`<<`**` `**
`       `**` `**`>>`**` `**
`       `**` `**`>>>`**` `**

### 左移位运算符（\<\<） 

对左边参数执行右边参数指定大小的左移位运算。

产生式 ** **:** ** **\<\<** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lnum</var> 为 [ToInt32](ES5/conversion#to-int32 "wikilink")(<var>lval</var>)。
6.  令 <var>rnum</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>rval</var>)。
7.  令 <var>shiftCount</var> 为用掩码算出 <var>rnum</var> 的最后五个比特位，即计算 <var>rnum</var> & **0x1F** 的结果。
8.  返回 <var>lnum</var> 左移 <var>shiftCount</var> 比特位的结果。结果是一个有符号 32位 整数。

### 带号右移位运算符（\>\>） 

对左边参数执行右边参数指定大小的右移位带号填充运算。

产生式 ** **:** ** **\>\>** ** 按照下面的过程执行 :

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lnum</var> 为 [ToInt32](ES5/conversion#to-int32 "wikilink")(<var>lval</var>)。
6.  令 <var>rnum</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>rval</var>)。
7.  令 <var>shiftCount</var> 为用掩码算出 <var>rnum</var> 的最后五个比特位，即计算 <var>rnum</var> & **0x1F** 的结果。
8.  返回 <var>lnum</var> 带符号扩展的右移 <var>shiftCount</var> 比特位的结果。将位用最大的比特填满。结果是一个有符号 32位 整数。

### 不带号右移位运算符（\>\>\>） 

对左边参数执行右边参数指定大小的右移位填零运算。

产生式 ** **:** ** **\>\>\>** ** 按照下面的过程执行 :

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lnum</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lval</var>)。
6.  令 <var>rnum</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>rval</var>)。
7.  令 <var>shiftCount</var> 为用掩码算出 <var>rnum</var> 的最后五个比特位，即计算 <var>rnum</var> & **0x1F** 的结果。
8.  返回 <var>lnum</var> 做零填充右移 <var>shiftCount</var> 比特位的结果。缺少的比特位填零。结果是一个无符号 32位 整数。

关系运算符
----------

`   `*<b id="RelationalExpression">`RelationalExpression`</b>*` :`
`       `**
`       `**` `**`<`**` `**
`       `**` `**`>`**` `**
`       `**` `**`<=`**` `**
`       `**` `**`>=`**` `**
`       `**` `**`instanceof`**` `**
`       `**` `**`in`**` `**

`   `*<b id="RelationalExpressionNoIn">`RelationalExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`<`**` `**
`       `**` `**`>`**` `**
`       `**` `**`<=`**` `**
`       `**` `**`>=`**` `**
`       `**` `**`instanceof`**` `**

关系运算符的执行结果总是一个表示运算符代表的关系在两个参数之间成立与否的 **Boolean** 值。

除了要执行内有的 ** 而不是** 以外，产生式 ** 的执行方式与产生式 ** 的执行方式相同。

### 小于运算符（\>）

产生式 ** **:** ** **\<** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为启用[抽象关系比较](#relational-algorithm "wikilink") <var>lval</var> \< <var>rval</var>（参见 [11.8.5](#relational-algorithm "wikilink")) 的结果。
6.  如果 <var>r</var> 为 **undefined**，返回 **false**。否则，返回 <var>r</var>。

### 大于运算符（\>）

产生式 ** **:** ** **\>** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为启用[抽象关系比较](#relational-algorithm "wikilink") <var>rval</var> \< <var>lval</var> 的结果，参数 <var>LeftFirst</var> 设为 **false**。（参见 [11.8.5](#relational-algorithm "wikilink"))
6.  如果 <var>r</var> 为 **undefined**，返回 **false**。否则，返回 <var>r</var>。

=== 小于等于运算符（\<=） ===

产生式 ** **:** ** **\<=** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为启用[抽象关系比较](#relational-algorithm "wikilink") <var>rval</var> \< <var>lval</var> 的结果，参数 <var>LeftFirst</var> 设为 **false**。（参见 [11.8.5](#relational-algorithm "wikilink"))
6.  如果 <var>r</var> 为 **true** 或者 **undefined** ，返回 **false**。否则，返回 **true**。

=== 大于等于运算符（\>=） ===

产生式 ** **:** ** **\>=** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为启用[抽象关系比较](#relational-algorithm "wikilink") <var>lval</var> \< <var>rval</var> 的结果。（参见 [11.8.5](#relational-algorithm "wikilink"))
6.  如果 <var>r</var> 为 **true** 或者 **undefined**，返回 **false**。否则，返回 **true**。

### 抽象关系比较算法  

以 <var>x</var> 和 <var>y</var> 为值进行小于比较（<var>x</var> \< <var>y</var> 的比较），会产生的结果可为 **true**、**false** 或 **undefined**（这说明 <var>x</var>、<var>y</var> 中最少有一个操作数是 **NaN**）。除了 <var>x</var> 和 <var>y</var>，这个算法另外需要一个名为 <var>LeftFirst</var> 的布尔值标记作为参数。这个标记用于解析顺序的控制，因为操作数 <var>x</var> 和 <var>y</var> 在执行的时候会有潜在可见的副作用。这个标志的存在是必须的，因为 ECMAScript 规定了表达式是从左到右顺序执行。<var>LeftFirst</var> 的默认值是 **true**，这表明在相关的表达式中，参数 <var>x</var> 出现在参数 <var>y</var> 之前。如果 <var>LeftFirst</var> 值是 **false**，情况会相反，操作数的执行必须是先 <var>y</var> 后 <var>x</var>。这样的一个小于比较的执行步骤如下：

1.  如果 <var>LeftFirst</var> 标志是 **true**，那么
    1.  让 <var>px</var> 为调用 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>x</var>, 暗示 **Number** 类型) 的结果。
    2.  让 <var>py</var> 为调用 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>y</var>, 暗示 **Number** 类型) 的结果。

2.  否则解释执行的顺序需要反转，从而保证从左到右的执行顺序
    1.  让 <var>py</var> 为调用 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>y</var>, 暗示 **Number** 类型) 的结果。
    2.  让 <var>px</var> 为调用 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>x</var>, 暗示 **Number** 类型) 的结果。

3.  如果 [Type](ES5/types#Type "wikilink")(<var>px</var>) 和 [Type](ES5/types#Type "wikilink")(<var>py</var>) 得到的结果不都是 **String** 类型，那么
    1.  让 <var>nx</var> 为调用 [ToNumber](ES5/conversion#to-number "wikilink")(<var>px</var>) 的结果。因为 <var>px</var> 和 <var>py</var> 都已经是[基本数据类型](ES5/types#primitive "wikilink")（primitive values 也作原始值），其执行顺序并不重要。
    2.  让 <var>ny</var> 为调用 [ToNumber](ES5/conversion#to-number "wikilink")(<var>py</var>) 的结果。
    3.  如果 <var>nx</var> 是 **NaN**，返回 **undefined**。
    4.  如果 <var>ny</var> 是 **NaN**，返回 **undefined**。
    5.  如果 <var>nx</var> 和 <var>ny</var> 的数字值相同，返回 **false**。
    6.  如果 <var>nx</var> 是 **+0** 且 <var>ny</var> 是 **-0**，返回 **flase**。
    7.  如果 <var>nx</var> 是 **-0** 且 <var>ny</var> 是 **+0**，返回 **false**。
    8.  如果 <var>nx</var> 是 **+∞**，返回 **fasle**。
    9.  如果 <var>ny</var> 是 **+∞**，返回 **true**。
    10. 如果 <var>ny</var> 是 **-∞**，返回 **false**。
    11. 如果 <var>nx</var> 是 **-∞**，返回 **true**。
    12. 如果 <var>nx</var> 数学上的值小于 <var>ny</var> 数学上的值（注意这些数学值都不能是无限的且不能都为 0），返回 **ture**。否则返回 **false**。

4.  否则，<var>px</var> 和 <var>py</var> 都是 Strings 类型
    1.  如果 <var>py</var> 是 <var>px</var> 的一个前缀，返回 **false**。（当字符串 <var>q</var> 的值可以是字符串 <var>p</var> 和一个其他的字符串 <var>r</var> 拼接而成时，字符串 <var>p</var> 就是 <var>q</var> 的前缀。注意：任何字符串都是自己的前缀，因为 <var>r</var> 可能是空字符串。）
    2.  如果 <var>px</var> 是 <var>py</var> 的前缀，返回 **true**。
    3.  让 <var>k</var> 成为最小的非负整数，能使得在 <var>px</var> 字符串中位置 <var>k</var> 的字符与字符串 <var>py</var> 字符串中位置 <var>k</var> 的字符不相同。（因为 <var>px</var> 与 <var>py</var> 不是彼此的前綴，这里 <var>k</var> 必然存在。）
    4.  让 <var>m</var> 为字符串 <var>px</var> 中位置 <var>k</var> 的字符的编码单元值。
    5.  让 <var>n</var> 成为字符串 <var>py</var> 中位置 <var>k</var> 的字符的编码单元值。
    6.  如果 <var>m</var> \< <var>n</var>，返回 **true**。否则，返回 **false**。

### instanceof 运算符  

产生式 ****:** ** **instanceof** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  如果 [Type](ES5/types#Type "wikilink")(<var>rval</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
6.  如果 <var>rval</var> 没有 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内置方法，抛出一个 **TypeError** 异常。
7.  返回以参数 <var>lval</var> 调用 <var>rval</var> 的 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内置方法的结果。

### in 运算符  

产生式 ** **:** ** **in** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  如果 [Type](ES5/types#Type "wikilink")(<var>rval</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
6.  返回以参数 [ToString](ES5/conversion#to-string "wikilink")(<var>lval</var>) 调用 <var>rval</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内置方法的结果。

等值运算符
----------

`   `*<b id="EqualityExpression">`EqualityExpression`</b>*` :`
`       `**
`       `**` `**`==`**` `**
`       `**` `**`!=`**` `**
`       `**` `**`===`**` `**
`       `**` `**`!==`**` `**

`   `*<b id="EqualityExpressionNoIn">`EqualityExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`==`**` `**
`       `**` `**`!=`**` `**
`       `**` `**`===`**` `**
`       `**` `**`!==`**` `**

等值运算符的执行结果总是一个表示运算符代表的关系在两个参数之间成立与否的 **Boolean** 值。

除了要执行内有的 ** 与 ** 而不是** 与 ** 以外，产生式 ** 的执行方式与产生式 ** 的执行方式相同。

=== 等于运算符（==） ===

产生式 ** **:** ** **==** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  返回做用[抽象相等比较算法于](#equility-algorithm "wikilink") <var>rval</var> == <var>lval</var>（参见 [11.9.3](#equility-algorithm "wikilink")）的结果。

=== 不等于运算符（!=） ===

产生式 ** **:** ** **!=** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为做用[抽象相等比较算法于](#equility-algorithm "wikilink") <var>rval</var> == <var>lval</var>（参见 [11.9.3](#equility-algorithm "wikilink")）的结果。
6.  如果 <var>r</var> 为 **true**，返回 **false**。否则，返回 **true**。

### 抽象相等比较算法 

以 <var>x</var> 和 <var>y</var> 为值进行 <var>x</var> == <var>y</var> 比较会产生的结果可为 **true** 或 **false**。比较的执行步骤如下：

1.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 与 [Type](ES5/types#Type "wikilink")(<var>y</var>) 相同， 则
    1.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **Undefined**， 返回 **true**。
    2.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>)为 **Null**， 返回 **true**。
    3.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>)为 **Number**，则
        1.  若 <var>x</var> 为 **NaN**，返回 **false**。
        2.  若 <var>y</var> 为 **NaN**，返回 **false**。
        3.  若 <var>x</var> 与 <var>y</var> 为相等数值，返回 **true**。
        4.  若 <var>x</var> 为 **+0** 且 <var>y</var> 为 **?0**，返回 **true**。
        5.  若 <var>x</var> 为 **?0** 且 <var>y</var> 为 **+0**，返回 **true**。
        6.  返回 **false**。

    4.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **String**，则当 <var>x</var> 和 <var>y</var> 为完全相同的字符序列（长度相等且相同字符在相同位置）时返回 **true**。否则，返回 **false**。
    5.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **Boolean**，当 <var>x</var> 和 <var>y</var> 为同为 **true** 或者同为 **false** 时返回 **true**。否则，返回 **false**。
    6.  当 <var>x</var> 和 <var>y</var> 为引用同一对象时返回 **true**。否则，返回 **false**。

2.  若 <var>x</var> 为 **null** 且 <var>y</var> 为 **undefined**，返回 **true**。
3.  若 <var>x</var> 为 **undefined** 且 <var>y</var> 为 **null**，返回 **true**。
4.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **Number** 且 [Type](ES5/types#Type "wikilink")(<var>y</var>) 为 **String**，返回 <var>x</var> == [ToNumber](ES5/conversion#to-number "wikilink")(<var>y</var>) 的结果。
5.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **String** 且 [Type](ES5/types#Type "wikilink")(<var>y</var>) 为 **Number**，返回比较 [ToNumber](ES5/conversion#to-number "wikilink")(<var>x</var>) == <var>y</var> 的结果。
6.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **Boolean**，返回比较 [ToNumber](ES5/conversion#to-number "wikilink")(<var>x</var>) == <var>y</var> 的结果。
7.  若 [Type](ES5/types#Type "wikilink")(<var>y</var>) 为 **Boolean**，返回比较 <var>x</var> == [ToNumber](ES5/conversion#to-number "wikilink")(<var>y</var>) 的结果。
8.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **String** 或 **Number**，且 [Type](ES5/types#Type "wikilink")(<var>y</var>) 为 **Object**，返回比较 <var>x</var> == [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>y</var>) 的结果。
9.  若 [Type](ES5/types#Type "wikilink")(<var>x</var>) 为 **Object** 且 [Type](ES5/types#Type "wikilink")(<var>y</var>) 为 **String** 或 **Number**，返回比较 [ToPrimitive](ES5/conversion#to-primitive "wikilink")(<var>x</var>) == <var>y</var> 的结果。
10. 返回 **false**。

### 严格等于运算符（

） ===

产生式 ** **:** ** **===** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  返回做用[严格等于比较算法于](#strict-equality-comparison "wikilink") <var>rval</var> === <var>lval</var>（参见 [11.9.6](#strict-equality-comparison "wikilink")）的结果。

=== 严格不等于运算符（!==） ===

产生式 ** **:** ** **!==** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为做用[严格等于比较算法于](#strict-equality-comparison "wikilink") <var>rval</var> === <var>lval</var>（参见 [11.9.6](#strict-equality-comparison "wikilink")）的结果。
6.  如果 <var>r</var> 为 **true**，返回 **false**。否则，返回 **true**。

### 严格等于比较算法 

比较 <var>x</var> === <var>y</var>，<var>x</var> 和 <var>y</var> 为值，需要产出 **true** 或 **false**。比较过程如下：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 与 [Type](ES5/types#Type "wikilink")(<var>y</var>) 的结果不一致，返回 **false**。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Undefined**，返回 **true**。
3.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Null**，返回 **true**。
4.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Number**，则
    1.  如果 <var>x</var> 为 **NaN**，返回 **false**。
    2.  如果 <var>y</var> 为 **NaN**，返回 **false**。
    3.  如果 <var>x</var> 与 <var>y</var> 为同一个数字，返回 **true**。
    4.  如果 <var>x</var> 为 **+0**，<var>y</var> 为 **-0**，返回 **true**。
    5.  如果 <var>x</var> 为 **-0**，<var>y</var> 为 **+0**，返回 **true**。
    6.  返回 **false**。

5.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **String**，如果 <var>x</var> 与 <var>y</var> 为完全相同的字符序列（相同的长度和相同的字符对应相同的位置），返回 **true**，否则，返回 **false**。
6.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Boolean**，如果 <var>x</var> 与 <var>y</var> 都为 **true** 或 **false**，则返回 **true**，否则，返回 **false**。
7.  如果 <var>x</var> 和 <var>y</var> 引用到同一个 **Object** 对象，返回 **true**，否则，返回 **false**。

二元按位运算符
--------------

`   `*<b id="BitwiseANDExpression">`BitwiseANDExpression`</b>*` :`
`       `**
`       `**` `**`&`**` `**

`   `*<b id="BitwiseANDExpressionNoIn">`BitwiseANDExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`&`**` `**

`   `*<b id="BitwiseXORExpression">`BitwiseXORExpression`</b>*` :`
`       `**
`       `**` `**`^`**` `**

`   `*<b id="BitwiseXORExpressionNoIn">`BitwiseXORExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`^`**` `**

`   `*<b id="BitwiseORExpression">`BitwiseORExpression`</b>*` :`
`       `**
`       `**` `**`|`**` `**

`   `*<b id="BitwiseORExpressionNoIn">`BitwiseORExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`|`**` `**

产生式 <var>A</var> **:** <var>A</var> *@* <var>B</var>，其中 @ 是上述产生式中其中一个位运算符，按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 <var>A</var> 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 <var>B</var> 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>lnum</var> 为 [ToInt32](ES5/conversion#to-int32 "wikilink")(<var>lval</var>)。
6.  令 <var>rnum</var> 为 [ToInt32](ES5/conversion#to-int32 "wikilink")(<var>rval</var>)。
7.  返回作用位运算符 @ 作用到 <var>lnum</var> 和 <var>rnum</var> 的结果，是一个 32位 有符号整数。

二元逻辑运算符
--------------

`   `*<b id="LogicalANDExpression">`LogicalANDExpression`</b>*` :`
`       `**
`       `**` `**`&&`**` `**

`   `*<b id="LogicalANDExpressionNoIn">`LogicalANDExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`&&`**` `**

`   `*<b id="LogicalORExpression">`LogicalORExpression`</b>*` :`
`       `**
`       `**` `**`||`**` `**

`   `*<b id="LogicalORExpressionNoIn">`LogicalORExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`||`**` `**

产生式 ** **:** ** **&&** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>lval</var>) 为 **false**，返回 <var>lval</var>。
4.  令 <var>rref</var> 为解释执行 ** 的结果。
5.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。

产生式 ** **:** ** **||** ** 按照下面的过程执行 :

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>lval</var>) 为 **true**，返回 <var>lval</var>。
4.  令 <var>rref</var> 为解释执行 ** 的结果。
5.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。

除了要执行内有的 **、** 与 ** 而不是**、** 与 ** 以外，产生式 ** 与 ** 的执行方式与产生式 ** 与 ** 的执行方式相同。

条件运算符 
-----------

`   `*<b id="ConditionalExpression">`ConditionalExpression`</b>*` :`
`       `**
`       `**` `**`?`**` `**` `**`:`**` `**

`   `*<b id="ConditionalExpressionNoIn">`ConditionalExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`?`**` `**` `**`:`**` `**

产生式 ** **:** ** **?** ** **:** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)) 为 **true**，那么：
    1.  令 <var>trueRef</var> 为解释执行第一个 ** 的结果。
    2.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>trueRef</var>)。

3.  否则
    1.  令 <var>falseRef</var> 为解释执行第二个 ** 的结果。
    2.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>falseRef</var>)。

除了要执行内有的 **、** 与 ** 而不是**、** 与 ** 以外，产生式 ** 的执行方式与产生式 ** 的执行方式相同。

赋值运算符 
-----------

`   `*<b id="AssignmentExpression">`AssignmentExpression`</b>*` :`
`       `**
`       `**` `**` `**

`   `*<b id="AssignmentExpressionNoIn">`AssignmentExpressionNoIn`</b>*` :`
`       `**
`       `**` `**` `**

`   `*<b id="AssignmentOperator">`AssignmentOperator`</b>*` : 以下之一 `
`       `**`=` `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `>>>=` `&=` `^=` `|=`**` `

除了要执行内有的 ** 与 ** 而不是** 与 ** 以外，产生式 ** 的执行方式与产生式 ** 的执行方式相同。

=== 简单赋值（=） ===

产生式 ** **:** ** **=** ** 按照下面的过程执行 :

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>rref</var> 为解释执行 ** 的结果。
3.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
4.  抛出一个 **SyntaxError** 异常，当以下条件都成立 :
    -   [Type](ES5/types#Type "wikilink")(<var>lref</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>lref</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>lref</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>lref</var>) 为 **"eval"** 或 **"arguments"**

5.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lref</var>, <var>rval</var>)。
6.  返回 <var>rval</var>。

=== 组合赋值（op=） ===

产生式 ** **:** ** *@***=** **，其中 @ 表示上述的运算符其一，按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  令 <var>lval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  令 <var>rval</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。
5.  令 <var>r</var> 为作用运算符 @ 于 <var>lval</var> 和 <var>rval</var> 的结果。
6.  抛出一个 **SyntaxError** 异常，当以下条件都成立 :
    -   [Type](ES5/types#Type "wikilink")(<var>lref</var>) 为 [Reference](ES5/types#Reference "wikilink")
    -   [IsStrictReference](ES5/types#IsStrictReference "wikilink")(<var>lref</var>) 为 **true**
    -   [Type](ES5/types#Type "wikilink")([GetBase](ES5/types#GetBase "wikilink")(<var>lref</var>)) 为[环境记录项](ES5/execution#environment-record "wikilink")
    -   [GetReferencedName](ES5/types#GetReferencedName "wikilink")(<var>lref</var>) 为 **"eval"** 或 **"arguments"**

7.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lref</var>, <var>r</var>)。
8.  返回 <var>r</var>。

逗号运算符
----------

`   `*<b id="Expression">`Expression`</b>*` :`
`       `**
`       `**` `**`,`**` `**

`   `*<b id="ExpressionNoIn">`ExpressionNoIn`</b>*` :`
`       `**
`       `**` `**`,`**` `**

产生式 ** **:** ** **,** ** 按照下面的过程执行：

1.  令 <var>lref</var> 为解释执行 ** 的结果。
2.  调用 [GetValue](ES5/types#GetValue "wikilink")(<var>lref</var>)。
3.  令 <var>rref</var> 为解释执行 ** 的结果。
4.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>rref</var>)。

除了要执行内有的 ** 与 ** 而不是 ** 与 ** 以外，产生式 ** 的执行方式与产生式 ** 的执行方式相同。

