`   `*<b id="Program">`Program`</b>*` :`
`       `**<sub>`opt`</sub>

`   `*<b id="SourceElements">`SourceElements`</b>*` :`
`       `**` `
`       `**`  `**

`   `*<b id="SourceElement">`SourceElement`</b>*` :`
`       `*[`Statement`](ES5/statements#Statement "wikilink")*` `
`       `*[`FunctionDeclaration`](ES5/functions#FunctionDeclaration "wikilink")*

产生式 ** **:** *<sub>opt</sub>* 依照下面的步骤来解释执行：

1.  若 ** 的指令序言（参考 [14.1](#directive-prologue "wikilink") 章）中，包含严格模式指令， 或者满足 [10.1.1](ES5/execution#strict-mode-code "wikilink") 章节所描述的任何一个条件，则 ** 的代码就是一段[严格模式代码](ES5/execution#strict-mode-code "wikilink")，并对应性的，以[严格模式或](ES5/execution#strict-mode-code "wikilink")[非严格模式](ES5/execution#strict-mode-code "wikilink")，依照下面列出的步骤来解释执行代码。
2.  若没有 ** 部分 , 则返回 (**normal**, **empty**, **empty**)。
3.  令 <var>progCxt</var> 为一个新的，如 [10.4.1](ES5/execution#entering-global-code "wikilink") 章节所描述的，应用于[全局代码的执行环境](ES5/execution#global-code "wikilink")。
4.  令 <var>result</var> 为解释执行 ** 的结果。
5.  退出 <var>progCxt</var> 这个执行环境。
6.  返回 <var>result</var>。

产生式 ** **:** ** ** 依照下面的步骤来解释执行 :

1.  令 <var>headResult</var> 为解释执行 ** 的结果。
2.  若 <var>headResult</var> 是[非常规性完结的](ES5/types#abrupt-completion "wikilink")，返回 <var>headResult</var>。
3.  令 <var>tailResult</var> 为解释执行 ** 的结果。
4.  若 <var>tailResult</var>**.value** 为 **empty**，令 <var>V</var> = <var>headResult</var>**.value**，其他情况，令 <var>V</var> = <var>tailResult</var>**.value**。
5.  返回 (<var>tailResult</var>**.type**, <var>V</var>, <var>tailResult</var>**.target**)。

产生式 : ** **:** *[Statement](ES5/statements#Statement "wikilink")* 依照下面的步骤来解释执行：

1.  返回解释执行 [Statement](ES5/statements#Statement "wikilink") 的结果。

产生式 : ** **:** *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")* 依照下面的步骤来解释执行：

1.  返回 (**normal**, **empty**, **empty**)。

指令序言和严格模式指令
----------------------

一个**指令序言**，是那些从 ** 或 *[FunctionBody](ES5/functions#FunctionBody "wikilink")* 的首个 ** 开始，到那些完全由一个字符串字面量后面跟一个分号，所构成的最长的 *[ExpressionStatement](ES5/statements#x12.4 "wikilink")* 序列。*[ExpressionStatement](ES5/statements#x12.4 "wikilink")* 序列中的每一个都是 *[StringLiteral](ES5/lexical#x7.8.4 "wikilink")* 后面接分号，可以显式的插入，或者借助[分号自动插入机制来插入](ES5/lexical#automatic-semicolon-insertion "wikilink")。一个指令序言也可以是一个空的序列。

**严格模式指令**是一个 **"use strict"** 或 **'use strict'** 的 *[StringLiteral](ES5/lexical#x7.8.4 "wikilink")*。一个严格模式指令不应该包含 *[EscapeSequence](ES5/lexical#EscapeSequence "wikilink")* 或 *[LineContinuation](ES5/lexical#LineContinuation "wikilink")*。

一个指令序言，可以不仅仅包含一个严格模式指令。然而，当这种情况出现的时候，ECMAScript 实现可以发出一个相关警告。

