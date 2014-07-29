## 句法和词法

### 上下文无关文法

<b title="Context-Free Grammar">上下文无关文法</b>由一系列的[产生式](#production "wikilink")组成。每个产生式的<b title="left-hand side">左边部分</b>是一个被称为[非终结符](#nonterminal "wikilink")的抽象符号，<b title="right-hand side">右边部分</b>是零或多个[非终结符](#nonterminal "wikilink")和[终结符](#terminal "wikilink")的序列。任何文法，其[终结符](#terminal "wikilink")都来自指定的<b title="alphabet">字母集</b>。

当从一个名为<b title="goal symbol">目标符</b>的由特殊非终结符组成的句子开始，给定的上下文无关文法就表示了<b title="language">语言</b>，即：将[产生式](#production "wikilink")右边序列的[非终结符](#nonterminal "wikilink")当作左边，进行反复替换,其结果就成为可能的[终结符序列集合](#terminal "wikilink")（该集合可能无限）。

### 词法和正则表达式文法

[第7章](ES5/lexical "wikilink")给出了ECMAScript的<b title="lexical grammar">词法</b>。该文法的[终结符字符](#terminal "wikilink")（Unicode代码单元）符合[第6章](ES5/source "wikilink")定义的*[SourceCharacter](ES5/source#SourceCharacter "wikilink")*的规则。该词法定义了一组[产生式](#production "wikilink")，从目标符*[InputElementDiv](ES5/lexical#InputElementDiv "wikilink")*或*[InputElementRegExp](ES5/lexical#InputElementRegExp "wikilink")*开始，描述了如何将诸如此类的字符序列转换成一个输入元素序列。

除[空白字符](ES5/lexical#white-space "wikilink")和[注释](ES5/lexical#comments "wikilink")之外的**输入元素**构成了ECMAScript句法的[终结符](#terminal "wikilink")，同时这些输入元素被称为 ECMAScript的<b title="tokens" id="Token">Token</b>。这些[Token](#Token "wikilink")是ECMAScript语言的[保留字](ES5/lexical#reserved-words "wikilink")、[标识符](ES5/lexical#x7.6 "wikilink")、[字面量](ES5/lexical#literals "wikilink")及[标点符号](ES5/lexical#x7.7 "wikilink")。此外，[行终止符](ES5/lexical#line-terminator "wikilink")虽然不被视为[Token](#Token "wikilink")，但会成为**输入元素**流的一部分，用于引导处理[自动插入分号](ES5/lexical#x7.9 "wikilink")。[空白字符](ES5/lexical#white-space "wikilink")和[单行注释](ES5/lexical#SingleLineComment "wikilink")会被简单地丢弃，而不会出现在句法的**输入元素**流中。如果一个[多行注释](ES5/lexical#MultiLineComment "wikilink")（即形式为“/\*...\*/”的注释，不管其是否跨行）不包含[行终止符](ES5/lexical#line-terminator "wikilink")也会被简单地丢弃；但如果一个[多行注释](ES5/lexical#MultiLineComment "wikilink")包含一个或多个[行终止符](ES5/lexical#line-terminator "wikilink")，那么注释会被替换为一个[行终止符](ES5/lexical#line-terminator "wikilink")，进而成为**句法**的**输入元素**流的一部分。

[15.10](ES5/builtins#x15.10 "wikilink")给出了ECMAScript的[<span title="RegExp grammar">正则表达式文法</span>](ES5/builtins#x15.10 "wikilink")。该文法的[终结符](#terminal "wikilink")也由*[SourceCharacter](ES5/source#SourceCharacter "wikilink")*定义。该文法定义了一组[产生式](#production "wikilink")，从**目标符***[Pattern](ES5/builtins#Patterns-Pattern "wikilink")*开始，描述了如何将诸如此类的字符序列翻译成一个正则表达式模式。

双冒号“::”作为分隔符分割了词法和正则表达式的文法[产生式](#production "wikilink")。同时，词法和正则表达式的文法共享乐某些[产生式](#production "wikilink")。

### 数字字符串文法

用于将字符串转换为数字值的另一种文法。此文法与部分词法类似，都与数字字面量有关；该文法有作为[终结符](#terminal "wikilink")的*[SourceCharacter](ES5/source#SourceCharacter "wikilink")*。此文法将出现在[9.3.1](ES5/conversion#x9.3.1 "wikilink") 。

三冒号“:::”作为分隔符分割数字字符串文法的[产生式](#production "wikilink")。

### 句法

第 [11](ES5/expressions "wikilink")、[12](ES5/statements "wikilink")、[13](ES5/functions "wikilink")、[14](ES5/program "wikilink") 章给出了 ECMAScript 的句法。词法定义的 ECMAScript [Token](#Token "wikilink") 是此文法的[终结符](#terminal "wikilink")（[5.1.2](#x5.1.2 "wikilink")）。它定义了一组起始于 *[Program](ES5/program#Program "wikilink")* 目标符的[产生式](#production "wikilink")，描述了怎样的 [Token](#Token "wikilink") 序列才能形成句法上正确的 ECMAScript 程序。

当一个字符流被解析为 ECMAScript 程序时，它首先通过词法应用程序反复转换为一个**输入元素**流；然后再用一个句法应用程序解析这个**输入元素**流。当**输入元素**流没有更多 [Token](#Token "wikilink") 时，如果 [Token](#Token "wikilink") 不能解析为 *[Program](ES5/program#Program "wikilink")* 目标[非终结符的单一实例](#nonterminal "wikilink")，那么程序在句法上存在错误。

只用一个冒号“:”作为分隔符分割句法的[产生式](#production "wikilink")。

事实上第 [11](ES5/expressions "wikilink")、[12](ES5/statements "wikilink")、[13](ES5/functions "wikilink")、[14](ES5/program "wikilink") 章给出的句法，并不能完全说明一个正确的 ECMAScript 程序能接受的 [Token](#Token "wikilink") 序列。一些额外的 [Token](#Token "wikilink") 序列也被接受，即某些特殊位置（如[行结束符前](ES5/lexical#line-terminator "wikilink")）加入分号可以被文法接受。此外，文法描述的某些 [Token](#Token "wikilink") 序列不被文法接受，如一个[行结束符出现在了](ES5/lexical#line-terminator "wikilink")“尴尬”的位置。

### JSON 文法

JSON 文法用于描述 ECMAScript 对象的字符串转换为实际的对象。[15.12.1](ES5/builtins#x15.12.1 "wikilink") 给出了 JSON 文法 。

JSON 文法由 JSON 词法和 JSON 句法组成。JSON 词法用于将字符序列转换为 [Token](#Token "wikilink")，类似 ECMAScript 词法。JSON 句法说明 JSON 词法给出怎样的 [Token](#Token "wikilink") 序列才能转换为句法上是正确的 JSON 对象。

两个冒号“::”作为分隔符分割 JSON 词法的[产生式](#production "wikilink")。JSON 词法使用某些 ECMAScript 词法的[产生式](#production "wikilink")。JSON 句法与 ECMAScript 句法类似。JSON 句法[产生式被一个冒号](#production "wikilink")“:”作为分隔符分割。

### 文法标记法

词法、正则表达式文法、字符串数字文法，以及一些其它文法，每当这些文法的<b id="terminal" title="terminal symbols">终结符</b>被文本直接涉及到时，使用<b title="Fixed width">等宽</b>字符来显示，它们都在文法<b titlie="production" id="production">产生式</b> 中，并且贯穿这份文档。他们表示程序书写正确。所有以这种方式指定的<b title="terminal symbols">终结符</b>，都可以理解为 Unicode 字符的完整的 ASCII 范围，不是任何其他乌焉成马的 Unicode 范围字符。

<b title="nonterminal" id="nonterminal">非终结符</b>以<i title="italic">斜体</i>显示。一个<b title="nonterminal">非终结符</b>的定义由<b title="nonterminal">非终结符</b>名称和其后定义的一个或多个冒号给出。（冒号的数量表示[产生式所属的文法](#production "wikilink")。）<b title="nonterminal">非终结符</b>的右侧有一个或多个替代子紧跟在下一行。 例如，句法定义：

` `***`WhileStatement`***` :`
`   `**`while` `(`**` `*`Expression`*` `**`)`**` `*`Statement`*

表示这个[非终结符](#nonterminal "wikilink") *WhileStatement* 代表 **while** [Token](#Token "wikilink")，其后跟左括号 [Token](#Token "wikilink")，其后跟 *Expression*，其后跟右括号 [Token](#Token "wikilink")，其后跟 *Statement*。这里出现的 *Expression* 和 *Statement* 本身是[非终结符](#nonterminal "wikilink")。另一个例子，句法定义：

` `***`ArgumentList`***` :`
`   `*`AssignmentExpression`*
`   `*`ArgumentList`*` `**`,`**` `*`AssignmentExpression`*

表示这个 *ArgumentList* 可以代表一个 *AssignmentExpression*，或 *ArgumentList*，其后跟一个逗号，其后跟一个 *AssignmentExpression*。这个 *ArgumentList* 的定义是递归的，也就是说，它定义它自身。其结果是，一个 *ArgumentList* 可能包含用逗号隔开的任意正数个参数，每个参数表达式是一个 *AssignmentExpression*。这样，[非终结符共用了递归的定义](#nonterminal "wikilink")。

[终结符或](#terminal "wikilink")[非终结符可能会出现后缀下标](#nonterminal "wikilink") “<sub>opt</sub>”，表示它是可选符号。实际上包含可选符号的<b title="alternative">替代子</b>包含两个右边部分，一个是省略可选元素的，另一个是包含可选元素的。这意味着：

` `***`VariableDeclaration`***` :`
`   `*`Identifier`*` `*`Initialiser`*<sub>`opt`</sub>

是以下的一种缩写：

` `***`VariableDeclaration`***` :`
`   `*`Identifier`*
`   `*`Identifier`*` `*`Initialiser`*

并且：

` `***`IterationStatement`***` :`
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*<sub>`opt`</sub>` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`)`**` `*`Statement`*

是以下的一种缩写：

` `***`IterationStatement`***` :`
`   `**`for`**` `**`(`**` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`)`**` `*`Statement`*

是以下的一种缩写 :

` `***`IterationStatement`***` :`
`   `**`for`**` `**`(`**` `**`;`**` `**`;`**` `*`Expression`*<sub>`opt`</sub>` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `**`;`**` `*`Expression`*` `**`;`**` `*`Expression`*<sub>`opt`</sub>**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `**`;`**` `*`Expression`*<sub>`opt`</sub>**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `*`Expression`*` `**`;`**` `*`Expression`*<sub>`opt`</sub>**`)`**` `*`Statement`*

是以下的一种缩写：

` `***`IterationStatement`***` :`
`   `**`for`**` `**`(`**` `**`;`**` `**`;`**` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `**`;`**` `**`;`**` `*`Expression`*` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `**`;`**` `*`Expression`*` `**`;`**` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `**`;`**` `*`Expression`*` `**`;`**` `*`Expression`*` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `**`;`**` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `**`;`**` `*`Expression`*` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `*`Expression`*` `**`;`**` `**`)`**` `*`Statement`*
`   `**`for`**` `**`(`**` `*`ExpressionNoIn`*` `**`;`**` `*`Expression`*` `**`;`**` `*`Expression`*` `**`)`**` `*`Statement`*

因此，非终结 *IterationStatement* 实际上有 8 个右侧替代子。

如果文法定义的冒号后面出现文字 “**one of**”，那么其后一行或多行出现的每个[终结符都是一个选择定义](#terminal "wikilink")。例如，ECMAScript 包含的词法生产器：

` `***`NonZeroDigit`***` :: `**`one` `of`**
`   `**`1` `2` `3` `4` `5` `6` `7` `8` `9`**

这仅仅下面写法的一种缩写：

` `***`NonZeroDigit`***` ::`
`   `**`1`**
`   `**`2`**
`   `**`3`**
`   `**`4`**
`   `**`5`**
`   `**`6`**
`   `**`7`**
`   `**`8`**
`   `**`9`**

如果[产生式的右侧是出现](#production "wikilink") “<b id="empty">[empty]</b>”，它表明，生产器的右侧不包含[终结符或](#terminal "wikilink")[非终结符](#nonterminal "wikilink")。

如果[产生式的右侧出现](#production "wikilink") “<b id="lookahead-not-in">[lookahead ? <var>set</var>]</b>”，它表明，给定 <var>set</var> 的成员不得成为[产生式紧随其后的](#production "wikilink") [Token](#Token "wikilink")。这个 <var>set</var> 可以写成一个大括号括起来的[终结符列表](#terminal "wikilink")。为方便起见，<var>set</var> 也可以写成一个[非终结符](#nonterminal "wikilink")，在这种情况下，它代表了这个[非终结符](#nonterminal "wikilink") <var>set</var> 可扩展所有[终结符](#terminal "wikilink")。例如，给出定义

` `***`DecimalDigit`***` :: `**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9`**

` `***`DecimalDigits`***` ::`
`   `*`DecimalDigit`*
`   `*`DecimalDigits`*` `*`DecimalDigit`*

再定义

` `***`LookaheadExample`***` ::`
`   `**`n`**` [lookahead ? {`**`1`**` , `**`3`**` , `**`5`**` , `**`7`**` , `**`9`**`}] `*`DecimalDigits`*
`   `*`DecimalDigit`*` [lookahead ? `*`DecimalDigit`*`]`

匹配，字母 **n** 后跟随由偶数起始的一个或多个十进制数字，或一个十进制数字后面跟随一个非十进制数字。

如果[产生式的右侧出现](#production "wikilink") <b id="restricted-production">“[no *[LineTerminator](ES5/lexical#LineTerminator "wikilink")* here]”</b>，那么它表示此[产生式是个受限的](#production "wikilink")[产生式](#production "wikilink")：如果 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")* 在输入流的指定位置出现，那么此[产生式将不会被适用](#production "wikilink")。例如，[产生式](#production "wikilink")：

` `***`ThrowStatement`***` :`
`   `**`throw`**` `*`[no` [`LineTerminator`](ES5/lexical#LineTerminator "wikilink") `here]`*` `*`Expression`*` `**`;`**

表示如果程序中 **throw** [Token](#Token "wikilink") 和 *Expression* 之间的出现 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")*，那么不得使用此产生式。

*[LineTerminator](ES5/lexical#LineTerminator "wikilink")* 除了禁止出现在受限的[产生式](#production "wikilink")，可以在**输入元素**流的任何两个 [Token](#Token "wikilink") 之间出现任意次数，而不会影响程序的句法验证。

当一个词法[产生式或数字字符串文法中出现多字符](#production "wikilink") [Token](#Token "wikilink")，它表示此字符序列将注册一个 [Token](#Token "wikilink")。

使用词组 “**but not**” 可以指定某些不允许在[产生式右侧的扩展](#production "wikilink")，它说明排除这个扩展。例如，[产生式](#production "wikilink")：

` `***`Identifier`***` ::`
`   `*`IdentifierName`*` `**`but` `not`**` `*`ReservedWord`*

此[非终结符](#nonterminal "wikilink") *Identifier* 可以由可替换成 *IdentifierName* 的字符序列替换，相同的字符序列不能替换 *ReservedWord*。

最后，对于实际上不可能列出全部可变元的少量[非终结符](#nonterminal "wikilink")，我们用普通字体写出描述性的短语来描述它们：

` `***`SourceCharacter`***` ::`
`   any Unicode code unit`

算法约定
--------

此规范通常使用带编号的列表来指定算法的步骤。这些算法是用来精确地指定 ECMAScript 语言结构所需的语义。该算法无意暗示任何具体实现使用的技术。在实践中，也许可用更有效的算法实现一个给定功能。

为了方便其使用本规范的多个部分，叫做<b title="abstract operations">抽象操作</b>的一些算法编写成带名称的可传参函数化形式，所以在其他算法里可以通过名称引用它们。

当一个算法产生返回值 ，“<b title="return">返回</b> <var>x</var>” 指令说明该算法的返回值是 <var>x</var>，并且算法应该终止。“第 <var>n</var> 步的结果” 的简写是 **Result**(<var>n</var>) 。

为了表达清晰，算法的步骤可细分为有序的子步骤。子步骤被缩进，可以将自身进一步划分为缩进子步骤。大纲编号约定用于识别分步骤，第一层次的子步骤适用小写字母标记，第二层次的子步骤使用小写罗马数字标记。如果需要超过三个层次，则重复这些规则，第四层次使用数字标记。

例如 :

1.  Top-level step
    1.  Substep.
    2.  Substep
        1.  Subsubstep.
        2.  Subsubstep.
            1.  Subsubsubstep
                1.  Subsubsubsubstep

一个步骤或子步骤可使用谓词“<b title="if">若</b>”作为其子步骤的条件。在这种情况下，当谓词为真时子步骤才适用。如果一个步骤或子步骤由单词“<b title="else">否则</b>”开始，那么它也是一个谓词，否定前面的同一层级的谓词“<b title="if">若</b>”。

一个步骤可以表示其子步骤的迭代应用可能指定其子步的迭代应用程序。

数学运算，如加法、减法、取反、乘法、除法，以及稍后在本节中定义的数学函数，他们应该总是被理解为对数学实数计算精确的数学结果，其中不包括无穷大，不包括负零区别于正零。本标准中的浮点运算算法模型，包括明确的步骤，在必要情况下处理无穷大和有符号零和执行四舍五入。如果一个数学运算或函数应用一个浮点数，它应该被应用为代表此浮点数的确切的数学值，一个浮点数必须是有限的 ，如果是 **+0** 或 **-0** ，则相应的数学值就是 **0**。

数学函数 <b id="abs">abs(<var>x</var>)</b> 产生 <var>x</var> 的绝对值，如果 <var>x</var> 是负数（小于零），它是这是 -<var>x</var>，否则是 <var>x</var> 本身。

如果 <var>x</var> 是正数，数学函数 <b id="sign">sign(<var>x</var>)</b> 产生 **1**，如果 <var>x</var> 是负数产生 **-1**。此标准中 <var>x</var> 为零的情况下不使用 **sign** 函数。

符号 <b id="modulo">“<var>x</var> modulo <var>y</var>”</b>（<var>y</var> 必须有限且非零）计算一个满足以下条件的 <var>k</var> 值 ，与 <var>y</var> 同号 ( 或是零 ) ，abs(<var>k</var>) \< abs(<var>y</var>) ，对一些整数 <var>q</var> 满足 <var>x</var>-<var>k</var> = <var>k</var>×<var>k</var>。

数学函数 <b id="floor">floor(<var>x</var>)</b> 产生不大于 <var>x</var> 的最大整数（最大可为正无穷）。

如果算法定义“**抛出一个异常**”，算法的执行将被终止，且没有返回结果。已调用的算法也被终止，直到算法步骤使用术语“**如果一个异常被抛出 ...**”明确指出异常处理。一旦遇到这种算法步骤，异常将不再被视已发生过。

