语法

` `*<b id="FunctionDeclaration">`FunctionDeclaration`</b>*` :`
`   `**`function`**` `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**`(`**` `*<sub>`opt`</sub>*` `**`)`**` `**`{`**` `**` `**`}`**

` `*<b id="FunctionExpression">`FunctionExpression`</b>*` :`
`   `**`function`**` `*[`Identifier`](ES5/lexical#Identifier "wikilink")<sub>`opt`</sub>*` `**`(`**` `*<sub>`opt`</sub>*` `**`)`**` `**`{`**` `**` `**`}`**

` `*<b id="FormalParameterList">`FormalParameterList`</b>*` :`
`   `*[`Identifier`](ES5/lexical#Identifier "wikilink")*
`   `**` `**`,`**` `*[`Identifier`](ES5/lexical#Identifier "wikilink")*

` `*<b id="FunctionBody">`FunctionBody`</b>*` :`
`   `*[`SourceElements`](ES5/program#SourceElements "wikilink")<sub>`opt`</sub>*

语义

产生式 : **function** [Identifier](ES5/lexical#Identifier "wikilink") **(** <sub>opt</sub> **)** **{** **}** 依照定义绑定初始化 ([10.5](ES5/execution#declartioin-binding-Instantiation "wikilink")) 如下初始化：

1.  依照 [13.2](#creating-function-objects "wikilink")，指定 <sub>opt</sub> 为<var>参数列表</var>，指定 为 <var>函数体</var>，创建一个新函数对象，返回结果。运行中的执行环境的 [VariableEnvironment](ES5/execution#VariableEnvironment "wikilink") 传递为 <var>Scope</var>。如果 包含在[严格模式代码里或](ES5/execution#strict-mode-code "wikilink") 是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，那么传递 **true** 为 <var>Strict</var> 标志。

产生式 : **function** **(** <sub>opt</sub> **)** **{** **}** 的解释执行如下：

1.  依照 [13.2](#creating-function-objects "wikilink")，指定 <sub>opt</sub> 为<var>参数列表</var>，指定 为 <var>函数体</var>，创建一个新函数对象，返回结果。运行中的执行环境的 [LexicalEnvironment](ES5/execution#LexicalEnvironment "wikilink") 传递为 <var>Scope</var>。如果 包含在[严格模式代码里或](ES5/execution#strict-mode-code "wikilink") 是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，那么传递 **true** 为 <var>Strict</var> 标志。

产生式 : **function** [Identifier](ES5/lexical#Identifier "wikilink") **(** <sub>opt</sub> **)** **{** **}** 的解释执行如下：

1.  令 <var>funcEnv</var> 为以运行中执行环境的 [LexicalEnvironment](ES5/execution#LexicalEnvironment "wikilink") 为参数调用 [NewDeclarativeEnvironment](ES5/execution#NewDeclarativeEnvironment "wikilink") 的结果。
2.  令 <var>envRec</var> 为 <var>funcEnv</var> 的环境记录项。
3.  以 [Identifier](ES5/lexical#Identifier "wikilink") 的字符串值为参数调用 <var>envRec</var> 的具体方法 [CreateImmutableBinding](ES5/execution#CreateImmutableBinding "wikilink")(N)。
4.  令 <var>closure</var> 为依照 [13.2](#creating-function-objects "wikilink")，指定 <sub>opt</sub> 为参数，指定 为 <var>函数体</var>，创建一个新函数对象的结果。传递 <var>funcEnv</var> 为 <var>Scope</var>。如果 包含在[严格模式代码里或](ES5/execution#strict-mode-code "wikilink") 是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，那么传递 **true** 为 <var>Strict</var> 标志。
5.  以 [Identifier](ES5/lexical#Identifier "wikilink") 的字符串值和 <var>closure</var> 为参数调用 <var>envRec</var> 的具体方法 [InitializeImmutableBinding](ES5/execution#InitializeImmutableBinding "wikilink")(N,V)。
6.  返回 <var>closure</var>。

产生式 **:** *[SourceElements](ES5/program#SourceElements "wikilink")<sub>opt</sub>* 的解释执行如下：

1.  如果这个 所在 或 包含在[严格模式代码内](ES5/execution#strict-mode-code "wikilink")，或其 *[SourceElements](ES5/program#SourceElements "wikilink")* 的指令序言（[14.1](ES5/program#directive-prologue "wikilink")）包含一个 use strict 指令，或满足 [10.1.1](ES5/execution#strict-mode-code "wikilink") 的任何条件，那么其代码[严格模式代码](ES5/execution#strict-mode-code "wikilink")。如果 的代码是[严格模式代码](ES5/execution#strict-mode-code "wikilink")，*[SourceElements](ES5/program#SourceElements "wikilink")* 的解释执行为以下的[严格模式代码步骤](ES5/execution#strict-mode-code "wikilink")。否则，*[SourceElements](ES5/program#SourceElements "wikilink")* 的解释执行为以下的非[严格模式代码](ES5/execution#strict-mode-code "wikilink")。
2.  如果 *[SourceElements](ES5/program#SourceElements "wikilink")* 存在，则返回 *[SourceElements](ES5/program#SourceElements "wikilink")* 的解释执行结果。
3.  否则返回 (**normal**, **undefined**, **empty**)。

严格的模式的限制
----------------

如果[严格模式](ES5/execution#strict-mode-code "wikilink") 或 的 里出现多个相同 [Identifier](ES5/lexical#Identifier "wikilink") 值，那么这是个 **SyntaxError**。

如果[严格模式](ES5/execution#strict-mode-code "wikilink") 或 的 里出现标识符 **"eval"** 或标识符 **"arguments"**，那么这是个 **SyntaxError**。

如果[严格模式](ES5/execution#strict-mode-code "wikilink") 或 的 [Identifier](ES5/lexical#Identifier "wikilink") 是标识符 **"eval"** 或标识符 **"arguments"**，那么这是个 **SyntaxError**。

创建函数对象
------------

指定 为可选的 <var>参数列表</var>，指定 为 <var>函数体</var>，指定 <var>Scope</var> 为[词法环境](ES5/execution#lexical-environments "wikilink")，<var>Strict</var> 为布尔标记，按照如下步骤构建函数对象：

1.  创建一个新的 ECMAScript 原生对象，令 <var>F</var> 为此对象。
2.  依照 [8.12](ES5/types#object-internal-methods "wikilink") 描述设定 <var>F</var> 的除 [[[Get]]](ES5/types#Get "wikilink") 以外的所有内部方法。
3.  设定 <var>F</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Function"**。
4.  设定 <var>F</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 [15.3.3.1](ES5/builtins#x15.3.3.1 "wikilink") 指定的标准内置 **Function** 对象的 **prototype** 属性。
5.  依照 [15.3.5.4](ES5/builtins#x15.3.5.4 "wikilink") 描述，设定 <var>F</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部属性。
6.  依照 [13.2.1](#Call-impl "wikilink") 描述，设定 <var>F</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部属性。
7.  依照 [13.2.2](#Construct-impl "wikilink") 描述，设定 <var>F</var> 的 [[[Construct]]](ES5/types#Construct "wikilink") 内部属性。
8.  依照 [15.3.5.3](ES5/builtins#x15.3.5.3 "wikilink") 描述，设定 <var>F</var> 的 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内部属性。
9.  设定 <var>F</var> 的 [[[Scope]]](ES5/types#Scope "wikilink") 内部属性为 <var>Scope</var> 的值。
10. 令 <var>names</var> 为一个[列表容器](ES5/types#List "wikilink")，其中元素是以从左到右的文本顺序对应 的标识符的字符串。
11. 设定 <var>F</var> 的 [[[FormalParameters]]](ES5/types#FormalParameters "wikilink") 内部属性为 <var>names</var>。
12. 设定 <var>F</var> 的 [[[Code]]](ES5/types#Code "wikilink") 内部属性为 。
13. 设定 <var>F</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **true**。
14. 令 <var>len</var> 为 指定的形式参数的个数。如果没有指定参数，则令 <var>len</var> 为 **0**。
15. 以参数 **"length"**、属性描述符 {[[Value]]: <var>len</var>, [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false**}、**false** 调用 <var>F</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
16. 令 <var>proto</var> 为仿佛使用 **new Object()** 表达式创建新对象的结果，其中 Object 是[标准内置构造器名](ES5/builtins#object-objects "wikilink")。
17. 以参数 **"constructor"**、属性描述符 {[[Value]]: <var>F</var>, { [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **true**}、**false** 调用 <var>proto</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
18. 以参数 **"prototype"**、属性描述符 {[[Value]]: <var>proto</var>, [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **false**}、**false** 调用 <var>F</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
19. 如果 <var>Strict</var> 是 **true**，则
    1.  令 <var>thrower</var> 为 [[[ThrowTypeError]]](#ThrowTypeError "wikilink") 函数对象（[13.2.3](#ThrowTypeError "wikilink")）。
    2.  以参数 **"caller"**、属性描述符 {[[Get]]: <var>thrower</var>, [[Set]]: <var>thrower</var>, [[Enumerable]]: **false**, [[Configurable]]: **false**}、**false** 调用 <var>F</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
    3.  以参数 **"arguments"**、属性描述符 {[[Get]]: <var>thrower</var>, [[Set]]: <var>thrower</var>, [[Enumerable]]: **false**, [[Configurable]]: **false**}、**false** 调用 <var>F</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

20. 返回 <var>F</var>。

### [[Call]]

当用一个 **this** 值、一个参数列表调用函数对象 <var>F</var> 的 <b>[[Call]]</b> 内部方法，采用以下步骤：

1.  用 <var>F</var> 的 [[[FormalParameters]]](ES5/types#FormalParameters "wikilink") 内部属性值、参数[列表](ES5/types#List "wikilink") <var>args</var>、[10.4.3](ES5/execution#entering-function-code "wikilink") 描述的 **this** 值来建立[函数代码的一个新执行环境](ES5/execution#function-code "wikilink")，令 <var>funcCtx</var> 为其结果。
2.  令 <var>result</var> 为 （也就是 <var>F</var> 的 [[[Code]]](ES5/types#Code "wikilink") 内部属性）解释执行的结果。如果 F 没有 [[[Code]]](ES5/types#Code "wikilink") 内部属性或其值是空的 ，则 <var>result</var> 是 (**normal**, **undefined**, **empty**)。
3.  退出 <var>funcCtx</var> 运行环境，恢复到之前的执行运行环境。
4.  如果 <var>result</var>**.type** 是 **throw** 则抛出 <var>result</var>**.value**。
5.  如果 <var>result</var>**.type** 是 **return** 则返回 <var>result</var>**.value**。
6.  否则 <var>result</var>**.type** 必定是 **normal**。返回 **undefined**。

### [[Construct]]

当以一个可能的空的参数列表调用函数对象 <var>F</var> 的 <b>[[Construct]]</b> 内部方法，采用以下步骤：

1.  令 <var>obj</var> 为新创建的 ECMAScript 原生对象。
2.  依照 [8.12](ES5/types#object-internal-methods "wikilink") 设定 <var>obj</var> 的所有内部方法。
3.  设定 <var>obj</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Object"**。
4.  设定 <var>obj</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **true**。
5.  令 <var>proto</var> 为以参数 **"prototype"** 调用 <var>F</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部属性的值。
6.  如果 [Type](ES5/types#Type "wikilink")(<var>proto</var>) 是 **Object**，设定 <var>obj</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 <var>proto</var>。
7.  如果 [Type](ES5/types#Type "wikilink")(<var>proto</var>) 不是 **Object**，设定 <var>obj</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 [15.2.4](ES5/builtins#x15.2.4 "wikilink") 描述的标准内置的 **Object** 原型对象。
8.  以 <var>obj</var> 为 **this** 值，调用 [[[Construct]]](ES5/types#Construct "wikilink") 的参数列表为 <var>args</var>，调用 <var>F</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部属性，令 <var>result</var> 为调用结果。
9.  如果 [Type](ES5/types#Type "wikilink")(<var>result</var>) 是 **Object**，则返回 <var>result</var>。
10. 返回 <var>obj</var>。

### [[ThrowTypeError]] 函数对象

**[[ThrowTypeError]]** 对象是个唯一的函数对象，如下只定义一次：

1.  创建一个新 ECMAScript 原生对象，令 <var>F</var> 为此对象。
2.  依照 [8.12](ES5/types#object-internal-methods "wikilink") 设定 <var>F</var> 的所有内部属性。
3.  设定 <var>F</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Function"**。
4.  设定 <var>F</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 [15.3.3.1](ES5/builtins#x15.3.3.1 "wikilink") 指定的标准内置 [Function](ES5/builtins#x15.3.3.1 "wikilink") 的原型对象。
5.  依照 [13.2.1](#Call-impl "wikilink") 描述设定 <var>F</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部属性。
6.  设定 <var>F</var> 的 [[[Scope]]](ES5/types#Scope "wikilink") 内部属性为[全局环境](ES5/execution#the-global-environment "wikilink")。
7.  设定 <var>F</var> 的 [[[FormalParameters]]](ES5/types#FormalParameters "wikilink") 内部属性为一个空[列表](ES5/types#List "wikilink")。
8.  设定 <var>F</var> 的 [[[Code]]](ES5/types#Code "wikilink") 内部属性为一个 ，它无条件抛出一个 **TypeError** 异常，不做其他事情。
9.  以参数 **"length"**、属性描述符 {[[Value]]: **0**, [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false**}、**false** 调用 <var>F</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
10. 设定 <var>F</var> 的 [[[Extensible]]](ES5/types "wikilink") 内部属性为 **false**。
11. 令 **[[ThrowTypeError]]** 为 <var>F</var>。

