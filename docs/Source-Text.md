ECMAScript源代码文本使用Unicode 3.0或更高版本的字符编码的字符序列来表示。该文本预期已经<b title="Normalised">正规化</b>为[Unicode Technical Report \#15](http://www.unicode.org/reports/tr15/)中所描述的Unicode<b title="Normalization Form">正规形式</b>C（<b title="canonical composition">标准等价重组</b>）。符合ECMAScript的实现不要求对文本执行正规化，也不要求将其表现为像执行了正规化一样。本规范假定ECMAScript源代码文本都是由16位代码单元组成的序列。像这样包含16位代码单元序列的源代码文本可能不是有效的UTF-16字符编码。如果实际源代码文本没有使用16位代码单元形式的编码，那就必须将其转换为UTF-16来处理。

语法：

` `*<b id="SourceCharacter">`SourceCharacter`</b>*` ::`<br/>
`   any Unicode code unit`

贯穿本文档的短语“<b title="code unit" id="code-unit">代码单元</b>”和单词“<b title="character" id="character">字符</b>”特指用来表示文本的单个16位单元的16位无符号值。短语“<b title="Unicode character" id="unicode-character">Unicode字符</b>”特指单个Unicode标量值（该值可能大于16位，因此可用来表示多个代码单位）所表示的语言或排版上的抽象单位。短语“<b title="code point" id="code-point">代码点</b>”就是这样一个Unicode标量值。“[Unicode字符](#unicode-character "wikilink")”仅指由单一的Unicode标量值所表示的实体：组合字符序列的每个组成部分都是单个“[Unicode字符](#unicode-character "wikilink")”，尽管用户可能会认为整个序列是单个字符。

在[字符串字面量](ES5/lexical#x7.8.4 "wikilink")、[正则表达式字面量](ES5/lexical#x7.8.5 "wikilink")、[标识符](ES5/lexical#x7.6 "wikilink")中，任意字符（[代码单元](#code-unit "wikilink")）都可以是由六个字符组成的Unicode转义序列，即`\u`加上四个16进制数字。在注释中，像这样的转义序列会被当作注释的一部分而忽略掉。在[字符串字面量](ES5/lexical#x7.8.4 "wikilink")或[正则表达式字面量](ES5/lexical#x7.8.5 "wikilink")中，Unicode转义序列会给该字面量的值贡献一个字符。在[标识符](ES5/lexical#x7.6 "wikilink")中，转义序列给[标识符](ES5/lexical#x7.6 "wikilink")贡献一个字符。

注：虽然本文档有时会提到“<b title="string">字符串</b>”中的“<b title="character">字符</b>”和代表字符代码单元的16位无符号整数之间的“<b title="transformation">变换</b>”。事实上并没有变换，因为实际上就是用16位无符号值来表示“<b title="string">字符串</b>”中的“<b title="character">字符</b>”。

ECMAScript与Java编程语言对Unicode转义序列有不同的解释。在Java程序中，如果Unicode转义序列`\u000A`出现在单行注释中，它会被解释成行终止符(Unicode字符`000A`是换行)，因此该行后续的字符不是注释的一部分。类似地，如果Java程序中的字符串字面量里出现Unicode转义序列`\u000A`，它同样会被解释成行终止符，而字符串字面量里不允许出现行终止符，所以必须将作为字符串字面量字符值的换行符的`\u000A`替换成`\n`。在ECMAScript程序中，始终不会解释注释里出现的Unicode转义序列，因此无法给注释贡献终止符。类似地，如果ECMAScript程序中的[字符串字面量](ES5/lexical#x7.8.4 "wikilink")中出现Unicode转义序列，它始终会给该字面量值贡献一个字符，并且始终不会被解释成有可能终止[字符串字面量](ES5/lexical#x7.8.4 "wikilink")的[行终止符](ES5/lexical#line-terminator "wikilink")或者引号标记。
