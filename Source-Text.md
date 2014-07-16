ECMAScript 源代码文本使用 Unicode 3.0 或更高版本的字符编码的字符序列来表示。该文本预期已经<b title="Normalised">正规化</b>为 [Unicode Technical Report \#15](http://www.unicode.org/reports/tr15/) 中描述的 Unicode <b title="Normalization Form">正规形式</b> C (<b title="canonical composition">标准等价重组</b>) 。符合 ECMAScript 的实现不要求对文本执行正规化，也不要求将其表现为像执行了正规化一样。本规范的目的是假定 ECMAScript 源代码文本都是由16位代码单元组成的序列。像这样包含16位代码单元序列的源文本可能不是有效的的 UTF-16 字符编码。如果实际源代码文本没有用16位代码单元形式的编码，那就必须把它看作已经转换为 UTF-16 一样处理。

` `*<b id="SourceCharacter">`SourceCharacter`</b>*` ::`
`   any Unicode code unit`

贯穿本文档的短语“<b title="code unit" id="code-unit">代码单元</b>”和单词“<b title="character" id="character">字符</b>”特指表示文本的单个16位单元的16位无符号值。短语“<b title="Unicode character" id="unicode-character">Unicode 字符</b>”特指单个 Unicode 标量值（这可能大于16位，因此它可能代表多个代码单位）表示的语言或排版上的抽象单位。短语“<b title="code point" id="code-point">代码点</b>”是指这样一个 Unicode 标量值。“[Unicode 字符](#unicode-character "wikilink")”仅指由单一的 Unicode 标量值表示的实体：组合字符序列的每个组成部分都是单个“[Unicode 字符](#unicode-character "wikilink")”，尽管用户可能会认为整个序列是单个字符。

在[字符串字面量](ES5/lexical#x7.8.4 "wikilink")、[正则表达式字面量](ES5/lexical#x7.8.5 "wikilink")、[标识符中的任意字符](ES5/lexical#x7.6 "wikilink")（[代码单元](#code-unit "wikilink")），可以是由六个字符组成的 Unicode 转义序列，即 **\\u** 加上四个16进制数字。在注释中，这样的转义序列被当作注释的一部分忽略掉。在[字符串字面量或](ES5/lexical#x7.8.4 "wikilink")[正则表达式字面量](ES5/lexical#x7.8.5 "wikilink")，Unicode 转义序列会给字面量值贡献一个字符。在[标识符中](ES5/lexical#x7.6 "wikilink")，转义序列给[标识符贡献一个字符](ES5/lexical#x7.6 "wikilink")。

ECMAScript 与 Java 编程语言对 Unicode 转义序列有不同的解释。在 Java 程序中，如果 Unicode 转义序列 **\\u000A** 出现在单行注释中，它会被解释成行终止符 ([Unicode 字符](#unicode-character "wikilink") **000A** 是换行)，因此接下来的一个字符不是注释的一部分。与此类似，如果 Java 程序中的字符串字面量里出现 Unicode 转义序列 **\\u000A**，它同样会被解释成行终止符，字符串字面量里不允许出现行终止符，不得不将作为字符串字面量字符值的换行符的 **\\u000A** 替换成 **\\n**。在 ECMAScript 程序中，始终不会解释注释里出现的 Unicode 转义序列，因此无法给注释贡献终止符。与此类似，如果 ECMAScript 程序中的[字符串字面量里出现](ES5/lexical#x7.8.4 "wikilink") Unicode 转义序列，它始终会贡献一个字符给字面量值，并且始终不会解释成有可能终止[字符串字面量的](ES5/lexical#x7.8.4 "wikilink")[行终止符或引号标记](ES5/lexical#line-terminator "wikilink")。

