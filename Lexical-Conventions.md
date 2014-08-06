ECMAScript程序的源代码文本首先转换成一个由[Token](#Token "wikilink")、[行终止符](#line-terminator "wikilink")、[注释](#comments "wikilink")、[空白字符](#white-space "wikilink") 组成的输入元素序列；从左到右扫描源代码文本，反复获取尽可能长的字符序列来作为下一个输入元素。

词法有两个目标符。*InputElementDiv*目标符用于允许以除法（**/**）或除赋值（**/=**）运算符开始的句法上下文中。*InputElementRegExp*目标符用于其他句法文法上下文中。

注：不存在既允许以除法或除赋值运算符开头又允许以*RegularExpressionLiteral*开头的句法上下文。这一点不会受分号插入的影响（见7.9节）；如下示例：

`  a = b `<br/>
`  /hi/g.exec(c).map(d);`

其中， *LineTerminator*之后的第一个非空白、非注释字符是斜杠（**/**），并且该句法上下文允许除法或除赋值运算符，所以不会在*LineTerminator*位置插入分号。换言之，上面的例子解释为：

`  a = b / hi / g.exec(c).map(d);`

**语法**：

` `*<b id="InputElementDiv">`InputElementDiv`</b>*` ::`<br/>
`   `*`WhiteSpace`*<br/>
`   `*`LineTerminator`*<br/>
`   `*`Comment`*<br/>
`   `*`Token`*<br/>
`   `*`DivPunctuator`*

` `*<b id="InputElementRegExp">`InputElementRegExp`</b>*` ::`<br/>
`   `*`WhiteSpace`*<br/>
`   `*`LineTerminator`*<br/>
`   `*`Comment`*<br/>
`   `*`Token`*<br/>
`   `*`RegularExpressionLiteral`*

## Unicode格式控制字符

Unicode格式控制字符（例如，Unicode字符数据库中[Cf分类](http://www.fileformat.info/info/unicode/category/Cf/list.htm)中的字符，如“<span title="left-to-right mark">左至右符号</span>”或“<span title="left-to-right mark">右至左符号</span>”）用来控制被更高层级协议（如标记语言）忽略的某个范围内文本格式化的控制代码。

允许在源代码文本中出现控制字符非常有利于编辑和显示。所有格式控制字符均可用于注释、字符串字面量、正则表达式字面量。

`<ZWNJ>`和`<ZWJ>`是格式控制字符，可用于在某些语言中形成单词或段落时产生必要的差异。在ECMAScript源代码文本中，`<ZWNJ>`和`<ZWJ>`也可用于首字符之后的标识符。

`<BOM>`是一个格式控制字符，主要用于文本的开头，将文本标记为Unicode，且允许检查文本编码和字节顺序。为此目的，`<BOM>`字符有时也可显示在文本的开始位置之后，例如作为一个合并文件的结果。`<BOM>`字符还可用作[空白字符](#white-space "wikilink")（见[7.2](#7.2 "wikilink")节）

**表1**总结了一些在注释、字符串字面量、正则表达式字面量之外被特殊对待的格式控制字符。

|代码单元值|名称|正式名称|用法|
|:---------|:---|:-------|:---|
|`\u200C`|<span title="Zero width non-joiner">零宽度非连接器</span>|`<ZWNJ>`|*[IdentifierPart](#IdentifierPart "wikilink")*|
|`\u200D`|<span title="Zero width joiner">零宽度连接器</span>|`<ZWJ>`|*[IdentifierPart](#IdentifierPart "wikilink")*|
|`\uFEFF`|<span title="Byte Order Mark">字节顺序标记</span>|`<BOM>`|*[Whitespace](#Whitespace "wikilink")*|

## 空白字符

空白字符用来改善源文本的可读性和分割 [Token](ES5/notation#Token "wikilink")（不可分割的词法单位），此外就无关紧要。空白字符可以出现在两个 [Token](ES5/notation#Token "wikilink") 之间，还可以出现在输入的开始或结束位置，也可以出现在 *[StringLiteral](#StringLiteral "wikilink")* 或 *[RegularExpressionLiteral](#RegularExpressionLiteral "wikilink")*（在这里它表示组成字面量的字符）或 *[Comment](#Comment "wikilink")* 中，但是不能出现的其他任何 [Token](ES5/notation#Token "wikilink") 内。

**表2** 中列出了 ECMAScript 空白字符。

|代码单元值|名称|正式名称|
|----------|----|--------|
|\\u0009|制表符|<TAB>|
|\\u000B|垂直制表符|<VT>|
|\\u000C|换页符|<FF>|
|\\u0020|空格符|<SP>|
|\\u00A0|非中断空格符|<NBSP>|
|\\uFEFF
其它 [Zs类字符](http://www.fileformat.info/info/unicode/category/Zs/list.htm)|字节顺序标记
其它 Unicode 空白分隔符|<BOM>
<USP>|

ECMAScript 实现必须认可 Unicode 3.0 中定义的所有空白字符。后续版本的 Unicode 标准可能定义其他空白字符。ECMAScript 实现可以认可更高版本 Unicode 标准里的空白字符。

语法：

` `*<b id="WhiteSpace">`WhiteSpace`</b>*` ::`
`   `<TAB>
`   `<VT>
`   `<FF>
`   `<SP>
`   `<NBSP>
`   `<BOM>
`   `<USP>

行终止符
--------

像空白字符一样，行终止字符用于改善源文本的可读性和分割 [Token](ES5/notation#Token "wikilink")（不可分割的词法单位）。然而，不像空白字符，行终止符对句法的行为有一定的影响。一般情况下，行终止符可以出现在任何两个 [Token](ES5/notation#Token "wikilink") 之间，但也有少数地方，句法禁止这样做。行终止符也影响自动插入分号的过程（[7.9](#automatic-semicolon-insertion "wikilink")）。行终止符不能出现在 ** 之外的任何 [Token](ES5/notation#Token "wikilink") 内。行终止符只能出现在作为 ** 的一部分的 ** 里。

行终止符可以出现在 ** 内，但不能出现在 ** 内。

正则表达式的 **\\s** 类匹配的空白字符集中包含行终止符。

**表3** 列出了 ECMAScript 的行终止字符。

|代码单元值|名称|正式名称|
|----------|----|--------|
|\\u000A|<span title="Line Feed">换行符</span>|<LF>|
|\\u000D|<span title="Carriage Return">回车符</span>|<CR>|
|\\u2028|<span title="Line separator">行分隔符</span>|<LS>|
|\\u2029|<span title="Paragraph separator">段落分割符</span>|<PS>|

只有 **表3** 中的字符才被视为行终止符。其他新行或折行字符被视为空白，但不作为行终止符。字符序列 **<CR><LF>** 作一个行终止符。计算行数时它应该被视为一个字符。

语法：

` `*<b id="LineTerminator">`LineTerminator`</b>*` ::`
`   `<LF>
`   `<CR>
`   `<LS>
`   `<PS>

` `*<b id="LineTerminatorSequence">`LineTerminatorSequence`</b>*` ::`
`   `<LF>
`   `<CR>` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `<LF>` ]`
`   `<LS>
`   `<PS>
`   `<CR>` `<LF>

注释
----

注释可以是单行或多行。多行注释不能嵌套。

因为单行注释可以包含除了 ** 字符之外的任何字符，又因为有一般规则：一个 [Token](ES5/notation#Token "wikilink") 总是尽可能匹配更长，所以一个单行注释总是包含从 **//** 到行终止符之间的所有字符。然而，在该行末尾的 ** 不被看成是单行注释的一部分，它被词法识别成句法输入元素流的一部分。这一点非常重要，因为这意味着是否存在单行注释都不影响自动分号插入进程（见 [7.9](#automatic-semicolon-insertion "wikilink")）。

像空白一样，注释会被句法简单丢弃，除了 ** 包含行终止符字符的情况，这种情况下整个注释会当作一个 ** 提供给句法文法解析。

语法：

` `*<b id="Comment">`Comment`</b>*` ::`
`   `**
`   `**

` `*<b id="MultiLineComment">`MultiLineComment`</b>*` ::`
`   `**`/*`**` `**` `**`*/`**

` `*<b id="MultilineCommentChars">`MultiLineCommentChars`</b>*` ::`
`   `**` `**
`   `**`*`**` `**

` `*<b id="PostAsteriskCommentChars">`PostAsteriskCommentChars`</b>*` ::`
`   `**` `**
`   `**`*`**` `**

` `*<b id="MultiLineNotAsteriskChar">`MultiLineNotAsteriskChar`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not` `*`**

` `*<b id="MultiLineNotForwardSlashOrAsteriskChar">`MultiLineNotForwardSlashOrAsteriskChar`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not` `/` `or` `*`**

` `*<b id="SingleLineComment">`SingleLineComment`</b>*` ::`
`   `**`//`**` `**

` `*<b id="SingleLineCommentChars">`SingleLineCommentChars`</b>*` ::`
`   `**` `**

` `*<b id="SingleLineCommentChar">`SingleLineCommentChar`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not`**` `**

Token 
------

语法：

` `*<b id="Token">`Token`</b>*` ::`
`   `**
`   `**
`   `**
`   `**

标识符名和标识符
----------------

标识符名属于 [Token](#Token "wikilink")，[Unicode标准第5章](http://www.unicode.org/versions/Unicode3.0.0/ch05.pdf) 的“Identifiers”节给出的文法加入了一些小修改来解释它。** 是一个 ** 但不是一个 **。Unicode 标识符文法基于 Unicode 标准指出的 normative 和 informative 字符分类 。所有符合 ECMAScript 的实现必须能够正确处理 Unicode 标准 3.0 版本中指定的分类里的字符的分类。

本标准增加了个别字符：在 ** 的任何位置允许出现美元符（**\$**）和下划线（**\_**）。

** 还允许出现 Unicode 转义序列，它们被 ** 的<b title="CV">字符值</b>计算成单个字符贡献给 **（见 [7.8.4](#string-literals "wikilink")）。** 前面的 **\\** 不给 ** 贡献字符。** 不能提供单个字符给将要成为非法字符的 **。换句话说，如果一个 **\\** ** 序列被 ** 的<b title="CV">字符值</b>替换，结果必须仍是有效的包含与原 ** 精确相同字符序列的 **。本规范说明的所有标识符是根据它的实际字符，不管转义序列贡献特定字符与否。

根据 Unicode 标准两个规范的 相等，是说除非他们的代码单元序列准确相等，否则不同（换句话说，符合 ECMAScript 的实现只需要按位比较 值）。其目的是为了传入编译器之前就把[源代码文本转换为](ES5/source "wikilink")<b title="Normalization Form">正规形式</b> C。

ECMAScript 实现可以识别后续版本 Unicode 标准定义的标识符字符。如果考虑可移植性，程序员应该只采用 Unicode 3.0 中定义的标识符字符。

语法：

` `*<b id="Identifier">`Identifier`</b>*` ::`
`   `**` `**`but` `not`**` `**

` `*<b id="IdentifierName">`IdentifierName`</b>*` ::`
`   `**
`   `**` `**

` `*<b id="IdentifierStart">`IdentifierStart`</b>*` ::`
`   `**
`   `**`$`**
`   `**`_`**
`   `**`\`**` `**

`  `*<b id="IdentifierPart">`IdentifierPart`</b>*` ::`
`   `**
`   `**
`   `**
`   `**
`   `<ZWNJ>
`   `<ZWJ>

` `*<b id="UnicodeLetter">`UnicodeLetter`</b>*
`   any character in the Unicode categories `
`   “`[`Uppercase` `letter` `(Lu)`](http://www.fileformat.info/info/unicode/category/Lu/list.htm)`”, “`[`Lowercase` `letter` `(Ll)`](http://www.fileformat.info/info/unicode/category/Ll/list.htm)`”, `
`   “`[`Titlecase` `letter` `(Lt)`](http://www.fileformat.info/info/unicode/category/Lt/list.htm)`”, “`[`Modifier` `letter` `(Lm)`](http://www.fileformat.info/info/unicode/category/Lm/list.htm)`”,`
`   “`[`Other` `letter` `(Lo)`](http://www.fileformat.info/info/unicode/category/Lo/list.htm)`”,or “`[`Letter` `number` `(Nl)`](http://www.fileformat.info/info/unicode/category/Nl/list.htm)`”.`

` `*<b id="UnicodeCombiningMark">`UnicodeCombiningMark`</b>*
`   any character in the Unicode categories “`[`Non-spacing` `mark` `(Mn)`](http://www.fileformat.info/info/unicode/category/Mn/list.htm)`”`
`   or “`[`Combining` `spacing` `mark` `(Mc)`](http://www.fileformat.info/info/unicode/category/Mc/list.htm)`”`

` `*<b id="UnicodeDigit">`UnicodeDigit`</b>*
`   any character in the Unicode category “`[`Decimal` `number` `(Nd)`](http://www.fileformat.info/info/unicode/category/Nd/list.htm)`”`

` `*<b id="UnicodeConnectorPunctuation">`UnicodeConnectorPunctuation`</b>*
`   any character in the Unicode category “`[`Connector` `punctuation` `(Pc)`](http://www.fileformat.info/info/unicode/category/Pc/list.htm)`”`

### 保留字

保留字不能作为 ** 的 **。

语法

` `*<b id="ReservedWord">`ReservedWord`</b>*` ::`
`   `**
`   `**
`   `**
`   `**

#### 关键词

下列 [Token](#x7.5 "wikilink") 是 ECMAScript 的关键词，不能用作 ECMAScript 程序的 **。

语法

` `*<b id="Keyword">`Keyword`</b>*` :: `**`one` `of`**
`    `**`break`**`      `**`do`**`         `**`instanceof`**`        `**`typeof`**
`    `**`case`**`       `**`else`**`       `**`new`**`               `**`var`**
`    `**`catch`**`      `**`finally`**`    `**`return`**`            `**`void`**
`    `**`continue`**`   `**`for`**`        `**`switch`**`            `**`while`**
`    `**`debugger`**`   `**`function`**`   `**`this`**`              `**`with`**
`    `**`default`**`    `**`if`**`         `**`throw`**`             `**`delete`**
`    `**`in`**`         `**`try`**

#### 未来保留字

下列词被用作建议扩展关键字，因此保留，以便未来可能采用这些扩展。

语法

` `*<b id="FutureReservedWord">`FutureReservedWord`</b>*` :: `**`one` `of`**
`    `**`class`**`      `**`enum`**`       `**`extends`**`       `**`super`**
`    `**`const`**`      `**`export`**`     `**`import`**

当下列 [Token](#x7.5 "wikilink") 出现在[严格模式代码 (strict mode code )](ES5/execution#strict-mode-code "wikilink")（见 [10.1.1](ES5/execution#strict-mode-code "wikilink")）里，将被当成是 **。任意这些 [Token](#x7.5 "wikilink") 出现在任意上下文中的[严格模式代码中](ES5/execution#strict-mode-code "wikilink")，如果 ** 出现的位置会产生错误，那么必须抛出对应的异常：

` `**`implements`**`      `**`let`**`         `**`private`**`       `**`public`**`      `**`yield`**
` `**`interface`**`       `**`package`**`     `**`protected`**`     `**`static`**

标点符号
--------

语法

` `*<b id="Punctuator">`Punctuator`</b>*` :: `**`one` `of`**
`   `**`{`**`       `**`}`**`       `**`(`**`       `**`)`**`       `**`[`**`       `**`]`**
`   `**`.`**`       `**`;`**`       `**`,`**`       `**`<`**`       `**`>`**`       `**`<=`**
`   `**`>=`**`      `**`==`**`      `**`!=`**`      `**`===`**`     `**`!==`**
`   `**`+`**`       `**`-`**`       `**`*`**`       `**`%`**`       `**`++`**`      `**`--`**
`   `**`<<`**`      `**`>>`**`      `**`>>>`**`     `**`&`**`       `**`|`**`       `**`^`**
`   `**`!`**`       `**`~`**`       `**`&&`**`      `**`||`**`      `**`?`**`       `**`:`**
`   `**`=`**`       `**`+=`**`      `**`-=`**`      `**`*=`**`      `**`%=`**`      `**`<<=`**
`   `**`>>=`**`     `**`>>>=`**`    `**`&=`**`      `**`|=`**`      `**`^=`**

` `*<b id="DivPunctuator">`DivPunctuator`</b>*` :: `**`one` `of`**
`   `**`/`**`       `**`/=`**

字面量
------

语法

` `*<b id="Literal">`Literal`</b>*` ::`
`   `**
`   `**
`   `**
`   `**` `
`   `**

### 空值字面量

语法：

` `*<b id="NullLiteral">`NullLiteral`</b>*` ::`
`   `**`null`**

语义：

空值字面量的值 **null**，是 [Null类型](ES5/types#Null "wikilink") 的唯一值。

### 布尔值字面量

语法：

` `*<b id="BooleanLiteral">`BooleanLiteral`</b>*` ::`
`   `**`true`**
`   `**`false`**

语义：

布尔值字面量的值 **true** 是个 [Boolean类型](ES5/types#Boolean "wikilink") 值 ，即 **true**。 布尔值字面量的值 **false** 是个 [Boolean类型](ES5/types#Boolean "wikilink") 值 ，即 **false**。

### 数值字面量

语法：

` `*<b id="NumericLiteral">`NumericLiteral`</b>*` ::`
`   `**
`   `**

` `*<b id="DecimalLiteral">`DecimalLiteral`</b>*` ::`
`   `**` `**`.`**` `**` `**
`   `**`.`**` `**` `**
`   `**` `**

` `*<b id="DecimalIntegerLiteral">`DecimalIntegerLiteral`</b>*` ::`
`   `**`0`**
`   `**` `**

` `*<b id="DecimalDigits">`DecimalDigits`</b>*` ::`
`   `**
`   `**` `**

` `*<b id="DecimalDigit">`DecimalDigit`</b>*` :: `**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9`**

` `*<b id="NonZeroDigit">`NonZeroDigit`</b>*` :: `**`one` `of`**
`   `**`1` `2` `3` `4` `5` `6` `7` `8` `9`**

` `*<b id="ExponentPart">`ExponentPart`</b>*` ::`
`   `**` `**

` `*<b>`ExponentIndicator`</b>*` :: `**`one` `of`**
`   `**`e` `E`**

` `*<b id="SignedInteger">`SignedInteger`</b>*` ::`
`   `**
`   `**`+`**` `**
`   `**`-`**` `**

` `*<b id="HexIntegerLiteral">`HexIntegerLiteral`</b>*` ::`
`   `**`0x`**` `**
`   `**`0X`**` `**
`   `**` `**

` `*<b id="HexDigit">`HexDigit`</b>*` :: `**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9` `a` `b` `c` `d` `e` `f` `A` `B` `C` `D` `E` `F`**

源字符中的 ** 后面不允许紧跟着 ** 或 **。

语义：

一个数值字面量代表一个 [Number类型](ES5/types#Number "wikilink") 的值。此值取决于两个步骤：第一，由字面量得出的<b title="mathematical value（MV）">数学值</b>）；第二，这个数学值按照后面描述的规则舍入。

-   ** :: ** 的数学值是 ** 的数学值。

-   ** :: ** 的数学值是 ** 的数学值。

-   ** :: ** **.** 的数学值是 ** 的数学值。

-   ** :: ** **.** ** 的数学值是 ** 的数学值加上 (** 的数学值乘 **10**<sup>-<var>n</var></sup>), 这里的 <var>n</var> 是 ** 的字符个数。

-   ** :: ** **.** ** 的数学值是 ** 的数学值乘 **10**<sup><var>e</var></sup>, 这里的 <var>e</var> 是 ** 的数学值。

-   ** :: ** **.** ** ** 的数学值是 (** 的数学值加 (** 的数学值乘 **10**<sup>-<var>n</var></sup>)) 乘 **10**<sup><var>e</var></sup>, 这里的 <var>n</var> 是 ** 的字符个数，<var>e</var> 是 ** 的数学值。

-   ** :: **.** ** 的数学值是 ** 的数学值乘 **10**<sup>-<var>n</var></sup>, 这里的 <var>n</var> 是 ** 的字符个数。

-   ** :: **.** ** ** 的数学值是 ** 的数学值乘 **10**<sup><var>e</var>-<var>n</var></sup>, 这里的 <var>n</var> 是 ** 的字符个数，<var>e</var> 是 ** 的数学值。

-   ** :: ** 的数学值是 ** 的数学值。

-   ** :: ** ** 的数学值是 ** 的数学值乘 **10**<sup><var>e</var></sup>, 这里的 <var>e</var> 是 ** 的数学值。

-   ** :: **0** 的数学值是 **0**。

-   ** :: ** ** 的数学值是 (** 的数学值乘 **10**<sup><var>n</var></sup>) 加 ** 的数学值, 这里的 <var>n</var> 是 ** 的字符个数。

-   ** :: ** 的数学值是 ** 的数学值。

-   ** :: ** ** 的数学值是 (** 的数学值乘 **10**) 加 ** 的数学值。

-   ** :: ExponentIndicator ** 的数学值是 ** 的数学值。

-   ** :: ** 的数学值是 ** 的数学值。

-   ** :: **+** ** 的数学值是 ** 的数学值。

-   ** :: **-** ** 的数学值是 ** 的数学值取负。

-   ** :: **0** 或 ** :: **0** 的数学值是 **0**。

-   ** :: **1** 或 ** :: **1** 或 ** :: **1** 的数学值是 **1**。

-   ** :: **2** 或 ** :: **2** 或 ** :: **2** 的数学值是 **2**。

-   ** :: **3** 或 ** :: **3** 或 ** :: **3** 的数学值是 **3**。

-   ** :: **4** 或 ** :: **4** 或 ** :: **4** 的数学值是 **4**。

-   ** :: **5** 或 ** :: **5** 或 ** :: **5** 的数学值是 **5**。

-   ** :: **6** 或 ** :: **6** 或 ** :: **6** 的数学值是 **6**。

-   ** :: **7** 或 ** :: **7** 或 ** :: **7** 的数学值是 **7**。

-   ** :: **8** 或 ** :: **8** 或 ** :: **8** 的数学值是 **8**。

-   ** :: **9** 或 ** :: **9** 或 ** :: **9** 的数学值是 **9**。

-   ** :: **a** 或 ** :: **A** 的数学值是 **10**。

-   ** :: **b** 或 ** :: **B** 的数学值是 **11**。

-   ** :: **c** 或 ** :: **C** 的数学值是 **12**。

-   ** :: **d** 或 ** :: **D** 的数学值是 **13**。

-   ** :: **e** 或 ** :: **E** 的数学值是 **14**。

-   ** :: **f** 或 ** :: **F** 的数学值是 **15**。

-   ** :: **0x** ** 的数学值是 ** 的数学值。

-   ** :: **0X** ** 的数学值是 ** 的数学值。

-   ** :: ** ** 的数学值是 (** 的数学值乘 **16**) 加 ** 的数学值。

数值字面量的确切数学值一旦被确定，它就会舍入成 [Number类型](ES5/types#Number "wikilink") 的值。如果数学值是 **0**，那么舍入值是 **+0**；否则，舍入值必须是数学值对应的[数字值](ES5/types#Number "wikilink")，除非此字面量是<b title="significant digit">有效数字</b>超过20位的 **，这种情况下，数字值的产生方式可以是下面两种方式中的一种：一，将20位后的每个<b title="significant digit">有效数字</b>用 **0** 替换后产生的数学值；二，将20位后的每个<b title="significant digit">有效数字</b>用 **0** 替换，并且递增第20位<b title="significant digit">有效数字</b>位置的字面量值所产生的数学值 。<b title="significant digit">有效数字</b>必须满足这么几个条件，首先它不能是 ** 的一部分，并且

-   它不是 **0**；或

-   它的左侧是非零数字，它的右侧是不在 ** 的非零数字。

符合标准的实现，在处理[严格模式代码时](ES5/execution#strict-mode-code "wikilink")，按照 [B.1.1](ES5/annexB#numeric-literals "wikilink") 的描述，不得扩展 ** 包含 *[OctalIntegerLiteral](ES5/annexB#OctalIntegerLiteral "wikilink")* 的语法。

### 字符串字面量

字符串字面量是在闭合的单引号或双引号中的零个或多个字符。每个字符都可以用一个转义序列代表。除了<b title="closing quote character">闭合用的引号字符</b>、<b title="backslash">反斜杠</b>、<b title="carriage return">回车符</b>、<b title="line separator">行分隔符</b>、<b title="paragraph separator">段落分隔符</b>、<b title="line feed">换行符</b>之外的所有字符都可以直接出现的字符串字面量里。任何字符都可以通过转移序列的形式出现。

语法

` `*<b id="StringLiteral">`StringLiteral`</b>*` ::`
`   `**`"`**` `**` `**`"`**
`   `**`'`**` `**` `**`'`**

` `*<b id="DoubleStringCharacters">`DoubleStringCharacters`</b>*` ::`
`   `**` `**

` `*<b id="SingleStringCharacters">`SingleStringCharacters`</b>*` ::`
`   `**` `**

` `*<b id="DoubleStringCharacter">`DoubleStringCharacter`</b>*` ::`
`   `*[`SourceCharacter`](ES5/source#SourceCharacter "wikilink")*` `**`but` `not` `"` `or` `\` `or`**` `**
`   `**`\`**` `**
`   `**

` `*<b id="SingleStringCharacter">`SingleStringCharacter`</b>*` ::`
`   `*[`SourceCharacter`](ES5/source#SourceCharacter "wikilink")*` `**`but` `not` `'` `or` `\` `or`**` `**
`   `**`\`**` `**
`   `**

` `*<b id="LineContinuation">`LineContinuation`</b>*` ::`
`   `**`\`**` `**

` `*<b id="EscapeSequence">`EscapeSequence`</b>*` ::`
`   `**
`   `**`0`**` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `**`]`
`   `**
`   `**

` `*<b id="CharacterEscapeSequence">`CharacterEscapeSequence`</b>*` ::`
`   `**
`   `**

` `*<b id="SingleEscapeCharacter">`SingleEscapeCharacter`</b>*` :: `**`one` `of`**
`   `**`'` `"` `\` `b` `f` `n` `r` `t` `v`**

` `*<b id="NonEscapeCharacter">`NonEscapeCharacter`</b>*` ::`
`   `*[`SourceCharacter`](ES5/source#SourceCharacter "wikilink")*` `**`but` `not`**` `**` `**`or`**` `**

` `*<b id="EscapeCharacter">`EscapeCharacter`</b>*` ::`
`   `**
`   `**
`   `**`x`**
`   `**`u`**

` `*<b id="HexEscapeSequence">`HexEscapeSequence`</b>*` ::`
`   `**`x`**` `**` `**

` `*<b id="UnicodeEscapeSequence">`UnicodeEscapeSequence`</b>*` ::`
`   `**`u`**` `**` `**` `**` `**

[7.8.3](#numeric-literals "wikilink") 给出了 ** 非终结符的定义。[第6章](ES5/source "wikilink") 定义了 *[SourceCharacter](ES5/source#SourceCharacter "wikilink")*。

语义

一个字符串字面量代表一个 [String类型](ES5/types#String "wikilink") 的值。字面量的<b title="String Value (SV)">字符串值</b>由字符串字面量各部分贡献的<b title="CharacterValue (CV)">字符值</b>描述。作为这一过程的一部分，字符字面量里的某些字符字符会被解释成包含<b title="Mathematical Value (MV)">数学值</b>，如 [7.8.3](#numeric-literals "wikilink") 和下面描述的。

-   ** :: **""** 的字符串值是空字符序列。

-   ** :: **''** 的字符串值是空字符序列。

-   ** :: **"** ** **"** 的字符串值是 ** 的字符串值。

-   ** :: **'** ** **'** 的字符串值是 ** 的字符串值。

-   ** :: ** 的字符串值是包含一个字符的序列，此字符的字符值是 ** 的字符值。

-   ** :: ** ** 的字符串值是 （** 的字符值后面跟着 ** 的字符串值里所有字符的）序列。

-   ** :: ** 的字符串值是包含一个字符的序列，此字符的字符值是 ** 的字符值。

-   ** :: ** ** 的字符串值是（** 的字符值后面跟着 ** 的字符串值里所有字符的）序列。

-   ** :: **\\** ** 的字符串值是空字符序列。

-   ** :: *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* **but not " or \\ or** ** 的字符值是 *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* 字符自身。

-   ** :: **\\** ** 的字符值是 ** 的字符值。

-   ** :: ** 的字符值是空字符序列。

-   ** :: *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* **but not ' or \\ or** **的字符值是 *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* 字符自身。

-   ** :: **\\** ** 的字符值是 ** 的字符值。

-   ** :: ** 的字符值是空字符序列。

-   ** :: ** 的字符值是 ** 的字符值。

-   ** :: **0** [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") **] 的字符值是 **<NUL>** 字符（Unicode 值 0000）。

-   ** :: ** 的字符值是 ** 的字符值。

-   ** :: ** 的字符值是 ** 的字符值。

-   ** :: ** 的字符值是 **表4** 里的 ** 确定的代码单元值字符：

|转义序列|代码单元值|名称|符号|
|--------|----------|----|----|
|\\b|\\u0008|<b title="backspace">退格符</b>|<BS>|
|\\t|\\u0009|<b title="horizontal tab">水平制表符</b>|<HT>|
|\\n|\\u000A|<b title="line feed (new line)">换行符</b>|<LF>|
|\\v|\\u000B|<b title="vertical tab">垂直制表符</b>|<VT>|
|\\f|\\u000C|<b title="form feed">换页符</b>|<FF>|
|\\r|\\u000D|<b title="carriage return">回车符</b>|<CR>|
|\\"|\\u0022|<b title="double quote">双引号</b>|"|
|\\'|\\u0027|<b title="single quote">单引号</b>|'|
|\\\\|\\u005C|<b title="backslash">反斜杠</b>|\\|

-   ** :: ** 的字符值是 ** 的字符值。

-   ** :: *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* **but not** ** **or** ** 的字符值是 *[SourceCharacter](ES5/source#SourceCharacter "wikilink")* 字符自身。

-   ** :: **x** ** ** 的字符值是 ((**16** 乘第一个 ** 的数学值) 加第二个 ** 的数学值) 代码单元确定的字符。

-   ** :: **u** ** ** ** ** 的字符值是 (**4096** 乘第一个 ** 的数学值) 加 (**256** 乘第二个 ** 的数学值) 加 (**16** 乘第三个 ** 的数学值) 加 ( 第四个 ** 的数学值) 代码单元确定的字符。

符合标准的实现，在处理[严格模式代码时](ES5/execution#strict-mode-code "wikilink")，按照 [B.1.2](ES5/annexB#string-literals "wikilink") 的描述，不得扩展 ** 包含 *[OctalEscapeSequence](ES5/annexB#OctalEscapeSequence "wikilink")* 的语法。

### 正则表达式字面量

正则表达式字面量是一个输入元素，它在每次被解析执行时候都会转换成一个 [RegExp对象](ES5/builtins#x15.10 "wikilink") 的。当程序中的两个正则表达式字面量解释执行为正则表达式对象后就不能用 **===** 来比较它们是否相等，即使它们所包含的内容相同。[RegExp对象](ES5/builtins#x15.10 "wikilink") 也可以在运行时使用 [new RegExp](ES5/builtins#x15.10.4 "wikilink") 或以函数方式调用 [RegExp](ES5/builtins#x15.10.3 "wikilink") 构造器来创建。

下面的产生式描述了正则表达式字面量的语法，输入元素扫描器还用它搜索正则表达式字面量的结束位置。** 和 ** 包含的字符组成的字符串会直接传递给正则表达式构造器，在那里用更严格文法进行解析。一个实现可以扩展正则表达式构造器的文法。但它不能扩展 ** 和 ** 产生式或使用这些产生式的产生式。

语法

` `*<b id="RegularExpressionLiteral ">`RegularExpressionLiteral`</b>*` ::`
`   `**`/`**` `**` `**`/`**` `**

` `*<b id="RegularExpressionBody">`RegularExpressionBody`</b>*` ::`
`   `**` `**

` ''`<b id="RegularExpressionChars">`RegularExpressionChars`</b>` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

` `*<b id="RegularExpressionFirstChar">`RegularExpressionFirstChar`</b>*` ::`
`   `**` `**`but` `not` `*` `or` `\` `or` `/` `or` `[`**
`   `**
`   `**

` `*<b id="RegularExpressionChar">`RegularExpressionChar`</b>*` ::`
`   `**` `**`but` `not` `\` `or` `/` `or` `[`**
`   `**
`   `**

` `*<b id="RegularExpressionBackslashSequence">`RegularExpressionBackslashSequence`</b>*` ::`
`   `**`\`**` `**

` `*<b id="RegularExpressionNonTerminator">`RegularExpressionNonTerminator`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not`**` `**

` `*<b id="RegularExpressionClass">`RegularExpressionClass`</b>*` ::`
`   `**`[`**` `**` `**`]`**

` `*<b id="RegularExpressionClassChars">`RegularExpressionClassChars`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

` `*<b id="RegularExpressionClassChar">`RegularExpressionClassChar`</b>*` ::`
`   `**` `**`but` `not` `]` `or` `\`**
`   `**

` `*<b id="RegularExpressionFlags">`RegularExpressionFlags`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

语义

正则表达式字面量会解释执行为一个 [Object类型](ES5/types#Object "wikilink") 值，它是标准内置构造器 [RegExp](ES5/builtins#x15.10 "wikilink") 的一个实例。此值取决于两个步骤：首先，展开组成正则表达式产生式 ** 和 ** 的字符，将其以未解析形式分别存成两个字符串 <var>Pattern</var> 和 <var>Flags</var>。然后，在每次解释执行字面量时创建新对象，仿佛使用 **new RegExp(**<var>Pattern</var>**,**<var>Flags</var>**)** 一样，这里的 [RegExp](ES5/builtins#x15.10 "wikilink") 是标准内置构造器名。新构造的对象将成为 ** 的值。如果调用 **new RegExp** 会产生 [15.10.4.1](ES5/builtins#x15.10.4.1 "wikilink") 指定的错误，那么必须把错误当作是早期错误 ( 见[第16章](ES5#x16 "wikilink"))。

自动分号插入
------------

必须用分号终止某些 ECMAScript 语句（[空语句](ES5/statements#x12.3 "wikilink")、[变量语句](ES5/statements#x12.2 "wikilink")、[表达式语句](ES5/statements#x12.4 "wikilink")、[**do-while** 语句](ES5/statements#x12.6.1 "wikilink")、[**continue** 语句](ES5/statements#x12.7 "wikilink")、[**break** 语句](ES5/statements#x12.8 "wikilink")、[**return** 语句](ES5/statements#x12.9 "wikilink")、[**throw** 语句](ES5/statements#x12.13 "wikilink")）。这些分号总是明确地显示在源文本里。然而，为了方便起见，某些情况下这些分号可以在源文本里省略。描述这种情况会说：这种情况下给源代码的 [Token](#Token "wikilink") 流自动插入分号。

### 自动分号插入规则

分号插入有三个基本规则：

1.  从左到右解析程序，当遇到一个不符合任何文法产生式的 [Token](#Token "wikilink")（叫做<b title="offending token">违规Token</b>），那么只要满足下面条件之一就在 **违规Token** 前面自动插入分号。
    -   至少一个 *[LineTerminator](#LineTerminator "wikilink")* 分割了 **违规Token** 和前一个 [Token](#Token "wikilink")。
    -   **违规Token** 是 **}**。

2.  从左到右解析程序，[Token](#Token "wikilink") 输入流已经结束，当解析器无法将输入 [Token](#Token "wikilink") 流解析成单个完整 ECMAScript *[Program](ES5/program#Program "wikilink")*，那么就在输入流的结束位置自动插入分号。
3.  从左到右解析程序，遇到一个某些文法产生式允许的 [Token](#Token "wikilink")，但是此产生式是受限产生式，受限产生式的里紧跟在 [[no *LineTerminator* here](ES5/notation#restricted-production "wikilink")] 后的第一个终结符或非终结符的 [Token](#Token "wikilink") 叫做受限的 [Token](#Token "wikilink")，当至少一个 *[LineTerminator](#LineTerminator "wikilink")* 分割了受限的 [Token](#Token "wikilink") 和前一个 [Token](#Token "wikilink")，那么就在受限 [Token](#Token "wikilink") 前面自动插入分号。

然而，上述规则有一个附加的优先条件：如果插入分号后解析结果是[空语句](ES5/statements#x12.3 "wikilink")，或如果插入分号后它成为 [**for** 语句](ES5/statements#x12.6.3 "wikilink") 头部的两个分号之一，那么不会自动插入分号。

` `***[`PostfixExpression`](ES5/expressions#PostfixExpression "wikilink")***` :`
`   `*[`LeftHandSideExpression`](ES5/expressions#LeftHandSideExpression "wikilink")*` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`++`**` `
`   `*[`LeftHandSideExpression`](ES5/expressions#LeftHandSideExpression "wikilink")*` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`--`**

` `***[`ContinueStatement`](ES5/statements#ContinueStatement "wikilink")***` :`
`   `**`continue`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Identifier`](#Identifier "wikilink")*` `**`;`**

` `***[`BreakStatement`](ES5/statements#BreakStatement "wikilink")***` :`
`   `**`break`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Identifier`](#Identifier "wikilink")*` `**`;`**

` `***[`ReturnStatement`](ES5/statements#ReturnStatement "wikilink")***` :`
`   `**`return`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**

` `***[`ThrowStatement`](ES5/statements#ThrowStatement "wikilink")***` :`
`   `**`throw`**` `[`[no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `*[`Expression`](ES5/expressions#Expression "wikilink")*` `**`;`**

这些受限产生式的实际效果如下：

当遇到一个被解析器作为[后缀运算符来对待的](ES5/expressions#x11.3 "wikilink") **++** 或 **--**，并且在 **++** 或 **--** 与其前面的 [Token](#Token "wikilink") 之间出现至少一个 **，这时分号会被自动插入到 **++** 或 **--** 的前面。

当遇到 **continue**、**break**、**return**、**throw** 这些 [Token](#Token "wikilink")，并且在下一个 [Token](#Token "wikilink") 前面遇到 ** 时，在 **continue**、**break**、**return**、**throw** 后面自动插入一个分号。

这对 ECMAScript 程序员的实际影响是：

[后缀运算符](ES5/expressions#x11.3 "wikilink") **++** 或 **--** 和它的操作数应该出现在同一行。

[**return** 语句](ES5/statements#x12.9 "wikilink") 或 [**throw** 语句](ES5/statements#x12.13 "wikilink") 的 *[Expression](ES5/expressions#Expression "wikilink")* 开始位置应该和 **return** 或 **throw** 这些 [Token](#Token "wikilink") 本身处于同一行。

[**break** 语句](ES5/statements#x12.8 "wikilink") 或 [**continue** 语句](ES5/statements#x12.7 "wikilink") 的 *[Identifier](#Identifier "wikilink")* 应该和 **break** 或 **continue** 这些 [Token](#Token "wikilink") 本身处于同一行。

### 自动分号插入的例子

源代码：

` { 1 2 } 3`

即使在自动分号插入规则下，它也不符合 ECMAScript 文法。做为对比，源代码：

` { 1`
` 2 } 3`

它还是不符合 ECMAScript 文法，但是它会被自动分号插入成为一下形式：

` { 1`
` ;2 ;} 3;`

这符合 ECMAScript 文法。

源代码：

` for (a; b`
` )`

不符合 ECMAScript 文法，并且不会被自动分号插入所更改，因为是 [**for** 语句](ES5/statements#x12.6.3 "wikilink") 头部需要分号。自动分号插入永远不会插入成 [**for** 语句](ES5/statements#x12.6.3 "wikilink") 头部的两个分号之一。

源代码：

` return`
` a + b`

会被自动分号插入转换成以下形式：

` return;`
` a + b;`

源代码：

` a = b`
` ++c`

会被自动分号插入转换成以下形式：

` a = b;`
` ++c;`

源代码：

` if (a > b)`
` else c = d`

它不符合 ECMAScript 文法，**else** 这个 [Token](#Token "wikilink") 前不会被自动插入分号，即使没有文法产生式适用这一位置，因为自动插入分号不该解析成[空语句](ES5/statements#x12.3 "wikilink")。

源代码：

` a = b + c`
` (d + e).print()`

它不会被自动分号插入改变，因为第二行开始位置的括号表达式可以解释成函数调用的参数列表：

` a = b + c(d + e).print()`

在赋值语句必须用左括号开头的情况下，程序员在前面语句的结束位置明确地提供一个分号是个好主意，而不是依赖于自动分号插入。

