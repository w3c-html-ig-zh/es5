可执行代码类型
--------------

一共有三种 ECMA 脚本可执行代码：

-   <b id="global-code">全局代码</b>是指被作为 ECMAScript *[Program](ES5/program#Program "wikilink")* 处理的源代码文本。一个特定 *[Program](ES5/program#Program "wikilink")* 的全局代码不包括作为 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 被解析的源代码文本。
-   <b id="eval-code">Eval 代码</b>是指提供给 [eval](ES5/builtins#x15.1.2.1 "wikilink") 内置函数的源代码文本。更精确地说，如果传递给 [eval](ES5/builtins#x15.1.2.1 "wikilink") 内置函数的参数为一个字符串，该字符串将被作为 ECMA 脚本 *[Program](ES5/program#Program "wikilink")* 进行处理。在特定的一次对 [eval](ES5/builtins#15.1.2.1 "wikilink") 的调用过程中，[eval](ES5/builtins#x15.1.2.1 "wikilink") 代码作为该 *[Program](ES5/program#Program "wikilink")* 的[全局代码部分](#global-code "wikilink")。
-   <b id="function-code">函数代码</b>是指作为 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 被解析的源代码文本。一个 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 的[函数代码不包括作为其嵌套函数的](#function-code "wikilink") *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 被解析的源代码文本。[函数代码同时还特指以构造器方式调用](#function-code "wikilink") [Function](ES5/builtins#x15.3.2 "wikilink") 内置对象时所提供的源代码文本。更精确地说，调用 [Function](ES5/builtins#x15.3.2 "wikilink") 构造器时传递的最后一个参数将被转换为字符串并作为 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 使用。如果调用 [Function](ES5/builtins#x15.3.2 "wikilink") 构造器时，传递了一个以上的参数，除最后一个参数以外的其他参数都将转换为字符串，并以逗号作为分隔符连接在一起成为一个字符串，该字符串被解析为 *[FormalParameterList](ES5/functions#FormalParameterList "wikilink")* 供由最后一个参数定义的 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 使用。初始化 [Function](ES5/builtins#x15.3.2 "wikilink") 对象时所提供的函数代码，并不包括作为其嵌套函数的 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 被解析的源代码文本。

#### 严格模式下的代码

一个 ECMA 脚本程序的语法单元可以使用非严格或严格模式下的语法及语义进行处理。当使用严格模式进行处理时，以上三种代码将被称为严格全局代码、严格 [eval](ES5/builtins#x15.1.2.1 "wikilink") 代码和严格函数代码。当符合以下条件时，代码将被解析为严格模式下的代码：

-   当[全局代码以](#global-code "wikilink")[指令序言开始](ES5/program#x14.1 "wikilink")，且该[指令序言包含一个使用](ES5/program#x14.1 "wikilink")[严格模式指令](ES5/program#x14.1 "wikilink")（参考 [14.1 章](ES5/program#x14.1 "wikilink")）时，即为严格全局代码。
-   当 [Eval 代码以](#eval-code "wikilink")[指令序言开始](ES5/program#x14.1 "wikilink")，且该[指令序言包含一个使用](ES5/program#x14.1 "wikilink")[严格模式指令时](ES5/program#x14.1 "wikilink")；或者在[严格模式下的代码中通过直接调用](#strict-mode-code "wikilink") [eval 函数](ES5/builtins#x15.1.2.1.1 "wikilink")（参考 [15.1.2.1.1 章](ES5/builtins#x15.1.2.1.1 "wikilink")）时，即为严格 [eval](ES5/builtins#x15.1.2.1 "wikilink") 代码。
-   当一个 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")*、*[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 或 *[PropertyAssignment](ES5/expressions#inlinePropertyAssignment "wikilink")* 访问器处在一段[严格模式下的代码中](#strict-mode-code "wikilink")，或其函数代码以[指令序言开始](ES5/program#x14.1 "wikilink")，且该[指令序言包含一个使用严格模式的](ES5/program#x14.1 "wikilink")[指令序言时](ES5/program#x14.1 "wikilink")，该[函数代码即为严格函数代码](#function-code "wikilink")。
-   当调用内置的 [Function](ES5/builtins#x15.3.2 "wikilink") 构造器时，如果最后一个参数所表达的字符串在作为 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 处理时以指令序言开始，且该[指令序言包含一个使用严格模式的指令](ES5/program#x14.1 "wikilink")，则该[函数代码即为严格函数代码](#function-code "wikilink")。

词法环境
--------

**词法环境**是一个用于定义特定变量和函数[标识符在](ES5/lexical#x7.6 "wikilink") ECMAScript 代码的词法嵌套结构上关联关系的[规范类型](ES5/types#specification-type "wikilink")。一个词法环境由一个[环境记录项和可能为空的](#environment-record "wikilink")[外部词法环境引用构成](#outer-environment-reference "wikilink")。通常词法环境会与 ECMAScript 代码诸如 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")*、*[WithStatement](ES5/statements#WithStatement "wikilink")* 或者 *[TryStatement](ES5/statements#TryStatement "wikilink")* 的 *[Catch](ES5/statements#Catch "wikilink")* 块这样的特定句法结构相联系，且类似代码每次执行都会有一个新的**词法环境**被创建出来。

[环境记录项记录了在其关联的词法环境范围中创建的](#environment-record "wikilink")[标识符绑定](ES5/lexical#x7.6 "wikilink")。

**外部词法环境引用**用于表示词法环境的逻辑嵌套关系模型。（内部）词法环境的外部引用是逻辑上包含内部词法环境的词法环境。外部词法环境自然也可能有多个内部词法环境。例如，如果一个 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")* 包含两个嵌套的 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")*，那么每个内嵌函数的词法环境都是外部函数本次执行所产生的词法环境。

--[Undefined](User:Undefined "wikilink") ([talk](User talk:Undefined "wikilink")) 04:46, 28 January 2014 (UTC)词法环境和环境记录项是纯粹的规范机制，而不需要 ECMAScript 的实现保持一致。ECMAScript 程序不可能直接访问或者更改这些值。

### 环境记录项

在本标准中，共有两类环境记录项：[声明式环境记录项和](#x10.2.1.1 "wikilink")[对象式环境记录项](#x10.2.1.2 "wikilink")。[声明式环境记录项用于定义那些将](#x10.2.1.1 "wikilink")[标识符与语言值直接绑定的](ES5/lexical#x7.6 "wikilink") ECMA 脚本语法元素，例如 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")*、*[VariableDeclaration](ES5/functions#VariableDeclaration "wikilink")* 以及 *[Catch](ES5/statements#Catch "wikilink")* 语句。[对象式环境记录项用于定义那些将](#x10.2.1.2 "wikilink")[标识符与具体对象的属性绑定的](ES5/lexical#x7.6 "wikilink") ECMA 脚本元素，例如 *[Program](ES5/program#Program "wikilink")* 以及 *[WithStatement](ES5/statements#WithStatement "wikilink")* 表达式。

出于标准规范的目的，可以将环境记录项理解为面向对象中的一个简单继承结构，其中环境记录项是一个抽象类，有两个具体实现类，分别为[声明式环境记录项和](#x10.2.1.1 "wikilink")[对象式环境记录项](#x10.2.1.2 "wikilink")。抽象类包含了 **表17** 所描述的抽象方法定义，针对每一个具体实现类，每个抽象方法都有不同的具体算法。

|---|---|
|nowrap | 方法|作用|
|nowrap |**HasBinding**(<var>N</var>)|判断环境记录项是否包含对某个[标识符的绑定](ES5/lexical#x7.6 "wikilink")。如果包含该绑定则返回 **true**，反之返回 **false**。其中字符串 <var>N</var> 是[标识符文本](ES5/lexical#x7.6 "wikilink")。|
|nowrap |**CreateMutableBinding**(<var>N</var>, <var>D</var>)|在环境记录项中创建一个新的可变绑定。其中字符串 <var>N</var> 指定绑定名称。如果可选参数 <var>D</var> 的值为 **true**，则该绑定在后续操作中可以被删除。|
|nowrap |**SetMutableBinding**(<var>N</var>, <var>V</var>, <var>S</var>)|在环境记录项中设置一个已经存在的绑定的值。其中字符串 <var>N</var> 指定绑定名称。<var>V</var> 用于指定绑定的值，可以是任何 ECMA 脚本[语言的类型](ES5/types#language-type "wikilink")。<var>S</var> 是一个布尔类型的标记，当 <var>S</var> 为 **true** 并且该绑定不允许赋值时，则抛出一个 **TypeError** 异常。<var>S</var> 用于指定是否为严格模式。|
|nowrap |**GetBindingValue**(<var>N</var>, <var>S</var>)|返回环境记录项中一个已经存在的绑定的值。其中字符串 <var>N</var> 指定绑定的名称。<var>S</var> 用于指定是否为严格模式。如果 <var>S</var> 的值为 **true** 并且该绑定不存在或未初始化，则抛出一个 **ReferenceError** 异常。|
|nowrap |**DeleteBinding**(<var>N</var>)|从环境记录项中删除一个绑定。其中字符串 <var>N</var> 指定绑定的名称。如果 <var>N</var> 指定的绑定存在，将其删除并返回 **true**。如果绑定存在但无法删除则返回 **false**。如果绑定不存在则返回 **true**。|
|nowrap |**ImplicitThisValue**()|当从该环境记录项的绑定中获取一个函数对象并且调用时，该方法返回该函数对象使用的 **this** 对象的值。|

#### 声明式环境记录项

每个[声明式环境记录项都与一个包含变量和](#x10.2.1.1 "wikilink")（或）函数声明的 ECMA 脚本的程序作用域相关联。[声明式环境记录项用于绑定作用域内定义的一系列](#x10.2.1.1 "wikilink")[标识符](ES5/lexical#x7.6 "wikilink")。

除了所有环境记录项都支持的可变绑定外，[声明式环境记录项还提供不可变绑定](#x10.2.1.1 "wikilink")。 在<b id="immutable-binding">不可变绑定</b>中，一个[标识符与它的值之间的关联关系建立之后](ES5/lexical#x7.6 "wikilink")，就无法改变。创建和初始化不可变绑定是两个独立的过程，因此类似的绑定可以处在已初始化阶段或者未初始化阶段。除了环境记录项定义的抽象方法外，[声明式环境记录项还支持](#x10.2.1.1 "wikilink") **表18** 中列出的方法：

|---|---|
|nowrap | 方法|作用|
|nowrap | [CreateImmutableBinding](#CreateImmutableBinding "wikilink")(<var>N</var>)|在环境记录项中创建一个未初始化的[不可变绑定](#immutable-binding "wikilink")。其中字符串 <var>N</var> 指定绑定名称。|
|nowrap | [InitializeImmutableBinding](#InitializeImmutableBinding "wikilink")(<var>N</var>, <var>V</var>)|在环境记录项中设置一个已经创建但未初始化的[不可变绑定的值](#immutable-binding "wikilink")。其中字符串 <var>N</var> 指定绑定名称。<var>V</var> 用于指定绑定的值，可以是任何 ECMA 脚本[语言的类型](ES5/types#language-type "wikilink")。|

环境记录项定义的方法的具体行为将由以下算法给予描述。

##### HasBinding(N)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **HasBinding** 具体方法用于简单地判断作为参数的[标识符是否是当前对象绑定的](ES5/lexical#x7.6 "wikilink")[标识符之一](ES5/lexical#x7.6 "wikilink")：

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  如果 <var>envRec</var> 有一个名称为 <var>N</var> 的绑定，返回 **true**。
3.  如果没有该绑定，返回 **false**。

##### CreateMutableBinding(N, D)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **CreateMutableBinding** 具体方法会创建一个名称为 <var>N</var> 的绑定，并初始化其值为 **undefined**。方法调用时，当前环境记录项中不能存在 <var>N</var> 的绑定。如果调用时提供了布尔类型的参数 <var>D</var> 且其值为 **true**，则新建的绑定被标记为可删除。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  执行断言：<var>envRec</var> 没有 <var>N</var> 的绑定。
3.  在 <var>envRec</var> 中为 <var>N</var> 创建一个可变绑定，并将绑定的值设置为 **undefined**。如果 <var>D</var> 为 **true** 则新创建的绑定可在后续操作中通过调用 [DeleteBinding](#DER-DeleteBinding "wikilink") 删除。

##### SetMutableBinding(N, V, S)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **SetMutableBinding** 具体方法尝试将当前名称为参数 <var>N</var> 的绑定的值修改为参数 <var>V</var> 指定的值。方法调用时，必须存在 <var>N</var> 的绑定。如果该绑定为不可变绑定，并且 <var>S</var> 的值为 **true**，则抛出一个 **TypeError** 异常。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  执行断言：<var>envRec</var> 必须有 <var>N</var> 的绑定。
3.  如果 <var>envRec</var> 中 <var>N</var> 的绑定为可变绑定，则将其值修改为 <var>V</var>。
4.  否则该操作会尝试修改一个不可变绑定的值，因此如果 <var>S</var> 的值为 **true**，则抛出一个 **TypeError** 异常。

##### GetBindingValue(N, S)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **GetBindingValue** 具体方法简单地返回名称为参数 <var>N</var> 的绑定的值。方法调用时，该绑定必须存在。如果 <var>S</var> 的值为 **true** 且该绑定是一个未初始化的不可变绑定，则抛出一个 **ReferenceError** 异常。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  执行断言：<var>envRec</var> 必须有 <var>N</var> 的绑定。
3.  如果 <var>envRec</var> 中 <var>N</var> 的绑定是一个未初始化的不可变绑定，则：
    1.  如果 <var>S</var> 为 **false**，返回 **undefined**，否则抛出一个 **ReferenceError** 异常。

4.  否则返回 <var>envRec</var> 中与 <var>N</var> 绑定的值。

##### DeleteBinding(N)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **DeleteBinding** 具体方法只能删除显示指定可被删除的那些绑定。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  如果 <var>envRec</var> 不包含名称为 <var>N</var> 的绑定，返回 **true**。
3.  如果 <var>envRec</var> 中 <var>N</var> 的绑定不能删除，返回 **false**。
4.  移除 <var>envRec</var> 中 <var>N</var> 的绑定。
5.  返回 **true**。

##### ImplicitThisValue()

[声明式环境记录项永远将](#x10.2.1.1 "wikilink") **undefined** 作为其 **ImplicitThisValue** 返回。

1.  返回 **undefined**。

##### CreateImmutableBinding(N)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **CreateImmutableBinding** 具体方法会创建一个不可变绑定，其名称为 <var>N</var> 且初始化其值为 **undefined**。调用方法时，该环境记录项中不得存在 <var>N</var> 的绑定。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  执行断言：<var>envRec</var> 不存在 <var>N</var> 的绑定。
3.  在 <var>envRec</var> 中为 <var>N</var> 创建一个不可变绑定，并记录为未初始化。

##### InitializeImmutableBinding(N, V)

[声明式环境记录项的](#x10.2.1.1 "wikilink") **InitializeImmutableBinding** 具体方法用于将当前名称为参数 <var>N</var> 的绑定的值修改为参数 <var>V</var> 指定的值。方法调用时，必须存在 <var>N</var> 对应的未初始化的不可变绑定。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  执行断言：<var>envRec</var> 存在一个与 <var>N</var> 对应的未初始化的不可变绑定。
3.  在 <var>envRec</var> 中将 <var>N</var> 的绑定的值设置为 <var>V</var>。
4.  在 <var>envRec</var> 中将 <var>N</var> 的不可变绑定记录为已初始化。

#### 对象式环境记录项

每一个[对象式环境记录项都有一个关联的对象](#x10.2.1.2 "wikilink")，这个对象被称作*'绑定对象 **。[对象式环境记录项直接将一系列](#x10.2.1.2 "wikilink")[标识符与其](ES5/lexical#x7.6 "wikilink")**绑定对象**的属性名称建立一一对应关系。不符合 *[IdentifierName](ES5/lexical#IdentifierName "wikilink")* 的属性名不会作为绑定的[标识符使用](ES5/lexical#x7.6 "wikilink")。无论是对象自身的，还是继承的属性都会作为绑定，无论该属性的 [[[Enumerable]]](ES5/types#Enumerable "wikilink") 特性的值是什么。由于对象的属性可以动态的增减，因此[对象式环境记录项所绑定的](#x10.2.1.2 "wikilink")[标识符集合也会隐匿地变化](ES5/lexical#x7.6 "wikilink")，这是增减**绑定对象*'的属性而产生的副作用。通过以上描述的副作用而建立的绑定，均被视为可变绑定，即使该绑定对应的属性的 [[[Writable]]](ES5/types#Writable "wikilink") 特性的值为 **false**。[对象式环境记录项没有](#x10.2.1.2 "wikilink")[不可变绑定](#immutable-binding "wikilink")。

[对象式环境记录项可以通过配置的方式](#x10.2.1.2 "wikilink")，将其绑定对象合为函数调用时的隐式 **this** 对象的值。这一功能用于规范 *[WithStatement](ES5/statements#WithStatement "wikilink")* 引入的绑定行为。该行为通过[对象式环境记录项中布尔类型的](#x10.2.1.2 "wikilink") <var>provideThis</var> 值控制，默认情况下，<var>provideThis</var> 的值为 **false**。

环境记录项定义的方法的具体行为将由以下算法给予描述。

##### HasBinding(N)

[对象式环境记录项的](#x10.2.1.2 "wikilink") **HasBinding** 具体方法判断其关联的[绑定对象是否有名为](#binding-object "wikilink") <var>N</var> 的属性：

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  令 <var>bindings</var> 为 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")。
3.  以 <var>N</var> 为属性名，调用 <var>bindings</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法，并返回调用的结果。

##### CreateMutableBinding(N, D)

[对象式环境记录项的](#x10.2.1.2 "wikilink") [CreateMutableBinding具体方法会在其关联的](#OER-CreateMutableBinding "wikilink")[绑定对象上创建一个名称为](#binding-object "wikilink") <var>N</var> 的属性，并初始化其值为 **undefined**。调用方法时，[绑定对象不得包含名称为](#binding-object "wikilink") <var>N</var> 的属性。如果调用方法时提供了布尔类型的参数 <var>D</var> 且其值为 **true**，则设置新创建的属性的 [[[Configurable]]](ES5/types#Configurable "wikilink") 特性的值为 **true**，否则设置为 **false**。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  令 <var>bindings</var> 为 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")。
3.  执行断言：以 <var>N</var> 为属性名，调用 <var>bindings</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法，调用的结果为 **false**。
4.  如果 <var>D</var> 的值为 **true**，则令 <var>configValue</var> 的值为 **true**，否则令 <var>configValue</var> 的值为 **false**。
5.  以 <var>N</var>、属性描述符 {[[Value]]:**undefined**, [[Writable]]: **true**, [[Enumerable]]: **true** , [[Configurable]]: <var>configValue</var>} 和布尔值 **true** 为参数，调用 <var>bindings</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

##### SetMutableBinding(N, V, S)

[对象式环境记录项的](#x10.2.1.2 "wikilink") **SetMutableBinding** 具体方法会尝试设置其关联的[绑定对象中名为](#binding-object "wikilink") <var>N</var> 的属性的值为 <var>V</var>。方法调用时，[绑定对象中应当存在该属性](#binding-object "wikilink")，如果该属性不存在或属性不可写，则根据 <var>S</var> 参数的值来执行错误处理。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  令 <var>bindings</var> 为 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")
3.  以 <var>N</var>、<var>V</var> 和 <var>S</var> 为参数，调用 <var>bindings</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

##### GetBindingValue(N, S)

[对象式环境记录项的](#x10.2.1.2 "wikilink") **GetBindingValue** 具体方法返回其关联的[绑定对象中名为](#binding-object "wikilink") <var>N</var> 的属性的值。方法调用时，[绑定对象中应当存在该属性](#binding-object "wikilink")，如果该属性不存在，则方法的返回值由 <var>S</var> 参数决定：

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  令 <var>bindings</var> 为 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")
3.  以 <var>N</var> 为属性名，调用 <var>bindings</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法，并令 <var>value</var> 为调用的结果。
4.  如果 <var>value</var> 的值为 **false**，则：
    1.  如果 <var>S</var> 的值为 **false**，则返回 **undefined**，否则抛出一个 **ReferenceError** 异常。

5.  以 <var>N</var> 为参数，调用 <var>bindings</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法，并返回调用的结果。

##### DeleteBinding(N)

[对象式环境记录项的](#x10.2.1.2 "wikilink") **DeleteBinding** 具体方法只能用于删除其关联的[绑定对象上](#binding-object "wikilink") [[[Configurable]]](ES5/types#Configurable "wikilink") 特性的值为 **true** 的属性所对应的绑定。

1.  令 <var>envRec</var> 为函数调用时对应的[声明式环境记录项](#x10.2.1.1 "wikilink")。
2.  令 <var>bindings</var> 为 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")
3.  以 <var>N</var> 和布尔值 **false** 为参数，调用 <var>bindings</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

##### ImplicitThisValue()

[对象式环境记录项的](#x10.2.1.2 "wikilink") **ImplicitThisValue** 通常返回 **undefined**，除非其 <var>provideThis</var> 标识的值为 **true**。

1.  令 <var>envRec</var> 为函数调用时对应的[对象式环境记录项](#object-environment-record "wikilink")。
2.  如果 <var>envRec</var> 的 <var>provideThis</var> 标识的值为 **true**，返回 <var>envRec</var> 的[绑定对象](#binding-object "wikilink")。
3.  否则返回 **undefined**。

### 词法环境的运算

在本标准中，以下抽象运算将被用于操作环境记录项：

#### GetIdentifierReference(lex, name, strict)

当调用 **GetIdentifierReference** 抽象运算时，需要指定一个[词法环境](#lexical-environment "wikilink") <var>lex</var>，一个[标识符字符串](ES5/lexical#x7.6 "wikilink") <var>name</var> 以及一个布尔型标识 <var>strict</var>。<var>lex</var> 的值可以为 **null**。当调用该运算时，按以下步骤进行：

1.  如果 <var>lex</var> 的值为 **null**，则：
    1.  返回一个类型为[引用的对象](ES5/types#Reference "wikilink")，其基值为 **undefined**，引用的名称为 <var>name</var>，严格模式标识的值为 <var>strict</var>。

2.  令 <var>envRec</var> 为 <var>lex</var> 的[环境数据](#environment-record "wikilink")。
3.  以 <var>name</var> 为参数 <var>N</var>，调用 <var>envRec</var> 的 (<var>N</var>) 具体方法，并令 <var>exists</var> 为调用的结果。
4.  如果 <var>exists</var> 为 **true**，则：
    1.  返回一个类型为[引用的对象](ES5/types#Reference "wikilink")，其基值为 <var>envRec</var>，引用的名称为 <var>name</var>，严格模式标识的值为 <var>strict</var>。

5.  否则：
    1.  令 <var>outer</var> 为 <var>lex</var> 的[外部环境引用](#outer-environment-reference "wikilink")。
    2.  以 <var>outer</var>、<var>name</var> 和 <var>strict</var> 为参数，调用 **GetIdentifierReference**，并返回调用的结果。

#### NewDeclarativeEnvironment(E)

当调用 **NewDeclarativeEnvironment** 抽象运算时，需指定一个[词法环境](#lexical-environment "wikilink") <var>E</var>，其值可以为 **null**，此时按以下步骤进行：

1.  令 <var>env</var> 为一个新建的[词法环境](#lexical-environment "wikilink")。
2.  令 <var>envRec</var> 为一个新建的[声明式环境数据](#declarative-environment-record "wikilink")，该[环境数据不包含任何绑定](#environment-record "wikilink")。
3.  令 <var>env</var> 的[环境数据为](#environment-record "wikilink") <var>envRec</var>。
4.  令 <var>env</var> 的[外部词法环境引用至](#outer-environment-reference "wikilink") <var>E</var>。
5.  返回 <var>env</var>。

#### NewObjectEnvironment(O, E)

当调用 **NewObjectEnvironment** 抽象运算时，需指定一个对象 <var>O</var> 及一 个[词法环境](#lexical-environment "wikilink") <var>E</var>（其值可以为 **null**），此时按以下步骤进行：

1.  令 <var>env</var> 为一个新建的[词法环境](#lexical-environment "wikilink")。
2.  令 <var>envRec</var> 为一个新建的[对象环境数据](#object-environment-record "wikilink")，该[环境数据包含](#environment-record "wikilink") <var>O</var> 作为绑定对象。
3.  令 <var>env</var> 的[环境数据为](#environment-record "wikilink") <var>envRec</var>。
4.  令 <var>env</var> 的[外部词法环境引用至](#outer-environment-reference "wikilink") <var>E</var>。
5.  返回 <var>env</var>。

### 全局环境

**全局环境**是一个唯一的[词法环境](#lexical-environment "wikilink")，它在任何 ECMA 脚本的代码执行前创建。全局环境的[环境数据是一个](#environment-record "wikilink")[对象环境数据](#object-environment-record "wikilink")，该环境数据使用[全局对象](ES5/builtins#x15.1 "wikilink")（[15.1](ES5/builtins#x15.1 "wikilink")）作为[绑定对象](#binding-object "wikilink")。全局环境的[外部环境引用为](#outer-environment-reference "wikilink") **null**。

在 ECMA 脚本的代码执行过程中，可能会向[全局对象添加额外的属性](ES5/builtins#x15.1 "wikilink")，也可能修改其初始属性的值。

执行环境
--------

当控制器转入 ECMA 脚本的可执行代码时，控制器会进入一个执行环境。当前活动的多个执行环境在逻辑上形成一个栈结构。该逻辑栈的最顶层的执行环境称为当前运行的执行环境。任何时候，当控制器从当前运行的执行环境相关的可执行代码转入与该执行环境无关的可执行代码时，会创建一个新的执行环境。新建的这个执行环境会推入栈中，成为当前运行的执行环境。

执行环境包含所有用于追踪与其相关的代码的执行进度的状态。精确地说，每个执行环境包含如 **表19** 列出的组件。

|---|---|
|nowrap | 组件|作用目的|
|nowrap | 词法环境组件|指定一个[词法环境对象](#lexical-environment "wikilink")，用于解析该执行环境内的代码创建的[标识符引用](ES5/lexical#x7.6 "wikilink")。|
|nowrap | 变量环境组件|指定一个[词法环境对象](#lexical-environment "wikilink")，其环境数据用于保存由该执行环境内的代码通过 *[VariableStatement](ES5/statements#VariableStatement "wikilink")* 和 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")* 创建的绑定。|
|nowrap | this 绑定|指定该执行环境内的 ECMA 脚本代码中 **this** 关键字所关联的值。|

其中执行环境的[词法环境组件和](#LexicalEnvironment "wikilink")[变量环境组件始终为](#VariableEnvironment "wikilink")[词法环境对象](#lexical-environment "wikilink")。当创建一个执行环境时，其[词法环境组件和](#LexicalEnvironment "wikilink")[变量环境组件最初是同一个值](#VariableEnvironment "wikilink")。在该执行环境相关联的代码的执行过程中，[变量环境组件永远不变](#VariableEnvironment "wikilink")，而[词法环境组件有可能改变](#LexicalEnvironment "wikilink")。

在本标准中，通常情况下，只有正在运行的执行环境（执行环境栈里的最顶层对象）会被算法直接修改。因此当遇到“**词法环境组件**”、“**变量环境组件**”、“**this 绑定组件**”这三个术语时，指的是正在运行的执行环境的对应组件。

执行环境是一个纯粹的标准机制，并不代表任何 ECMA 脚本实现的工件。在 ECMA 脚本程序中是不可能访问到执行环境的。

#### 标识符解析

**标识符解析**是指使用正在运行的执行环境中的[词法环境组件](#LexicalEnvironment "wikilink")，通过一个 *[Identifier](ES5/lexical#Identifier "wikilink")* 获得其对应的绑定的过程。在 ECMA 脚本代码执行过程中，*[PrimaryExpression](ES5/expressions#inlinePrimaryExpression "wikilink")* **:** *[Identifier](ES5/lexical#Identifier "wikilink")* 这一语法产生式将按以下算法进行解释执行：

1.  令 <var>env</var> 为正在运行的执行环境的 [词法环境组件](#LexicalEnvironment "wikilink")。
2.  如果正在解释执行的语法产生式处在[严格模式下的代码中](#strict-mode-code "wikilink")，则仅 <var>strict</var> 的值为 **true**，否则令 <var>strict</var> 的值为 **false**。
3.  以 <var>env</var>、*[Identifier](ES5/lexical#Identifier "wikilink")* 和 <var>strict</var> 为参数，调用 [GetIdentifierReference](#GetIdentifierReference "wikilink") 函数，并返回调用的结果。

解释执行一个[标识符得到的结果必定是](ES5/lexical#x7.6 "wikilink")[引用类型的对象](ES5/types#Reference "wikilink")，且其引用名属性的值与 *[Identifier](ES5/lexical#Identifier "wikilink")* 字符串相等。

建立执行环境
------------

解释执行[全局代码或使用](#global-code "wikilink") [eval](ES5/builtins#x15.1.2.1 "wikilink") 函数输入的代码会创建并进入一个新的执行环境。每次调用 ECMA 脚本代码定义的函数（[13.2.1](ES5/functions#Call-impl "wikilink")）也会建立并进入一个新的执行环境，即便函数是自身递归调用的。每一次 [return](ES5/statements#ReturnStatement "wikilink") 都会退出一个执行环境。抛出异常也可退出一个或多个执行环境。

当控制流进入一个执行环境时，会设置该执行环境的 [this 绑定组件](#ThisBinding "wikilink")，定义[变量环境和初始](#VariableEnvironment "wikilink")[词法环境](#LexicalEnvironment "wikilink")，并执行[声明式绑定初始化过程](#declaration-binding-instantiation "wikilink")。以上这些步骤的严格执行方式由进入的代码的类型决定。

### 进入全局代码

当控制流进入[全局代码的执行环境时](#global-code "wikilink")，执行以下步骤：

1.  按 [10.4.1.1](#initialize-global-context "wikilink") 描述的方案，使用[全局代码初始化执行环境](#global-code "wikilink")。
2.  按 [10.5](#declaration-binding-instantiation "wikilink") 描述的方案，使用[全局代码执行](#global-code "wikilink")[声明式绑定初始化化步骤](#declaration-binding-instantiation "wikilink")。

#### 初始化全局执行环境

以下步骤描述 ECMA 脚本的全局执行环境 **C** 的创建过程：

1.  将 [变量环境组件设置为](#VariableEnvironment "wikilink")[全局环境](#the-global-environment "wikilink")。
2.  将 [词法环境组件设置为](#LexicalEnvironment "wikilink")[全局环境](#the-global-environment "wikilink")。
3.  将 [this绑定设置为](#ThisBinding "wikilink")[全局对象](ES5/builtins#x15.1 "wikilink")。

### 进入 eval 代码

当控制流进入 [eval代码](#eval-code "wikilink") 的执行环境时，执行以下步骤：

1.  如果没有调用环境，或者 [eval代码](#eval-code "wikilink") 并非通过直接调用 [eval](ES5/builtins#x15.1.2.1.1 "wikilink") 函数来解释执行的 ，则
    1.  按（[10.4.1.1](#x10.4.1.1 "wikilink")）描述的初始化全局执行环境的方案，以 [eval代码](#eval-code "wikilink") 作为 **C** 来初始化执行环境。

2.  否则
    1.  将 [this 绑定组件](#ThisBinding "wikilink") 设置为当前执行环境下的 [this 绑定组件](#ThisBinding "wikilink")。
    2.  将 [词法环境组件](#LexicalEnvironment "wikilink") 设置为当前执行环境下的 [词法环境组件](#LexicalEnvironment "wikilink")。
    3.  将 [变量环境组件](#VariableEnvironment "wikilink") 设置为当前执行环境下的 [变量环境组件](#VariableEnvironment "wikilink")。

3.  如果 [eval 代码是](#eval-code "wikilink")[严格模式下的代码](#strict-mode-code "wikilink")，则
    1.  令 <var>strictVarEnv</var> 为以词法环境为参数调用 [NewDeclarativeEnvironment](#NewDeclarativeEnvironment "wikilink") 得到的结果。
    2.  设置 [词法环境组件](#LexicalEnvironment "wikilink") 为 <var>strictVarEnv</var>。
    3.  设置 [变量环境组件](#VariableEnvironment "wikilink") 为 <var>strictVarEnv</var>。

4.  按 [10.5](#x10.5 "wikilink") 描述的方案，使用 [eval代码](#eval-code "wikilink") 执行[声明式绑定初始化化步骤](#declaration-binding-instantiation "wikilink")。

#### 严格模式下的限制

如果调用环境的代码或 [eval 代码是](#eval-code "wikilink")[严格模式下的代码](#strict-mode-code "wikilink")，则 [eval](ES5/builtins#x15.1.2.1.1 "wikilink") 代码不能在调用环境的 [变量环境组件](#VariableEnvironment "wikilink") 中[初始化变量及函数绑定](#declaration-binding-instantiation "wikilink")。与之相对的，变量及函数绑定将在一个新的 [变量环境组件](#VariableEnvironment "wikilink") 中被初始化，该 [变量环境组件](#VariableEnvironment "wikilink") 仅可被 [eval 代码访问](#eval-code "wikilink")。

### 进入函数代码

当控制流根据一个函数对象 <var>F</var>、调用者提供的 <var>thisArg</var> 以及调用者提供的 <var>argumentList</var>，进入[函数代码的执行环境时](#function-code "wikilink")，执行以下步骤：

1.  如果[函数代码是](#function-code "wikilink")[严格模式下的代码](#strict-mode-code "wikilink")，设 [this 绑定](#ThisBinding "wikilink") 为 <var>thisArg</var>。
2.  否则如果 <var>thisArg</var> 是 **null** 或 **undefined**，则设 [this 绑定](#ThisBinding "wikilink") 为[全局对象](ES5/builtins#x15.1 "wikilink")。
3.  否则如果 [Type](ES5/types#Type "wikilink")(<var>thisArg</var>) 的结果不为 **Object**，则设 [this 绑定](#ThisBinding "wikilink") 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>thisArg</var>)。
4.  否则设 [this 绑定](#ThisBinding "wikilink") 为 <var>thisArg</var>。
5.  以 <var>F</var> 的 [[[Scope]]](ES5/types#Scope "wikilink") 内部属性为参数调用 [NewDeclarativeEnvironment](#NewDeclarativeEnvironment "wikilink")，并令 <var>localEnv</var> 为调用的结果。
6.  设 [词法环境组件](#LexicalEnvironment "wikilink") 为 <var>localEnv</var>。
7.  设 [变量环境组件](#VariableEnvironment "wikilink") 为 <var>localEnv</var>。
8.  令 <var>code</var> 为 <var>F</var> 的 [[[Code]]](ES5/types#Code "wikilink") 内部属性的值。
9.  按 [10.5](#declaration-binding-instantiation "wikilink") 描述的方案，使用[函数代码](#function-code "wikilink") <var>code</var> 和 <var>argumentList</var> 执行[声明式绑定初始化化步骤](#declaration-binding-instantiation "wikilink")。

声明式绑定初始化
----------------

每个执行环境都有一个关联的 [变量环境组件](#VariableEnvironment "wikilink")。当在一个执行环境下评估一段 ECMA 脚本时，变量和函数定义会以绑定的形式添加到这个 [变量环境组件](#VariableEnvironment "wikilink") 的[环境记录中](#environment-record "wikilink")。对于[函数代码](#function-code "wikilink")，参数也同样会以绑定的形式添加到这个 [变量环境组件](#VariableEnvironment "wikilink") 的[环境记录中](#environment-record "wikilink")。

选择使用哪一个、哪一类型的[环境记录来绑定定义](#environment-record "wikilink")，是由执行环境下执行的 ECMA 脚本的类型决定的，而其它部分的逻辑是相同的。当进入一个执行环境时，会按以下步骤在 [变量环境组件](#VariableEnvironment "wikilink") 上创建绑定，其中使用到调用者提供的代码设为 <var>code</var>，如果执行的是[函数代码](#function-code "wikilink")，则设[参数列表为](ES5/types#List "wikilink") <var>args</var>：

1.  令 <var>env</var> 为当前运行的执行环境的[变量环境组件的](#VariableEnvironment "wikilink")[环境记录项](#environment-record "wikilink")。
2.  如果 <var>code</var> 是 [eval 代码](#eval-code "wikilink")，则令 <var>configurableBindings</var> 为 **true**，否则令 <var>configurableBindings</var> 为 **false**。
3.  如果代码是[严格模式下的代码](#strict-mode-code "wikilink")，则令 <var>strict</var> 为 **true**，否则令 <var>strict</var> 为 **false**。
4.  如果代码为[函数代码](#function-code "wikilink")，则：
    1.  令 <var>func</var> 为通过 [[[Call]]](ES5/types#Call "wikilink") 内部属性初始化 <var>code</var> 的执行的函数对象。令 <var>names</var> 为 <var>func</var> 的 [[[FormalParameters]]](ES5/types#FormalParameters "wikilink") 内部属性的值。
    2.  令 <var>argCount</var> 为 <var>args</var> 中元素的数量。
    3.  令 <var>n</var> 为数值 **0**。
    4.  按列表顺序遍历 <var>names</var>，对于每一个字符串 <var>argName</var>：
        1.  令 <var>n</var> 的值为 <var>n</var> 当前值加 **1**。
        2.  如果 <var>n</var> 大于 <var>argCount</var>，则令 <var>v</var> 为 **undefined**，否则令 <var>v</var> 为 <var>args</var> 中的第 <var>n</var> 个元素。
        3.  以 <var>argName</var> 为参数，调用 <var>env</var> 的 [HasBinding](#HasBinding "wikilink") 具体方法，并令 <var>argAlreadyDeclared</var> 为调用的结果。
        4.  如果 <var>argAlreadyDeclared</var> 的值为 **false**，以 <var>argName</var> 为参数调用 <var>env</var> 的 [CreateMutableBinding](#CreateMutableBinding "wikilink") 具体方法。
        5.  以 <var>argName</var>、<var>v</var> 和 <var>strict</var> 为参数，调用 <var>env</var> 的 [SetMutableBinding](#SetMutableBinding "wikilink") 具体方法。

5.  按源码顺序遍历 <var>code</var>，对于每一个 [FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink") <var>f</var>：
    1.  令 <var>fn</var> 为 [FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink") <var>f</var> 中的 *[Identifier](ES5/lexical#Identifier "wikilink")*。
    2.  按[第 13 章中所述的步骤初始化](ES5/functions "wikilink") [FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink") <var>f</var> ，并令 <var>fo</var> 为初始化的结果。
    3.  以 <var>fn</var> 为参数，调用 <var>env</var> 的 [HasBinding](#HasBinding "wikilink") 具体方法，并令 <var>argAlreadyDeclared</var> 为调用的结果。
    4.  如果 <var>argAlreadyDeclared</var> 的值为 **false**，以 <var>fn</var> 和 <var>configurableBindings</var> 为参数调用 <var>env</var> 的 [CreateMutableBinding](#CreateMutableBinding "wikilink") 具体方法。
    5.  否则如果 <var>env</var> 是全局环境的[环境记录对象](#environment-record "wikilink")，则：
        1.  令 <var>go</var> 为全局对象。
        2.  以 <var>fn</var> 为参数，调用 <var>go</var> 和 [[[GetProperty]]](ES5/types#GetProperty "wikilink") 内部方法，并令 <var>existingProp</var> 为调用的结果。
        3.  如果 <var>existingProp</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 的值为 **true**，则：
            1.  以 <var>fn</var>、由 {[[Value]]: **undefined**, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: <var>configurableBindings</var> } 组成的[属性描述符和](ES5/types#property-descriptor "wikilink") **true** 为参数，调用 <var>go</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

        4.  否则如果 [IsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>existingProp</var>) 的结果为真，或 <var>existingProp</var> 的特性中没有 {[[Writable]]: **true**, [[Enumerable]]: **true**}，则：
            1.  抛出一个 **TypeError** 异常。

    6.  以 <var>fn</var>、<var>fo</var> 和 <var>strict</var> 为参数，调用 <var>env</var> 的 具体方法。

6.  以 **"arguments"** 为参数，调用 <var>env</var> 的 具体方法，并令 <var>argumentsAlreadyDeclared</var> 为调用的结果。
7.  如果 <var>code</var> 是[函数代码](#function-code "wikilink")，并且 <var>argumentsAlreadyDeclared</var> 为 **false**，则：
    1.  以 <var>fn</var>、<var>names</var>、<var>args</var>、<var>env</var> 和 <var>strict</var> 为参数，调用 抽象运算函数，并令 <var>argsObj</var> 为调用的结果。
    2.  如果 <var>strict</var> 为 **true**，则：
        1.  以字符串**"arguments"**为参数，调用 <var>env</var> 的 [CreateImmutableBinding](#CreateImmutableBinding "wikilink") 具体方法。
        2.  以字符串 **"arguments"** 和 <var>argsObj</var> 为参数，调用 <var>env</var> 的 [InitializeImmutableBinding](#InitializeImmutableBinding "wikilink") 具体函数。

    3.  否则：
        1.  以字符串 **"arguments"**为参数，调用 <var>env</var> 的 具体方法。
        2.  以字符串**"arguments"**、<var>argsObj</var> 和 **false** 为参数，调用 <var>env</var> 的 具体函数。

8.  按源码顺序遍历 <var>code</var>，对于每一个 *[VariableDeclaration](ES5/statements#VariableDeclaration "wikilink")* 和 *[VariableDeclarationNoIn](ES5/statements#VariableDeclarationNoIn "wikilink")* 表达式作为 <var>d</var> 执行：
    1.  令 <var>dn</var> 为 <var>d</var> 中的[标识符](ES5/lexical#x7.6 "wikilink")。
    2.  以 <var>dn</var> 为参数，调用 <var>env</var> 的 具体方法，并令 <var>varAlreadyDeclared</var> 为调用的结果。
    3.  如果 <var>varAlreadyDeclared</var> 为 **false**，则：
        1.  以 <var>dn</var> 和 <var>configurableBindings</var> 为参数，调用 <var>env</var> 的 具体方法。
        2.  以 <var>dn</var>、**undefined** 和 <var>strict</var> 为参数，调用 <var>env</var> 的 具体方法。

创建 Arguments 对象
-------------------

当控制器进入到[函数代码的执行环境时](#function-code "wikilink")，将创建一个 **arguments** 对象（透过 [10.5](#x10.5 "wikilink") 指定的方式），除非它作为[标识符](ES5/lexical#x7.6 "wikilink") **arguments** 出现在该函数的形参列表中，或者是该函数代码内部的变量声明[标识符或函数声明](ES5/lexical#x7.6 "wikilink")[标识符](ES5/lexical#x7.6 "wikilink")。

**arguments** 对象通过调用抽象方法 **CreateArgumentsObject** 创建，调用时将以下参数传入：<var>func</var>、<var>names</var>、<var>args</var>、<var>env</var>、<var>strict</var>。将要执行的函数对象作为 <var>func</var> 参数，将该函数的所有形参名加入一个[列表](ES5/types#List "wikilink")，称为 <var>names</var> 参数，将所有传给内部方法 [[[Call]]](ES5/types#Call "wikilink") 的实际参数，称为 <var>args</var> 参数，将该[函数代码的变量环境称为](#function-code "wikilink") <var>env</var> 参数，将该[函数代码是否为](#function-code "wikilink")[严格代码作为](#strict-mode-code "wikilink") <var>strict</var> 参数。当 **CreateArgumentsObject** 调用时，按照以下步骤执行：

1.  令 <var>len</var> 为参数 <var>args</var> 的元素个数。
2.  令 <var>obj</var> 为一个新建的 ECMAScript 对象。
3.  按照 [8.12](ES5/types#object-internal-methods "wikilink") 章节中的规范去设定 <var>obj</var> 对象的所有内部方法。
4.  将 <var>obj</var> 对象的内部属性 [[[Class]]](ES5/types#Class "wikilink") 设置为 **"Arguments"**。
5.  令 <var>Object</var> 为标准的内置对象的构造函数（[15.2.2](ES5/builtins#object-objects "wikilink")）。
6.  将 <var>obj</var> 对象的内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 设置为标准的内置对象的原型对象。
7.  调用 <var>obj</var> 的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 **"length"** 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Value]]: <var>len</var>, [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **true**}，参数为 **false**。
8.  令 <var>map</var> 为表达式 **new Object()** 创建的对象，就是名为 **Object** 的[标准的内置构造函数](ES5/builtins#object-objects "wikilink")。
9.  令 <var>mappedNames</var> 为一个空的[列表](ES5/types#List "wikilink")。
10. 令 <var>indx</var> = <var>len</var> - **1**
11. 当 <var>indx</var> \>= **0** 的时候，重复此过程：
    1.  令 <var>val</var> 为 <var>args</var>（维度从 0 开始的列表）的第 <var>indx</var> 维度所在的元素。
    2.  调用 <var>obj</var> 的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 [ToString](ES5/conversion#to-string "wikilink")(<var>indx</var>) 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Value]]: <var>val</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}，参数为 **false**。
    3.  如果 <var>indx</var> 小于 <var>names</var> 的元素个数，则
        1.  令 <var>name</var> 为 <var>names</var>（维度从 0 开始的列表）的第 <var>indx</var> 维度所在的元素。
        2.  如果 <var>strict</var> 值为 **false**，且 <var>name</var> 不是一个 <var>mappedNames</var> 元素，则
            1.  将 <var>name</var> 添加到 <var>mappedNames</var> 列表中，作为它的一个元素
            2.  令 <var>g</var> 为调用抽象操作 的结果，其参数为 <var>name</var> 和 <var>env</var>。
            3.  令 <var>p</var> 为调用抽象操作 的结果，其参数为 <var>name</var> 和 <var>env</var>。
            4.  调用 <var>map</var> 对象的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 [ToString](ES5/conversion#to-string "wikilink")(<var>indx</var>) 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Set]]: <var>p</var>, [[Get]]: <var>g</var>, [[Configurable]]: **true**}，参数为 **false**。

    4.  令 <var>indx</var> = <var>indx</var> - **1**

12. 如果 <var>mappedNames</var> 不为空，则
    1.  将 <var>obj</var> 对象的内部属性 [[[ParameterMap]]](ES5/types#ParameterMap "wikilink") 设置为 <var>map</var>。
    2.  将 <var>obj</var> 对象的内部方法 [[[Get]]](ES5/types#Get "wikilink")、[[[dGetOwnProperty]]](ES5/types#GetOwnProperty "wikilink")、[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")、[[[Delete]]](ES5/types#Delete "wikilink") 按下面给出的定义进行设置。

13. 如果 <var>strict</var> 值为 **false**，则
    1.  调用 <var>obj</var> 对象的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 **"callee"** 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Value]]: <var>func</var>, [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **true**}，参数为 **false**。

14. 否则，<var>strict</var> 值为 **true**，那么
    1.  令 <var>thrower</var> 为 [[[ThrowTypeError]]](ES5/functions#ThrowTypeError "wikilink") 函数对象（[13.2.3](ES5/functions#ThrowTypeError "wikilink")）。
    2.  调用 <var>obj</var> 对象的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 **"caller"** 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Get]]: <var>thrower</var>, [[Set]]: <var>thrower</var>, [[Enumerable]]: **false**, [[Configurable]]: **false**}，参数为 **false**。
    3.  调用 <var>obj</var> 对象的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")，将 **"callee"** 传递进去，[属性描述符为](ES5/types#property-descriptor "wikilink")：{[[Get]]: <var>thrower</var>, [[Set]]: <var>thrower</var>, [[Enumerable]]: **false**, [[Configurable]]: **false**}，参数为 **false**。

15. 返回 <var>obj</var>。

抽象操作 **MakeArgGetter** 以字符串 <var>name</var> 和环境记录 <var>env</var> 作为参数被调用时，会创建一个函数对象，当执行完后，会返回在 <var>env</var> 中绑定的 <var>name</var> 的值。执行步骤如下：

1.  令 <var>body</var> 为字符 **"return "**、<var>name</var>、**";"** 的连接字符串。
2.  返回一个按照 [13.2](ES5/functions#x13.2 "wikilink") 章节中描述的方式创建的函数对象，它不需要形参列表，以 <var>body</var> 作为它的 *[FunctionBody](ES5/functions#FunctionBody "wikilink")*，以 <var>env</var> 作为它的 *Scope*，并且 <var>strict</var> 值为 **true**。

抽象操作 **MakeArgSetter** 以字符串 <var>name</var> 和环境记录 <var>env</var> 作为参数被调用时，会创建一个函数对象，当执行完后，会给在 <var>env</var> 中绑定的 <var>name</var> 设置一个值。执行步骤如下：

1.  令 <var>param</var> 为 <var>name</var> 和字符串 **"\_arg"** 的连接字符串。
2.  令 <var>body</var> 为字符串 **"<name>=<param>;"**；将 **<name>** 替换为 <var>name</var> 的值，将 **<param>** 替换为 <var>param</var> 的值。
3.  返回一个按照 [13.2](ES5/functions#13.2 "wikilink") 章节中描述的方式创建的函数对象，以一个只包含字符串 <var>param</var> 的[列表作为它的形参](ES5/types#List "wikilink")，以 <var>body</var> 作为它的函数体（*[FunctionBody](ES5/functions#FunctionBody "wikilink")*），以 <var>env</var> 作为它的 [<var>Scope</var>](ES5/functions#13.2 "wikilink")，并且 [<var>strict</var>](ES5/functions#13.2 "wikilink") 值为 **true**。

当 **arguments** 对象的内部方法 **[[Get]]** 在一个非严格模式下带有形参的函数中，在一个属性名为 <var>P</var> 的条件下被调用时，其执行步骤如下：

1.  令 <var>map</var> 为 **arguments** 对象的内部属性 [[[ParameterMap]]](ES5/types#ParameterMap "wikilink")。
2.  令 <var>isMapped</var> 为 <var>map</var> 对象的内部方法 [[[GetOwnPropery]]](ES5/types#GetOwnProperty "wikilink") 传入参数 <var>P</var> 的执行结果。
3.  如果 <var>isMapped</var> 值为 **undefined**，则
    1.  令 <var>v</var> 为 **arguments** 对象的内部默认的 [[[Get]]](ES5/types#Get "wikilink") 方法（[8.12.3](ES5/types#Get-impl "wikilink")），传入参数 <var>P</var> 的执行结果。
    2.  如果 <var>P</var> 为 **"caller"**，且 <var>v</var> 为[严格模式下的](#strict-mode-code "wikilink") **Function** 对象，则抛出一个 **TypeError** 的异常。
    3.  返回 <var>v</var>。

4.  否则，<var>map</var> 包含一个 <var>P</var> 的形参映射表。
    1.  返回 <var>map</var> 对象的内部方法 [[[Get]]](ES5/types#Get "wikilink") 传入参数 <var>P</var> 的执行结果。

当 **arguments** 对象的内部方法 **[[GetOwnProperty]]** 在一个非严格模式下带有形参的函数中，在一个属性名为 <var>P</var> 的条件下被调用时，其执行步骤如下：

1.  令 <var>desc</var> 为 **arguments** 对象的内部方法 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink")（[8.12.1](ES5/types#GetOwnProperty-impl "wikilink")）传入参数 <var>P</var> 的执行结果。
2.  如果 <var>desc</var> 为 **undefined**，返回 <var>desc</var>。
3.  令 <var>map</var> 为 **arguments** 对象内部属性 [[[ParameterMap]]](ES5/types#ParameterMap "wikilink") 的值。
4.  令 <var>isMapped</var> 为 <var>map</var> 对象的内部方法 [[[GetOwnPropery]]](ES5/types#GetOwnProperty "wikilink") 传入参数 <var>P</var> 的执行结果。
5.  如果 <var>isMapped</var> 的值不是 **undefined**，则
    1.  将 <var>desc</var>.[[[Value]]](ES5/types#Value "wikilink") 的值设置为 <var>map</var> 对象的内部方法 [[[Get]]](ES5/types#Get "wikilink") 传入参数 <var>P</var> 的执行结果。

6.  返回 <var>desc</var>。

当 **arguments** 对象的内部方法 **[[DefineOwnProperty]]** 在一个非严格模式下带有形参的函数中，在一个属性名为 <var>P</var>，属性描述符为 <var>Desc</var>，布尔标志为 <var>Throw</var> 的条件下被调用时，其执行步骤如下：

1.  令 <var>map</var> 为 **arguments** 对象的内部属性 [[[ParameterMap]]](ES5/types#ParameterMap "wikilink") 的值。
2.  令 <var>isMapped</var> 为 <var>map</var> 对象的内部方法 [[[GetOwnPropery]]](ES5/types#GetOwnProperty "wikilink") 传入参数 <var>P</var> 的执行结果。
3.  令 <var>allowed</var> 为 **arguments** 对象的内部方法 [[[DefineOwnPropery]]](ES5/types#DefineOwnProperty "wikilink")（[8.12.9](ES5/types#DefineOwnProperty-impl "wikilink")）传入参数 <var>P</var>、<var>Desc</var>、**false** 的执行结果。
4.  如果 <var>allowed</var> 为 **false**，则
    1.  如果 <var>Throw</var> 为 **true**，则抛出一个 **TypeError** 的异常，否则，返回 **false**。

5.  如果 <var>isMapped</var> 的值不为 **undefined**，则
    1.  如果 [IsIsAccessorDescriptor](ES5/types#IsAccessorDescriptor "wikilink")(<var>Desc</var>) 为 **true**，则
        1.  调用 <var>map</var> 对象的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")，传入 <var>P</var> 和 **false** 作为参数。

    2.  否则
        1.  如果 <var>Desc</var>.[[[Value]]](ES5/types#Value "wikilink") 存在，则
            1.  调用 <var>map</var> 对象的内部方法 [[[Put]]](ES5/types#Put "wikilink")，传入 <var>P</var>、<var>Desc</var>.[[[Value]]](ES5/types#Value "wikilink") 和 <var>Throw</var> 作为参数。

        2.  如果 <var>Desc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 存在，且其值为 **false**，则
            1.  调用 <var>map</var> 对象的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")，传入 <var>P</var> 和 **false** 作为参数。

6.  返回 **true**。

当 **arguments** 对象的内部方法 **[[Delete]]** 在一个非严格模式下带有形参的函数中，在一个属性名为 <var>P</var>，布尔标志为 <var>Throw</var> 的条件下被调用时，其执行步骤如下：

1.  令 <var>map</var> 为 **arguments** 对象的内部属性 [[[ParameterMap]]](ES5/types#ParameterMap "wikilink") 的值。
2.  令 <var>isMapped</var> 为 <var>map</var> 对象的内部方法 [[[GetOwnPropery]]](ES5/types#GetOwnProperty "wikilink") 传入参数 <var>P</var> 的执行结果。
3.  令 <var>result</var> 为 **arguments** 对象的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")（[8.12.7](ES5/types#Delete-impl "wikilink")）传入参数 <var>P</var> 和 <var>Throw</var> 的执行结果。
4.  如果 <var>result</var> 为 **true**，且 <var>isMapped</var> 不为 **undefined**，则
    1.  调用 <var>map</var> 对象的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")，传入 <var>P</var> 和 **false** 作为参数。

5.  返回 <var>result</var>。

