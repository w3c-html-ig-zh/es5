语法：

` `*<b id="Statement">`Statement`</b>*` :`
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**

语义：

一个 ** 可以是 ** 的一部分，这个 ** 自身也可以是 ** 的一部分，以 此类推。当描述个别语句时引入标签的这种方式统称为 <b id="current-label-set">“当前标签组”</b>。一个 ** 介绍了一个标签到一个 **标签组**，此外没有其他语义。一个 ** 或 ** 的标签组最初包含单个 **empty** 元素。任何其他语句的标签组最初是空的。

块 
---

语法：

` `*<b id="Block">`Block`</b>*` :`
`   `**`{`**` `**<sub>`opt`</sub>` `**`}`**

` `*<b id="StatementList">`StatementList`</b>*` :`
`   `**
`   `**` `**

语义：

产生式 ** **:** **{** **}** 按照下面的过程执行 :

1.  返回 (**normal**, **empty**, **empty**)。

产生式 ** **:** **{** ** **}** 按照下面的过程执行 :

1.  返回解释执行 ** 的结果。

产生式 ** **:** ** 按照下面的过程执行 :

1.  令 <var>s</var> 为解释执行 ** 的结果。
2.  如果有一个异常被抛出，返回 (**throw**, <var>V</var>, **empty**)，这里的 <var>V</var> 是异常。( 仿佛没有抛出异常一样继续运行。)
3.  返回 <var>s</var>。

产生式 ** **:** * * 按照下面的过程执行 :

1.  令 <var>sl</var> 为解释执行 ** 的结果。
2.  如果 <var>sl</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>sl</var>。
3.  令 <var>s</var> 为解释执行 ** 的结果。
4.  如果有一个异常被抛出，返回 (**throw**, <var>V</var>, **empty**)，这里的 <var>V</var> 是异常。 ( 仿佛没有抛出异常一样继续运行。)
5.  如果 <var>s</var>**.value** 是 **empty** ，令 <var>V</var> = <var>sl</var>**.value**, 否则令 <var>V</var> = <var>s</var>**.value**。
6.  返回 (<var>s</var>**.type**, <var>V</var>, <var>s</var>**.target**)。

变量语句 
---------

语法：

`   `*<b id="VariableStatement">`VariableStatement`</b>*` :`
`       `**`var`**` `**` `**`;`**

`   `*<b id="VariableDeclarationList">`VariableDeclarationList`</b>*` :`
`       `**
`       `**` `**`,`**` `**

`   `*<b id="VariableDeclarationListNoIn">`VariableDeclarationListNoIn`</b>*` :`
`       `**
`       `**` `**`,`**` `**

`   `*<b id="VariableDeclaration">`VariableDeclaration`</b>*` :`
`       `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**

`   `*<b id="VariableDeclarationNoIn">`VariableDeclarationNoIn`</b>*` :`
`       `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**

`   `*<b id="Initialiser">`Initialiser`</b>*` :`
`       `**`=`**` `*[`AssignmentExpression`](ES5/expressions#AssignmentExpression "wikilink")*

`   `*<b id="InitialiserNoIn">`InitialiserNoIn`</b>*` :`
`       `**`=`**` `*[`AssignmentExpressionNoIn`](ES5/expressions#AssignmentExpressionNoIn "wikilink")*

一个变量语句声明依 [10.5](ES5/execution#declaration-binding-instantiation "wikilink") 中定义创建的变量。当创建变量时初始化为 **undefined**。当 ** 被执行时变量关联的 ** 会被分配 *[AssignmentExpression](ES5/expressions#AssignmentExpression "wikilink")* 的值，而不是在变量创建时。

语义：

产生式 ** **:** **var** ** **;** 按照下面的过程执行 :

1.  解释执行 **。
2.  返回 (**normal**, **empty**, **empty**)。

产生式 ** **:** ** 按照下面的过程执行 :

1.  解释执行 **。

产生式 ** **:** ** **,** ** 按照下面的过程执行 :

1.  解释执行 **。
2.  解释执行 **。

产生式 ** **:** *[Identifier](ES5/lexical#Identifier "wikilink")* 按照下面的过程执行 :

1.  返回一个包含跟 *[Identifier](ES5/lexical#Identifier "wikilink")* 完全相同的字符序列的字符串值。

产生式 ** **:** *[Identifier](ES5/lexical#Identifier "wikilink")* ** 按照下面的过程执行 :

1.  令 <var>lhs</var> 为解释执行 *[Identifier](ES5/lexical#Identifier "wikilink")* 的结果，如 [11.1.2](ES5/expressions#identifier-reference "wikilink") 所述。
2.  令 <var>rhs</var> 为解释执行 ** 的结果。
3.  令 <var>value</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>rhs</var>)。
4.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lhs</var>, <var>value</var>)。
5.  返回一个包含跟 *[Identifier](ES5/lexical#Identifier "wikilink")* 完全相同的字符序列的字符串值。

如果 ** 嵌套在 [with](ES5/statements#WithStatement "wikilink") 语句里并且 ** 里的标识符与 [with](ES5/statements#WithStatement "wikilink") 语句的[对象式环境记录项关联的](ES5/execution#object-environment-record "wikilink")[绑定对象的一个属性名相同](ES5/execution#binding-object "wikilink")，则第 4 步将给这个属性分配值，而不是为 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 [VariableEnvironment](ES5/execution#VariableEnvironment "wikilink") 绑定分配值。

产生式 ** **:** **=** *[AssignmentExpression](ES5/expressions#AssignmentExpression "wikilink")* 按照下面的过程执行 :

1.  返回解释执行 *[AssignmentExpression](ES5/expressions#AssignmentExpression "wikilink")* 的结果。

产生式 **, **, ** 解释执行的方式与产生式 **, **，** 相同，除了他们包含的 **, **, **, *[AssignmentExpressionNoIn](ES5/expressions#AssignmentExpressionNoIn "wikilink")* 会分别替代 **, **, **, *[AssignmentExpression](ES5/expressions#AssignmentExpression "wikilink")* 来解释执行。

### 严格模式的限制

如果一个 ** 或 ** 出现在[严格模式代码里并且其](ES5/execution#strict-mode-code "wikilink") *[Identifier](ES5/lexical#Identifier "wikilink")* 是 **"eval"** 或 **"arguments"**，那么这是个 **SyntaxError**。

空语句 
-------

语法 :

` `*<b id="EmptyStatement">`EmptyStatement`</b>*` :`
`   `**`;`**

语义：

产生式 ** **:** **;** 按照下面的过程执行 :

1.  返回 (**normal**, **empty**, **empty**)。

表达式语句 
-----------

语法：

` `*<b id="ExpressionStatement">`ExpressionStatement`</b>*` :`
`   [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` {`**`{`**`, `**`function`**`}] `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**

语义：

产生式 ** **:** [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") {**{**, **function**}] *[Expression](ES5/expressions#Expression "wikilink")* **;** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  返回 (<var>normal</var>, [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>), **empty**)。

if 语句 
--------

语法：

` `*<b id="IfStatement">`IfStatement`</b>*` :`
`   `**`if` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**` `**`else`**` `**
`   `**`if` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**

每个 **else** 选择与它相关联的 **if** 是不确定的，应与此 **else** 最近的并且原本没有与其对应的 **else** 的可能的 **if** 对应。

语义：

产生式 ** **:** **if** **(** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** **else** ** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果 .
2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)) 为 **true** ，则
    1.  返回解释执行第一个 ** 的结果。

3.  否则,
    1.  返回解释执行第二个 ** 的结果。

产生式 ** **:** **if** **(** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink") (<var>exprRef</var>)) 为 **false** 则返回 (**normal**, **empty**, **empty**).
3.  返回解释执行 ** 的结果。

迭代语句
--------

语法：

` `*<b id="IterationStatement">`IterationStatement`</b>*` :`
`   `**`do`**` `**` `**`while` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)` `;`**` `
`   `**`while` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**
`   `**`for` `(`**` `*[`ExpressionNoIn`](ES5/expressions#ExpressionNoIn "wikilink")*` `**`;`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**
`   `**`for` `(` `var`**` `**` `**`;`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**
`   `**`for` `(`**` `*[`LeftHandSideExpression`](ES5/expressions#LeftHandSideExpression "wikilink")*` `**`in`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**
`   `**`for` `(` `var`**` `**` `**`in`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**

### do-while 语句 

产生式 **do** ** **while** **(** *[Expression](ES5/expressions#Expression "wikilink")* **) ;** 按照下面的过程执行 :

1.  令 <var>V</var> = **empty**。
2.  令 <var>iterating</var> 为 **true**。
3.  只要 <var>iterating</var> 为 **true**，就重复
    1.  令 <var>stmt</var> 为解释执行 ** 的结果。
    2.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    3.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>V</var>, **empty**)。
        2.  如果 <var>stmt</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

    4.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
    5.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)) 是 **false**，设定 <var>iterating</var> 为 **false**。

4.  返回 (**normal**, <var>V</var>, **empty**)。

### while 语句 

产生式 ** **:** **while** **(** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>V</var> = **empty**。
2.  重复
    1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
    2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)) 是 **false**，返回 (**normal**, <var>V</var>, **empty**)。
    3.  令 <var>stmt</var> 为解释执行 ** 的结果。
    4.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    5.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组内](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，则
            1.  返回 (**normal**, <var>V</var>, **empty**)。

        2.  如果 <var>stmt</var> 是一个[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

### for 语句 

产生式 ** **:** **for** **(** *[ExpressionNoIn](ES5/expressions#ExpressionNoIn "wikilink")*<sub>opt</sub> **;** *[Expression](ES5/expressions#Expression "wikilink")*<sub>opt</sub> **;** *[Expression](ES5/expressions#Expression "wikilink")*<sub>opt</sub> **)** ** 按照下面的过程执行 :

1.  如果 *[ExpressionNoIn](ES5/expressions#ExpressionNoIn "wikilink")* 存在，则
    1.  令 <var>exprRef</var> 为解释执行 *[ExpressionNoIn](ES5/expressions#ExpressionNoIn "wikilink")* 的结果。
    2.  调用 [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)。（不会用到此值。)

2.  令 <var>V</var> = **empty**。
3.  重复
    1.  如果第一个 *[Expression](ES5/expressions#Expression "wikilink")* 存在，则
        1.  令 <var>testExprRef</var> 为解释执行第一个 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
        2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>testExprRef</var>)) 是 **false**，返回 (**normal**, <var>V</var>, **empty**)。

    2.  令 <var>stmt</var> 为解释执行 ** 的结果。
    3.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    4.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>V</var>, **empty**)。
    5.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组内](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

    6.  如果第二个 *[Expression](ES5/expressions#Expression "wikilink")* 存在，则
        1.  令 <var>incExprRef</var> 为解释执行第二个 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
        2.  调用 [GetValue](ES5/types#GetValue "wikilink")(<var>incExprRef</var>)。（不会用到此值。）

产生式 ** **:** **for** **(** **var** ** **;** *[Expression](ES5/expressions#Expression "wikilink")*<sub>opt</sub> **;** *[Expression](ES5/expressions#Expression "wikilink")*<sub>opt</sub> **)** ** 按照下面的过程执行 :

1.  解释执行 **。
2.  令 <var>V</var> = **empty**。
3.  重复
    1.  如果第一个 *[Expression](ES5/expressions#Expression "wikilink")* 存在，则
        1.  令 <var>testExprRef</var> 为解释执行第一个 *[Expression](ES5/expressions#Expression "wikilink")* 的结果 .
        2.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>testExprRef</var>)) 是 **false**，则返回 (**normal**, <var>V</var>, **empty**)。

    2.  令 <var>stmt</var> 为解释执行 ** 的结果。
    3.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    4.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>V</var>, **empty**)。
    5.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组内](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

    6.  如果第二个 *[Expression](ES5/expressions#Expression "wikilink")* 存在，则
        1.  令 <var>incExprRef</var> 为解释执行第二个 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
        2.  调用 [GetValue](ES5/types#GetValue "wikilink")(<var>incExprRef</var>)。（不会用到此值。）

### for-in 语句 

产生式 ** **:** **for** **(** ''' ''' *[LeftHandSideExpression](ES5/expressions#LeftHandSideExpression "wikilink")* **in** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  令 <var>experValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)。
3.  如果 <var>experValue</var> 是 **null** 或 **undefined**，返回 (**normal**, **empty**, **empty**)。
4.  令 <var>obj</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>experValue</var>)。
5.  令 <var>V</var> = **empty**。
6.  重复
    1.  令 <var>P</var> 为 <var>obj</var> 的下一个 [[[Enumerable]]](ES5/types#Enumerable "wikilink") 特性为 **true** 的属性的名。如果不存在这样的属性，返回 (**normal**, <var>V</var>, **empty**)。
    2.  令 <var>lhsRef</var> 为解释执行 *[LeftHandSideExpression](ES5/expressions#LeftHandSideExpression "wikilink")* 的结果（它可能解释执行多次）。
    3.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>lhsRef</var>, <var>P</var>)。
    4.  令 <var>stmt</var> 为解释执行 ** 的结果。
    5.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    6.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>V</var>, **empty**)。
    7.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组内](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var> 是[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

产生式 ** **:** **for** **(** **var** ** **in** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>varName</var> 为解释执行 ** 的结果。
2.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
3.  令 <var>experValue</var> 为 [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)。
4.  如果 <var>experValue</var> 是 **null** 或 **undefined**，返回 (**normal**, **empty**, **empty**)。
5.  令 <var>obj</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>experValue</var>)。
6.  令 <var>V</var> = **empty**。
7.  重复
    1.  令 <var>P</var> 为 <var>obj</var> 的下一个 [[[Enumerable]]](ES5/types#Enumerable "wikilink") 特性为 **true** 的属性的名。如果不存在这样的属性，返回 (**normal**, <var>V</var>, **empty**)。
    2.  令 <var>varRef</var> 为解释执行 <var>varName</var> 的结果，仿佛它是个标示符引用（[11.1.2](ES5/expressions#identifier-reference "wikilink")）。它可能解释执行多次。
    3.  调用 [PutValue](ES5/types#PutValue "wikilink")(<var>varRef</var>, <var>P</var>)。
    4.  令 <var>stmt</var> 为解释执行 ** 的结果。
    5.  如果 <var>stmt</var>**.value** 不是 **empty**，令 <var>V</var> = <var>stmt</var>**.value**。
    6.  如果 <var>stmt</var>**.type** 是 **break** 并且 <var>stmt</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>V</var>, **empty**)。
    7.  如果 <var>stmt</var>**.type** 不是 **continue** || <var>stmt</var>**.target** 不在[当前标签组内](#current-label-set "wikilink")，则
        1.  如果 <var>stmt</var> 是[非常规完结](ES5/types#abrupt-completion "wikilink")，返回 <var>stmt</var>。

枚举的属性（第一个算法中的 **第6.1步**、第二个算法中的 **第7.1步**）的机制和顺序并没有指定。在枚举过程中枚举的对象属性可能被删除。如果在枚举过程中，删除了还没有被访问到的属性，那么它将不会被访问到。如果在枚举过程中添加新属性到列举的对象，新增加的属性也无法保证被当前执行中的枚举访问到。在任何枚举中对同一个属性名称的访问不得超过一次。

从对象中枚举属性时也包括对象的原型链。但如果一个原型中的属性是“**被遮住的**”（原型链中靠前的对象有同样的属性名）就不会枚举。当一个原型对象的属性被原型链中靠前的对象属性遮住时就不考虑它的[[[Enumerable]]特性](ES5/types#Enumerable "wikilink")。

continue 语句 
--------------

语法：

` `*<b id="ContinueStatement">`ContinueStatement`</b>*` :`
`   `**`continue` `;`**
`   `**`continue`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**`;`**

语义：

如果以下任意一个为真，那么程序被认为是语法错误的：

-   程序包含一个不带可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 **continue** 语句，没有直接或间接（不跨越函数边界）的嵌套在 ** 里。
-   程序包含一个有可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 **continue** 语句，这个 *[Identifier](ES5/lexical#Identifier "wikilink")* 没有出现在 ** 中闭合[标签组里](#current-label-set "wikilink")（不跨越函数边界）。

一个没有 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 ** 按照下面的过程执行 :

1.  返回 (**continue**, **empty**, **empty**)。

一个有可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 ** 按照下面的过程执行 :

1.  返回 (**continue**, **empty**, *[Identifier](ES5/lexical#Identifier "wikilink")*)。

break 语句 
-----------

语法：

` `*<b id="BreakStatement">`BreakStatement`</b>*` :`
`   `**`break` `;`**
`   `**`break`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**`;`**

语义：

如果以下任意一个为真，那么程序被认为是语法错误的：

-   程序包含一个不带可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 **break** 语句，没有直接或间接（不跨越函数边界）的嵌套在 ** 或 ** 里。
-   程序包含一个有可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 **break** 语句，这个 *[Identifier](ES5/lexical#Identifier "wikilink")* 没有出现在 ** 中闭合[标签组里](#current-label-set "wikilink")（不跨越函数边界）。

一个没有 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 ** 按照下面的过程执行 :

1.  返回 (**break**, **empty**, **empty**)。

一个有可选的 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 ** 按照下面的过程执行 :

1.  返回 (**break**, **empty**, *[Identifier](ES5/lexical#Identifier "wikilink")*)。

return 语句 
------------

语法：

` `*<b id="ReturnStatement">`ReturnStatement`</b>*` :`
`   `**`return` `;`**
`   `**`return`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**

语义：

在一个 ECMAScript 程序中包含的 **return** 语句没有在 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 里面，那么就是语法错误的。一个 **return** 语句导致函数停止执行，并返回一个值给调用者。如果省略 *[Expression](ES5/expressions#Expression "wikilink")*，返回值是 **undefined**。否则，返回值是 *[Expression](ES5/expressions#Expression "wikilink")* 的值。

产生式 ** **:** **return** [[no *LineTerminator* here](ES5/notation#restricted-production "wikilink")] *[Expression](ES5/expressions#Expression "wikilink")*<sub>opt</sub> **;** 按照下面的过程执行 :

1.  如果 *[Expression](ES5/expressions#Expression "wikilink")* 不存在，返回 (**return**, **undefined**, **empty**)。
2.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
3.  返回 (**return**, [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>), **empty**)。

with 语句 
----------

语法：

` `*<b id="WithStatement">`WithStatement`</b>*` :`
`   `**`with` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**

**with** 语句为计算对象给当前执行上下文的[词法环境添加一个](ES5/execution#lexical-environment "wikilink")[对象环境记录项](ES5/execution#object-environment-record "wikilink")。然后，用这个增强的[词法环境执行一个语句](ES5/execution#lexical-environment "wikilink")。最后，恢复到原来的[词法环境](ES5/execution#lexical-environment "wikilink")。

语义 :

产生式 ** **:** **with** **(** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>val</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  令 <var>obj</var> 为 [ToObject](ES5/conversion#to-object "wikilink")([GetValue](ES5/types#GetValue "wikilink")(<var>val</var>))。
3.  令 <var>oldEnv</var> 为运行中的执行上下文的[词法环境组件](ES5/execution#LexicalEnvironment "wikilink")。
4.  令 <var>newEnv</var> 为以 <var>obj</var> 和 <var>oldEnv</var> 为参数调用 [NewObjectEnvironment](ES5/execution#NewObjectEnvironment "wikilink") 的结果。
5.  设定 <var>newEnv</var> 的 <var>provideThis</var> 标志为 **true**。
6.  设定运行中的执行上下文的[词法环境组件为](ES5/execution#LexicalEnvironment "wikilink") <var>newEnv</var>。
7.  令 <var>C</var> 为解释执行 ** 的结果，但如果解释执行是由异常抛出，则令 <var>C</var> 为 (**throw**, <var>V</var>, **empty**)，这里的 <var>V</var> 是异常。（现在继续执行，仿佛没有抛出异常。)
8.  设定运行中的执行上下文的[词法环境组件为](ES5/execution#LexicalEnvironment "wikilink") <var>oldEnv</var>。
9.  返回 <var>C</var>。

### 严格模式的限制

严格模式代码中不能包含 **。出现 ** 的上下文被当作一个 **SyntaxError**。

switch 语句 
------------

语法：

` `*<b id="SwitchStatement">`SwitchStatement`</b>*` :`
`   `**`switch` `(`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`)`**` `**

` `*<b id="CaseBlock">`CaseBlock`</b>*` :`
`   `**`{`**` `**` `**`}`**` `
`   `**`{`**` `**` `**` `**` `**`}`**

` `*<b id="CaseClauses">`CaseClauses`</b>*` :`
`   `**
`   `**` `**

` `*<b id="CaseClause">`CaseClause`</b>*` :`
`   `**`case`**` `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`:`**` `**

` `*<b id="DefaultClause">`DefaultClause`</b>*` :`
`   `**`default` `:`**` `**

语义：

产生式 ** **:** **switch** **(** *[Expression](ES5/expressions#Expression "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  令 <var>R</var> 为以 [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>) 作为参数解释执行 ** 的结果。
3.  如果 <var>R</var>**.type** 是 **break** 并且 <var>R</var>**.target** 在[当前标签组内](#current-label-set "wikilink")，返回 (**normal**, <var>R</var>**.value**, **empty**)。
4.  返回 <var>R</var>。

产生式 ** **:** **{** **<sub>opt</sub> **}** 以一个给定输入参数 <var>input</var>, 按照下面的过程执行 :

1.  令 <var>V</var> = **empty**。
2.  令 <var>A</var> 为以源代码中顺序排列的 ** 列表。
3.  令 <var>searching</var> 为 **true**。
4.  只要 <var>searching</var> 为 **true**，就重复
    1.  令 <var>C</var> 为 <var>A</var> 里的下一个 **。 如果没有 ** 了，返回 (**normal**, <var>V</var>, **empty**)。
    2.  令 <var>clauseSelector</var> 为解释执行 <var>C</var> 的结果。
    3.  如果 <var>input</var> 和 <var>clauseSelector</var> 是 [===](ES5/expressions#strict-equality-comparison "wikilink") 操作符定义的相等，则
        1.  设定 <var>searching</var> 为 **false**。
        2.  如果 <var>C</var> 有一个 **, 则
            1.  令 <var>R</var> 为解释执行 <var>C</var> 的 ** 的结果。
            2.  如果 <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 <var>R</var>。
            3.  令 <var>V</var> = <var>R</var>**.value**

5.  重复
    1.  令 <var>C</var> 为 <var>A</var> 里的下一个 **。 如果没有 ** 了，返回 (**normal**, <var>V</var>, **empty**)。
    2.  如果 <var>C</var> 有一个 **，则
        1.  令 <var>R</var> 为解释执行 <var>C</var> 的 ** 的结果。
        2.  如果 <var>R</var>**.value** 不是 **empty**，则令 <var>V</var> = <var>R</var>**.value**。
        3.  如果 <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 (<var>R</var>**.type**, <var>V</var>, <var>R</var>**.target**)。

产生式 ** **:** **{** **<sub>opt</sub> ** **<sub>opt</sub> **}** 以一个给定输入 参数 <var>input</var>，按照下面的过程执行 :

1.  令 <var>V</var> = **empty**。
2.  令 <var>A</var> 为第一个 ** 中以源代码中顺序排列的 ** 列表。
3.  令 <var>B</var> 为第二个 ** 中以源代码中顺序排列的 ** 列表。
4.  令 <var>found</var> 为 **false**。
5.  重复，使 <var>C</var> 为 <var>A</var> 中的依次每个 **。
    1.  如果 <var>found</var> 是 **false**，则
        1.  令 <var>clauseSelector</var> 为解释执行 <var>C</var> 的结果 .
        2.  如果 <var>input</var> 和 <var>clauseSelector</var> 是 [===](ES5/expressions#strict-equality-comparison "wikilink") 操作符定义的相等，则设定 <var>found</var> 为 **true**。

    2.  如果 <var>found</var> 是 **true**，则
        1.  如果 <var>C</var> 有一个 **，则
            1.  令 <var>R</var> 为解释执行 <var>C</var> 的 ** 的结果。
            2.  如果 <var>R</var>**.value** 不是 **empty**，则令 <var>V</var> = <var>R</var>**.value**。
            3.  <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 (<var>R</var>**.type**, <var>V</var>, <var>R</var>**.target**)。

6.  令 <var>foundInB</var> 为 **false**。
7.  如果 <var>found</var> 是 **false**，则
    1.  只要 <var>foundInB</var> 为 **false** 并且所有 <var>B</var> 中的元素都没有被处理，就重复
        1.  令 <var>C</var> 为 <var>B</var> 里的下一个 **。
        2.  令 <var>clauseSelector</var> 为解释执行 <var>C</var> 的结果。
        3.  如果 <var>input</var> 和 <var>clauseSelector</var> 是 [===](ES5/expressions#strict-equality-comparison "wikilink") 操作符定义的相等，则
            1.  设定 <var>foundInB</var> 为 **true**。
            2.  如果 <var>C</var> 有一个 **，则
                1.  令 <var>R</var> 为解释执行 <var>C</var> 的 ** 的结果。
                2.  如果 <var>R</var>**.value** 不是 **empty**，则令 <var>V</var> = <var>R</var>**.value**。
                3.  <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 (<var>R</var>**.type**, <var>V</var>, <var>R</var>**.target**)。

8.  如果 <var>foundInB</var> 是 **false** 并且 ** 有个 **，则
    1.  令 <var>R</var> 为解释执行 ** 的 ** 的结果。
    2.  如果 <var>R</var>**.value** 不是 **empty**，则令 <var>V</var> = <var>R</var>**.value**。
    3.  如果 <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 (<var>R</var>**.type**, <var>V</var>, <var>R</var>**.target**)。

9.  重复（注 : 如果已执行步骤 7.a.i, 此循环不从 B 的开头开始。）
    1.  令 <var>C</var> 为 <var>B</var> 的下一个 **。如果没有 ** 了，返回 (**normal**, <var>V</var>, **empty**)。
    2.  如果 <var>C</var> 有个 **，则
        1.  令 <var>R</var> 为解释执行 <var>C</var> 的 ** 的结果。
        2.  如果 <var>R</var>**.value** 不是 **empty**，则令 <var>V</var> = <var>R</var>**.value**。
        3.  如果 <var>R</var> 是个[非常规完结](ES5/types#abrupt-completion "wikilink")，则返回 (<var>R</var>**.type**, <var>V</var>, <var>R</var>**.target**)。

产生式 ** **:** **case** *[Expression](ES5/expressions#Expression "wikilink")* **:** **<sub>opt</sub> 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  返回 [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>)。

标签语句 
---------

语法：

` `*<b id="LabelledStatement">`LabelledStatement`</b>*` :`
`   `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**`:`**` `**

语义：

一个 ** 可以由一个标签作为前缀。标签语句仅与标签化的 **break** 和 **continue** 语句一起使用。ECMAScript 没有 **goto** 语句。

如果一个 ECMAScript 程序包含有相同 *[Identifier](ES5/lexical#Identifier "wikilink")* 作为标签的 ** 闭合的 **，那么认为它是是语法错误的。这不适用于直接或间接嵌套在标签语句里面的 *[FunctionDeclaration](#ES5/functions#FunctionDeclaration "wikilink")* 的函数体里出现标签的情况。

产生式 *[Identifier](ES5/lexical#Identifier "wikilink")* : ** 的解释执行方式是，先添加 *[Identifier](ES5/lexical#Identifier "wikilink")* 到 ** 的[标签组](#current-label-set "wikilink")，再解释执行 **。如果 ** 自身有一个非空标签组，这些标签还是会添加到解释执行前的 ** 的标签组里。如果 ** 的解释执行结果是 (**break**, <var>V</var>, <var>L</var>)，这里的 <var>L</var> 等于 *[Identifier](ES5/lexical#Identifier "wikilink")*，则产生式的结果是 (**normal**, <var>V</var>, **empty**)。

在解释执行 ** 之前，认为包含的 ** 拥有一个空标签组，除非它是 ** 或 **，这种情况下认为它拥有一个包含单个元素 **empty** 的标签组。

throw 语句 
-----------

语法：

` `*<b id="ThrowStatement">`ThrowStatement`</b>*` :`
`   `**`throw`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**

语义：

产生式 ** **:** **throw** [[no *LineTerminator* here](ES5/notation#restricted-production "wikilink")] *[Expression](ES5/expressions#Expression "wikilink")* **;** 按照下面的过程执行 :

1.  令 <var>exprRef</var> 为解释执行 *[Expression](ES5/expressions#Expression "wikilink")* 的结果。
2.  返回 (**throw**, [GetValue](ES5/types#GetValue "wikilink")(<var>exprRef</var>), **empty**)。

try 语句 
---------

语法：

` `*<b id="TryStatement">`TryStatement`</b>*` :`
`   `**`try`**` `**` `**
`   `**`try`**` `**` `**
`   `**`try`**` `**` `**` `**

` `*<b id="Catch">`Catch`</b>*` :`
`   `**`catch` `(`**` `*[`Identifier`](ES5/lexical#Identifier "wikilink")*` `**`)`**` `**

` `*<b id="Finally">`Finally`</b>*` :`
`   `**`finally`**` `**

**try** 语句包裹一个可以出现特殊状况，如果运行时错误或 **throw** 语句的代码块。**catch** 子句提供了异常处理代码。如果 **catch** 子句捕获到一个异常，这个异常会绑定到它的 **[Identifier](ES5/lexical#Identifier "wikilink")** 上。

语义：

产生式 ** **:** **try** ** ** 按照下面的过程执行 :

1.  令 <var>B</var> 为解释执行 ** 的结果。
2.  如果 <var>B</var>**.type** 不是 **throw**，返回 <var>B</var>。
3.  返回一参数 <var>B</var> 解释执行 ** 的结果。

产生式 ** **:** **try** ** ** 按照下面的过程执行 :

1.  令 <var>B</var> 为解释执行 ** 的结果。
2.  令 <var>F</var> 为解释执行 ** 的结果。
3.  如果 <var>F</var>**.type** 是 **normal**，返回 <var>B</var>。
4.  返回 <var>F</var>。

产生式 ** **:** **try** ** ** ** 按照下面的过程执行 :

1.  令 <var>B</var> 为解释执行 ** 的结果。
2.  如果 <var>B</var>**.type** 是 **throw**，则
    1.  令 <var>C</var> 为以参数 <var>B</var> 解释执行 ** 的结果。

3.  否则，<var>B</var>**.type** 不是 **throw**，
    1.  令 <var>C</var> 为 <var>B</var>。

4.  令 <var>F</var> 为解释执行 ** 的结果。
5.  如果 <var>F</var>**.type** 是 **normal**，返回 <var>C</var>。
6.  返回 <var>F</var>。

产生式 ** **:** **catch** '''( ''' *[Identifier](ES5/lexical#Identifier "wikilink")* **)** ** 按照下面的过程执行 :

1.  令 <var>C</var> 为传给这个产生式的参数。
2.  令 <var>oldEnv</var> 为运行中执行上下文的[词法环境组件](ES5/execution#LexicalEnvironment "wikilink")。
3.  令 <var>catchEnv</var> 为以 <var>oldEnv</var> 为参数调用 [NewDeclarativeEnvironment](ES5/execution#NewDeclarativeEnvironment "wikilink") 的结果。
4.  以 *[Identifier](ES5/lexical#Identifier "wikilink")* 字符串值为参数调用 <var>catchEnv</var> 的 [CreateMutableBinding](ES5/execution#CreateMutableBinding "wikilink") 具体方法。
5.  以 *[Identifier](ES5/lexical#Identifier "wikilink")*、<var>C</var>、<var>false</var> 为参数调用 <var>catchEnv</var> 的 [SetMutableBinding](ES5/execution#SetMutableBinding "wikilink") 具体方法。注：这种情况下最后一个参数无关紧要。
6.  设定运行中执行上下文的[词法环境组件为](ES5/execution#LexicalEnvironment "wikilink") <var>catchEnv</var>。
7.  令 <var>B</var> 为解释执行 ** 的结果。
8.  设定运行中执行上下文的[词法环境组件为](ES5/execution#LexicalEnvironment "wikilink") <var>oldEnv</var>。
9.  返回 <var>B</var>。

产生式 ** **: finally** ** 按照下面的过程执行 :

1.  返回解释执行 ** 的结果。

### 严格模式的限制 

如果一个有 ** 的 ** 出现在 [严格模式代码里](ES5/execution#strict-mode-code "wikilink")，并且 ** 产生式的 *[Identifier](ES5/lexical#Identifier "wikilink")* 是 "**eval**" 或 "**arguments**"，那么这是个 **SyntaxError**。

debugger 语句 
--------------

语法：

` `*<b id="DebuggerStatement">`DebuggerStatement`</b>*` :`
`   `**`debugger` `;`**

语义：

解释执行 ** 产生式可允许让一个实现在调试器下运行时设置断点。如果调试器不存在或是非激活状态，这个语句没有可观测效果。

产生式 ** **:** **debugger ;** 按照下面的过程执行 :

1.  如果一个实现定义了可用的调试工具并且是开启的，则
    1.  执行实现定义的调试动作。
    2.  令 <var>result</var> 为实现定义的[完结值](ES5/types#Completion "wikilink")。

2.  否则
    1.  令 <var>result</var> 为 (**normal**, **empty**, **empty**)。

3.  返回 <var>result</var>。

