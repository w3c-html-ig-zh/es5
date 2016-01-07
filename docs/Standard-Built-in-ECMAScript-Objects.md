ECMAScript 代码运行时会有一些可用的内置对象。一是作为执行程序[词法环境的一部分的](ES5/execution#lexical-environment "wikilink")[全局对象](#the-global-object "wikilink")。其他的可通过全局对象的初始属性访问。

除非另外指明，如果内置对象拥有 [[[Call]]](ES5/types#Call "wikilink") 内部属性，那么它的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 "**Function**"，如果没有 [[[Call]]](ES5/types#Call "wikilink") 内部属性，那么它的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 "**Object**"。除非另外指明，内置对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性的初始值是 **true**。

许多内置对象是函数：它们可以通过参数调用。其中有些还作为构造器：这些函数可被 **new** 运算符调用。对于每个内置函数，本规范描述了这些函数的必须参数和作为函数对象的属性。对于每个内置构造器，本规范还描述了这些构造器原型对象的属性，还描述了用 **new** 表达式调用这个构造器后返回的具体实例对象的属性。

除非另外指明了某一特定函数的描述，如果在调用本章中描述的函数或构造器时传入的参数少于必须的参数个数，那么这些函数或构造器将表现为仿佛传入了足够的参数，而那些缺少的参数会设定为 **undefined** 值。

除非另外指明了某一特定函数的描述，如果在调用本章中描述的函数或构造器时传入了比函数指定允许的更多的参数时，额外的参数会被函数忽略。然而，一个实现可以为这样的参数列表定义依赖于实现的特别行为，只要这种行为在单纯添加额外参数时不抛出 **TypeError** 异常。

所有内置函数和内置构造器都有作为其 [[[Prototype]]](ES5/types#Prototype "wikilink") 内置属性值的 **Function** 原型对象，它的初始值是 [Function.prototype](#x15.3.4 "wikilink") 表达式的值。

除非另外指定，每一个内置原型对象都有作为其 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的 **Object** 原型对象，它的初始值是表达式 [Object.prototype](#x15.2.4 "wikilink") 的值，Object 自己的原型对象例外。

除非另外指明了特定函数的描述，否则本章描述的内置函数中不存在不是构造器而要实现 [[[Construct]]](ES5/types#Construct "wikilink") 内部方法的内置函数。除非另外指明了特定函数的描述，否则本章描述的内置函数都没有 **prototype** 属性。

本章通常描述构造器的 “作为函数调用” 和 “用 **new** 表达式调用” 有不同行为。“作为函数调用” 的行为对应于调用构造器的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，“用 **new** 表达式调用”的行为对应于调用构造器的 [[[Construct]]](ES5/types#Construct "wikilink") 内部方法。

本章描述的每个内置 Function 对象，无论是构造器还是普通函数甚至二者都是，他们都拥有一个 **length** 属性，其值是个整数。除非另外指明，此值等于显示在函数描述的子章节标题的形式参数的个数，包括可选参数。

任何情况下，本章描述的内置函数对象的 **length** 属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。除非另外指明，本章描述的所有其他属性拥有特性 { [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **true** }。

全局对象
--------

唯一的全局对象在控制进入任何[执行环境前被创建](ES5/execution#execution-contexts "wikilink")。

除非另外指明，全局对象的标准内置属性拥有特性 {[[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **true**}。

全局对象没有 [[[Construct]]](ES5/types#Construct "wikilink") 内部属性 ; 全局对象不可能当做构造器用 **new** 运算符调用。

全局对象没有 [[[Call]]](ES5/types#Call "wikilink") 内部属性，全局对象不可能当做函数来调用。

全局对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 和 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是依赖于实现的。

除了本规范定义的属性之外，全局对象还可以拥有额外的宿主定义的属性。全局对象可包含一个值是全局对象自身的属性；例如，在 HTML 文档对象模型中全局对象的 **window** 属性是全局对象自身。

### 全局对象的值属性

#### NaN

**NaN** 的值是 **NaN**（见 [8.5](ES5/types#x8.5 "wikilink")）。这个属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Infinity

**Infinity** 的值是 **+∞**（见 [8.5](ES5/types#x8.5 "wikilink")）。这个属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### undefined

**undefined** 的值是 **undefined**（见 [8.1](ES5/types#x8.1 "wikilink")）。这个属性拥有特性 \<{ [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### 全局对象的函数属性

#### eval (x)

当用一个参数 <var>x</var> 调用 **eval** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 不是 **String**，返回 <var>x</var>。
2.  令 <var>prog</var> 为 ECMAScript 代码，它是将 <var>x</var> 作为一个程序解析的结果。如果解析失败，抛出一个 **SyntaxError** 异常 ( 见 [16 章](ES5#x16 "wikilink") )。
3.  令 <var>evalCtx</var> 为给 **eval** 代码 <var>prog</var> 建立的新执行环境 ([10.4.2](ES5/execution#x10.4.2 "wikilink"))。
4.  令 <var>result</var> 为解释执行程序 <var>prog</var> 的结果。
5.  退出执行环境 <var>evalCtx</var>，恢复到之前的执行环境。
6.  如果 <var>result</var>.**type** 是 **normal** 并且其完结类型值是 <var>V</var>，则返回 <var>V</var> 值。
7.  如果 <var>result</var>.**type** 是 **normal** 并且其完结类型值是 **empty**，则返回 **undefined** 值。
8.  否则，<var>result</var>.**type** 必定是 **throw**。将 <var>result</var>.**value** 作为异常抛出。

##### 直接调用 Eval

一个 **eval** 函数的直接调用是表示为符合以下两个条件的 [CallExpression](ES5/expressions#CallExpression "wikilink")：

解释执行 [CallExpression](ES5/expressions#CallExpression "wikilink") 中的 [MemberExpression](ES5/expressions#MemberExpression "wikilink") 的结果是个[引用](ES5/types#x8.7 "wikilink")，这个引用拥有一个[环境记录项作为其基值](ES5/execution#x10.2.1 "wikilink")，并且这个引用的名称是 **"eval"**。

以这个[引用作为参数调用](ES5/types#x8.7 "wikilink") [GetValue](ES5/types#GetValue "wikilink") 抽象操作的结果是 [15.1.2.1](#x15.1.2.1 "wikilink") 定义的标准内置函数。

#### parseInt (string, radix)

**parseInt** 函数产生一个根据 <var>radix</var> 来解释 <var>string</var> 得到的整数值。 <var>string</var> 开头的空白会被忽略。如果 <var>radix</var> 是 **undefined** 或 **0**，则将 <var>radix</var> 当作 **10** 处理 ，除非数字是以字符对 **0x** 或 **0X** 开头，在这种情形下将 <var>radix</var> 当作是 **16**。如果传入的 <var>radix</var> 参数直接就是 **16**，那么在数字前面加上 **0x** 或 **0X** 也无妨。

当调用 **parseInt** 函数时，采用以下步骤：

1.  令 <var>inputString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>string</var>)。
2.  令 <var>S</var> 为一个新创建的子字符串，它由 <var>inputString</var> 的第一个非 [StrWhiteSpaceChar](ES5/conversion#x9.3.1 "wikilink") 字符和它后面跟着的所有字符组成。( 换句话说，删掉前面的空白。) 如果 <var>inputString</var> 不包含任何这样的字符，则令 <var>S</var> 为空字符串。
3.  令 <var>sign</var> 为 **1**。
4.  如果 <var>S</var> 不为空并且 <var>S</var> 的第一个字符是减号 **-**，则令 <var>sign</var> 为 **?1**。
5.  如果 <var>S</var> 不是空并且 <var>S</var> 的第一个字符加号 **+** 或减号 **-**，则删除 S 的第一个字符。
6.  令 <var>R</var> = [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>radix</var>)。
7.  令 <var>stripPrefix</var> 为 **true**。
8.  如果 <var>R</var> ≠ **0**，则
    1.  如果 <var>R</var> \< **2** 或 <var>R</var> \> **36**，则返回 **NaN**。
    2.  如果 <var>R</var> ≠ **16**，令 <var>stripPrefix</var> 为 **false**。

9.  否则，<var>R</var> = **0**
    1.  令 <var>R</var> = **10**。

10. 如果 <var>stripPrefix</var> 是 **true**，则
    1.  如果 <var>S</var> 长度大于 **2** 并且 <var>S</var> 的头两个字符是 “**0x**” 或 “**0X**”，则删除 <var>S</var> 的头两个字符并且令 <var>R</var> = **16**。

11. 如果 <var>S</var> 包含任何不是 **<var>R</var>进制** 数位的字符 ，则令 <var>Z</var> 为 <var>S</var> 中这样的字符之前的所有字符组成的子字符串；否则令 <var>Z</var> 为 <var>S</var> 。
12. 如果 <var>Z</var> 是空，返回 **NaN**。
13. 令 <var>mathInt</var> 为 <var>Z</var> 的 **<var>R</var>进制** 表示的数学值，用字母 **A-Z** 和 **a-z** 来表示 **10** 到 **35** 之间的值。( 但如果 <var>R</var> 是 **10** 并且 <var>Z</var> 包含多余 **20** 位的值，可以替换 **20** 位后的每个数字为 **0**，这是实现可选的功能；如果 <var>R</var> 不是 **2**、**4**、**8**、**10**、**16**、**32**，则 <var>mathInt</var> 可以是 <var>Z</var> 的 **<var>R</var>进制** 表示的依赖于实现的近似值。)
14. 令 <var>number</var> 为 <var>mathInt</var> 的 **Number** 值。
15. 返回 <var>sign</var> × <var>number</var>。

#### parseFloat (string)

**parseFloat** 函数根据 <var>string</var> 参数的内容解释为十进制字面量的结果来决定，产生一个数值。

当调用 **parseFloat** 函数，采用以下步骤：

1.  令 <var>inputString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>string</var>)。
2.  令 <var>trimmedString</var> 为一个新创建的子字符串，它由 <var>inputString</var> 的非 [StrWhiteSpaceChar](ES5/conversion#x9.3.1 "wikilink") 字符的最左边字符和它右边跟着的所有字符组成。( 换句话说，删掉前面的空白。) 如果 <var>inputString</var> 不包含任何这样的字符，则令 <var>trimmedString</var> 为空字符串。
3.  如果 <var>trimmedString</var> 或 <var>trimmedString</var> 的任何前缀都不满足 [StrDecimalLiteral](ES5/conversion#ToNumber-StringNumericLiteral "wikilink") 的语法，返回 **NaN**。
4.  令 <var>numberString</var> 为满足 [StrDecimalLiteral](ES5/conversion#ToNumber-StringNumericLiteral "wikilink") 语法的 <var>trimmedString</var> 的最长前缀，可能是 <var>numberString</var> 自身。
5.  返回 <var>numberString</var> 数学值的 **Number** 值。

#### isNaN (number)

如果指定参数为 **NaN**，则返回 **true**，否则返回 **false**。

1.  如果 [ToString](ES5/conversion#ToString "wikilink")(number) 是 **NaN**，返回 **true**。
2.  否则 ，返回 **false**。

#### isFinite (number)

如果指定参数为 **NaN** 或 **+∞**或**?∞**，则返回 **false**，否则返回 **true**。

1.  如果 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>number</var>) 是 **NaN** 或 **+∞** 或 **?∞**，返回 **false**。
2.  否则，返回 **true**。

### 处理 URI 的函数属性

统一资源标识符，或叫做 URI，是用来标识互联网上的资源（例如，网页或文件）和怎样访问这些资源的传输协议（例如，HTTP 或 FTP）的字符串。除了 [15.1.3.1](#x15.1.3.1 "wikilink"), [15.1.3.2](#x15.1.3.2 "wikilink"), [15.1.3.3](#x15.1.3.3 "wikilink")，[15.1.3.4](#x15.1.3.4 "wikilink") 说明的用来编码和解码 URI 的函数之外 ECMAScript 语言自身不提供任何使用 URL 的支持。

一个 URI 是由组件分隔符分割的组件序列组成。其一般形式是：

*Scheme* : *First* / *Second* ; *Third* ? *Fourth*

其中斜体的名字代表组件；“:”, “/”, “;”，“?”是当作分隔符的保留字符。[encodeURI](#encodeURI "wikilink") 和 [decodeURI](#decodeURI "wikilink") 函数操作的是完整的 URI；这俩函数假定 URI 中的任何保留字符都有特殊意义，所有不会编码它们。[encodeURIComponent](#encodeURIComponent "wikilink") 和 [decodeURIComponent](#decodeURIComponent "wikilink") 函数操作的是组成 URI 的个别组件；这俩函数假定任何保留字符都代表普通文本，所以必须编码它们，所以它们出现在组成一个完整 URI 的组件里面时不会解释成保留字符了。

以下词法文法指定了编码后 URI 的形式。

` `<b id="uri">`uri`</b>` :::`
`   `**<sub>`opt`</sub>

` `<b id="uriCharacters">`uriCharacters`</b>` :::`
`   `**` `**<sub>`opt`</sub>

` `<b id="uriCharacter">`uriCharacter`</b>` :::`
`   `**
`   `**
`   `**

` `<b id="uriReserved">`uriReserved`</b>` ::: `**`one` `of`**
`   `**`;` `/` `?` `:` `@` `&` `=` `+` `$` `,`**

` `<b id="uriUnescaped">`uriUnescaped`</b>` :::`
`   `**
`   `*[`DecimalDigit`](ES5/lexical#DecimalDigit "wikilink")*
`   `**

` `<b id="uriEscaped">`uriEscaped`</b>` :::`
`   `**`%`**` `[`HexDigit`](ES5/lexical#HexDigit "wikilink")` `[`HexDigit`](ES5/lexical#HexDigit "wikilink")

` `<b id="uriAlpha">`uriAlpha`</b>` ::: `**`one` `of`**
`   '''a b c d e f g h i j k l m n o p q r s t u v w x y z`
`   A B C D E F G H I J K L M N O P Q R S T U V W X Y Z'''`

` `<b id="uriMark">`uriMark`</b>` ::: `**`one` `of`**
`   `**`-` `_` `.` `!` `~` `*` `'` `(` `)`**

当 URI 里包含一个没在上面列出的字符或有时不想让给定的保留字符有特殊意义，那么必须编码这个字符。字符被转换成 UTF-8 编码，首先从 UT??F-16 转换成相应的代码点值的替代。（注：对于 [0,127] 范围的代码单元，转换到单字节时它们的值是相同的。）然后返回的字节序列转换为一个字符串，每个字节用一个“%xx”形式的转移序列表示。

描述编码和转义过程的抽象操作 **Encode** 需要两个字符串参数 <var>string</var> 和 <var>unescapedSet</var>。

1.  令 <var>strLen</var> 为 <var>string</var> 的字符个数。
2.  令 <var>R</var> 为空字符串。
3.  令 <var>k</var> 为 **0**。
4.  重复
    1.  如果 <var>k</var> 等于 <var>strLen</var>，返回 <var>R</var>。
    2.  令 <var>C</var> 为 <var>string</var> 中位置为 <var>k</var> 的字符。
    3.  如果 <var>C</var> 在 <var>unescapedSet</var> 里，则
        1.  令 <var>S</var> 为一个只包含字符 <var>C</var> 的字符串。
        2.  令 <var>R</var> 为之前 <var>R</var> 的值和 <var>S</var> 连接得到的一个新字符串值。

    4.  否则，<var>C</var> 不在 <var>unescapedSet</var> 里
        1.  如果 <var>C</var> 的代码单元值不小于 **0xDC00** 并且不大于 **0xDFFF**，则抛出一个 **URIError** 异常。
        2.  如果 <var>C</var> 的代码单元值小于 **0xD800** 或大于 **0xDBFF**，则
            1.  令 <var>V</var> 为 <var>C</var> 的代码单元值。

        3.  否则
            1.  <var>k</var> 递增 **1**。
            2.  如果 <var>k</var> 等于 <var>strLen</var>，抛出一个 **URIError** 异常。
            3.  令 <var>kChar</var> 为 <var>string</var> 的 <var>k</var> 位置的字符的代码单元值。
            4.  如果 <var>kChar</var> 小于 **0xDC00** 或大于 **0xDFFF**，则抛出一个 **URIError** 异常。
            5.  令 <var>V</var> 为 (((<var>C</var>的代码单元值 ) – **0xD800**) \* **0x400** + (<var>kChar</var> – **0xDC00**) + **0x10000**)。

        4.  令 <var>Octets</var> 为 <var>V</var> 执行 UTF-8 转换的结果字节数组，令 <var>L</var> 为这个字节数组的长度。
        5.  令 <var>j</var> 为 **0**。
        6.  只要 <var>j</var> \< <var>L</var>，就重复
            1.  令 <var>jOctet</var> 为 <var>Octets</var> 的 <var>j</var> 位置的值。
            2.  令 <var>S</var> 为一个包含三个字符“%<var>XY</var>”的字符串，这里 <var>XY</var> 是编码 <var>jOctet</var> 值的两个大写16进制数字。
            3.  令 <var>R</var> 为之前 <var>R</var> 的值和 <var>S</var> 连接得到的一个新字符串值。
            4.  <var>j</var> 递增 **1**。

    5.  <var>k</var> 递增 **1**。

描述反转义和解码过程的抽象操作 **Decode** 需要两个字符串参数 <var>string</var> 和 <var>reservedSet</var>。

1.  令 <var>strLen</var> 为 <var>string</var> 的字符个数。
2.  令 <var>R</var> 为空字符串。
3.  令 <var>k</var> 为 **0**。
4.  重复
    1.  如果 <var>k</var> 等于 <var>strLen</var>，返回 <var>R</var>。
    2.  令 <var>C</var> 为 <var>string</var> 的 <var>k</var> 位置的字符。
    3.  如果 <var>C</var> 不是‘**%**’，则
        1.  令 <var>S</var> 为只包含字符 <var>C</var> 的字符串。

    4.  否则，<var>C</var> 是‘**%**’
        1.  令 <var>start</var> 为 <var>k</var>。
        2.  如果 <var>k</var> + **2** 大于或等于 <var>strLen</var>，抛出一个 **URIError** 异常。
        3.  如果 <var>string</var> 的 (<var>k</var> + **1**) 和 (<var>k</var> + **2**) 位置的字符没有表示为16进制数字，则抛出一个 **URIError** 异常。
        4.  令 <var>B</var> 为 (<var>k</var> + **1**) 和 (<var>k</var> + **2**) 位置的两个16进制数字表示的8位值。
        5.  <var>k</var> 递增 **2**.
        6.  如果 <var>B</var> 的最高有效位是 **0**，则
            1.  令 <var>C</var> 为代码单元值是 <var>B</var> 的字符。
            2.  如果 <var>C</var> 不在 <var>reservedSet</var> 里，则
                1.  令 <var>S</var> 为只包含字符 <var>C</var> 的字符串。

            3.  否则，<var>C</var> 在 <var>reservedSet</var> 里
                1.  令 <var>S</var> 为 <var>string</var> 的从位置 <var>start</var> 到位置 <var>k</var> 的子字符串。

        7.  否则，<var>B</var> 的最高有效位是 **1**
            1.  令 <var>n</var> 为满足 (<var>B</var> \<\< <var>n</var>) & **0x80** 等于 **0** 的最小非负数。
            2.  如果 <var>n</var> 等于 **1** 或 <var>n</var> 大于 **4**，抛出一个 **URIError** 异常。
            3.  令 <var>Octets</var> 为一个长度为 <var>n</var> 的字节数组。
            4.  将 <var>B</var> 放到 <var>Octets</var> 的 **0** 位置。
            5.  如果 <var>k</var> + (**3** \* (<var>n</var> – **1**)) 大于或等于 <var>strLen</var>，抛出一个 **URIError** 异常。
            6.  令 <var>j</var> 为 **1**。
            7.  重复，直到 <var>j</var> \< <var>n</var>
                1.  <var>k</var> 递增 **1**。
                2.  如果 <var>string</var> 的 <var>k</var> 位置的字符不是‘%’，抛出一个 **URIError** 异常。
                3.  如果 <var>string</var> 的 (<var>k</var> + **1**) 和 (<var>k</var> + **2**) 位置的字符没有表示为16进制数字，抛出一个 **URIError** 异常。
                4.  令 <var>B</var> 为 <var>string</var> 的 (<var>k</var> + *1*') 和 (<var>k</var> + **2**) 位置的两个16进制数字表示的8位值。
                5.  如果 <var>B</var> 的两个最高有效位不是二进制的 **10**，抛出一个 **URIError** 异常。
                6.  <var>k</var> 递增 **2**。
                7.  将 <var>B</var> 放到 <var>Octets</var> 的 <var>j</var> 位置。
                8.  <var>j</var> 递增 **1**。

            8.  令 <var>V</var> 为给 <var>Octets</var> 执行 UTF-8 转换得到的值，这是从一个字节数组到一个21位值的转换过程。如果 <var>Octets</var> 不包含有效的 UTF-8 编码的 Unicode 代码点，则抛出一个 **URIError** 异常。
            9.  如果 <var>V</var> 小于 **0x10000**，则
                1.  令 <var>C</var> 为代码单元值是 <var>V</var> 的字符。
                2.  如果 <var>C</var> 不在 <var>reservedSet</var> 里，则
                    1.  令 <var>S</var> 为只包含字符 <var>C</var> 的字符串。

                3.  否则，<var>C</var> 在 <var>reservedSet</var> 里
                    1.  令 <var>S</var> 为 <var>string</var> 的从位置 <var>start</var> 到位置 <var>k</var> 的子字符串。

            10. 否则，<var>V</var> ≥ **0x10000**
                1.  令 <var>L</var> 为 (((<var>V</var> – **0x10000**) & **0x3FF**) + **0xDC00**)。
                2.  令 <var>H</var> 为 ((((<var>V</var> – **0x10000**) \>\> **10**) & **0x3FF**) + **0xD800**)。
                3.  令 <var>S</var> 为代码单元值是 <var>H</var> 和 <var>L</var> 的两个字符组成的字符串。

5.  令 <var>R</var> 为之前的 <var>R</var> 和 <var>S</var> 连接成的新字符串。
6.  k 递增 **1**。

在 UTF-8 中，用 1 到 6 个位的字节序列来编码字符。只有“序列”中高阶位设置为 **0** 的字节，其余的 7 位才用于编码字符值。在一个 <var>n</var> 个字节的序列中，<var>n</var> \> **1**，初始字节有 <var>n</var> 个设置为 **1** 的高阶位，其后的一位设置为 **0**。这个字节的其它位包含了字符编码的位。随后的其它字节都是最高位为 **1**、次高位为 **0**、剩下的 6 位为字符编码。**表21** 指定了 ECMAScript 字符可能的 UTF-8 编码。

|单位代码值|表现|第一字节|第二字节|第三字节|第四字节|
|----------|----|--------|--------|--------|--------|
|0x0000 - 0x007F|00000000 0zzzzzzz|0zzzzzzz||||
|0x0080 - 0x07FF|00000yyy yyzzzzzz|110yyyyy|10zzzzzz|||
|0x0800 - 0xD7FF|xxxxyyyy yyzzzzzz|1110xxxx|10yyyyyy|10zzzzzz||
|0xD800 - 0xDBFF
挨着
0xDC00 - 0xDFFF|110110vv vvwwwwxx
挨着
110111yy yyzzzzzz|11110uuu|10uuwwww|10xxyyyy|10zzzzzz|
|0xD800 - 0xDBFF
不挨着
0xDC00 - 0xDFFF|引发URIError|||||
|0xDC00 - 0xDFFF|引发URIError|||||
|0xE000 - 0xFFFF|xxxxyyyy yyzzzzzz|1110xxxx|10yyyyyy|10zzzzzz||

在这里

uuuuu = vvvv + 1

以补足替代符的 0x10000 附加值，在 Unicode 标准 3.7 章节。

**0xD800-0xDFFF** 范围的代码单元值用来编码替代符对；如上将 UTF-16 替代符对转换组合成一个 UTF-32 表示法，并将其编码到一个 UTF-8 的21位值中。这就是替代符对的解码方式。

RFC 3629 禁止对无效 UTF-8 字节序列的解码。例如，无效序列 **C0 80** 不能解码成字符 **U+0000**。当 算法的实现遇到这样的无效序列必须抛出一个 **URIError** 异常。

#### decodeURI (encodedURI)

**decodeURI** 函数计算出一个新版 URI，将 URI 中可能是 **encodeURI** 函数引入的每个转义序列和 UTF-8 编码组替换为代表它们的字符。不是 **encodeURI** 导入的转义序列不会被替换。

当以一个参数 <var>encodedURI</var> 调用 **decodeURI** 函数，采用如下步骤：

1.  令 <var>uriString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>encodedURI</var>)。
2.  令 <var>reservedURISet</var> 为一个包含 中的所有字符组成的字符串连接上 "**\#**" 组成的字符串。
3.  返回调用 [Decode](#Decode "wikilink")(<var>uriString</var>, <var>reservedURISet</var>) 的结果。

#### decodeURIComponent (encodedURIComponent)

**decodeURIComponent** 函数计算出一个新版 URI，将 URI 中可能是 **encodeURIComponent** 函数引入的每个转义序列和 UTF-8 编码组替换为代表它们的字符。

当以一个参数 <var>encodedURIComponent</var> 调用 **decodeURIComponent** 函数，采用如下步骤：

1.  令 <var>componentString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>encodedURIComponent</var>)。
2.  令 <var>reservedURIComponentSet</var> 为一个空字符串。
3.  返回调用 [Decode](#Decode "wikilink")(<var>componentString</var>, <var>reservedURIComponentSet</var>) 的结果。

#### encodeURI (uri)

**encodeURI** 函数计算出一个新版 URI，将 URI 中某些字符的每个实例替换为代表这些字符 UTF-8 编码的一个，两个或三个转义序列。

当以一个参数 <var>uri</var> 调用 **encodeURI** 函数，采用如下步骤：

1.  令 <var>uriString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>uri</var>)。
2.  令 <var>unescapedURISet</var> 为一个包含 和 中所有字符组成的字符串连接上 "**\#**" 组成的字符串。
3.  返回调用 [Encode](#Encode "wikilink")(<var>uriString</var>, <var>unescapedURISet</var>) 的结果。

#### encodeURIComponent (uriComponent)

**encodeURIComponent** 函数计算出一个新版 URI，将 URI 中某些字符的每个实例替换为代表这些字符 UTF-8 编码的一个，两个或三个转义序列。

当以一个参数 <var>uriComponent</var> 调用 **encodeURIComponent** 函数，采用如下步骤：

1.  令 <var>componentString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>uriComponent</var>)。
2.  令 <var>unescapedURIComponentSet</var> 为一个包含 中所有字符组成的字符串。
3.  返回调用 [Encode](#Encode "wikilink")(<var>componentString</var>, <var>unescapedURIComponentSet</var>) 的结果。

### 全局对象的构造器属性 

#### Object ( . . . )

见 [15.2.1](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8Object.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink") 和 [15.2.2](#Object.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### Function ( . . . )

见 [15.3.1](#Object.prototype "wikilink") 和 [15.3.2](#Object.getPrototypeOf_.28_O_.29 "wikilink")

#### Array ( . . . )

见 [15.4.1](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8Array.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink") 和 [15.4.2](#Array.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### String ( . . . )

见 [15.5.1](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8String.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink") 和 [15.5.2](#String.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### Boolean ( . . . )

见 [15.6.1](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8.E5.B8.83.E5.B0.94.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink") 和 [15.6.2](#.E5.B8.83.E5.B0.94.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### Number ( . . . )

见 [15.7.1](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8.E7.9A.84Number.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink") 和 [15.7.2](#Number.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### Date ( . . . )

见 [15.9.2](#.E4.BD.9C.E4.B8.BA.E5.87.BD.E6.95.B0.E8.B0.83.E7.94.A8Date.E6.9E.84.E9.80.A0.E5.99.A8 "wikilink").

#### RegExp ( . . . )

见 [15.10.3](#The_RegExp_Constructor_Called_as_a_Function "wikilink") 和 [15.10.4](#The_RegExp_Constructor "wikilink").

#### Error ( . . . )

见 [15.11.1](#The_Error_Constructor_Called_as_a_Function "wikilink") 和 [15.11.2](#The_Error_Constructor "wikilink").

#### EvalError ( . . . )

见 15.11.6.1.

#### RangeError ( . . . )

见 [15.11.6.2](#RangeError "wikilink").

#### ReferenceError ( . . . )

见 [15.11.6.3](#ReferenceError "wikilink").

#### SyntaxError ( . . . )

见 [15.11.6.4](#SyntaxError "wikilink").

#### TypeError ( . . . )

见 [15.11.6.5](#TypeError "wikilink").

#### URIError ( . . . )

见 [15.11.6.6](#URIError "wikilink").

### 全局对象的其他属性 

#### Math

见 [15.8](#Math.E5.AF.B9.E8.B1.A1 "wikilink").

#### JSON

见 [15.12](#The_JSON_Object "wikilink").

Object 对象
-----------

### 作为函数调用 Object 构造器

当把 **Object** 当做一个函数来调用，而不是一个构造器，它会执行一个类型转换。

#### Object ( [ value ] )

当以一个参数 <var>value</var> 或者无参数调用 **Object** 函数，采用如下步骤：

1.  如果 <var>value</var> 是 **null**、**undefined** 或未指定，则创建并返回一个新 **Object** 对象，这个对象与仿佛用相同参数调用标准内置的 **Object** 构造器 ([15.2.2.1](#x15.2.2.1 "wikilink")) 的结果一样。
2.  返回 [ToObject](ES5/conversion#ToObject "wikilink")(<var>value</var>)。

### Object 构造器

当 **Object** 是 **new** 表达式调用的一部分时，它是一个构造器，可创建一个对象。

#### new Object ( [ value ] )

当以一个参数 <var>value</var> 或者无参数调用 **Object** 构造器，采用如下步骤：

1.  如果提供了 <var>value</var>，则
    1.  如果 [Type](ES5/types#Type "wikilink")(<var>value</var>) 是 **Object**，则
        1.  如果 <var>value</var> 是个原生 ECMAScript 对象，不创建新对象，简单的返回 <var>value</var>。
        2.  如果 <var>value</var> 是宿主对象，则采取动作和返回依赖实现的结果的方式可以使依赖于宿主对象的。

    2.  如果 [Type](ES5/types#Type "wikilink")(<var>value</var>) 是 **String**，返回 [ToObject](ES5/conversion#ToObject "wikilink")(<var>value</var>)。
    3.  如果 [Type](ES5/types#Type "wikilink")(<var>value</var>) 是 **Boolean**，返回 [ToObject](ES5/conversion#ToObject "wikilink")(<var>value</var>)。
    4.  如果 [Type](ES5/types#Type "wikilink")(<var>value</var>) 是 **Number**，返回 [ToObject](ES5/conversion#ToObject "wikilink")(<var>value</var>)。

2.  断言：未提供参数 <var>value</var> 或其类型是 **Null** 或 **Undefined**。
3.  令 <var>obj</var> 为一个新创建的原生 ECMAScript 对象。
4.  设定 <var>obj</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为标准内置的 **Object** 的 **prototype** 对象 ([15.2.4](#x15.2.4 "wikilink"))。
5.  设定 <var>obj</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Object"**。
6.  设定 <var>obj</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **true**。
7.  设定 <var>obj</var> 的 [8.12](ES5/types#x8.12 "wikilink") 指定的所有内部方法
8.  返回 <var>obj</var>。

### Object 构造器的属性

**Object** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 **Function** 的 **prototype** 对象。

除了内部属性和 **length** 属性（其值是 **1**）之外，**Object** 构造器拥有以下属性：

#### Object.prototype

**Object.prototype** 的初始值是标准内置 **Object** 的 **prototype** 对象（[15.2.4](#x15.2.4 "wikilink")）。

这个属性包含特性 {[[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }

#### Object.getPrototypeOf ( O )

当以参数 <var>O</var> 调用 **getPrototypeOf** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  返回 <var>O</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值。

#### Object.getOwnPropertyDescriptor ( O, P )

当调用 **getOwnPropertyDescriptor** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  令 <var>name</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>P</var>)。
3.  令 <var>desc</var> 为以参数 <var>name</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
4.  返回调用 [FromPropertyDescriptor](ES5/types#FromPropertyDescriptor "wikilink")(<var>desc</var>) 的结果。

#### Object.getOwnPropertyNames ( O )

当调用 **getOwnPropertyNames** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  令 <var>array</var> 为仿佛是用表达式 **new Array ()** 创建新对象的结果，这里的 **Array** 是标准内置构造器名。
3.  令 <var>n</var> 为 **0**。
4.  对 <var>O</var> 的每个自身属性 <var>P</var>
    1.  令 <var>name</var> 为值是 <var>P</var> 的名称的字符串。
    2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>n</var>) 和属性描述 {[[Value]]: <var>name</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 为参数调用 <var>array</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
    3.  <var>n</var> 递增 **1**。

5.  返回 <var>array</var>。

#### Object.create ( O [, Properties] )

**create** 函数按照指定的原型创建一个新对象。当调用 **create** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object** 或 **Null**，则抛出一个 **TypeError** 异常。
2.  令 <var>obj</var> 为仿佛是用表达式 **new Object()** 创建新对象的结果，这里的 **Object** 是标准内置构造器名。
3.  设定 <var>obj</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 <var>O</var>。
4.  如果传入了 <var>Properties</var> 参数并且不是 **undefined**，则仿佛是用 <var>obj</var> 和 <var>Properties</var> 当作参数调用标准内置函数 **Object.defineProperties** 一样给 <var>obj</var> 添加自身属性。
5.  返回 <var>obj</var>。

#### Object.defineProperty ( O, P, Attributes )

**defineProperty** 函数用于给一个对象添加一个自身属性以及更新现有自身属性的特性。当调用 **defineProperty** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  令 <var>name</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>P</var>)。
3.  令 <var>desc</var> 为以 <var>Attributes</var> 作为参数调用 [ToPropertyDescriptor](ES5/types#ToPropertyDescriptor "wikilink") 的结果。
4.  以 <var>name</var>、<var>desc</var>、<var>true</var> 作为参数调用 <var>O</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 .
5.  返回 <var>O</var>。

#### Object.defineProperties ( O, Properties )

**defineProperties** 函数用于给一个对象添加一些自身属性以及更新现有的一些自身属性的特性。当调用 **defineProperties** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  令 <var>props</var> 为 [ToObject](ES5/conversion#ToObject "wikilink")(<var>Properties</var>)。
3.  令 <var>names</var> 为一个内部列表，它包含 <var>props</var> 的每个可遍历自身属性的名称。
4.  令 <var>descriptors</var> 为一个空的内部列表。
5.  对 <var>names</var> 的每个元素 <var>P</var>，按照列表顺序 ,
    1.  令 <var>descObj</var> 为以 <var>P</var> 作为参数调用 <var>props</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    2.  令 <var>desc</var> 为以 <var>descObj</var> 作为参数调用 [ToPropertyDescriptor](ES5/types#ToPropertyDescriptor "wikilink") 的结果。
    3.  将 <var>desc</var> 插入 <var>descriptors</var> 的尾部。

6.  对 <var>descriptors</var> 的每个元素 <var>desc</var>，按照列表顺序 ,
    1.  以参数 <var>P</var>、<var>desc</var>、**true** 调用 <var>O</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

7.  返回 <var>O</var>

如果一个实现为 [for-in 语句](ES5/statements#x12.6.4 "wikilink") 的定义了特定的枚举顺序，那么在这个算法的 **第3步** 中的列表元素**必须**也用相同的顺序排列。

#### Object.seal ( O )

当调用 <var>seal</var> 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  对 <var>O</var> 的每个命名自身属性名 <var>P</var>,
    1.  令 <var>desc</var> 为以参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
    2.  如果 <var>desc</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 是 **true**，设定 <var>desc</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 为 **false**。
    3.  以 <var>P</var>、<var>desc</var>、**true** 为参数调用 <var>O</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

3.  设定 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **false**。
4.  返回 <var>O</var>。

#### Object.freeze ( O )

当调用 **freeze** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  对 <var>O</var> 的每个命名自身属性名 <var>P</var>,
    1.  令 <var>desc</var> 为以参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
    2.  如果 [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(<var>desc</var>) 是 **true**，则
        1.  如果 <var>desc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 是 **true**，设定 <var>desc</var>。[[[Writable]]](ES5/types#Writable "wikilink") 为 **false**.

    3.  如果 <var>desc</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 是 **true**，设定 <var>desc</var>。[[[Configurable]]](ES5/types#Configurable "wikilink") 为 **false**。
    4.  以 <var>P</var>、<var>desc</var>、**true** 作为参数调用 <var>O</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

3.  设定 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **false**。
4.  返回 <var>O</var>。

#### Object.preventExtensions ( O )

当调用 **preventExtensions** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常 .
2.  设定 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **false**。
3.  返回 <var>O</var>。

#### Object.isSealed ( O )

当以参数 <var>O</var> 调用 **isSealed** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  对 <var>O</var> 的每个命名自身属性名 <var>P</var>，
    1.  令 <var>desc</var> 为以参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果 .
    2.  如果 <var>desc</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 是 **true**，则返回 **false**。

3.  如果 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性是 **false**，则返回 **true**。
4.  否则，返回 **false**。

#### Object.isFrozen ( O )

当以参数 <var>O</var> 调用 **isFrozen** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  对 <var>O</var> 的每个命名自身属性名 <var>P</var>,
    1.  令 <var>desc</var> 为以参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果 .
    2.  如果 [IsDataDescriptor](ES5/types#IsDataDescriptor "wikilink")(desc) 是 **true**，则
        1.  如果 <var>desc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 是 **true**，则返回 **false**。

    3.  如果 <var>desc</var>.[[[Configurable]]](ES5/types#Configurable "wikilink") 是 **true**，则返回 **false**。

3.  如果 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性是 **false**，则返回 **true**。
4.  否则，返回 **false**。

#### Object.isExtensible ( O )

当以参数 <var>O</var> 调用 **isExtensible** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  返回 <var>O</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性布尔值。

#### Object.keys ( O )

当以参数 <var>O</var> 调用 **keys** 函数，采用如下步骤：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，则抛出一个 **TypeError** 异常。
2.  令 <var>n</var> 为 <var>O</var> 的可遍历自身属性的个数
3.  令 <var>array</var> 为仿佛是用表达式 **new Array()** 创建新对象的结果，这里的 **Array** 是标准内置构造器名。
4.  令 <var>index</var> 为 **0**。
5.  对 <var>O</var> 的每个可遍历自身属性名 <var>P</var>，
    1.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>index</var>)，属性描述 {[[Value]]: P, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}，和 **false** 作为参数调用 array 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
    2.  <var>index</var> 递增 **1**。

6.  返回 <var>array</var>。

如果一个实现为 [for-in 语句](ES5/statements#x12.6.4 "wikilink") 的定义了特定的枚举顺序，那么在这个算法的 **第5步** 中的**必须**使用相同的枚举顺序。

### Object 的 prototype 对象的属性

**Object** 的 **prototype** 对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值是 **null** ，[[[Class]]](ES5/types#Class "wikilink") 内部属性的值是 **"Object"**，[[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性的初始值是 **true**。

#### Object.prototype.constructor

**Object.prototype.constructor** 的初始值是标准内置的 **Object** 构造器。

#### Object.prototype.toString ( )

当调用 **toString** 方法，采用如下步骤：

1.  如果 **this** 的值是 **undefined**，返回 **"[object Undefined]"**。
2.  如果 **this** 的值是 **null**，返回 **"[object Null]"**。
3.  令 <var>O</var> 为以 **this** 作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
4.  令 <var>class</var> 为 <var>O</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性的值。
5.  返回三个字符串 **"[object "**、<var>class</var> 和 **"]"** 连起来的字符串。

#### Object.prototype.toLocaleString ( )

当调用 **toLocaleString** 方法，采用如下步骤：

1.  令 <var>O</var> 为以 **this** 作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
2.  令 <var>toString</var> 为以 **"toString"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果.
3.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>toString</var>) 是 **false**，抛出一个 **TypeError** 异常。
4.  返回以 <var>O</var> 作为 **this** 值，无参数调用 <var>toString</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

#### Object.prototype.valueOf ( )

当调用 **valueOf** 方法，采用如下步骤：

1.  令 <var>O</var> 为以 **this** 作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
2.  如果 <var>O</var> 是以一个宿主对象 ([15.2.2.1](#15.2.2.1 "wikilink")) 为参数调用 **Object** 构造器的结果，则
    1.  返回 <var>O</var> 或返回先前传递给构造器的原宿主对象。返回的具体结果是由实现定义的。

3.  返回 <var>O</var>。

#### Object.prototype.hasOwnProperty (V)

当以参数 <var>V</var> 调用 **hasOwnProperty** 方法，采用如下步骤：

1.  令 <var>P</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>V</var>)。
2.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
3.  令 <var>desc</var> 为以 <var>P</var> 为参数调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
4.  如果 <var>desc</var> 是 **undefined**，返回 **false**。
5.  返回 **true**。

#### Object.prototype.isPrototypeOf (V)

当以参数 <var>V</var> 调用 **isPrototypeOf** 方法，采用如下步骤：

1.  如果 <var>V</var> 不是个对象，返回 **false**。
2.  令 <var>O</var> 为以 **this** 作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
3.  重复
    1.  令 <var>V</var> 为 <var>V</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值。
    2.  如果 <var>V</var> 是 **null**，返回 **false**
    3.  如果 <var>O</var> 和 <var>V</var> 指向同一个对象，返回 **true**。

#### Object.prototype.propertyIsEnumerable (V)

当以参数 <var>V</var> 调用 **propertyIsEnumerable** 方法，采用如下步骤：

1.  令 <var>P</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>V</var>)。
2.  令 <var>O</var> 为以 **this** 作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
3.  令 <var>desc</var> 为以 <var>P</var> 作为参数调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
4.  如果 <var>desc</var> 是 **undefined**，返回 **false**。
5.  返回 <var>desc</var>.[[[Enumerable]]](ES5/types#Enumerable "wikilink") 的值。

### Object 的实例的属性

**Object** 的实例除了拥从 **Object** 的 **prototype** 对象继承来的属性之外不包含特殊的属性。

Function 对象
-------------

### 作为函数调用 Function 构造器

当将 **Function** 作为函数来调用，而不是作为构造器，它会创建并初始化一个新函数对象。所以函数调用 **Function(**…**)** 与用相同参数的 new **Function(**…**)** 表达式创建的对象相同。

#### Function (p1, p2, … , pn, body)

当以 <var>p1</var>、<var>p2</var>、…、<var>pn</var> 和 <var>body</var> 作为参数调用 **Function** 函数（这里的 <var>n</var> 可以是 **0**，也就是说没有“<var>p</var>”参数，这时还可以不提供 <var>body</var>），采用如下步骤：

1.  创建并返回一个新函数对象，它仿佛是用相同参数给标准内置构造器 **Function** ([15.3.2.1](#x15.3.2.1 "wikilink")). 用一个 **new** 表达式创建的。

### Function 构造器

当 **Function** 作为 **new** 表达式的一部分被调用时，它是一个构造器：它初始化新创建的对象。

#### new Function (p1, p2, … , pn, body)

最后一个参数指定为函数的 <var>body</var>（可执行代码）；之前的任何参数都指定为形式参数。

当以 <var>p1</var>、<var>p2</var>、…、<var>pn</var> 和 <var>body</var> 作为参数调用 **Function** 构造器（这里的 <var>n</var> 可以是 **0**，也就是说没有“<var>p</var>”参数，这时还可以不提供 <var>body</var>），采用如下步骤：

1.  令 <var>argCount</var> 为传给这个函数调用的参数总数。
2.  令 <var>P</var> 为空字符串。
3.  如果 <var>argCount</var> = **0**，令 <var>body</var> 为空字符串。
4.  否则如果 <var>argCount</var> = **1**，令 <var>body</var> 为那个参数。
5.  否则，<var>argCount</var> \> **1**
    1.  令 <var>firstArg</var> 为第一个参数。
    2.  令 <var>P</var> 为 [ToString](ES5/conversion#ToString "wikilink")( <var>firstArg</var> )。
    3.  令 <var>k</var> 为 **2**。
    4.  只要 <var>k</var> \< <var>argCount</var> 就重复
        1.  令 <var>nextArg</var> 为第 <var>k</var> 个参数。
        2.  令 <var>P</var> 为之前的 <var>P</var> 值，字符串 **","**（一个逗号），[ToString](ES5/conversion#ToString "wikilink")( <var>nextArg</var> ) 串联的结果。
        3.  <var>k</var> 递增 **1**。

    5.  令 <var>body</var> 为第 <var>k</var> 个参数。

6.  令 <var>body</var> 为 [ToString](ES5/conversion#ToString "wikilink")( <var>body</var> )。
7.  如果 <var>P</var> 不可解析为一个 [FormalParameterList](ES5/functions#FormalParameterList "wikilink")，则抛出一个 **SyntaxError** 异常。
8.  如果 <var>body</var> 不可解析为 [FunctionBody](ES5/functions#FunctionBody "wikilink")，则抛出一个 **SyntaxError** 异常。
9.  如果 <var>body</var> 是严格模式代码 ( 见 [10.1.1](ES5/execution#x10.1.1 "wikilink"))，则令 <var>strict</var> 为 **true**，否则令 <var>strict</var> 为 **false**。
10. 如果 <var>strict</var> 是 **true**，适用 [13.1](ES5/functions#x13.1 "wikilink") 指定抛出的任何异常。
11. 返回一个新创建的函数对象，它是依照 [13.2](ES5/functions#x13.2 "wikilink") 专递 <var>P</var> 作为 [FormalParameterList](ES5/functions#FormalParameterList "wikilink")、<var>body</var> 作为 [FunctionBody](ES5/functions#FunctionBody "wikilink")、[全局环境作为](ES5/execution#x10.2.3 "wikilink") [Scope](ES5/types#Scope "wikilink") 参数、<var>strict</var> 作为严格模式标志。

每个函数都会自动创建一个 **prototype** 属性，用来支持函数被当做构造器使用的可能性。

` new Function("a", "b", "c", "return a+b+c")`
` new Function("a, b, c", "return a+b+c")`
` new Function("a,b", "c", "return a+b+c")`

### Function 构造器的属性

**Function** 构造器自身是个函数对象，它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"Function"**。**Function** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 **Function** 的 **prototype** 对象 ([15.3.4](#x15.3.4 "wikilink"))。

**Function** 构造器的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性值是 **true**.

Function 构造器有如下属性 :

#### Function.prototype

**Function.prototype** 的初始值是标准内置 **Function** 的 **prototype** 对象 ([15.3.4](#x15.3.4 "wikilink"))。

此属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Function.length

这是个值为 **1** 的数据属性。此属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### Function 的 prototype 对象的属性

**Function** 的 **prototype** 对象自身是一个函数对象 ( 它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"Function"**)，调用这个函数对象时，接受任何参数并返回 **undefined**。

**Function** 的 **prototype** 对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 **Object** 的 **prototype** 对象 ([15.2.4](#x15.2.4 "wikilink"))。**Function** 的 **prototype** 对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性的初始值是 **true**。

**Function** 的 **prototype** 对象自身没有 **valueOf** 属性 ; 但是，它从 **Object** 的 **prototype** 对象继承了 **valueOf** 属性。

**Function** 的 **prototype** 对象的 **length** 属性是 **0**。

#### Function.prototype.constructor

**Function.prototype.constructor** 的初始值是内置 **Function** 构造器。

#### Function.prototype.toString ( )

此函数的返回值的表示是依赖于实现的。这个表示包含 [FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink") 的语法。特别注意，怎样在这个字符串表示中使用和放置空白、行终止符、分号，是依赖于实现的。

这个 **toString** 不是通用的；如果它的 **this** 值不是一个函数对象，它会抛出一个 **TypeError** 异常。因此，它不能当做方法来转移到其他类型的对象中。

#### Function.prototype.apply (thisArg, argArray)

当以 <var>thisArg</var> 和 <var>argArray</var> 为参数在一个 <var>func</var> 对象上调用 **apply** 方法，采用如下步骤：

1.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")( <var>func</var> ) 是 **false**，则抛出一个 **TypeError** 异常。
2.  如果 <var>argArray</var> 是 **null** 或 **undefined**，则
    1.  返回提供 <var>thisArg</var> 作为 **this** 值并以空参数列表调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

3.  如果 [Type](ES5/types#Type "wikilink")( <var>argArray</var> ) 不是 **Object**，则抛出一个 **TypeError** 异常。
4.  令 <var>len</var> 为以 **"length"** 作为参数调用 <var>argArray</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
5.  令 <var>n</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")( <var>len</var> )。
6.  令 <var>argList</var> 为一个空列表。
7.  令 <var>index</var> 为 **0**。
8.  只要 <var>index</var> \< <var>n</var> 就重复
    1.  令 <var>indexName</var> 为 [ToString](ES5/conversion#ToString "wikilink")( <var>index</var> )。
    2.  令 <var>nextArg</var> 为以 <var>indexName</var> 作为参数调用 <var>argArray</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    3.  将 <var>nextArg</var> 作为最后一个元素插入到 <var>argList</var> 里。
    4.  设定 <var>index</var> 为 <var>index</var> + **1**。

9.  提供 <var>thisArg</var> 作为 **this** 值并以 <var>argList</var> 作为参数列表，调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

**apply** 方法的 **length** 属性是 **2**。

#### Function.prototype.call (thisArg [ , arg1 [ , arg2, … ] ] )

当以 <var>thisArg</var> 和可选的 <var>arg1</var>、<var>arg2</var> 等等作为参数在一个 <var>func</var> 对象上调用 **call** 方法，采用如下步骤：

1.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>func</var>) 是 **false**，则抛出一个 **TypeError** 异常。
2.  令 <var>argList</var> 为一个空列表。
3.  如果调用这个方法的参数多余一个，则从 <var>arg1</var> 开始以从左到右的顺序将每个参数插入为 <var>argList</var> 的最后一个元素。
4.  提供 <var>thisArg</var> 作为 **this** 值并以 <var>argList</var> 作为参数列表，调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

**call** 方法的 **length** 属性是 **1**。

#### Function.prototype.bind (thisArg [, arg1 [, arg2, …]])

**bind** 方法需要一个或更多参数，<var>thisArg</var> 和（可选的）<var>arg1</var>、<var>arg2</var>，等，执行如下步骤返回一个新函数对象：

1.  令 <var>Target</var> 为 **this** 值 .
2.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")( <var>Target</var> ) 是 **false**，抛出一个 **TypeError** 异常 .
3.  令 <var>A</var> 为一个（可能为空的）新内部列表，它包含按顺序的 <var>thisArg</var> 后面的所有参数（<var>arg1</var>、<var>arg2</var>，等）。
4.  令 <var>F</var> 为一个新原生 ECMAScript 对象。
5.  依照 [8.12](ES5/types#x8.12 "wikilink") 指定，设定 <var>F</var> 的除了 **[[Get]]** 之外的所有内部方法。
6.  依照 [15.3.5.4](ES5/builtins#x15.3.5.4 "wikilink") 指定，设定 <var>F</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部属性。
7.  设定 <var>F</var> 的 [[[TargetFunction]]](ES5/types#TargetFunction "wikilink") 内部属性为 <var>Target</var>。
8.  设定 <var>F</var> 的 [[[BoundThis]]](ES5/types#BoundThis "wikilink") 内部属性为 <var>thisArg</var> 的值。
9.  设定 <var>F</var> 的 [[[BoundArgs]]](ES5/types#BoundArgs "wikilink") 内部属性为 <var>A</var>。
10. 设定 <var>F</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Function"**。
11. 设定 <var>F</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性为 [15.3.3.1](#x15.3.3.1 "wikilink") 指定的标准内置 **Function** 的 **prototype** 对象。
12. 依照 [15.3.4.5.1](#x15.3.4.5.1 "wikilink") 描述，设定 <var>F</var> 的 **[[Call]]** 内置属性。
13. 依照 [15.3.4.5.2](#x15.3.4.5.2 "wikilink") 描述，设定 <var>F</var> 的 **[[Construct]]** 内置属性。
14. 依照 [15.3.4.5.3](#x15.3.4.5.3 "wikilink") 描述，设定 <var>F</var> 的 **[[HasInstance]]** 内置属性。
15. 如果 <var>Target</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"Function"**，则
    1.  令 <var>L</var> 为 <var>Target</var> 的 **length** 属性减 <var>A</var> 的长度。
    2.  设定 <var>F</var> 的 **length** 自身属性为 **0** 和 <var>L</var> 中更大的值。

16. 否则设定 <var>F</var> 的 **length** 自身属性为 **0**.
17. 设定 <var>F</var> 的 **length** 自身属性的特性为 [15.3.5.1](#x15.3.5.1 "wikilink") 指定的值。
18. 设定 <var>F</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性为 **true**。
19. 令 <var>thrower</var> 为 [[[ThrowTypeError]]](ES5/functions#ThrowTypeError "wikilink") 函数对象 ([13.2.3](ES5/functions#ThrowTypeError "wikilink"))。
20. 以 **"caller"**, 属性描述符 {[[Get]]: thrower, [[Set]]: thrower, [[Enumerable]]: **false**, [[Configurable]]: **false**}, 和 **false** 作为参数调用 F 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
21. 以 **"arguments"**, 属性描述符 {[[Get]]: <var>thrower</var>, [[Set]]: <var>thrower</var>, [[Enumerable]]: **false**, [[Configurable]]: **false**}, 和 **false** 作为参数调用 F 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
22. 返回 <var>F</var>.

**bind** 方法的 **length** 属性是 **1**。

##### [[Call]]

当调用一个用 **bind** 函数创建的函数对象 <var>F</var> 的 **[[Call]]** 内部方法，传入一个 **this** 值和一个参数列表 <var>ExtraArgs</var>，采用如下步骤：

1.  令 <var>boundArgs</var> 为 <var>F</var> 的 [[[BoundArgs]]](ES5/types#BoundArgs "wikilink") 内部属性值。
2.  令 <var>boundThis</var> 为 <var>F</var> 的 [[[BoundThis]]](ES5/types#BoundThis "wikilink") 内部属性值。
3.  令 <var>target</var> 为 <var>F</var> 的 [[[TargetFunction]]](ES5/types#TargetFunction "wikilink") 内部属性值。
4.  令 <var>args</var> 为一个新列表，它包含与列表 <var>boundArgs</var> 相同顺序相同值，后面跟着与 <var>ExtraArgs</var> 是相同顺序相同值。
5.  提供 <var>boundThis</var> 作为 **this** 值，提供 <var>args</var> 为参数调用 <var>target</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

##### [[Construct]]

当调用一个用 **bind** 函数创建的函数对象 <var>F</var> 的 **[[Construct]]** 内部方法，传入一个参数列表 <var>ExtraArgs</var>，采用如下步骤：

1.  令 <var>target</var> 为 <var>F</var> 的 [[[TargetFunction]]](ES5/types#TargetFunction "wikilink") 内部属性值。
2.  如果 <var>target</var> 不包含 [[[Construct]]](ES5/types#Construct "wikilink") 内部方法，抛出一个 **TypeError** 异常。
3.  令 <var>boundArgs</var> 为 <var>F</var> 的 [[[BoundArgs]]](ES5/types#BoundArgs "wikilink") 内部属性值。
4.  令 <var>args</var> 为一个新列表，它包含与列表 <var>boundArgs</var> 相同顺序相同值，后面跟着与 <var>ExtraArgs</var> 是相同顺序相同值。
5.  提供 <var>args</var> 为参数调用 <var>target</var> 的 [[[Construct]]](ES5/types#Construct "wikilink") 内部方法，返回结果。

##### [[HasInstance]] (V)

当调用一个用 **bind** 函数创建的函数对象 <var>F</var> 的 **[[HasInstance]]** 内部方法，并以 <var>V</var> 作为参数，采用如下步骤：

1.  令 <var>target</var> 为 <var>F</var> 的 [[[TargetFunction]]](ES5/types#TargetFunction "wikilink") 内部属性值。
2.  如果 <var>target</var> 不包含 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内部方法，抛出一个 **TypeError** 异常。
3.  提供 <var>V</var> 为参数调用 <var>target</var> 的 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内部方法，返回结果。

### Function 的实例的属性

除了必要的内部属性之外，每个函数实例还有一个 [[[Class]]](ES5/types#Class "wikilink") 内部属性并且在大多数情况下使用不同版本的 [[[Call]]](ES5/types#Call "wikilink") 内部属性。函数实例根据怎样创建的（见 [8.6.2](ES5/types#x8.6.2 "wikilink")、[13.2](ES5/functions#x13.2 "wikilink")、[15](# "wikilink")、[15.3.4.5](#x15.3.4.5 "wikilink")）可能还有一个 [[[HasInstance]]](ES5/types#HasInstance "wikilink") 内部属性、一个 [[[Scope]]](ES5/types#Scope "wikilink") 内部属性、一个 [[[Construct]]](ES5/types#Construct "wikilink") 内部属性、一个 [[[FormalParameters]]](ES5/types#FormalParameters "wikilink") 内部属性、一个 [[[Code]]](ES5/types#Code "wikilink") 内部属性、一个 [[[TargetFunction]]](ES5/types#TargetFunction "wikilink") 内部属性、一个 [[[BoundThis]]](ES5/types#BoundThis "wikilink") 内部属性、一个 [[[BoundArgs]]](ES5/types#BoundArgs "wikilink") 内部属性。

[[[Class]]](ES5/types#Class "wikilink") 内部属性的值是 **"Function"**。

对应于严格模式函数 ([13.2](ES5/functions#x13.2 "wikilink")) 的函数实例和用 **Function.prototype.bind** 方法 ([15.3.4.5](#x15.3.4.5 "wikilink")) 创建的函数实例有名为“**caller**”和 “**arguments**”的属性时，抛出一个 **TypeError** 异常。一个 ECMAScript 实现不得为在严格模式函数代码里访问这些属性关联任何依赖实现的特定行为。

#### length

**length** 属性值是个整数，它指出函数预期的“一般的”参数个数。然而，语言允许用其他数量的参数来调用函数。当以与函数的 **length** 属性指定的数量不同的参数个数调用函数时，它的行为依赖于函数自身。这个属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### prototype

**prototype** 属性的值用于初始化一个新创建对象的的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性，为了这个新创建对象要先将函数对象作为构造器调用。这个属性拥有特性 { [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### [[HasInstance]] (V)

设 <var>F</var> 是个函数对象。 当以 <var>V</var> 作为参数调用 <var>F</var> 的 **[[HasInstance]]** 内部方法，采用如下步骤：

1.  如果 <var>V</var> 不是个对象，返回 **false**。
2.  令 <var>O</var> 为用属性名 **"prototype"** 调用 <var>F</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
4.  重复
    1.  令 <var>V</var> 为 <var>V</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值。
    2.  如果 <var>V</var> 是 **null**，返回 **false**。
    3.  如果 <var>O</var> 和 <var>V</var> 指向相同对象，返回 **true**。

#### [[Get]] (P)

函数对象与其他原生 EMACScript 对象 ([8.12.3](ES5/types#x8.12.3 "wikilink")) 用不同的 **[[Get]]** 内部方法。

设 <var>F</var> 是一个函数对象，当以属性名 <var>P</var> 调用 <var>F</var> 的 **[[Get]]** 内部方法，采用如下步骤：

1.  令 <var>v</var> 为传入 <var>P</var> 作为属性名参数调用 <var>F</var> 的默认 [[[Get]]](ES5/types#Get "wikilink") 内部方法 ([8.12.3](ES5/types#8.12.3 "wikilink")) 的结果。
2.  如果 <var>P</var> 是 **"caller"** 并且 <var>v</var> 是个严格模式函数对象，抛出一个 **TypeError** 异常。
3.  返回 <var>v</var>。

Array 对象
----------

数组对象会给予一些特定种类的属性名特殊待遇。对一个属性名 <var>P</var>（字符串形式），当且仅当 [ToString](ES5/conversion#to-string "wikilink")([ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>P</var>)) 等于 <var>P</var> 并且 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>P</var>) 不等于 **2<sup>32</sup> - 1** 时，它是个*数组索引*。一个属性名是数组索引的属性还叫做''元素 ''。所有数组对象都有一个 **length** 属性，其值始终是一个小于 **2<sup>32</sup>** 的非负整数。**length** 属性值在数值上比任何名为数组索引的属性名称还要大；每当创建或更改一个数组对象的属性，都要调整其他属性以保持上面那个条件不变。具体来说，每当添加一个名为数组索引的属性时，如果需要就更改 **length** 属性为在数值上比这个数组索引大 **1** 的值；每当更改 **length** 属性，所有属性名是数组索引并且其值不小于新 **length** 的属性会被自动删除。 这个限制只应用于数组对象的自身属性，并且从原型中继承的 **length** 或数组索引不影响这个限制。

对一个对象 <var>O</var>，如果以下算法返回 **true**，那么就叫这个对象为 <b title="sparse">稀疏</b> 的：

1.  令 <var>len</var> 为以 **"length"** 作为参数调用 O 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
2.  对每个范围在 **0** ≤ <var>i</var> \< [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>len</var>) 的整数 <var>i</var>
    1.  令 <var>elem</var> 为以 [ToString](ES5/conversion#to-string "wikilink")(<var>i</var>) 作为参数调用 <var>O</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
    2.  如果 <var>elem</var> 是 **undefined**，返回 **true**。

3.  返回 **false**。

### 作为函数调用 Array 构造器

当将 **Array** 作为函数来调用，而不是作为构造器，它会创建并初始化一个新数组对象。所以函数调用 **Array(…)** 与用相同参数的 **new Array(…)** 表达式创建的对象相同。

#### Array ( [ item1 [ , item2 [ , … ] ] ] )

当调用 **Array** 函数，采用如下步骤：

1.  创建并返回一个新函数对象，它仿佛是用相同参数给标准内置构造器 **Array** 用一个 **new** 表达式创建的 ([15.4.2](ES5/builtins#x15.4.2 "wikilink"))。

### Array 构造器

当 **Array** 作为 **new** 表达式的一部分被调用时，它是一个构造器：它初始化新创建的对象。

#### new Array ( [ item0 [ , item1 [ , … ] ] ] )

当且仅当以无参数或至少两个参数调用 **Array** 构造器时，适用这里的描述。

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性要设定为原始的数组原型对象，他是 Array.prototype([15.4.3.1](ES5/builtins#x15.4.3.1 "wikilink")) 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性要设定为 **"Array"**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性要设定为 **true**。

新构造对象的 **length** 属性要设定为参数的个数。

新构造对象的 **0** 属性要设定为 <var>item0</var>（如果提供了）；新构造对象的 **1** 属性要设定为 <var>item1</var>（如果提供了）；更多的参数可应用普遍规律，新构造对象的 <var>k</var> 属性要设定为第 <var>k</var> 个参数，这里的 <var>k</var> 是从 **0** 开始的。所有这些属性都有特性 { [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true** }。

#### new Array (len)

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性要设定为原始的数组原型对象，他是 Array.prototype([15.4.3.1](ES5/builtins#x15.4.3.1 "wikilink")) 的初始值。新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性要设定为 **"Array"**。新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性要设定为 **true**。

如果参数 <var>len</var> 是个[Number值](ES5/types#Number "wikilink") 并且 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>len</var>) 等于 <var>len</var>，则新构造对象的 **length** 属性要设定为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>len</var>)。如果参数 <var>len</var> 是个数字值并且 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>len</var>) 不等于 <var>len</var>，则抛出一个 **RangeError** 异常。

如果参数 <var>len</var> 不是[Number值](ES5/types#Number "wikilink")，则新构造对象的 **length** 属性要设定为 **0**，并且新构造对象的 **0** 属性要设定为 <var>len</var>，设定它的特性为 { [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true** }。

### Array 构造器的属性

**Array** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是函数原型对象 ([15.3.4](ES5/builtins#x15.3.4 "wikilink"))。

**Array** 构造器除了有一些内部属性和 **length** 属性（其值是 **1**）之外，还有如下属性：

#### Array.prototype

**Array.prototype** 的初始值是数组原型对象 ([15.4.4](ES5/builtins#x15.4.4 "wikilink"))。

此属性拥有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Array.isArray ( arg )

**isArray** 函数需要一个参数 arg，如果参数是个对象并且 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"Array"**，返回布尔值 **true**；否则它返回 **false**。采用如下步骤：

1.  如果 [Type](ES5/types "wikilink")(arg) 不是 **Object**，返回 **false**。
2.  如果 arg 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Array"**，则返回 **true**。
3.  返回 **false**。

### 数组原型对象的属性

数组原型对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 [Object](ES5/builtins#x15.2 "wikilink") 原型对象 ([15.2.4](ES5/builtins#x15.2.4 "wikilink"))。

数组原型对象自身是个数组；它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"Array"**，它拥有一个 **length** 属性（初始值是 **+0**）和 [15.4.5.1](ES5/builtins#x15.4.5.1 "wikilink") 描述的特殊的 [[[DefineOwnProperty]]](ES5/builtins#x15.4.5.1 "wikilink") 内部方法。

在以下的对数组原型对象的属性函数的描述中，短语**“this 对象”**指的是调用这个函数时的 **this** 值对象。允许 **this** 是 [[[Class]]](ES5/types#Class "wikilink") 内部属性值不是 **"Array"** 的对象。

#### Array.prototype.constructor

**Array.prototype.constructor** 的初始值是标准内置 **Array** 构造器。

#### Array.prototype.toString ( )

当调用 **toString** 方法，采用如下步骤：

1.  令 <var>array</var> 为用 **this** 值调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>func</var> 为以 **"join"** 作为参数调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>func</var>) 是 **false**，则令 <var>func</var> 为标准内置方法 **Object.prototype.toString** ([15.2.4.2](ES5/builtins#x15.2.4.2 "wikilink"))。
4.  提供 <var>array</var> 作为 **this** 值并以空参数列表调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

#### Array.prototype.toLocaleString ( )

先用数组元素的 **toLocaleString** 方法，将他们转换成字符串。然后将这些字符串串联，用一个分隔符分割，这里的分隔符字符串是与特定语言环境相关，由实现定义的方式得到的。调用这个函数的结果除了与特定语言环境关联之外，与 **toString** 的结果类似。

结果是按照一下方式计算的：

1.  令 <var>array</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>arrayLen</var> 为以 **"length"** 作为参数调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>arrayLen</var>)。
4.  令 <var>separator</var> 为宿主环境的当前语言环境对应的列表分隔符字符串（这是实现定义的方式得到的）。
5.  如果 <var>len</var> 是零，返回空字符串。
6.  令 <var>firstElement</var> 为以 **"0"** 作为参数调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
7.  如果 <var>firstElement</var> 是 **undefined** 或 **null**，则
    1.  令 <var>R</var> 为空字符串。

8.  否则
    1.  令 <var>elementObj</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>firstElement</var>).
    2.  令 <var>func</var> 为以 **"toLocaleString"** 作为参数调用 <var>elementObj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    3.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>func</var>) 是 **false**，抛出一个 **TypeError** 异常。
    4.  令 <var>R</var> 为提供 <var>elementObj</var> 作为 **this** 值并以空参数列表调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

9.  令 <var>k</var> 为 **1**。
10. 只要 <var>k</var> \< <var>len</var> 就重复
    1.  令 <var>S</var> 为串联 <var>R</var> 和 <var>separator</var> 产生的字符串。
    2.  令 <var>nextElement</var> 为以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 作为参数调用 <var>array</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    3.  如果 <var>nextElement</var> 是 **undefined** 或 **null**，则
        1.  令 <var>R</var> 为空字符串。

    4.  否则
        1.  令 <var>elementObj</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>nextElement</var>).
        2.  令 <var>func</var> 为以 **"toLocaleString"** 作为参数调用 <var>elementObj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        3.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>func</var>) 是 **false**，抛出一个 **TypeError** 异常。
        4.  令 <var>R</var> 为提供 <var>elementObj</var> 作为 **this** 值并以空参数列表调用 <var>func</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

    5.  令 <var>R</var> 为串联 <var>S</var> 和 <var>R</var> 产生的字符串。
    6.  <var>k</var> 递增 **1**。

11. 返回 <var>R</var>

#### Array.prototype.concat ( [ item1 [ , item2 [ , … ] ] ] )

当以零个或更多个参数 <var>item1</var>、<var>item2</var>，等，调用 **concat** 方法时，会返回一个数组。 返回的数组包含 调用对象的数组元素 和随后顺序每个参数的数组元素。

采用如下步骤：

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>A</var> 为仿佛是用表达式 **new Array()** 创建的新数组，这里的 **Array** 是标准内置构造器名。
3.  令 <var>n</var> 为 **0**。
4.  令 <var>items</var> 为一个内部列表，他的第一个元素是 **O**，之后的元素是调用时传给这个函数的各参数（以从左到右的顺序）。
5.  只要 <var>items</var> 不是空就重复
    1.  删除 <var>items</var> 的第一个元素，并令 <var>E</var> 为这个元素值。
    2.  如果 <var>E</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"Array"**，则
        1.  令 <var>k</var> 为 **0**。
        2.  令 <var>len</var> 为以 **"length"** 为参数调用 <var>E</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        3.  只要 <var>k</var> \< <var>len</var> 就重复
            1.  令 <var>P</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>).
            2.  令 <var>exists</var> 为以 <var>P</var> 作为参数调用 <var>E</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
            3.  如果 <var>exists</var> 是 **true**，则
                1.  令 <var>subElement</var> 为以 <var>P</var> 作为参数调用 <var>E</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
                2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>n</var>)、属性描述符 { [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true** } 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

            4.  <var>n</var> 递增 **1**。
            5.  <var>k</var> 递增 **1**。

    3.  否则，<var>E</var> 不是数组
        1.  以 [ToString](ES5/conversion#ToString "wikilink")(n)、属性描述符 { [[Value]]: E, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **false** } 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
        2.  <var>n</var> 递增 **1**。

6.  返回 <var>A</var>。

**concat** 方法的 **length** 属性是 **1**。

#### Array.prototype.join (separator)

数组元素先被转换为字符串，再将这些字符串用 <var>separator</var> 分割连接在一起。如果没提供分隔符，将一个逗号用作分隔符。

**join** 方法需要一个参数 <var>separator</var>，执行以下步骤 :

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  如果 <var>separator</var> 是 **undefined**，令 <var>separator</var> 为单字符字符串 **","**。
5.  令 <var>sep</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>separator</var>)。
6.  如果 <var>len</var> 是零，返回空字符串。
7.  令 <var>element0</var> 为以 **"0"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
8.  如果 <var>element0</var> 是 **undefined** 或 **null**, 令 <var>R</var> 为空字符串；否则，令 <var>R</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>element0</var>)。
9.  令 <var>k</var> 为 **1**.
10. 只要 <var>k</var> \< <var>len</var> 就重复
    1.  令 <var>S</var> 为串联 <var>R</var> 和 <var>sep</var> 产生的字符串值。
    2.  令 <var>element</var> 为以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    3.  如果 <var>element</var> 是 **undefined** 或 **null**，令 <var>next</var> 为空字符串；否则，令 <var>next</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>element</var>)。
    4.  令 <var>R</var> 为串联 <var>S</var> 和 <var>next</var> 产生的字符串值。
    5.  <var>k</var> 递增 **1**。

11. 返回 <var>R</var>。

**join** 方法的 **length** 属性是 **1**。

#### Array.prototype.pop ( )

删除并返回数组的最后一个元素。

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果); Array.prototype.pop.call(1);</nowiki> 之类的副作用不会残留在 O 上（Array.prototype.pop.call(Object(1)); 的副作用就会残留）。很多的 Array.prototype 方法也有类似的问题。}}。
2.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  如果 <var>len</var> 是零
    1.  以 **"length"**、**0** 和 **true** 作为参数调用 *O* 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    2.  返回 **undefined**。

5.  否则，<var>len</var> \> **0**
    1.  令 <var>indx</var> 为 [ToString](ES5/conversion#to-string "wikilink")(<var>len</var> - **1**)。
    2.  令 <var>element</var> 为以 <var>indx</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    3.  以 <var>indx</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。
    4.  以 **"length"**、<var>indx</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    5.  返回 <var>element</var>。

#### Array.prototype.push ( [ item1 [ , item2 [ , … ] ] ] )

将参数以他们出现的顺序追加到数组末尾。数组的新 **length** 属性值会作为调用的结果返回。

当以零或更多个参数 <var>item1</var>、<var>item2</var>，等，调用 **push** 方法，采用以下步骤：

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
2.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>n</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  令 <var>items</var> 为一个内部列表，它的元素是调用这个函数时传入的参数（从左到右的顺序）。
5.  只要 <var>items</var> 不是空就重复
    1.  删除 <var>items</var> 的第一个元素，并令 <var>E</var> 为这个元素的值。
    2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>n</var>)、<var>E</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    3.  <var>n</var> 递增 **1**。

6.  以 **"length"**、<var>n</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
7.  返回 <var>n</var>。

**push** 方法的 **length** 属性是 **1**。

#### Array.prototype.reverse ( )

重新排列数组元素，以翻转它们的顺序。对象会被当做调用的结果返回。

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  令 <var>middle</var> 为 [floor](ES5/notation#x5.2 "wikilink")(<var>len</var> / **2**)。
5.  令 <var>lower</var> 为 **0**。
6.  只要 <var>lower</var> ≠ <var>middle</var> 就重复
    1.  令 <var>upper</var> 为 <var>len</var> - <var>lower</var> - **1**。
    2.  令 <var>upperP</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>upper</var>)。
    3.  令 <var>lowerP</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>lower</var>)。
    4.  令 <var>lowerValue</var> 为以 <var>lowerP</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    5.  令 <var>upperValue</var> 为以 <var>upperP</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
    6.  令 <var>lowerExists</var> 为以 <var>lowerP</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    7.  令 <var>upperExists</var> 为以 <var>upperP</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    8.  如果 <var>lowerExists</var> 是 **true** 并且 <var>upperExists</var> 是 **true**，则
        1.  以 <var>lowerP</var>、<var>upperValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
        2.  以 <var>upperP</var>、<var>lowerValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

    9.  否则如果 <var>lowerExists</var> 是 **false** 并且 <var>upperExists</var> 是 **true**，则
        1.  以 <var>lowerP</var>、<var>upperValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
        2.  以 <var>upperP</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

    10. 否则如果 <var>lowerExists</var> 是 **true** 并且 <var>upperExists</var> 是 **false**，则
        1.  以 <var>lowerP</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。
        2.  以 <var>upperP</var>、<var>lowerValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

    11. 否则，<var>lowerExists</var> 和 <var>upperExists</var> 都是 **false**
        1.  不需要做任何事情。

    12. <var>lower</var> 递增 **1**。

7.  返回 <var>O</var>。

#### Array.prototype.shift ( )

删除并返回数组的第一个元素。

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  如果 <var>len</var> 是零 , 则
    1.  以 **"length"**、**0** 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    2.  返回 **undefined**。

5.  令 <var>first</var> 为以 **"0"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
6.  令 <var>k</var> 为 **1**。
7.  只要 <var>k</var> \< <var>len</var> 就重复
    1.  令 <var>from</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>to</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> - **1**)。
    3.  令 <var>fromPresent</var> 为以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    4.  如果 <var>fromPresent</var> 是 **true**, 则
        1.  令 <var>fromVal</var> 为以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  以 <var>to</var>、<var>fromVal</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

    5.  否则，<var>fromPresent</var> 是 **false**
        1.  以 <var>to</var> 和 **ture** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

    6.  <var>k</var> 递增 **1**。

8.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>len</var> - **1**) 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。
9.  以 **"length"**、(<var>len</var> - **1**) 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
10. 返回 <var>first</var>。

#### Array.prototype.slice (start, end)

**slice** 方法需要 <var>start</var> 和 <var>end</var> 两个参数，返回一个数组，这个数组包含从下标为 <var>start</var> 的元素到下标为 <var>end</var>（不含 **end**）的元素（或如果 <var>end</var> 是 **undefined** 就到数组末尾）。如果 <var>start</var> 为负，它会被当做是 **length** + <var>start</var>，这里的 **length** 是数组长度。如果 <var>end</var> 为负，它会被当做是 **length** + <var>end</var>，这里的 **length** 是数组长度。采用如下步骤：

1.  令 <var>O</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>A</var> 为仿佛用表达式 **new Array()** 创建的新数组，这里的 **Array** 是标准内置构造器名。
3.  令 <var>lenVal</var> 为以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
4.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
5.  令 <var>relativeStart</var> 为 [ToInteger](ES5/conversion#to-integer "wikilink")(<var>start</var>)。
6.  如果 <var>relativeStart</var> 为负，令 <var>k</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")((<var>len</var> + <var>relativeStart</var>), **0**)；否则令 <var>k</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>relativeStart</var>, <var>len</var>)。
7.  如果 <var>end</var> 是 **undefined**，令 <var>relativeEnd</var> 为 <var>len</var>；否则令 <var>relativeEnd</var> 为 [ToInteger](ES5/conversion#to-integer "wikilink")(<var>end</var>)。
8.  如果 <var>relativeEnd</var> 为负，令 <var>final</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")((<var>len</var> + <var>relativeEnd</var>), **0**)；否则令 <var>final</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>relativeEnd</var>, <var>len</var>)。
9.  令 <var>n</var> 为 **0**。
10. 只要 <var>k</var> \< <var>final</var> 就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**, 则
        1.  令 <var>kValue</var> 为以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>n</var>)、属性描述符 {[[Value]]: <var>kValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

    4.  <var>k</var> 递增 **1**。
    5.  <var>n</var> 递增 **1**。

11. 返回 <var>A</var>。

**slice** 方法的 **length** 属性是 **2**。

#### Array.prototype.sort (comparefn)

给 **this** 数组的元素排序。排序不一定是稳定的（相等的元素们不一定按照他们原来的顺序排列）。如果 <var>comparefn</var> 不是 **undefined**，它就必须是个函数，这个函数接受两个参数 <var>x</var> 和 <var>y</var>，如果 <var>x</var> \< <var>y</var> 返回一个负值，如果 <var>x</var> = <var>y</var> 返回零，如果 <var>x</var> \> <var>y</var> 返回一个正值。

令 <var>obj</var> 为以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。

以 **"length"** 作为参数调用 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法，将结果作为参数调用 Uint32，令 <var>len</var> 为返回的结果。

如果 <var>comparefn</var> 不是 **undefined** 并且不是对 **this** 数组的元素保持一致的比较函数（见下面），那么这种情况下 **sort** 的行为是由实现来定义的。

令 <var>proto</var> 为 <var>obj</var> 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性。如果 <var>proto</var> 不是 **null** 并且存在一个整数 <var>j</var> 满足下面列出的全部条件，那么这种情况下 **sort** 的行为是实现定义的：

-   <var>obj</var> 是稀疏的（[15.4](ES5/builtins#x15.4 "wikilink")）
-   **0** ≤ <var>j</var> \< <var>len</var>
-   以 [ToString](ES5/conversion#ToString "wikilink")(<var>j</var>) 作为参数调用 <var>proto</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果是 **true**

如果 <var>obj</var> 是稀疏的并且以下任何条件为真，那么这种情况下 **sort** 的行为也是实现定义的：

-   <var>obj</var> 的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性是 **false**。
-   任何名为小于 <var>len</var> 的非负整数的数组索引属性中，有 [[[Configurable]]](ES5/types#Configurable "wikilink") 特性是 **false** 的数据属性。

任何名为小于 <var>len</var> 的非负整数的数组索引属性中，有[访问器属性](ES5/types#accessor-property-descriptor "wikilink")，或有 [[[Writable]]](ES5/types#Writable "wikilink") 特性是 **false** 的数据属性，那么这种情况下 **sort** 的行为也是实现定义的。

否则，采用如下步骤。

1.  根据实现定义的排序算法，通过调用若干次 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink")、[[[Put]]](ES5/types#Put "wikilink")、[[[Delete]]](ES5/types#Delete "wikilink") 内部方法和 的有机组合来完成排序。这里对每个 [[[Get]]](ES5/types#Get "wikilink")、[[[Put]]](ES5/types#Put "wikilink") 或 [[[Delete]]](ES5/types#Delete "wikilink") 调用的第一个参数是小于 <var>len</var> 的非负整数， 调用的参数是前面调用 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。调用 [[[Put]]](ES5/types#Put "wikilink") 和 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法时，<var>throw</var> 参数是 **true**。如果 <var>obj</var> 不是稀疏的，则必须不调用 [[[Delete]]](ES5/types#Delete "wikilink")。
2.  返回 <var>obj</var>。

返回的对象必须拥有下面两个性质。

-   必须有这样的数学排列 <var>π</var>，它是由比 <var>len</var> 小的非负整数组成，对于每个比 <var>len</var> 小的非负整数 <var>j</var>，如果属性 <var>old</var>[<var>j</var>] 存在 , 则 <var>new</var>[<var>π</var>(<var>j</var>)] 有与 <var>old</var>[<var>j</var>] 相同的值，如果属性 <var>old</var>[<var>j</var>] 不存在，则 <var>new</var>[<var>π</var>(<var>j</var>)] 也不存在。
-   对于都比 <var>len</var> 小的所有非负整数 <var>j</var> 和 <var>k</var>，如果 (<var>j</var>, <var>k</var>) \< <var>0</var>, 则 <var>π</var>(<var>j</var>) \< <var>π</var>(<var>k</var>).

这里的符号 <var>old</var>[<var>j</var>] 用来指：假定在执行这个函数之前以 <var>j</var> 作为参数调用 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果，符号 <var>new</var>[<var>j</var>] 用来指：假定在执行这个函数后以 <var>j</var> 作为参数调用 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。

如果对于集合 <var>S</var> 里的任何值 <var>a</var>、<var>b</var>、<var>c</var>（可以是相同值），都满足以下所有条件，那么函数 <var>comparefn</var> 是在集合 <var>S</var> 上保持一致的比较函数（以下，符号 <var>a</var> **\<**<sub>CF</sub> <var>b</var> 表示 <var>comparefn</var>(<var>a</var>, <var>b</var>) \< **0**；符号 <var>a</var> **=**<sub>CF</sub> <var>b</var> 表示 <var>comparefn</var>(<var>a</var>, <var>b</var>) = **0**（**不论正负**）； 符号 <var>a</var> **\>**<sub>CF</sub> <var>b</var> 表示 <var>comparefn</var>(<var>a</var>, <var>b</var>) \> **0**）：

-   当用指定值 <var>a</var> 和 <var>b</var> 作为两个参数调用 <var>comparefn</var>(<var>a</var>, <var>b</var>)，总是返回相同值 <var>v</var>。此外 [Type](ES5/types#Type "wikilink")(<var>v</var>) 是 **Number**, 并且 <var>v</var> 不是 **NaN**。注意，这意味着对于给定的 <var>a</var> 和 <var>b</var>，<var>a</var> **\<**<sub>CF</sub> <var>b</var>、<var>a</var> **=**<sub>CF</sub> <var>b</var>、<var>a</var> **\>**<sub>CF</sub> <var>b</var> 中正好有一个为真。
-   调用 <var>comparefn</var>(<var>a</var>, <var>b</var>) 不改变 **this** 对象。
-   <var>a</var> **=**<sub>CF</sub> <var>a</var>（自反性）
-   如果 <var>a</var> **=**<sub>CF</sub> <var>b</var>, 则 <var>b</var> **=**<sub>CF</sub> <var>a</var>（对称性）
-   如果 <var>a</var> **=**<sub>CF</sub> <var>b</var> 并且 <var>b</var> **=**<sub>CF</sub> <var>c</var>，则 <var>a</var> **=**<sub>CF</sub> <var>c</var>（**=**<sub>CF</sub> 传递）
-   如果 <var>a</var> **\<**<sub>CF</sub> <var>b</var> 并且 <var>b</var> **\<**<sub>CF</sub> <var>c</var>, 则 <var>a</var> **\<**<sub>CF</sub> <var>c</var>（**\<**<sub>CF</sub> 传递）
-   如果 <var>a</var> **\>**<sub>CF</sub> <var>b</var> 并且 <var>b</var> **\>**<sub>CF</sub> <var>c</var>，则 <var>a</var> **\>**<sub>CF</sub> <var>c</var>（**\>**<sub>CF</sub> 传递）

当用两个参数 <var>j</var> 和 <var>k</var> 调用抽象操作 **SortCompare**，采用如下步骤：

1.  令 <var>jString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>j</var>)。
2.  令 <var>kString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
3.  令 <var>hasj</var> 为 以 <var>jString</var> 作为参数调用 <var>obj</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
4.  令 <var>hask</var> 为 以 <var>kString</var> 作为参数调用 <var>obj</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
5.  如果 <var>hasj</var> 和 <var>hask</var> 都是 **false**，则返回 **+0**。
6.  如果 <var>hasj</var> 是 **false**，则返回 **1**。
7.  如果 <var>hask</var> 是 **false**，则返回 **-1**。
8.  令 <var>x</var> 为 以 <var>jString</var> 作为参数调用 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
9.  令 <var>y</var> 为 以 <var>kString</var> 作为参数调用 <var>obj</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
10. 如果 <var>x</var> 和 <var>y</var> 都是 **undefined**，返回 **+0**。
11. 如果 <var>x</var> 是 **undefined**，返回 **1**。
12. 如果 <var>y</var> 是 **undefined**，返回 **?1**。
13. 如果 参数 <var>comparefn</var> 不是 **undefined**, 则
    1.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>comparefn</var>) 是 **false**，抛出一个 **TypeError** 异常。
    2.  传入 **undefined** 作为 **this** 值，以 <var>x</var> 和 <var>y</var> 作为参数调用 <var>comparefn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

14. 令 <var>xString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>x</var>)。
15. 令 <var>yString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>y</var>)。
16. 如果 <var>xString</var> \< <var>yString</var>，返回 **?1**。
17. 如果 <var>xString</var> \> <var>yString</var>，返回 **1**。
18. 返回 **+0**。

#### Array.prototype.splice (start, deleteCount [ , item1 [ , item2 [ , … ] ] ] )

当以两个或更多参数 <var>start</var>、<var>deleteCount</var> 和（可选的）<var>item1</var>、<var>item2</var>, 等，调用 **splice** 方法，从数组索引 <var>start</var> 开始的 <var>deleteCount</var> 个数组元素会被替换为参数 <var>item1</var>、<var>item2</var>, 等。返回一个包含参数元素（如果有）的数组。采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>A</var> 为 仿佛用表达式 **new Array()** 创建的新数组，这里的 **Array** 是标准内置构造器名。
3.  令 <var>lenVal</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
4.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
5.  令 <var>relativeStart</var> 为 [ToInteger](ES5/conversion#to-integer "wikilink")(<var>start</var>)。
6.  如果 <var>relativeStart</var> 为负，令 <var>actualStart</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")((<var>len</var> + <var>relativeStart</var>),**0**); 否则令 <var>actualStart</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>relativeStart</var>, <var>len</var>)。
7.  令 <var>actualDeleteCount</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")([ToInteger](ES5/conversion#to-integer "wikilink")(<var>deleteCount</var>),**0**),<var>len</var> - <var>actualStart</var>)。
8.  令 <var>k</var> 为 **0**。
9.  只要 <var>k</var> \< <var>actualDeleteCount</var> 就重复
    1.  令 <var>from</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>actualStart</var> + <var>k</var>)。
    2.  令 <var>fromPresent</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>fromPresent</var> 是 **true**，则
        1.  令 <var>fromValue</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>), 属性描述符 {[[Value]]: <var>fromValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}, 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

    4.  <var>k</var> 递增 **1**.

10. 令 <var>items</var> 为一个内部列表，它的元素是实际参数列表中 <var>item1</var> 开始的参数（从左到右的顺序）。如果没传入这些项目，则列表是空的。
11. 令 <var>itemCount</var> 为 <var>items</var> 的元素个数。
12. 如果 <var>itemCount</var> \< <var>actualDeleteCount</var>，则
    1.  令 <var>k</var> 为 <var>actualStart</var>。
    2.  只要 <var>k</var> \< (<var>len</var> - <var>actualDeleteCount</var>) 就重复
        1.  令 <var>from</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> + <var>actualDeleteCount</var>)。
        2.  令 <var>to</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> + <var>itemCount</var>)。
        3.  令 <var>fromPresent</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
        4.  如果 <var>fromPresent</var> 是 **true**，则
            1.  令 <var>fromValue</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
            2.  以 <var>to</var>、<var>fromValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

        5.  否则，<var>fromPresent</var> 是 **false**
            1.  以 <var>to</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

        6.  <var>k</var> 递增 **1**。

    3.  令 <var>k</var> 为 <var>len</var>。
    4.  只要 <var>k</var> \> (<var>len</var> - <var>actualDeleteCount</var> + <var>itemCount</var>) 就重复
        1.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> - **1**) 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。
        2.  <var>k</var> 递减 **1**.

13. 否则如果 <var>itemCount</var> \> <var>actualDeleteCount</var>，则
    1.  令 <var>k</var> 为 (<var>len</var> - <var>actualDeleteCount</var>)。
    2.  只要 <var>k</var> \> <var>actualStart</var> 就重复
        1.  令 <var>from</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> + <var>actualDeleteCount</var> - **1**)。
        2.  令 <var>to</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> + <var>itemCount</var> - **1**)
        3.  令 <var>fromPresent</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
        4.  如果 <var>fromPresent</var> 是 **true**, 则
            1.  令 <var>fromValue</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
            2.  以 <var>to</var>、<var>fromValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

        5.  否则，<var>fromPresent</var> 是 **false**
            1.  以 <var>to</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

        6.  <var>k</var> 递减 **1**。

14. 令 <var>k</var> 为 <var>actualStart</var>。
15. 只要 <var>items</var> 不是空 就重复
    1.  删除 <var>items</var> 的第一个元素，并令 <var>E</var> 为这个元素值。
    2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)、<var>E</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    3.  <var>k</var> 递增 **1**。

16. 以 **"length"**、(<var>len</var> - <var>actualDeleteCount</var> + <var>itemCount</var>) 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
17. 返回 <var>A</var>。

**splice** 方法的 **length** 属性是 **2**。

#### Array.prototype.unshift ( [ item1 [ , item2 [ , … ] ] ] )

将参数们插入到数组的开始位置，它们在数组中的顺序与它们出现在参数列表中的顺序相同。

当以零或更多个参数 <var>item1</var>、<var>item2</var>，等，调用 **unshift** 方法，采用如下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenVal</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenVal</var>)。
4.  令 <var>argCount</var> 为 实际参数的个数。
5.  令 <var>k</var> 为 <var>len</var>。
6.  只要 <var>k</var> \> **0**，就重复
    1.  令 <var>from</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> - **1**)。
    2.  令 <var>to</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var> + <var>argCount</var> - **1**)。
    3.  令 <var>fromPresent</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    4.  如果 <var>fromPresent</var> 是 **true**，则
        1.  令 <var>fromValue</var> 为 以 <var>from</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  以 <var>to</var>、<var>fromValue</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。

    5.  否则，<var>fromPresent</var> 是 <var>false</var>
        1.  以 <var>to</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法。

    6.  <var>k</var> 递减 **1**。

7.  令 <var>j</var> 为 **0**。
8.  令 <var>items</var> 为一个内部列表，它的元素是调用这个函数时传入的实际参数（从左到右的顺序）。
9.  只要 <var>items</var> 不是空，就重复
    1.  删除 <var>items</var> 的第一个元素，并令 <var>E</var> 为这个元素值 .
    2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>j</var>)、<var>E</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    3.  <var>j</var> 递增 **1**。

10. 以 **"length"**、<var>len</var> + <var>argCount</var> 和 **true** 作为参数调用 <var>O</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
11. 返回 <var>len</var> + <var>argCount</var>。

**unshift** 方法的 **length** 属性是 **1**。

#### Array.prototype.indexOf ( searchElement [ , fromIndex ] )

**indexOf** 按照索引的升序比较 <var>searchElement</var> 和数组里的元素们，它使用内部的严格相等比较算法（[11.9.6](ES5/expressions#x11.9.6 "wikilink")），如果找到一个或更多这样的位置，返回这些位置中第一个索引；否则返回 **-1**。

可选的第二个参数 <var>fromIndex</var> 默认是 **0**（即搜索整个数组）。如果它大于或等于数组长度，返回 **-1**，即不会搜索数组。如果它是负的，就把它当作从数组末尾到计算后的 <var>fromIndex</var> 的偏移量。如果计算后的索引小于 **0**，就搜索整个数组。

当用一个或两个参数调用 **indexOf** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 <var>len</var> 是 **0**，返回 **-1**。
5.  如果 传入了参数 <var>fromIndex</var>，则令 <var>n</var> 为 [ToInteger](ES5/conversion#to-integer "wikilink")(<var>fromIndex</var>)；否则令 <var>n</var> 为 **0**。
6.  如果 <var>n</var> ≥ <var>len</var>，返回 **-1**。
7.  如果 <var>n</var> ≥ **0**，则
    1.  令 <var>k</var> 为 <var>n</var>。

8.  否则，<var>n</var> \< **0**
    1.  令 <var>k</var> 为 <var>len</var> - [abs](ES5/notation#abs "wikilink")(<var>n</var>)。
    2.  如果 <var>k</var> 小于 **0**，则令 <var>k</var> 为 **0**。

9.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>kPresent</var> 为 以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    2.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>elementK</var> 为 以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>same</var> 为 对 <var>searchElement</var> 和 <var>elementK</var> 执行[严格相等比较算法的结果](ES5/expressions#x11.9.6 "wikilink")。
        3.  如果 <var>same</var> 是 **true**，返回 <var>k</var>。

    3.  <var>k</var> 递增 **1**。

10. 返回 **-1**。

**indexOf** 方法的 **length** 属性是 **1**。

#### Array.prototype.lastIndexOf ( searchElement [ , fromIndex ] )

**lastIndexOf** 按照索引的降序比较 <var>searchElement</var> 和数组里的元素们，它使用内部的严格相等比较算法 ([11.9.6](ES5/expressions#x11.9.6 "wikilink"))，如果找到一个或更多这样的位置，返回这些位置中最后一个索引；否则返回 **-1**。

可选的第二个参数 <var>fromIndex</var> 默认是数组的长度减一（即搜索整个数组）。如果它大于或等于数组长度，将会搜索整个数组。如果它是负的，就把它当作从数组末尾到计算后的 <var>fromIndex</var> 的偏移量。如果计算后的索引小于 **0**，返回 **-1**。

当用一个或两个参数调用 **lastIndexOf** 方法，采用如下步骤 :

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 <var>len</var> 是 **0**，返回 **-1**。
5.  如果 传入了参数 <var>fromIndex</var>，则令 <var>n</var> 为 [ToInteger](ES5/conversion#to-integer "wikilink")(<var>fromIndex</var>); 否则令 <var>n</var> 为 <var>len</var>。
6.  如果 <var>n</var> ≥ **0**，则令 <var>k</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>n</var>, <var>len</var> - **1**)。
7.  否则，<var>n</var> \< **0**
    1.  令 <var>k</var> 为 <var>len</var> - [abs](ES5/notation#abs "wikilink")(<var>n</var>)。

8.  只要 <var>k</var> ≥ **0** 就重复
    1.  令 <var>kPresent</var> 为 以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    2.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>elementK</var> 为 以 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>) 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>same</var> 为 对 <var>searchElement</var> 和 <var>elementK</var> 执行[严格相等比较算法的结果](ES5/expressions#x11.9.6 "wikilink")。
        3.  如果 <var>same</var> 是 **true**，返回 <var>k</var>。

    3.  <var>k</var> 递减 **1**。

9.  返回 **-1**。

**lastIndexOf** 方法的 **length** 属性是 **1**。

#### Array.prototype.every ( callbackfn [ , thisArg ] )

<var>callbackfn</var> 应该是个函数，它接受三个参数并返回一个可转换为布尔值 **true** 和 **false** 的值。**every** 按照索引的升序，对数组里存在的每个元素调用一次 <var>callbackfn</var>，直到他找到一个使 <var>callbackfn</var> 返回 **false** 的元素。如果找到这样的元素，**every** 马上返回 **false**，否则如果对所有元素 <var>callbackfn</var> 都返回 **true**，**every** 将返回 **true**。<var>callbackfn</var> 只被数组里实际存在的元素调用；它不会被缺少的元素调用。

如果提供了一个 <var>thisArg</var> 参数，它会被当作 **this** 值传给每个 <var>callbackfn</var> 调用。如果没提供它，用 **undefined** 替代。

调用 <var>callbackfn</var> 时将传入三个参数：元素的值，元素的索引，和遍历的对象。

对 **every** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**every** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **every** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**every** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **every** 调用开始后删除的和之前被访问过的元素们是不访问的。**every** 的行为就像数学量词“所有（for all）”。特别的，对一个空数组，它返回 **true**。

当以一个或两个参数调用 **every** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**，抛出一个 **TypeError** 异常。
5.  如果提供了 <var>thisArg</var>，令 <var>T</var> 为 <var>thisArg</var>；否则令 <var>T</var> 为 **undefined**。
6.  令 <var>k</var> 为 **0**。
7.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果 .
        2.  令 <var>testResult</var> 为 以 <var>T</var> 作为 **this** 值以包含 <var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。
        3.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>testResult</var>) 是 **false**，返回 **false**。

    4.  <var>k</var> 递增 **1**。

8.  返回 **true**。

**every** 方法的 **length** 属性是 **1**。

#### Array.prototype.some ( callbackfn [ , thisArg ] )

<var>callbackfn</var> 应该是个函数，它接受三个参数并返回一个可转换为布尔值 **true** 和 **false** 的值。**some** 按照索引的升序，对数组里存在的每个元素调用一次 <var>callbackfn</var>，直到他找到一个使 <var>callbackfn</var> 返回 **true** 的元素。如果找到这样的元素，**some** 马上返回 **true**，否则，**some** 返回 **false**。<var>callbackfn</var> 只被实际存在的数组元素调用；它不会被缺少的数组元素调用。

如果提供了一个 <var>thisArg</var> 参数，它会被当作 **this** 值传给每个 <var>callbackfn</var> 调用。如果没提供它，用 **undefined** 替代。

调用 <var>callbackfn</var> 时将传入三个参数：元素的值，元素的索引，和遍历的对象。

对 **some** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**some** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **some** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**some** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **some** 调用开始后删除的和之前被访问过的元素们是不访问的。**some** 的行为就像数学量词“存在（exists）”。特别的，对一个空数组，它返回 **false**。

当以一个或两个参数调用 **some** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**, 抛出一个 **TypeError** 异常。
5.  如果提供了 <var>thisArg</var>，令 <var>T</var> 为 <var>thisArg</var>；否则令 <var>T</var> 为 **undefined**。
6.  令 <var>k</var> 为 **0**。
7.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>testResult</var> 为 以 <var>T</var> 作为 **this** 值以包含 <var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。
        3.  如果 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>testResult</var>) 是 **true**，返回 **true**。

    4.  <var>k</var> 递增 **1**。

8.  返回 **false**。

**some** 方法的 **length** 属性是 **1**。

#### Array.prototype.forEach ( callbackfn [ , thisArg ] )

<var>callbackfn</var> 应该是个函数，它接受三个参数。**forEach** 按照索引的升序，对数组里存在的每个元素调用一次 <var>callbackfn</var>。<var>callbackfn</var> 只被实际存在的数组元素调用；它不会被缺少的数组元素调用。

如果提供了一个 <var>thisArg</var> 参数，它会被当作 **this** 值传给每个 <var>callbackfn</var> 调用。如果没提供它，用 **undefined** 替代。

调用 <var>callbackfn</var> 时将传入三个参数：元素的值，元素的索引，和遍历的对象。

对 **forEach** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**forEach** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **forEach** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**forEach** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **forEach** 调用开始后删除的和之前被访问过的元素们是不访问的。

当以一个或两个参数调用 **forEach** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**，抛出一个 **TypeError** 异常。
5.  如果提供了 <var>thisArg</var>，令 <var>T</var> 为 <var>thisArg</var>；否则令 <var>T</var> 为 **undefined**。
6.  令 <var>k</var> 为 **0**。
7.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  以 <var>T</var> 作为 **this** 值以包含 <var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 callbackfn 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法。

    4.  <var>k</var> 递增 **1**。

8.  返回 **undefined**。

**forEach** 方法的 **length** 属性是 **1**。

#### Array.prototype.map ( callbackfn [ , thisArg ] )

<var>callbackfn</var> 应该是个函数，它接受三个参数。**map** 按照索引的升序，对数组里存在的每个元素调用一次 <var>callbackfn</var>，并用结果构造一个新数组。<var>callbackfn</var> 只被实际存在的数组元素调用；它不会被缺少的数组元素调用。

如果提供了一个 <var>thisArg</var> 参数，它会被当作 **this** 值传给每个 <var>callbackfn</var> 调用。如果没提供它，用 **undefined** 替代。

调用 <var>callbackfn</var> 时将传入三个参数：元素的值，元素的索引，和遍历的对象。

对 **map** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**map** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **map** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**map** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **map** 调用开始后删除的和之前被访问过的元素们是不访问的。

当以一个或两个参数调用 **map** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**，抛出一个 **TypeError** 异常。
5.  如果提供了 <var>thisArg</var>，令 <var>T</var> 为 <var>thisArg</var>；否则令 <var>T</var> 为 **undefined**。
6.  令 <var>A</var> 为 仿佛用 **new Array(**<var>len</var>**)** 创建的新数组，这里的 **Array** 是标准内置构造器名，<var>len</var> 是 <var>len</var> 的值。
7.  令 <var>k</var> 为 **0**。
8.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>mappedValue</var> 为 以 <var>T</var> 作为 **this** 值以包含 <var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。
        3.  以 <var>Pk</var>，属性描述符 {[[Value]]: <var>mappedValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。

    4.  <var>k</var> 递增 **1**。

9.  返回 <var>A</var>。

**map** 方法的 **length** 属性是 **1**。

#### Array.prototype.filter ( callbackfn [ , thisArg ] )

<var>callbackfn</var> 应该是个函数，它接受三个参数并返回一个可转换为布尔值 **true** 和 **false** 的值。**filter** 按照索引的升序，对数组里存在的每个元素调用一次 <var>callbackfn</var>，并用使 <var>callbackfn</var> 返回 **true** 的所有值构造一个新数组。<var>callbackfn</var> 只被实际存在的数组元素调用；它不会被缺少的数组元素调用。

如果提供了一个 <var>thisArg</var> 参数，它会被当作 **this** 值传给每个 <var>callbackfn</var> 调用。如果没提供它，用 **undefined** 替代。

调用 <var>callbackfn</var> 时将传入三个参数：元素的值，元素的索引，和遍历的对象。

对 **filter** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**filter** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **filter** 调用开始后追加到数组里的元素们不会被 callbackfn 访问。如果更改以存在数组元素，**filter** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **filter** 调用开始后删除的和之前被访问过的元素们是不访问的。

当以一个或两个参数调用 **filter** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#to-object "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**, 抛出一个 **TypeError** 异常。
5.  如果提供了 <var>thisArg</var>，令 <var>T</var> 为 <var>thisArg</var>；否则令 T 为 **undefined**。
6.  令 <var>A</var> 为 仿佛用 **new Array()** 创建的新数组，这里的 **Array** 是标准内置构造器名。
7.  令 <var>k</var> 为 **0**。
8.  令 <var>to</var> 为 **0**。
9.  只要 <var>k</var> \< <var>len</var>，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 <var>true</var>，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>selected</var> 为 以 <var>T</var> 作为 **this** 值以包含 <var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。
        3.  如果 [ToBoolean](ES5/conversion#ToBoolean "wikilink")(<var>selected</var>) 是 **true**，则
            1.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>to</var>)，属性描述符 {[[Value]]: <var>kValue</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
            2.  <var>to</var> 递增 **1**。

    4.  <var>k</var> 递增 **1**。

10. 返回 <var>A</var>。

**filter** 方法的 **length** 属性是 **1**。

#### Array.prototype.reduce ( callbackfn [ , initialValue ] )

<var>callbackfn</var> 应该是个函数，它需要四个参数。**reduce** 按照索引的升序，对数组里存在的每个元素，将 <var>callbackfn</var> 作为回调函数调用一次。

调用 <var>callbackfn</var> 时将传入四个参数：<var>previousValue</var>（<var>initialValue</var> 的值或上次调用 <var>callbackfn</var> 的返回值）、<var>currentValue</var>（当前元素值）、<var>currentIndex</var> 和<var>遍历的对象</var>。第一次调用回调函数时，<var>previousValue</var> 和 <var>currentValue</var> 的取值可以是下面两种情况之一。如果为 **reduce** 调用提供了一个 <var>initialValue</var>，则 <var>previousValue</var> 将等于 <var>initialValue</var> 并且 <var>currentValue</var> 将等于数组的首个元素值。如果没提供 <var>initialValue</var>，则 <var>previousValue</var> 将等于数组的首个元素值并且 <var>currentValue</var> 将等于数组的第二个元素值。如果数组里没有元素并且没有提供 <var>initialValue</var>，则抛出一个 **TypeError** 异常。

对 **reduce** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**reduce** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **reduce** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**reduce** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **reduce** 调用开始后删除的和之前被访问过的元素们是不访问的。

当以一个或两个参数调用 **reduce** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**，抛出一个 **TypeError** 异常。
5.  如果 <var>len</var> 是 **0** 并且 <var>initialValue</var> 不是 <var>present</var>，抛出一个 **TypeError** 异常。
6.  令 <var>k</var> 为 **0**。
7.  如果 <var>initialValue</var> 参数有传入值，则
    1.  设定 <var>accumulator</var> 为 <var>initialValue</var>。

8.  否则，<var>initialValue</var> 参数没有传入值
    1.  令 <var>kPresent</var> 为 **false**。
    2.  只要 <var>kPresent</var> 是 **false** 并且 <var>k</var> \< <var>len</var>，就重复
        1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
        2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
        3.  如果 <var>kPresent</var> 是 **true**，则
            1.  令 <var>accumulator</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。

        4.  <var>k</var> 递增 **1**.

    3.  如果 <var>kPresent</var> 是 **false**，抛出一个 **TypeError** 异常。

9.  只要 <var>k</var> \< <var>len</var>，重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>accumulator</var> 为 以 **undefined** 作为 **this** 值并以包含 <var>accumulator</var>、<var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

    4.  <var>k</var> 递增 **1**。

10. 返回 <var>accumulator</var>。

**reduce** 方法的 **length** 属性是 **1**。

#### Array.prototype.reduceRight ( callbackfn [ , initialValue ] )

<var>callbackfn</var> 应该是个函数，它需要四个参数。**reduceRight** 按照索引的升序，对数组里存在的每个元素 , 将 <var>callbackfn</var> 作为回调函数调用一次。

调用 <var>callbackfn</var> 时将传入四个参数：<var>previousValue</var>（<var>initialValue</var> 的值或上次调用 <var>callbackfn</var> 的返回值），<var>currentValue</var>（当前元素值），<var>currentIndex</var> 和<var>遍历的对象</var>。第一次调用回调函数时，<var>previousValue</var> 和 <var>currentValue</var> 的取值可以是下面两种情况之一。如果为 **reduceRight** 调用提供了一个 <var>initialValue</var>，则 <var>previousValue</var> 将等于 <var>initialValue</var> 并且 <var>currentValue</var> 将等于数组的最后一个元素值。如果没提供 <var>initialValue</var>，则 <var>previousValue</var> 将等于数组的最后一个元素值并且 <var>currentValue</var> 将等于数组的倒数第二个元素值。如果数组里没有元素并且没有提供 <var>initialValue</var>，则抛出一个 **TypeError** 异常。

对 **reduceRight** 的调用不直接更改对象，但是对 <var>callbackfn</var> 的调用可能更改对象。

**reduceRight** 处理的元素范围是在首次调用 <var>callbackfn</var> 之前设定的。在 **reduceRight** 调用开始后追加到数组里的元素们不会被 <var>callbackfn</var> 访问。如果更改以存在数组元素，**reduceRight** 访问这些元素时的值会传给 <var>callbackfn</var>；在 **reduceRight** 调用开始后删除的和之前被访问过的元素们是不访问的。

当以一个或两个参数调用 **reduceRight** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值作为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
2.  令 <var>lenValue</var> 为 以 **"length"** 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
3.  令 <var>len</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>lenValue</var>)。
4.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>callbackfn</var>) 是 **false**，抛出一个 **TypeError** 异常。
5.  如果 <var>len</var> 是 **0** 并且 <var>initialValue</var> 不是 <var>present</var>，抛出一个 **TypeError** 异常。
6.  令 <var>k</var> 为 **0**。
7.  如果 <var>initialValue</var> 参数有传入值，则
    1.  设定 <var>accumulator</var> 为 <var>initialValue</var>。

8.  否则，<var>initialValue</var> 参数没有传入值
    1.  令 <var>kPresent</var> 为 **false**。
    2.  只要 <var>kPresent</var> 是 **false** 并且 <var>k</var> ≥ **0**，就重复
        1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
        2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
        3.  如果 <var>kPresent</var> 是 **true**，则
            1.  令 <var>accumulator</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。

        4.  <var>k</var> 递减 **1**。

    3.  如果 <var>kPresent</var> 是 **false**，抛出一个 **TypeError** 异常。

9.  只要 <var>k</var> ≥ **0**，就重复
    1.  令 <var>Pk</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>k</var>)。
    2.  令 <var>kPresent</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[HasProperty]]](ES5/types#HasProperty "wikilink") 内部方法的结果。
    3.  如果 <var>kPresent</var> 是 **true**，则
        1.  令 <var>kValue</var> 为 以 <var>Pk</var> 作为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        2.  令 <var>accumulator</var> 为 以 **undefined** 作为 **this** 值并以包含 <var>accumulator</var>、<var>kValue</var>、<var>k</var> 和 <var>O</var> 的参数列表调用 <var>callbackfn</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。

    4.  <var>k</var> 递减 **1**.

10. 返回 <var>accumulator</var>。

**reduceRight** 方法的 **length** 属性是 **1**。

### Array 实例的属性

**Array** 实例从数组原型对象继承属性，**Array** 实例的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"Array"**。**Array** 实例还有以下属性。

#### [[DefineOwnProperty]] ( P, Desc, Throw )

数组对象使用一个，用在其他原生 ECMAscript 对象的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink")) 的变化版。

设 <var>A</var> 为一个数组对象，<var>Desc</var> 为一个属性描述符，<var>Throw</var> 为一个布尔标示。

在以下算法中，术语“**拒绝**”指代“如果 <var>Throw</var> 是 **true**，则抛出 **TypeError** 异常，否则返回 **false**。

当用属性名 <var>P</var>、属性描述 <var>Desc</var>、布尔值 <var>Throw</var> 调用 <var>A</var> 的 **[[DefineOwnProperty]]** 内部方法，采用以下步骤：

1.  令 <var>oldLenDesc</var> 为 以 **"length"** 作为参数调用 <var>A</var> 的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。 结果绝不会是 **undefined** 或一个访问器描述符，因为在创建数组时的 **length** 是一个不可删除或重新配置的数据属性。
2.  令 <var>oldLen</var> 为 <var>oldLenDesc</var>.[[[Value]]](ES5/types#Value "wikilink")。
3.  如果 <var>P</var> 是 **"length"**, 则
    1.  如果 <var>Desc</var> 的 [[[Value]]](ES5/types#Value "wikilink") 字段不存在 , 则
        1.  以 **"length"**、<var>Desc</var>、和 <var>Throw</var> 作为参数在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink"))，返回结果。

    2.  令 <var>newLenDesc</var> 为 <var>Desc</var> 的一个拷贝。
    3.  令 <var>newLen</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>Desc</var>.[[[Value]]](ES5/types#Value "wikilink"))。
    4.  如果 <var>newLen</var> 不等于 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>Desc</var>.[[[Value]]](ES5/types#Value "wikilink"))，抛出一个 **RangeError** 异常。
    5.  设定 <var>newLenDesc</var>.[[[Value]]](ES5/types#Value "wikilink") 为 <var>newLen</var>。
    6.  如果 <var>newLen</var> ≥ <var>oldLen</var>，则
        1.  以 **"length"**、<var>newLenDesc</var> 和 <var>Throw</var> 作为参数在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink"))，返回结果。

    7.  如果 <var>oldLenDesc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 是 **false**，**拒绝**
    8.  如果 <var>newLenDesc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 不存在或值是 **true**，令 <var>newWritable</var> 为 **true**。
    9.  否则，
        1.  因为它将使得无法删除任何元素，所以需要延后设定 [[[Writable]]](ES5/types#Writable "wikilink") 特性为 **false**。
        2.  令 <var>newWritable</var> 为 **false**。
        3.  设定 <var>newLenDesc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 为 **true**。

    10. 令 <var>succeeded</var> 为 以 **"length"**、<var>newLenDesc</var> 和 <var>Throw</var> 作为参数在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink")) 的结果
    11. 如果 <var>succeeded</var> 是 **false**，返回 **false**。
    12. 只要 <var>newLen</var> \< <var>oldLen</var>，就重复，
        1.  设定 <var>oldLen</var> 为 <var>oldLen</var> – **1**。
        2.  令 <var>deleteSucceeded</var> 为 以 [ToString](ES5/conversion#ToString "wikilink")(<var>oldLen</var>) 和 **false** 作为参数调用 <var>A</var> 的 [[[Delete]]](ES5/types#Delete "wikilink") 内部方法的结果。
        3.  如果 <var>deleteSucceeded</var> 是 **false**，则
            1.  设定 <var>newLenDesc</var>.[[[Value]]](ES5/types#Value "wikilink") 为 <var>oldLen</var> + **1**。
            2.  如果 <var>newWritable</var> 是 **false**，设定 <var>newLenDesc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 为 **false**。
            3.  以 **"length"**、<var>newLenDesc</var> 和 **false** 为参数在 <var>A</var> 上调用默认的 [[DefineOwnProperty]] 内部方法。
            4.  **拒绝**。

    13. 如果 <var>newWritable</var> 是 **false**，则
        1.  以 **"length"**，属性描述符 {[[Writable]]: **false**} 和 **false** 作为参数在 <var>A</var> 上调用 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。这个调用始终返回 **true**。

    14. 返回 **true**。

4.  否则如果 <var>P</var> 是一个数组索引 ([15.4](ES5/builtins#x15.4 "wikilink"))，则
    1.  令 <var>index</var> 为 [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>P</var>)。
    2.  如果 <var>index</var> ≥ <var>oldLen</var> 并且 <var>oldLenDesc</var>.[[[Writable]]](ES5/types#Writable "wikilink") 是 **false**，**拒绝**。
    3.  令 <var>succeeded</var> 为 以 <var>P</var>、<var>Desc</var> 和 **false** 作为参数在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink")) 的结果。
    4.  如果 <var>succeeded</var> 是 **false**，**拒绝**。
    5.  如果 <var>index</var> ≥ <var>oldLen</var>
        1.  设定 <var>oldLenDesc</var>.[[[Value]]](ES5/types#Value "wikilink") 为 <var>index</var> + **1**。
        2.  以 "**length"**、<var>oldLenDesc</var> 和 **false** 作为参数在在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。这个调用始终返回 **true**。

    6.  返回 **true**。

5.  以 <var>P</var>、<var>Desc</var> 和 <var>Throw</var> 作为参数在在 <var>A</var> 上调用默认的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 ([8.12.9](ES5/types#DefineOwnProperty "wikilink"))，返回结果。

#### length

数组对象的 **length** 属性是个数据属性，其值总是在数值上大于任何属性名是数组索引的可删除属性的属性名。

**length** 属性拥有的初始特性是 { [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

String 对象
-----------

### 作为函数调用 String 构造器

当将 **String** 作为函数调用，而不是作为构造器，它执行一个类型转换。

#### String ( [ value ] )

返回一个由 [ToString](ES5/conversion#ToString "wikilink")(<var>value</var>) 计算出的字符串值（不是 **String** 对象）。如果没有提供 <var>value</var>，返回空字符串 ""。

### String 构造器

当 **String** 作为一个 [new](ES5/expressions#x11.2.2 "wikilink") 表达式的一部分被调用，它是个构造器：它初始化新创建的对象。

#### new String ( [ value ] )

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为标准内置的字符串原型对象，它是 [String.prototype](ES5/builtins#x15.5.3.1 "wikilink") 的初始值 ([15.5.3.1](ES5/builtins#x15.5.3.1 "wikilink"))。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"String"**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **true**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性设定为 [ToString](ES5/conversion#ToString "wikilink")(<var>value</var>)，或如果没提供 <var>value</var> 则设定为空字符串。

### String 构造器的属性

**String** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值是标准的内置 [Function 原型对象](ES5/builtins#x15.3.4 "wikilink")。

除了内部属性和 **length** 属性（值为 **1**）之外，**String** 构造器还有以下属性：

#### String.prototype

**String.prototype** 的初始值是标准的内置 [String 原型对象](ES5/builtins#x15.5.4 "wikilink")。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### String.fromCharCode ( [ char0 [ , char1 [ , … ] ] ] )

返回一个字符串值，包含的字符数与参数数目相同。每个参数指定返回字符串中的一个字符，也就是说第一个参数第一个字符，以此类推（从左到右）。一个参数转换为一个字符，通过先应用 [ToUint16](ES5/conversion#to-uint16 "wikilink") 操作，再将返回的16位整数看作字符的代码单元值。如果没提供参数，返回空字符串。

**fromCharCode** 函数的 **length** 属性是 **1**。

### 字符串原型对象的属性

字符串原型对象本身是一个值为空字符串的 **String** 对象（它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"String"**）。

字符串原型对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准的内置 [Object 原型对象](ES5/builtins#x15.2.4 "wikilink")。

#### String.prototype.constructor

**String.prototype.constructor** 的初始值是内置 **String** 构造器。

#### String.prototype.toString ( )

返回 **this** 字符串值。（注，对于一个 **String** 对象，**toString** 方法和 **valueOf** 方法返回相同值。）

**toString** 函数是**非通用**的；如果它的 **this** 值不是一个字符串或字符串对象，则抛出一个 **TypeError** 异常。因此它不能作为方法转移到其他类型对象上。

#### String.prototype.valueOf ( )

返回 **this** 字符串值。

**valueOf** 函数是**非通用**的；如果它的 **this** 值不是一个字符串或字符串对象，则抛出一个 **TypeError** 异常。因此它不能作为方法转移到其他类型对象上。

#### String.prototype.charAt (pos)

将 **this** 对象转换为一个字符串，返回包含了这个字符串 <var>pos</var> 位置的字符的字符串。如果那个位置没有字符，返回空字符串。返回结果是个**字符串值**，不是字符串对象。

如果 <var>pos</var> 是一个数字类型的整数值，则 <var>x</var>.**charAt**(<var>pos</var>) 与 <var>x</var>.**substring**(<var>pos</var>, <var>pos</var> + **1**) 的结果相等。

当用一个参数 <var>pos</var> 调用 **charAt** 方法，采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>position</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>pos</var>)。
4.  令 <var>size</var> 为 <var>S</var> 的字符数。
5.  如果 <var>position</var> \< **0** 或 <var>position</var> ≥ <var>size</var>，返回空字符串。
6.  返回一个长度为 **1** 的字符串，它包含 <var>S</var> 中 <var>position</var> 位置的一个字符，在这里 <var>S</var> 中的第一个（最左边）字符被当作是在位置 **0**，下一个字符被当作是在位置 **1**，等等。

#### String.prototype.charCodeAt (pos)

将 **this** 对象转换为一个字符串，返回一个代表这个字符串 <var>pos</var> 位置字符的代码单元值的数字（小于 **2<sup>16</sup>** 的非负整数）。如果那个位置没有字符，返回 **NaN**。

当用一个参数 <var>pos</var> 调用 **charCodeAt** 方法，采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>position</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>pos</var>)。
4.  令 <var>size</var> 为 <var>S</var> 的字符数。
5.  如果 <var>position</var> \< **0** 或 <var>position</var> ≥ <var>size</var>，返回 **NaN**.
6.  返回一个数字类型值，值是字符串 <var>S</var> 中 <var>position</var> 位置字符的代码单元值。 在这里 <var>S</var> 中的第一个（最左边）字符被当作是在位置 **0**，下一个字符被当作是在位置 **1**，等等。

#### String.prototype.concat ( [ string1 [ , string2 [ , … ] ] ] )

当用一个或更多参数 <var>string1</var>、<var>string2</var>，等，调用 **concat** 方法，它返回一个字符串，其中包含了转换成字符串类型的 **this** 对象中的所有字符和后面跟着的每个参数（例如：<var>string1</var>、<var>string2</var>，等）转换成字符串类型后里面的所有字符。返回结果是一个字符串值，不是一个字符串对象。采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>args</var> 为一个内部列表，它是传给这个函数的参数列表的拷贝。
4.  令 <var>R</var> 为 <var>S</var>。
5.  只要 <var>args</var> 不是空，就重复
    1.  删除 <var>args</var> 的第一个元素，并令 <var>next</var> 为这个元素。
    2.  令 <var>R</var> 为一个包含了 <var>R</var> 中原有的所有字符跟上 [ToString](ES5/conversion#ToString "wikilink")(<var>next</var>) 中的所有字符 的字符串值。

6.  返回 <var>R</var>。

**concat** 方法的 **length** 属性是 **1**.

#### String.prototype.indexOf (searchString, position)

将 **this** 对象转换为一个字符串，如果 <var>searchString</var> 在这个字符串里大于或等于 <var>position</var> 的位置中的一个或多个位置使它呈现为字符串的子串，那么返回这些位置中最小的索引；否则返回 **-1**。如果 <var>position</var> 是 **undefined**，就认为它是 **0**，以搜索整个字符串。

**indexOf** 需要两个参数 <var>searchString</var> 和 <var>position</var>，执行以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 S 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>searchStr</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>searchString</var>)。
4.  令 <var>pos</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>position</var>)。（如果 <var>position</var> 是 **undefined**，此步骤产生 **0**）。
5.  令 <var>len</var> 为 <var>S</var> 的字符数。
6.  令 <var>start</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")(<var>pos</var>, **0**), <var>len</var>)。
7.  令 <var>searchLen</var> 为 <var>SearchStr</var> 的字符数。
8.  返回 一个不小于 <var>start</var> 的可能的最小值整数 <var>k</var>，使得 <var>k</var> + <var>searchLen</var> 不大于 <var>len</var>，并且对所有小于 <var>searchLen</var> 的非负数整数 <var>j</var>、<var>S</var> 的 <var>k</var> + <var>j</var> 位置字符和 <var>searchStr</var> 的 <var>j</var> 位置字符相同；但如果没有这样的整数 <var>k</var>，则返回 **-1**。

**indexOf** 的 **length** 属性是 **1**。

#### String.prototype.lastIndexOf (searchString, position)

将 **this** 对象转换为一个字符串，如果 <var>searchString</var> 在这个字符串里小于或等于 <var>position</var> 的位置中的一个或多个位置使它呈现为字符串的子串，那么返回这些位置中最大的索引；否则返回 **-1**。如果 <var>position</var> 是 **undefined** ，就认为它是字符串值的长度，以搜索整个字符串。

<var>lastIndexOf</var> 需要两个参数 <var>searchString</var> 和 <var>position</var>，执行以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>searchStr</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>searchString</var>)。
4.  令 <var>numPos</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>position</var>)。( 如果 <var>position</var> 是 **undefined**，此步骤产生 **NaN**)。
5.  如果 <var>numPos</var> 是 **NaN**，令 <var>pos</var> 为 **+∞**；否则，令 <var>pos</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>numPos</var>)。
6.  令 <var>len</var> 为 <var>S</var> 的字符数。
7.  令 <var>start</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")(<var>pos</var>, **0**), **len**)。
8.  令 <var>searchLen</var> 为 <var>SearchStr</var> 的字符数。
9.  返回 一个不大于 <var>start</var> 的可能的最大值整数 <var>k</var>，使得 <var>k</var> + <var>searchLen</var> 不大于 <var>len</var>，并且对所有小于 <var>searchLen</var> 的非负数整数 <var>j</var>，<var>S</var> 的 <var>k</var> + <var>j</var> 位置字符和 <var>searchStr</var> 的 <var>j</var> 位置字符相同；但如果没有这样的整数 <var>k</var>，则返回 **-1**。。

**lastIndexOf** 的 **length** 属性是 **1**。

#### String.prototype.localeCompare (that)

当以一个参数 <var>that</var> 来调用 **localeCompare** 方法，它返回一个非 **NaN** 数字值，这个数字值反应了对 **this** 值（转换为字符串）和 <var>that</var> 值（转换为字符串）进行语言环境敏感的字符串比较的结果。两个字符串 <var>S</var> 和 <var>That</var> 用实现定义的一种方式进行比较。比较结果是按照系统默认语言环境指定的顺序来排列字符串。根据这三种情况：<var>S</var> 在 <var>That</var> 前面、两字符串相同、<var>S</var> 在 <var>That</var> 后面，分别返回：负数、零、正数。

在执行比较之前执行以下步骤以预备好字符串：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 S 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>That</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>that</var>)。

如果将 **localeCompare** 方法看做是将 <var>this</var> 和 <var>that</var> 作为两个参数的函数，那么它是在所有字符串集合上的保持一致的比较函数（在 [15.4.4.11](ES5/builtins#x15.4.4.11 "wikilink") 定义）。

实际返回值是实现定义的，允许实现者们在返回值里编码附加信息。但是函数需要定义一个在所有字符串上的总的顺序。并且，当比较的字符串们被认为是 Unicode 标准定义的标准等价，则返回 **0**。

如果宿主环境没有在所有字符串上语言敏感的比较，此函数可执行按位比较。

#### String.prototype.match (regexp)

当以 <var>regexp</var> 作为参数调用 **match** 方法，采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  如果 [Type](ES5/types#Type "wikilink")(<var>regexp</var>) 是 **Object** 并且 <var>regexp</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性的值是 **"RegExp"**，则令 <var>rx</var> 为 <var>regexp</var>；
4.  否则，令 <var>rx</var> 为 仿佛是用表达式 **new RegExp(**<var>regexp</var>**)** 创建的新正则对象，这里的 **RegExp** 是标准内置构造器名。
5.  令 <var>global</var> 为 以 **"global"** 为参数调用 <var>rx</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
6.  令 <var>exec</var> 为 标准内置函数 **RegExp.prototype.exec** ( 见 [15.10.6.2](ES5/builtins#x15.10.6.2 "wikilink"))
7.  如果 <var>global</var> 不是 **true**，则
    1.  以 <var>rx</var> 作为 **this** 值，用包含 <var>S</var> 的参数列表调用 <var>exec</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

8.  否则，<var>global</var> 是 **true**
    1.  以 **"lastIndex"** 和 **0** 作为参数调用 <var>rx</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
    2.  令 <var>A</var> 为 仿佛是用表达式 **new Array()** 创建的新数组，这里的 **Array** 是标准内置构造器名。
    3.  令 <var>previousLastIndex</var> 为 **0**。
    4.  令 <var>n</var> 为 **0**。
    5.  令 <var>lastMatch</var> 为 **true**。
    6.  只要 <var>lastMatch</var> 是 **true**，就重复
        1.  令 <var>result</var> 为 以 <var>rx</var> 作为 **this** 值，用包含 <var>S</var> 的参数列表调用 <var>exec</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法的结果。
        2.  如果 <var>result</var> 是 **null**，则设定 <var>lastMatch</var> 为 **false**。
        3.  否则，<var>result</var> 不是 **null**
            1.  令 <var>thisIndex</var> 为 以 **"lastIndex"** 为参数调用 <var>rx</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
            2.  如果 <var>thisIndex</var> = <var>previousLastIndex</var> 则
                1.  以 **"lastIndex"** 和 <var>thisIndex</var> + **1** 为参数调用 <var>rx</var> 的 [[[Put]]](ES5/types#Put "wikilink") 内部方法。
                2.  设定 <var>previousLastIndex</var> 为 <var>thisIndex</var> + **1**。

            3.  否则，设定 <var>previousLastIndex</var> 为 <var>thisIndex</var>。
            4.  令 <var>matchStr</var> 为 以 **0** 为参数调用 <var>result</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
            5.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>n</var>)，属性描述符 {[[Value]]: <var>matchStr</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
            6.  <var>n</var> 递增 **1**。

    7.  如果 <var>n</var> = **0**，则返回 **null**。
    8.  返回 <var>A</var>。

#### String.prototype.replace (searchValue, replaceValue)

首先根据以下步骤设定 <var>string</var>：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>string</var> 为 以 **this** 值作为为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。

如果 <var>searchValue</var> 是一个正则表达式（[[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"RegExp"** 的对象），按照如下执行：如果 <var>searchValue</var>.**global** 是 **false**，则搜索 <var>string</var>，找出匹配正则表达式 <var>searchValue</var> 的第一个子字符串。如果 <var>searchValue</var>.**global** 是 **true**，则搜索 <var>string</var>，找出匹配正则表达式 <var>searchValue</var> 的所有子字符串。搜索的做法与 **String.prototype.match** 相同，包括对 <var>searchValue</var>.**lastIndex** 的更新。令 <var>m</var> 为 <var>searchValue</var> 的左捕获括号的个数（使用 [15.10.2.1](ES5/builtins#x15.10.2.1 "wikilink") 指定的 **NcapturingParens**）。

如果 <var>searchValue</var> 不是正则表达式，令 <var>searchString</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>searchValue</var>)，并搜索 <var>string</var>，找出第一个出现的 <var>searchString</var> 的子字符串。令 <var>m</var> 为 **0**。

如果 <var>replaceValue</var> 是函数，则对每个匹配的子字符串，以 <var>m</var> + **3** 个参数调用这个函数。第一个参数是匹配的子字符串。如果 <var>searchValue</var> 是正则表达式，接下来 <var>m</var> 个参数是 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink") 里的所有捕获值。第 <var>m</var> + **2** 个参数是发生的匹配在 <var>string</var> 里的偏移量，第 <var>m</var> + **3** 个参数是 <var>string</var>。结果是将输入的原字符串里的每个匹配子字符串替换为相应函数调用的返回值（必要的情况下转换为字符串）得到的字符串。

否则，令 <var>newstring</var> 表示 <var>replaceValue</var> 转换为字符串的结果。结果是将输入的原字符串里的每个匹配子字符串替换为 <var>newstring</var> 里的字符根据**表22**指定的替代文本替换得到的字符串。替换这些 **\$** 是由左到右进行的，并且一旦执行了这样的替换，新替换的文本不受进一步替换。例如 ，**"\$1,\$2".replace(/(\\\$(\\d))/g, "\$\$1-\$1\$2")** 返回 **"\$1-\$11,\$1-\$22"**。<var>newstring</var> 里的一个 **\$** ，如果不符合以下任何格式，就保持原状。

|字符|替代文本|
|----|--------|
|\$\$|\$|
|\$&|匹配到的子字符串|
|\$\` {{extra note|字符\\u0060，键盘上ESC下面那个键。}}|string 中匹配到的子字符串之前部分。|
|\$' {{extra note|字符\\u0027，单引号。}}|string 中匹配到的子字符串之后部分。|
|\$n|第 <var>n</var> 个捕获结果，<var>n</var> 是范围在 **1** 到 **9** 的单个数字，并且紧接着 <var>\$n</var> 后面的不是十进制数字。如果 **n** ≤ **m** 且第 **n** 个捕获结果是 **undefined**，就用空字符串代替。如果 <var>n</var> \> <var>m</var>，结果是实现定义的。|
|\$nn|第 <var>nn</var> 个捕获结果，<var>nn</var> 是范围在 **01** 到 **99** 的十进制两位数。如果 <var>nn</var> ≤ <var>m</var> 且第 <var>nn</var> 个捕获结果是 **undefined**，就用空字符串代替。如果 <var>nn</var> \> <var>m</var>，结果是实现定义的。|

#### String.prototype.search (regexp)

当用参数 <var>regexp</var> 调用 **search** 方法，采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>string</var> 为 以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  如果 [Type](ES5/types#Type "wikilink")(<var>regexp</var>) 是 **Object** 且 <var>regexp</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性的值是 **"RegExp"**, 则令 <var>rx</var> 为 <var>regexp</var>；
4.  否则，令 <var>rx</var> 为仿佛是用表达式 **new RegExp(**<var>regexp</var>**)** 创建的新正则对象，这里的 **RegExp** 是标准内置构造器名。
5.  从 <var>string</var> 开始位置搜索正则表达式模式 <var>rx</var> 的匹配。如果找到匹配，令 <var>result</var> 为匹配在 <var>string</var> 里的偏移量；如果没有找到匹配，令 <var>result</var> 为 **-1**。执行搜索时 <var>regexp</var> 的 **lastIndex** 和 **global** 属性是被忽略的。<var>regexp</var> 的 **lastIndex** 属性保持不变。
6.  返回 <var>result</var>。

#### String.prototype.slice (start, end)

<var>slice</var> 方法需要两个参数 <var>start</var> 和 <var>end</var>，将 **this** 对象转换为一个字符串，返回这个字符串中从 <var>start</var> 位置的字符到（但不包含）<var>end</var> 位置的字符的一个子字符串（或如果 <var>end</var> 是 **undefined**，就直接到字符串尾部）。用 <var>sourceLength</var> 表示字符串长度，如果 <var>start</var> 是负数，就把它看做是 <var>sourceLength</var> + <var>start</var>；如果 <var>end</var> 是负数，就把它看做是 <var>sourceLength</var> + <var>end</var>。返回结果是一个字符串值，不是字符串对象。采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>len</var> 为 <var>S</var> 的字符数 .
4.  令 <var>intStart</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>start</var>)。
5.  如果 <var>end</var> 是 **undefined**，令 <var>intEnd</var> 为 <var>len</var>；否则 令 <var>intEnd</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>end</var>)。
6.  如果 <var>intStart</var> 是 <var>negative</var>，令 <var>from</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")(<var>len</var> + <var>intStart</var> , **0**)；否则 令 <var>from</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>intStart</var> , <var>len</var>)。
7.  如果 <var>intEnd</var> 是 <var>negative</var>，令 <var>to</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")(<var>len</var> + <var>intEnd</var>, **0**)；否则 令 <var>to</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>intEnd</var>，<var>len</var>)。
8.  令 <var>span</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")(<var>to</var> - <var>from</var>, **0** )。
9.  返回 一个包含 <var>S</var> 中 <var>form</var> 位置的字符开始的 <var>span</var> 个连续字符 的字符串。

**slice** 方法的 **length** 属性是 **2**。

#### String.prototype.split (separator, limit)

将 **this** 字符串转换为一个字符串，返回一个数组对象，里面存储了这个字符串的子字符串。子字符串是从左到右搜索 <var>separator</var> 的匹配来确定的；这些匹配结果不成为返回数组的任何子字符串元素，但被用来分割字符串。<var>separator</var> 的值可以是一个任意长度的字符串，也可以是一个正则对象（即，一个 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"RegExp"** 的对象；见 [15.10](ES5/builtins#x15.10 "wikilink")）。

<var>separator</var> 值可以是一个空字符串、一个空正则表达式或一个可匹配空字符串的正则表达式。这种情况下，<var>separator</var> 不匹配输入字符串开头和末尾的空的子串，也不匹配分隔符的之前匹配结果末尾的空字串。（例如，如果 <var>separator</var> 是空字符串，要将字符串分割为单个字符们；结果数组的长度等于字符串长度，且每个字串都包含一个字符。）如果 <var>separator</var> 是正则表达式，在 **this** 字符串的给定位置中只考虑首次匹配结果，即使如果在这个位置上回溯可产生一个非空的子串。（例如，**"ab".split(/a\*?/)** 的执行结果是数组 **["a","b"]**，而 **"ab".split(/a\*/)** 的执行结果是数组 **["","b"]** 。）

如果 **this** 对象是（或转换成）空字符串，返回的结果取决于 <var>separator</var> 是否可匹配空字符串。如果可以，结果是不包含任何元素的数组。否则，结果是包含一个空字符串元素的数组。

如果 <var>separator</var> 是包含捕获括号的正则表达式，则对 <var>separator</var> 的每次匹配，捕获括号的结果 ( 包括 **undefined** ) 都拼接为输出数组。

例如，

` "A<B>bold</B>and<CODE>coded</CODE>".split(/<(\/)?([^<>]+)>/)`

执行结果是数组：

` ["A", undefined, "B", "bold", "/", "B", "and", undefined,`
` "CODE", "coded", "/", "CODE", ""]`

如果 <var>separator</var> 是 **undefined**，则返回结果是只包含 **this** 值（转换为字符串）一个字符串元素的数组。如果 <var>limit</var> 不是 **undefined**，则输出数组被切断为包含不大于 <var>limit</var> 个元素。

当调用 **split** 方法，采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>A</var> 为 仿佛使用表达式 **new Array()** 创建的新对象，这里的 **Array** 是标准内置构造器名。
4.  令 <var>lengthA</var> 为 **0**。
5.  如果 <var>limit</var> 是 **undefined**，令 <var>lim</var> = **2<sup>32</sup>** - **1**; 否则 令 <var>lim</var> = [ToUint32](ES5/conversion#to-uint32 "wikilink")(<var>limit</var>)。
6.  令 <var>s</var> 为 <var>S</var> 的字符数。
7.  令 <var>p</var> = **0**。
8.  如果 <var>separator</var> 是正则对象（它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"RegExp"**），令 <var>R</var> = <var>separator</var>；否则，令 <var>R</var> = [ToString](ES5/conversion#ToString "wikilink")(<var>separator</var>)。
9.  如果 <var>lim</var> = **0**，返回 <var>A</var>。
10. 如果 <var>separator</var> 是 **undefined**, 则
    1.  以 **"0"**、属性描述符 {[[Value]]: <var>S</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
    2.  返回 <var>A</var>。

11. 如果 <var>s</var> = **0**，则
    1.  调用 [SplitMatch](#SplitMatch "wikilink")(<var>S</var>, **0**, <var>R</var>) 并 令 <var>z</var> 为 它的 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink") 结果。
    2.  如果 <var>z</var> 不是 **failure**，返回 <var>A</var>。
    3.  以 **"0"**、属性描述符 {[[Value]]: <var>S</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
    4.  返回 <var>A</var>。

12. 令 <var>q</var> = <var>p</var>。
13. 只要 <var>q</var> ≠ <var>s</var>，就重复
    1.  调用 [SplitMatch](#SplitMatch "wikilink")(<var>S</var>, <var>q</var>, <var>R</var>) 并 令 <var>z</var> 为 它的 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink") 结果。
    2.  如果 <var>z</var> 是 **failure**, 则 令 <var>q</var> = <var>q</var> + **1**。
    3.  否则，<var>z</var> 不是 **failure**
        1.  <var>z</var> 必定是一个 [State](ES5/builtins#Patterns-State "wikilink")。令 <var>e</var> 为 <var>z</var> 的 **endIndex** 并 令 <var>cap</var> 为 <var>z</var> 的 **captures** 数组。
        2.  如果 <var>e</var> = <var>p</var>，则 令 <var>q</var> = <var>q</var> + **1**。
        3.  否则，<var>e</var> ≠ <var>p</var>
            1.  令 <var>T</var> 为一个字符串，它的值等于包含 在 <var>S</var> 中 <var>p</var>（包括它）位置到 <var>q</var>（不包括）位置的字符 的子字符串的值。
            2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>lengthA</var>)、属性描述符 {[[Value]]: <var>T</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法 .
            3.  <var>lengthA</var> 递增 **1**。
            4.  如果 <var>lengthA</var> = <var>lim</var>，返回 <var>A</var>。
            5.  令 <var>p</var> = <var>e</var>。
            6.  令 <var>i</var> = **0**。
            7.  只要 <var>i</var> 不等于 <var>cap</var> 中的元素个数，就重复。
                1.  令 <var>i</var> = <var>i</var> + **1**。
                2.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>lengthA</var>)、属性描述符 {[[Value]]: <var>cap</var>[<var>i</var>], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 A 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
                3.  <var>lengthA</var> 递增 **1**。
                4.  如果 <var>lengthA</var> = <var>lim</var>，返回 <var>A</var>。

            8.  令 <var>q</var> = <var>p</var>。

14. 令 <var>T</var> 为 为一个字符串，它的值等于包含 在 <var>S</var> 中 <var>p</var>（包括它）位置到 <var>q</var>（不包括）位置的字符 的子字符串的值。
15. 以 [ToString](ES5/conversion#ToString "wikilink")(<var>lengthA</var>)、属性描述符 {[[Value]]: <var>T</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 作为参数调用 <var>A</var> 的 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink") 内部方法。
16. 返回 <var>A</var>。

**SplitMatch** 抽象操作需要三个参数，字符串 <var>S</var>、整数 <var>q</var>、字符串或正则对象 <var>R</var>，按照以下顺序执行并返回一个 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink")：

1.  如果 <var>R</var> 是个正则对象 ( 它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"RegExp"**)，则
    1.  以 <var>S</var> 和 <var>q</var> 作为参数调用 <var>R</var> 的 [[[Match]]](ES5/types#Match "wikilink") 内部方法，并返回 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink") 的结果。

2.  否则，[Type](ES5/types#Type "wikilink")(<var>R</var>) 必定是 **String**。令 <var>r</var> 为 <var>R</var> 的字符数。
3.  令 <var>s</var> 为 <var>S</var> 的字符数 .
4.  如果 <var>q</var> + <var>r</var> \> <var>s</var> 则返回 [MatchResult](ES5/builtins#Patterns-MatchResult "wikilink") **failure**。
5.  如果存在一个在 **0**（包括）到 <var>r</var>（不包括）之间的整数 <var>i</var>，使得 <var>S</var> 的 <var>q</var> + <var>i</var> 位置上的字符和 <var>R</var> 的 <var>i</var> 位置上的字符不同，则返回 **failure**。
6.  令 <var>cap</var> 为 **captures** 的空数组 ( 见 [15.10.2.1](#x15.10.2.1 "wikilink"))。
7.  返回 [State](ES5/builtins#Patterns-State "wikilink") 数据结构 (<var>q</var> + <var>r</var>, <var>cap</var>). ( 见 [15.10.2.1](#x15.10.2.1 "wikilink"))

**split** 方法的 **length** 属性是 **2**.

#### String.prototype.substring (start, end)

<var>substring</var> 方法需要两个参数 <var>start</var> 和 <var>end</var>，将 **this** 对象转换为一个字符串，返回一个子串，这个子串包含了在转换结果字符串中从 <var>start</var> 位置字符一直到（但不包括）<var>end</var> 位置的字符（或如果 <var>end</var> 是 **undefined**，就到字符串末尾）。返回结果是字符串值，不是字符串对象。

如果任一参数是 **NaN** 或负数，它被零取代；如果任一参数大于字符串长度，它被字符串长度取代。

如果 <var>start</var> 大于 <var>end</var>，交换它们的值。

采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>len</var> 为 <var>S</var> 的字符数。
4.  令 <var>intStart</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>start</var>)。
5.  如果 <var>end</var> 是 **undefined**，令 <var>intEnd</var> 为 <var>len</var>；否则 令 <var>intEnd</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>end</var>)。
6.  令 <var>finalStart</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")(<var>intStart</var>, **0** ), <var>len</var>)。
7.  令 <var>finalEnd</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")(<var>intEnd</var>, **0** ), <var>len</var>)。
8.  令 <var>from</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(<var>finalStart</var>, <var>finalEnd</var>)。
9.  令 <var>to</var> 为 [max](ES5/builtins#x15.8.2.11 "wikilink")(<var>finalStart</var>, <var>finalEnd</var>)。
10. 返回 一个长度是 <var>to</var> - <var>from</var> 的字符串，它包含 <var>S</var> 中从索引值 <var>form</var> 到 <var>to</var> - **1**（按照索引升序）的所有字符。

**substring** 方法的 **length** 属性是 **2**。

#### String.prototype.toLowerCase ( )

采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>L</var> 为一个字符串，<var>L</var> 的每个字符是 <var>S</var> 中相应字符的 Unicode 小写等量，或者（如果没有 Unicode 小写等量存在）是实际的 <var>S</var> 中相应字符值。
4.  返回 <var>L</var>。

为了此操作，字符串的16位代码单元被看作是 Unicode <b title="Basic Multilingual Plane">基本多文种平面</b>中的代码点。代理代码点直接从 <var>S</var> 转移到 <var>L</var>，不做任何映射。

返回结果必须是根据 Unicode 字符数据库里的大小写映射得到的（对此数据库明确规定，不仅包括 [UnicodeData.txt](http://www.unicode.org/Public/UNIDATA/UnicodeData.txt) 文件，而且还包括 Unicode 2.1.8 和更高版本里附带的 [SpecialCasings.txt](http://www.unicode.org/Public/UNIDATA/SpecialCasing.txt) 文件）。

#### String.prototype.toLocaleLowerCase ( )

此函数产生依照 宿主环境的当前语言设置 更正的结果，而不是独立于语言环境的结果，除此之外它的运作方式与 **toLowerCase** 完全一样。只有在少数情况下有一个区别（如，土耳其语），就是那个语言和正规 Unicode 大小写映射有冲突时的规则。

#### String.prototype.toUpperCase ( )

此函数的将字符映射到在 Unicode 字符数据库中与其等值的大写字符，除此之外此函数的行为采用与 **String.prototype.toLowerCase** 完全相同的方式。

#### String.prototype.toLocaleUpperCase ( )

此函数产生依照 宿主环境的当前语言设置 更正的结果，而不是独立于语言环境的结果，除此之外它的运作方式与 **toUpperCase** 完全一样。只有在少数情况下有一个区别（如，土耳其语），就是那个语言和正规 Unicode 大小写映射有冲突时的规则。

#### String.prototype.trim ( )

采用以下步骤：

1.  以 **this** 值作为参数调用 [CheckObjectCoercible](ES5/conversion#CheckObjectCoercible "wikilink")。
2.  令 <var>S</var> 为以 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink") 的结果。
3.  令 <var>T</var> 为一个字符串值，它是 <var>S</var> 的一个拷贝，并删除了开头和结尾中空白的。空白的定义是 [空白字符](ES5/lexical#white-space "wikilink") 和 [行终止符](ES5/lexical#line-terminator "wikilink") 的并集。
4.  返回 <var>T</var>。

### String 实例的属性

字符串实例从字符串原型对象继承属性，字符串实例的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"String"**。字符串实例还有 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性，**length** 属性，和一组属性名是数组索引的可遍历属性。

[[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性是代表这个字符串对象的字符串值。以数组索引命名的属性对应字符串值里的单字符。一个特殊的 **[[GetOwnProperty]]** 内部方法用来为数组索引命名的属性指定数字，值，和特性。

#### length

在代表这个字符串对象的字符串值里的字符数。

一旦创建了一个字符串对象，这个属性是不可变的。它有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### [[GetOwnProperty]] ( P )

数组对象使用一个，用在其他原生 ECMAscript 对象的 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的变化版。这个特殊内部方法用来给命名属性添加访问器，对应到字符串对象的单字符。

设 <var>S</var> 为一个字符串对象，<var>P</var> 为一个字符串。

当以属性名 <var>P</var> 调用 <var>S</var> 的 **[[GetOwnProperty]]** 内部方法，采用以下步骤：

1.  令 <var>desc</var> 为 以 <var>P</var> 为参数调用 <var>S</var> 的默认 [[[GetOwnProperty]]](ES5/types#GetOwnProperty "wikilink") 内部方法的结果。
2.  如果 <var>desc</var> 不是 **undefined**，返回 <var>desc</var>。
3.  如果 [ToString](ES5/conversion#ToString "wikilink")([abs](ES5/notation#abs "wikilink")( [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>P</var> ))) 与 <var>P</var> 的值不同，返回 **undefined**。
4.  令 <var>str</var> 为 <var>S</var> 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性字符串值。
5.  令 <var>index</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>P</var>)。
6.  令 <var>len</var> 为 <var>str</var> 里的字符数。
7.  如果 <var>len</var> ≤ <var>index</var>，返回 **undefined**。
8.  令 <var>resultStr</var> 为一个长度为 **1** 的字符串，里面包含 <var>str</var> 中 <var>index</var> 位置的一个字符，在这里 <var>str</var> 中的第一个（最左边）字符被认为是在位置 **0**，下一个字符在位置 **1**，依此类推。
9.  返回一个属性描述符 { [[Value]]: <var>resultStr</var>, [[Enumerable]]: **true**, [[Writable]]: **false**, [[Configurable]]: **false** }

Boolean 对象
------------

### 作为函数调用 Boolean 构造器

当把 **Boolean** 作为函数来调用，而不是作为构造器，它执行一个类型转换。

#### Boolean (value)

返回由 [ToBoolean](ES5/conversion#ToBoolean "wikilink")(<var>value</var>) 计算出的 **Boolean** 值（非 **Boolean** 对象）。

### Boolean 构造器

当 **Boolean** 作为 **new** 表达式的一部分来调用，那么它是一个构造器：它初始化新创建的对象。

#### new Boolean (value)

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为原始 [Boolean 原型对象](#15.6.4 "wikilink")，它是 [Boolean.prototype](#x15.6.3.1 "wikilink") 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"Boolean"**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性设定为 [ToBoolean](ES5/conversion#ToBoolean "wikilink")(<var>value</var>)。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **true**。

### Boolean 构造器的属性

**Boolean** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值是 [Function 原型对象](#15.3.4 "wikilink")。

除了内部属性和 **length** 属性（值为 **1**）外，**Boolean** 构造器还有以下属性：

#### Boolean.prototype

**Boolean.prototype** 的初始值是 [Boolean 原型对象](#15.6.4 "wikilink")。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### Boolean 原型对象的属性

[Boolean 原型对象自身是一个值为](#15.6.4 "wikilink") **false** 的 **Boolean** 对象（它的 [[[Class]]](ES5/types#Class "wikilink") 是 **"Boolean"**）。

[Boolean 原型对象的](#15.6.4 "wikilink") [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准的内置 [Object 原型对象](#15.2.4 "wikilink")。

#### Boolean.prototype.constructor

**Boolean.prototype.constructor** 的初始值是内置的 **Boolean** 构造器。

#### Boolean.prototype.toString ( )

采用以下步骤：

1.  令 <var>B</var> 为 **this** 值。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>B</var>) 是 **Boolean**，则令 <var>b</var> 为 <var>B</var>。
3.  否则如果 [Type](ES5/types#Type "wikilink")(<var>B</var>) 是 **Object** 且 <var>B</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Boolean"**，则令 <var>b</var> 为 <var>B</var> 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性值。
4.  否则抛出一个 **TypeError** 异常。
5.  如果 <var>b</var> 是 **true**，则返回 **"true"**；否则返回 **"false"**。

#### Boolean.prototype.valueOf ( )

采用以下步骤：

1.  令 <var>B</var> 为 **this** 值。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>B</var>) 是 **Boolean**，则令 <var>b</var> 为 <var>B</var>。
3.  否则如果 [Type](ES5/types#Type "wikilink")(<var>B</var>) 是 **Object** 且 <var>B</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Boolean"**，则令 <var>b</var> 为 <var>B</var> 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性值。
4.  否则抛出一个 **TypeError** 异常。
5.  返回 <var>b</var>。

### Boolean 实例的属性

**Boolean** 实例从 [Boolean 原型对象继承属性](#15.6.4 "wikilink")，且 **Boolean** 实例的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Boolean"**。**Boolean** 实例 还有一个 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性。

[[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性是代表这个 **Boolean** 对象的 **Boolean** 值。

Number 对象
-----------

### 作为函数调用的 Number 构造器

当把 **Number** 当作一个函数来调用，而不是作为构造器，它执行一个类型转换。

#### Number ( [ value ] )

如果提供了 <var>value</var>，返回 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>value</var>) 计算出的 **Number** 值（非 **Number** 对象），否则返回 **+0**。

### Number 构造器

当把 **Number** 作为 **new** 表达式的一部分来调用，它是构造器：它初始化新创建的对象。

#### new Number ( [ value ] )

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为原始 [Number 原型对象](#x15.7.4 "wikilink")，它是 [Number.prototype](#15.7.3.1 "wikilink") 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"Number"**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性在提供了 <var>value</var> 时设定为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>value</var>)，否则设定为 **+0**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **true**。

### Number 构造器的属性

**Number** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是 [Function 原型对象](#15.3.4 "wikilink")。

除了内部属性和 **length** 属性（值为 **1**）之外，**Number** 构造器还有以下属性：

#### Number.prototype

**Number.prototype** 的初始值是 [Number 原型对象](#x15.7.4 "wikilink")。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Number.MAX\_VALUE

**Number.MAX\_VALUE** 的值是 **Number** 类型的最大正有限值，约为 **1.7976931348623157×10<sup>308</sup>**。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Number.MIN\_VALUE

**Number.MIN\_VALUE** 的值是 **Number** 类型的最小正有限值，约为 **5×10<sup>-324</sup>**。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Number.NaN

**Number.NaN** 的值是 **NaN**。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Number.NEGATIVE\_INFINITY

**Number.NEGATIVE\_INFINITY** 的值是**-∞**。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Number.POSITIVE\_INFINITY

**Number.POSITIVE\_INFINITY** 的值是 **+∞**。

这个属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### Number 原型对象的属性

**Number** 原型对象其自身是 **Number** 对象（其 [[[Class]]](ES5/types#Class "wikilink") 是 **"Number"**），其值为 **+0**。

**Number** 原型对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 [Object 原型对象](#15.2.4 "wikilink")。

除非另外明确声明，以下定义的 **Number** 原型对象的方法是非通用的，传递给它们的 **this** 值必须是 **Number** 值或 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Number"** 的对象。

在以下对作为 **Number** 原型对象属性的函数的描述中，短语“**this Number 对象**”是指函数调用中的 **this**，或如果 [Type](ES5/types#Type "wikilink")( **this** ) 是 **Number**，“**this Number 对象**”指仿佛是用表达式 **new Number( this )** 创建的对象，这里 **Number** 是标准内置构造器名。此外，短语“**this Number 值**”是指代表 **this Number 对象** 的 **Number** 值，也就是 **this Number 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性值；或如果 **this** 是 **Number** 类型，“**this Number 值**”指 **this**。如果 **this** 值不是 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Number"** 的对象，也不是 **Number** 类型的值，则抛出一个 **TypeError** 异常。

#### Number.prototype.constructor

**Number.prototype.constructor** 的初始值是内置 **Number** 构造器。

#### Number.prototype.toString ( [ radix ] )

可选参数 <var>radix</var> 应当是 **2** 到 **36** 闭区间上的整数。如果 <var>radix</var> 不存在或是 **undefined**，用数字 **10** 作为 <var>radix</var> 的值。如果 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>radix</var>) 是数字 **10**，则将 **this Number 对象** 作为一个参数传给 [ToString](ES5/conversion#ToString "wikilink") 抽象操作；返回结果字符串值。

如果 [ToInteger](ES5/conversion#ToInteger "wikilink")( <var>radix</var> ) 不是在 **2** 到 **36** 闭区间上的整数，则抛出一个 **RangeError** 异常。如果 [ToInteger](ES5/conversion#ToInteger "wikilink")( <var>radix</var> ) 是 **2** 到 **36** 的整数，但不是 **10**，则结果是 **this Number 值** 使用指定基数表示法的字符串。字母 **a-z** 用来指值为 **10** 到 **35** 的数字。基数不为 **10** 时的精确算法是依赖于实现的，然而算法应当是 [9.8.1](ES5/conversion#x9.8.1 "wikilink") 指定算法的推广形式。

**toString** 函数不是通用的；如果 **this** 值不是数字或 **Number** 对象，抛出一个 **TypeError** 异常。因此它不能当作方法转移到其他类型对象上。

#### Number.prototype.toLocaleString()

根据宿主环境的当前语言环境惯例来格式化 **this Number 值**，生成代表这个值的字符串。此函数是依赖于实现的，允许但不鼓励它的返回值与 **toString** 相同。

#### Number.prototype.valueOf ( )

返回 **this Number 值**。

**valueOf** 函数不是通用的；如果 **this** 值不是数字或 **Number** 对象，抛出一个 **TypeError** 异常。因此它不能当作方法转移到其他类型对象上。

#### Number.prototype.toFixed (fractionDigits)

返回一个包含了 代表 **this Number 值**的留有小数点后 <var>fractionDigits</var> 个数字的十进制固定小数点记法 的字符串。如果 <var>fractionDigits</var> 是 **undefined**，就认为是 **0**。具体来说，执行以下步骤：

1.  令 <var>f</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>fractionDigits</var>)。（如果 <var>fractionDigits</var> 是 **undefined**，此步骤产生 **0** 值。）
2.  如果 <var>f</var> \< **0** 或 <var>f</var> \> **20**，抛出一个 **RangeError** 异常。
3.  令 <var>x</var> 为 **this Number 值**。
4.  如果 <var>x</var> 是 **NaN**，返回字符串 **"NaN"**。
5.  令 <var>s</var> 为空字符串。
6.  如果 <var>x</var> \< **0**，则
    1.  令 <var>s</var> 为 **"-"**。
    2.  令 <var>x</var> = -<var>x</var>。

7.  如果 <var>x</var> ≥ **10<sup>21</sup>**，则
    1.  令 <var>m</var> = [ToString](ES5/conversion#ToString "wikilink")(<var>x</var>)。

8.  否则，<var>x</var> \< **10<sup>21</sup>**
    1.  令 <var>n</var> 为一个整数，让 <var>n</var> ÷ **10**<sup><var>f</var></sup> - <var>x</var> 准确的数学值尽可能接近零。如果有两个这样 <var>n</var> 值，选择较大的 <var>n</var>。
    2.  如果 <var>n</var> = **0**，令 <var>m</var> 为字符串 **"0"**。否则，令 <var>m</var> 为由 <var>n</var> 的十进制表示里的数 组成的字符串（为了没有前导零）。
    3.  如果 <var>f</var> ≠ **0**，则
        1.  令 <var>k</var> 为 <var>m</var> 里的字符数目。
        2.  如果 <var>k</var> ≤ <var>f</var>，则
            1.  令 <var>z</var> 为 <var>f</var> + **1** - <var>k</var> 个 **'0'** 组成的字符串。
            2.  令 <var>m</var> 为 串联字符串 <var>z</var> 和 <var>m</var> 的结果。
            3.  令 <var>k</var> = <var>f</var> + **1**。

        3.  令 <var>a</var> 为 <var>m</var> 的前 <var>k</var> – <var>f</var> 个字符，令 <var>b</var> 为其余 <var>f</var> 个字符。
        4.  令 <var>m</var> 为 串联三个字符串 <var>a</var>、**"."** 和 <var>b</var> 的结果。

9.  返回串联字符串 <var>s</var> 和 <var>m</var> 的结果。

**toFixed** 方法的 **length** 属性是 **1**。

如果以多个参数调用 **toFixed** 方法，则行为是不确定的（[见15章](# "wikilink")）。

实现是被允许在 <var>fractionDigits</var> 小于 **0** 或大于 **20** 时扩展 **toFixed** 的行为。在这种情况下，对这样的 <var>fractionDigits</var> 值 **toFixed** 将未必抛出 **RangeError**。

#### Number.prototype.toExponential (fractionDigits)

返回一个代表 **this Number 值** 的科学计数法的字符串，它的有效数字的小数点前有一个数字，有效数字的小数点后有 <var>fractionDigits</var> 个数字。如果 <var>fractionDigits</var> 是 **undefined**，包括指定唯一 **Number** 值需要的尽可能多的有效数字（就像 [ToString](ES5/conversion#ToString "wikilink")，但在这里总是以科学计数法输出）。具体来说执行以下步骤：

1.  令 <var>x</var> 为 **this Number 值**。
2.  令 <var>f</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>fractionDigits</var>)。
3.  如果 <var>x</var> 是 **NaN**，返回字符串 **"NaN"**。
4.  令 <var>s</var> 为空字符串。
5.  如果 <var>x</var> \< **0**，则
    1.  令 <var>s</var> 为 **"-"**。
    2.  令 <var>x</var> = -<var>x</var>。

6.  如果 <var>x</var> = **+∞**，则
    1.  返回串联字符串 <var>s</var> 和 **"Infinity"** 的结果。

7.  如果 <var>fractionDigits</var> 不是 **undefined** 且（<var>f</var> \< **0** 或 <var>f</var> \> **20**），抛出一个 **RangeError** 异常。
8.  如果 <var>x</var> = **0**，则
    1.  令 <var>f</var> = **0**。
    2.  令 <var>m</var> 为包含 <var>f</var> + **1** 个 **'0'** 的字符串。
    3.  令 <var>e</var> = **0**。

9.  否则，<var>x</var> ≠ **0**
    1.  如果 <var>fractionDigits</var> 不是 **undefined**，则
        1.  令 <var>e</var> 和 <var>n</var> 为整数，使得满足 **10**<sup><var>f</var></sup> ≤ <var>n</var> \< **10**<sup><var>f</var>+**1**</sup> 且 <var>n</var> × **10**<sup><var>e</var>-<var>f</var></sup> - <var>x</var> 的准确数学值尽可能接近零。如果 <var>e</var> 和 <var>n</var> 有两个这样的组合，选择使 <var>n</var> × **10**<sup><var>e</var>-<var>f</var></sup> 更大的组合。

    2.  否则，<var>fractionDigits</var> 是 **undefined**
        1.  令 <var>e</var>、<var>n</var> 和 <var>f</var> 为整数，使得满足 <var>f</var> ≥ **0**、**10**<sup><var>f</var></sup>≤ <var>n</var> \< **10**<sup><var>f</var>+**1**</sup>、<var>n</var> × **10**<sup><var>e</var>-<var>f</var></sup> 的 **Number** 值是 <var>x</var>，且 <var>f</var> 的值尽可能小。注：<var>n</var> 的十进制表示有 <var>f</var> + **1** 个数字，<var>n</var> 不能被 **10** 整除，并且 <var>n</var> 的最少有效位数不一定唯一由这些条件确定。

    3.  令 <var>m</var> 为由 <var>n</var> 的十进制表示里的数 组成的字符串（没有前导零）。

10. 如果 <var>f</var> ≠ **0**，则
    1.  令 <var>a</var> 为 <var>m</var> 中的第一个字符，令 <var>b</var> 为 <var>m</var> 中的其余字符。
    2.  令 <var>m</var> 为串联三个字符串 <var>a</var>、**"."** 的 <var>b</var> 的结果。

11. 如果 <var>e</var> = **0**，则
    1.  令 <var>c</var> = **"+"**。
    2.  令 <var>d</var> = **"0"**。

12. 否则
    1.  如果 <var>e</var> \> **0**，则 令 <var>c</var> = **"+"**。
    2.  否则，<var>e</var> ≤ **0**
        1.  令 <var>c</var> = **"-"**。
        2.  令 <var>e</var> = -<var>e</var>。

    3.  令 <var>d</var> 为有 <var>e</var> 的十进制表示里的数 组成的字符串（没有前导零）。

13. 令 <var>m</var> 为串联四个字符串 <var>m</var>、**"e"**、<var>c</var> 和 <var>d</var> 的结果。
14. 返回串联字符串 <var>s</var> 和 <var>m</var> 的结果。

**toExponential** 方法的 **length** 属性是 **1**。

如果用多于一个参数调用 **toExponential** 方法，则行为是未定义的（[见15章](# "wikilink")）。

一个实现可以扩展 <var>fractionDigits</var> 的值小于 **0** 或大于 **20** 时 **toExponential** 的行为。这种情况下对这样的 <var>fractionDigits</var> 值，**toExponential** 不一定抛出 **RangeError** 异常。

1.  令 <var>e</var>、<var>n</var> 和 <var>f</var> 为整数，使得满足 <var>f</var> ≥ **0**，**10**<sup><var>f</var></sup> ≤ <var>n</var> \< **10**<sup><var>f</var>+**1**</sup>，<var>n</var> × **10**<sup><var>e</var>-<var>f</var></sup> 的 **Number** 值是 <var>x</var>，且 <var>f</var> 的值尽可能小。如果这样的 <var>n</var> 值可能多个，选择使 <var>n</var> × **10**<sup><var>e</var>-<var>f</var></sup> 的值尽可能接近 <var>x</var> 的 <var>n</var> 值。如果有两个这样的 <var>n</var> 值，选择偶数。

#### Number.prototype.toPrecision (precision)

返回一个字符串，它代表 **this Number 值** 的科学计数法（有效数字的小数点前有一个数字，有效数字的小数点后有 <var>precision</var> - **1** 个数字）或十进制固定计数法（<var>precision</var> 个有效数字）。如果 <var>precision</var> 是 **undefined**，用 [ToString](ES5/conversion#ToString "wikilink") 调用代替。具体来说执行以下步骤：

1.  令 <var>x</var> 为 **this** 数字值。
2.  如果 <var>precision</var> 是 **undefined**，返回 [ToString](ES5/conversion#ToString "wikilink")(<var>x</var>)。
3.  令 <var>p</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>precision</var>)。
4.  如果 x 是 **NaN**，返回字符串 **"NaN"**。
5.  令 <var>s</var> 为空字符串。
6.  如果 <var>x</var> \< **0**，则
    1.  令 <var>s</var> 为 **"-"**。
    2.  令 <var>x</var> = -<var>x</var>。

7.  如果 <var>x</var> = **+∞**，则
    1.  返回串联字符串 <var>s</var> 和 **"Infinity"** 的结果。

8.  如果 <var>p</var> \< **1** 或 <var>p</var> \> **21**，抛出一个 **RangeError** 异常。
9.  如果 <var>x</var> = **0**，则
    1.  令 <var>m</var> 为 <var>p</var> 个 **'0'** 组成的字符串。
    2.  令 <var>e</var> = **0**。

10. 否则 <var>x</var> ≠ **0**，
    1.  令 <var>e</var> 和 <var>n</var> 为整数，使得满足 **10**<sup><var>p</var>-**1**</sup> ≤ <var>n</var> \< **10**<sup><var>p</var></sup> 且 <var>n</var> × **10**<sup><var>e</var>-<var>p</var>+**1**</sup> - <var>x</var> 的准确数学值尽可能接近零。如果 <var>e</var> 和 <var>n</var> 有两个这样的组合，选择使 <var>n</var> × **10**<sup><var>e</var>-<var>p</var>+**1**</sup> 更大的组合。
    2.  令 <var>m</var> 为由 <var>n</var> 的十进制表示里的数 组成的字符串（没有前导零）。
    3.  如果 <var>e</var> \< **-6** 或 <var>e</var> ≥ <var>p</var>。则
        1.  令 <var>a</var> 为 <var>n</var> 的第一个字符，令 <var>b</var> 为 <var>m</var> 的其余 <var>p</var>-**1** 个字符/
        2.  令 <var>m</var> 为串联三个字符串 <var>a</var>、**"."** 和 <var>b</var> 的结果。
        3.  如果 <var>e</var> = **0**，则
            1.  令 <var>c</var> = **"+"**，令 <var>d</var> = **"0"**。

        4.  否则 <var>e</var> ≠ **0**，
            1.  如果 <var>e</var> \> **0**，则
                1.  令 <var>c</var> = **"+"**。

            2.  否则 <var>e</var> \< **0**，
                1.  令 <var>c</var> = **"-"**。
                2.  令 <var>e</var> = -<var>e</var>。

            3.  令 <var>d</var> 为由 <var>e</var> 的十进制表示里的数 组成的字符串（没有前导零）。

        5.  令 <var>m</var> 为串联五个字符串 <var>s</var>、<var>m</var>、**"e"**、<var>c</var> 和 <var>d</var> 的结果。

11. 如果 <var>e</var> = <var>p</var> - **1**，则返回串联字符串 <var>s</var> 和 <var>m</var> 的结果。
12. 如果 <var>e</var> ≥ **0**，则
    1.  令 <var>m</var> 为 <var>m</var> 的前 <var>e</var> + **1** 个字符，字符 **'.'**，<var>m</var> 的其余 <var>p</var> - (<var>e</var> + **1**) 个字符 串联的结果。

13. 否则 <var>e</var> \< **0**，
    1.  令 <var>m</var> 为 字符串 **"0."**、- (<var>e</var> + **1**) 个字符 **'0'**、字符串 <var>m</var> 串联的结果。

14. 返回字符串 <var>s</var> 和 <var>m</var> 串联的结果。

**toPrecision** 方法的 **length** 属性是 **1**。

如果用多于一个参数调用 **toPrecision** 方法，则行为是未定义的（[见15章](# "wikilink")）。

一个实现可以扩展 <var>precision</var> 的值小于 **1** 或大于 **21** 时 **toPrecision** 的行为。这种情况下对这样的 <var>precision</var> 值，**toPrecision** 不一定抛出 **RangeError** 异常。

### Number 实例的属性

**Number** 实例从 **Number** 原型对象继承属性，**Number** 实例的 [[[Class]]](ES5/types#Class "wikilink") 内部属性是 **"Number"**。**Number** 实例还有一个 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性。

[[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性是代表 **this Number 对象** 的 **Number** 值。

Math 对象
---------

**Math** 对象是拥有一些命名属性的单一对象，其中一些属性值是函数。

**Math** 对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性值是标准内置 **Object** 原型对象 ([15.2.4](#15.2.4 "wikilink"))。**Math** 对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Math"**。

**Math** 对象没有 [[[Construct]]](ES5/types#Construct "wikilink") 内部属性 ; **Math** 对象不能作为构造器被 **new** 运算符调用。

**Math** 对象没有 [[[Call]]](ES5/types#Call "wikilink") 内部属性；**Math** 对象不能作为函数被调用。

### Math 对象的值属性

#### E

自然对数的底数 **e** 的 **Number** 值，约为 **2.7182818284590452354**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### LN10

**10** 的自然对数的 **Number** 值，约为 **2.302585092994046**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### LN2

**2** 的自然对数的 **Number** 值，约为 **0.6931471805599453**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### LOG2E

自然对数的底数*' e*' 的以 **2** 为底数的对数的 **Number** 值；约为 **1.4426950408889634**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### LOG10E

自然对数的底数 **e** 的以 **10** 为底数的对数的 **Number** 值；约为 **0.4342944819032518**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### PI

圆的周长与直径之比 **π** 的 **Number** 值，约为 **3.1415926535897932**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### SQRT1\_2

**?** 的平方根的 **Number** 值，约为 **0.7071067811865476**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

#### SQRT2

**2** 的平方根的 **Number** 值，约为 **1.4142135623730951**。

此属性有特性 { [[Writable]]: **false** , [[Enumerable]]: **false** , [[Configurable]]: **false** } 。

### Math 对象的函数属性

对以下每个 **Math** 对象函数的每个参数（如果有多个，以左到右的顺序）应用 [ToNumber](ES5/conversion#ToNumber "wikilink") 抽象操作，然后对结果 **Number** 值执行计算。

下面对函数的描述中，符号 **NaN**、**-0**、**+0**、**-∞**、**+∞** 指 [8.5](ES5/types#8.5 "wikilink") 描述的 **Number** 值。

尽管算法的选择由实现来决定的，但它被推荐（不是由这个标准指定）使用包含在fdlibm的IEEE754算法的近似算法来实现，这个可以自由分配的数学库来自Sun公司([<http://www.netlib.org/fdlibm>](http://www.netlib.org/fdlibm)).

#### abs (x)

返回 <var>x</var> 的绝对值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **-0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-∞**，返回结果是 **+∞**。

#### acos (x)

返回 <var>x</var> 的反余弦的依赖实现的近似值。结果以弧度形式表示，范围是 **+0** 到 **+π**。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 大于 **1**，返回结果是 **NaN**。
-   若 <var>x</var> 小于 **-1**，返回结果是 **NaN**。
-   若 <var>x</var> 正好是 **1**，返回结果是 **+0**。

#### asin (x)

返回 <var>x</var> 的反正弦的依赖实现的近似值。结果以弧度形式表示，范围是 **-π/2** 到 **+π/2**。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 大于 **1**，返回结果是 **NaN**。
-   若 <var>x</var> 小于 **–1**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。

#### atan (x)

返回 <var>x</var> 的反正切的依赖实现的近似值。结果以弧度形式表示，范围是 **-π/2** 到 **+π/2**。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 一个依赖于实现的近似值 **+π/2**。
-   若 <var>x</var> 是 **-∞**，返回结果是 一个依赖于实现的近似值 **-π/2**。

#### atan2 (y, x)

返回 参数 <var>y</var> 和 <var>x</var> 的商 <var>y</var> / <var>x</var> 的反正切 的依赖实现的近似值，<var>y</var> 和 <var>x</var> 的符号用于确定返回值的象限。注：命名为 <var>y</var> 的参数为第一个，命名为 <var>x</var> 的参数为第二个，这是有意的，是反正切函数俩参数的惯例。结果以弧度形式表示，范围是 **-π** 到 **+π**。

-   若 <var>x</var> 和 <var>y</var> 至少一个是 **NaN**，返回结果是 **NaN**。
-   若 <var>y</var> \> **0** 且 <var>x</var> 是 **+0**，返回结果是 一个依赖于实现的近似值 **+π/2**。
-   若 <var>y</var> \> **0** 且 <var>x</var> 是 **-0**，返回结果是 一个依赖于实现的近似值 **+π/2**。
-   若 <var>y</var> 是 **+0** 且 <var>x</var> \> **0**，返回结果是 **+0**。
-   若 <var>y</var> 是 **+0** 且 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>y</var> 是 **+0** 且 <var>x</var> 是 **-0**，返回结果是 一个依赖于实现的近似值 **+π**。
-   若 <var>y</var> 是 **+0** 且 <var>x</var> \< **0**，返回结果是 一个依赖于实现的近似值 **+π**。
-   若 <var>y</var> 是 **-0** 且 <var>x</var> \> **0**，返回结果是 **-0**。
-   若 <var>y</var> 是 **-0** 且 <var>x</var> 是 **+0**，返回结果是 **-0**。
-   若 <var>y</var> 是 **-0** 且 <var>x</var> 是 **-0**，返回结果是 一个依赖于实现的近似值 **-π**。
-   若 <var>y</var> 是 **-0** 且 <var>x</var> \< **0**，返回结果是 一个依赖于实现的近似值 **-π**。
-   若 <var>y</var> \< **0** 且 <var>x</var> 是 **+0**，返回结果是 一个依赖于实现的近似值 **-π/2**。
-   若 <var>y</var> \< **0** 且 <var>x</var> 是 **-0**，返回结果是 一个依赖于实现的近似值 **-π/2**。
-   若 <var>y</var> \> **0** 且 <var>y</var> 是 有限的 且 <var>x</var> 是 **+∞**，返回结果是 **+0**。
-   若 <var>y</var> \> **0** 且 <var>y</var> 是 有限的 且 <var>x</var> 是 **-∞**，返回结果是 一个依赖于实现的近似值 **+π**。
-   若 <var>y</var> \< **0** 且 <var>y</var> 是 有限的 且 <var>x</var> 是 **+∞**，返回结果是 **-0**。
-   若 <var>y</var> \< **0** 且 <var>y</var> 是 有限的 且 <var>x</var> 是 **-∞**，返回结果是 一个依赖于实现的近似值 **-π**。
-   若 <var>y</var> 是 **+∞** 且 <var>x</var> 是 有限的，返回结果是 返回结果是 一个依赖于实现的近似值 +π/2。
-   若 <var>y</var> 是 **-∞** 且 <var>x</var> 是 有限的，返回结果是 返回结果是 一个依赖于实现的近似值 -π/2。
-   若 <var>y</var> 是 **+∞** 且 <var>x</var> 是 **+∞**，返回结果是 一个依赖于实现的近似值 **+π/4**。
-   若 <var>y</var> 是 **+∞** 且 <var>x</var> 是 **-∞**，返回结果是 一个依赖于实现的近似值 **+3π/4**。
-   若 <var>y</var> 是 **-∞** 且 <var>x</var> 是 **+∞**，返回结果是 一个依赖于实现的近似值 **-π/4**。
-   若 <var>y</var> 是 **-∞** 且 <var>x</var> 是 **-∞**，返回结果是 一个依赖于实现的近似值 **-3π/4**。

#### ceil (x)

返回不小于 <var>x</var> 的且为数学整数的最小 ( 接近 **-∞** ) **Number** 值。如果 <var>x</var> 已是整数，则返回 <var>x</var>。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **-∞**，返回结果是 **-∞**。
-   若 <var>x</var> 小于 **0** 但大于 **-1**，返回结果是 **-0**。

#### cos (x)

返回 <var>x</var> 的余弦的依赖实现的近似值。参数被当做是弧度值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **1**。
-   若 <var>x</var> 是 **-0**，返回结果是 **1**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **-∞**，返回结果是 **NaN**。

#### exp (x)

返回 <var>x</var> 的指数的依赖实现的近似值（**e** 为 <var>x</var> 次方，**e** 为自然对数的底）。

-   若 x 是 **NaN**, 返回结果是 **NaN**.
-   若 x 是 **+0**, 返回结果是 **1**.
-   若 x 是 **-0**, 返回结果是 **1**.
-   若 x 是 **+∞**, 返回结果是 **+∞**.
-   若 x 是 **-∞**, 返回结果是 **+0**.

#### floor (x)

返回不大于 <var>x</var> 的且为数学整数的最大 ( 接近 **+∞** ) **Number** 值。如果 <var>x</var> 已是整数，则返回 <var>x</var>。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **-∞**，返回结果是 **-∞**。
-   若 <var>x</var> 大于 **0** 但小于 **1**，返回结果是 **+0**。

#### log (x)

返回 **x** 的自然对数的依赖于实现的近似值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 小于 **0**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0** 或 **-0**，返回结果是 **-∞**。
-   若 <var>x</var> 是 **1**，返回结果是 **+0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **+∞**。

#### max ( [ value1 [ , value2 [ , … ] ] ] )

给定零或多个参数，对每个参数调用 [ToNumber](ES5/conversion#ToNumber "wikilink") 并返回调用结果里的最大值。

-   若 没有给定参数，返回结果是 **-∞**。
-   若 任何值是 **NaN**，返回结果是 **NaN**。
-   按照 [11.8.5](ES5/expressions#x11.8.5 "wikilink") 指定方式进行值比较，确定最大值，与 [11.8.5](ES5/expressions#x11.8.5 "wikilink") 指定方式的一个不同点是在这里 **+0** 被看作大于 **-0**。

**max** 方法的 **length** 属性是 **2**。

#### min ( [ value1 [ , value2 [ , … ] ] ] )

给定零或多个参数，对每个参数调用 [ToNumber](ES5/conversion#ToNumber "wikilink") 并返回调用结果里的最小值。

-   若 没有给定参数，返回结果是 **+∞**。
-   若 任何值是 **NaN**，返回结果是 **NaN**。
-   按照 [11.8.5](ES5/expressions#x11.8.5 "wikilink") 指定方式进行值比较，确定最小值，与 [11.8.5](ES5/expressions#x11.8.5 "wikilink") 指定方式的一个不同点是在这里 **+0** 被看作大于 **-0**。

**min** 方法的 **length** 属性是 **2**。

#### pow (x, y)

返回 <var>x</var> 的 <var>y</var> 次方的依赖于实现的近似值。

-   若 <var>y</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>y</var> 是 **+0**，返回结果是 **1**，即使 <var>x</var> 是 **NaN**。
-   若 <var>y</var> 是 **-0**，返回结果是 **1**，即使 <var>x</var> 是 **NaN**。
-   若 <var>x</var> 是 **NaN** 且 <var>y</var> 是 非零，返回结果是 **NaN**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) \> **1** 且 <var>y</var> 是 **+∞**，返回结果是 **+∞**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) \> **1** 且 <var>y</var> 是 **-∞**，返回结果是 **+0**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) == **1** 且 <var>y</var> 是 **+∞**，返回结果是 **NaN**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) == **1** 且 <var>y</var> 是 **-∞**，返回结果是 **NaN**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) \< **1** 且 <var>y</var> 是 **+∞**，返回结果是 **+0**。
-   若 [abs](ES5/notation#abs "wikilink")(<var>x</var>) \< **1** 且 <var>y</var> 是 **-∞**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **+∞** 且 <var>y</var> \> **0**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **+∞** 且 <var>y</var> \< **0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-∞** 且 <var>y</var> \> **0** 且 <var>y</var> 是 一个奇数，返回结果是 **-∞**。
-   若 <var>x</var> 是 **-∞** 且 <var>y</var> \> **0** 且 <var>y</var> 不是 一个奇数，返回结果是 **+∞**。
-   若 <var>x</var> 是 **-∞** 且 <var>y</var> \< **0** 且 <var>y</var> 是 一个奇数，返回结果是 **-0**。
-   若 <var>x</var> 是 **-∞** 且 <var>y</var> \< **0** 且 <var>y</var> 不是 一个奇数，返回结果是 **+0**。
-   若 <var>x</var> 是 **+0** 且 <var>y</var> \> **0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **+0** 且 <var>y</var> \< **0**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **-0** 且 <var>y</var> \> **0** 且 <var>y</var> 是 一个奇数，返回结果是 **-0**。
-   若 <var>x</var> 是 **-0** 且 <var>y</var> \> **0** 且 <var>y</var> 不是 一个奇数，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0** 且 <var>y</var> \< **0** 且 <var>y</var> 是 一个奇数，返回结果是 **-∞**。
-   若 <var>x</var> 是 **-0** 且 <var>y</var> \< **0** 且 <var>y</var> 不是 一个奇数，返回结果是 **+∞**。
-   若 <var>x</var> \< **0** 且 <var>x</var> 是有限的 且 <var>y</var> 是有限的 且 <var>y</var> 不是整数，返回结果是 **NaN**。

#### random ( )

返回一个大于或等于 **0** 但小于 **1** 的符号为正的 **Number** 值，选择随机或在该范围内近似均匀分布的伪随机，用一个依赖与实现的算法或策略。此函数不需要参数。

#### round (x)

返回最接近 <var>x</var> 且为数学整数的 **Number** 值。如果两个整数同等接近 <var>x</var>，则结果是接近 **+∞** 的 **Number** 值 。如果 <var>x</var> 已是整数，则返回 <var>x</var>。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **+∞**。
-   若 <var>x</var> 是 **-∞**，返回结果是 **-∞**。
-   若 <var>x</var> 大于 **0** 但小于 **0.5**，返回结果是 **+0**。
-   若 <var>x</var> 小于 **0** 但大于或等于 **-0.5**，返回结果是 **-0**。

#### sin (x)

返回 <var>x</var> 的正弦的依赖实现的近似值。参数被当做是弧度值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞** 或 **-∞**，返回结果是 **NaN**。

#### sqrt (x)

返回 <var>x</var> 的平方根的依赖实现的近似值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 小于 **0**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞**，返回结果是 **+∞**。

#### tan (x)

返回 <var>x</var> 的正切的依赖实现的近似值。参数被当做是弧度值。

-   若 <var>x</var> 是 **NaN**，返回结果是 **NaN**。
-   若 <var>x</var> 是 **+0**，返回结果是 **+0**。
-   若 <var>x</var> 是 **-0**，返回结果是 **-0**。
-   若 <var>x</var> 是 **+∞** 或 **-∞**，返回结果是 **NaN**。

Date 对象
---------

### Date 对象的概述和抽象操作的定义

下面的抽象操作函数用来操作时间值（ 定义）。注：任何情况下，如果这些函数之一的任意参数是 **NaN**，则结果将是 **NaN**。

#### 时间值和时间范围

一个 **Date** 对象包含一个表示特定时间瞬间的毫秒的数字值。这样的数字值叫做<b title="time value">时间值</b>。一个时间值也可以是 **NaN**，说明这个 **Date** 对象不表示特定时间瞬间。

ECMAScript 中测量的时间是从协调世界时 **1970 年 1 月 1 日** 开始的毫秒数。在时间值中闰秒是被忽略的，假设每天正好有 **86,400,000** 毫秒。ECMAScript 数字值可表示的所有从**-9,007,199,254,740,991** 到 **9,007,199,254,740,991** 的整数；这个范围足以衡量协调世界时 **1970 年 1 月 1 日** 前后约 **285,616 年** 内任何时间瞬间的精确毫秒。

ECMAScript **Date** 对象支持的实际时间范围是略小一些的：相对协调世界时 **1970 年 1 月 1 日** 午夜 **0** 点的精确的 **-100,000,000** 天到 **100,000,000** 天。这给出了协调世界时 **1970 年 1 月 1 日** 前后 **8,640,000,000,000,000** 毫秒的范围。

精确的协调世界时 **1970 年 1 月 1 日** 午夜 **0** 点用 **+0** 表示。

#### 天数和天内时间

一个给定时间值 <var>t</var> 所属的天数是

` `**`Day`**`(`<var>`t`</var>`) = `[`floor`](ES5/notation#floor "wikilink")`(`<var>`t`</var>` / ``)`

其中每天的毫秒数是

` `**`msPerDay`**` = `**`86400000`**` `

余数叫做天内时间

` `**`TimeWithinDay`**`(`<var>`t`</var>`) = `<var>`t`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `

#### 年数

ECMAScript 使用一个推算公历系统，来将一个天数映射到一个年数，并确定在那年的月份的日期。在这个系统中，闰年是且仅是（可被 **4** 整除）且（（不可被 **100** 整除）或（可被 **400** 整除））的年份。因此，<var>y</var> 年的天的数目定义为

` `**`DaysInYear`**`(`<var>`y`</var>`) = `**`365`**` { 如果 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`4`**`) ≠ 0 }`
`                 = `**`366`**` { 如果 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`4`**`) = `**`0`**` 且 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`100`**`) ≠ `**`0`**` }`
`                 = `**`365`**` { 如果 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`100`**`) = `**`0`**` 且 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`400`**`) ≠ `**`0`**` }`
`                 = `**`366`**` { 如果 (`<var>`y`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `**`400`**`) = `**`0`**` }`

所有非闰年有 **365** 天，其中每月的天的数目是常规的。闰年的二月里有个多出来的一天。 <var>y</var> 年第一天的天数是 :

` `**`DayFromYear`**`(`<var>`y`</var>`) = `**`365`**` × (`<var>`y`</var>` - `**`1970`**`) + `[`floor`](ES5/notation#floor "wikilink")`((`<var>`y`</var>` - `**`1969`**`) / `**`4`**`) - `[`floor`](ES5/notation#floor "wikilink")`((`<var>`y`</var>` - `**`1901`**`) / `**`100`**`) + `[`floor`](ES5/notation#floor "wikilink")`((`<var>`y`</var>` - `**`1601`**`)/`**`400`**`)`

<var>y</var> 年的起始时间值是：

` `**`TimeFromYear`**`(`<var>`y`</var>`) = `` × ``(`<var>`y`</var>`)`

一个时间值决定的年数是：

` `**`YearFromTime`**`(`<var>`t`</var>`) = 满足条件 ``(`<var>`y`</var>`) ≤ `<var>`t`</var>` 的最大整数 `<var>`y`</var>` （接近正无穷）`

若时间值在闰年内，闰年函数返回 **1**，否则返回 **0**：

` `**`InLeapYear`**`(`<var>`t`</var>`) = `**`0`**` { 如果 ``(``(`<var>`t`</var>`)) = `**`365`**` }`
`               = `**`1`**` { 如果 ``(``(`<var>`t`</var>`)) = `**`366`**` }`

#### 月数

月份是由闭区间 **0** 到 **11** 内的一个整数确定。一个时间值 <var>t</var> 到一个月数的映射 **MonthFromTime**(<var>t</var>) 的定义为：

` `**`MonthFromTime`**`(`<var>`t`</var>`) = `**`0`**` 如果 `**`0`**` ≤ ``(`<var>`t`</var>`) < `**`31`**
`                    = `**`1`**` 如果 `**`31`**` ≤ `` (`<var>`t`</var>`) < `**`59`**` + ``(`<var>`t`</var>`)`
`                    = `**`2`**` 如果 `**`59`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`90`**` + ``(`<var>`t`</var>`)`
`                    = `**`3`**` 如果 `**`90`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`120`**` + ``(`<var>`t`</var>`)`
`                    = `**`4`**` 如果 `**`120`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`151`**` + ``(`<var>`t`</var>`)`
`                    = `**`5`**` 如果 `**`151`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`181`**` + ``(`<var>`t`</var>`)`
`                    = `**`6`**` 如果 `**`181`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`212`**` + ``(`<var>`t`</var>`)`
`                    = `**`7`**` 如果 `**`212`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`243`**` + ``(`<var>`t`</var>`)`
`                    = `**`8`**` 如果 `**`243`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`273`**` + ``(`<var>`t`</var>`)`
`                    = `**`9`**` 如果 `**`273`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`304`**` + ``(`<var>`t`</var>`)`
`                    = `**`10`**` 如果 `**`304`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`334`**` + ``(`<var>`t`</var>`)`
`                    = `**`11`**` 如果 `**`334`**` + ``(`<var>`t`</var>`) ≤ `` (`<var>`t`</var>`) < `**`365`**` + ``(`<var>`t`</var>`)`

其中

` `**`DayWithinYear`**`(`<var>`t`</var>`) = ``(`<var>`t`</var>`) - ``(``(`<var>`t`</var>`))`

月数值 **0** 指一月；**1** 指二月；**2** 指三月；**3** 指四月；**4** 指五月；**5** 指六月；**6** 指七月；**7** 指八月；**8** 指九月；**9** 指十月；**10** 指十一月；**11** 指十二月。注：(**0**) = **0**，对应 **1970 年 1 月 1 日**，星期四。

#### 日期数

一个日期数用闭区间 **1** 到 **31** 内的一个整数标识。从一个时间值 <var>t</var> 到一个日期数的映射 **DateFromTime**(<var>t</var>) 的定义为：

` `**`DateFromTime`**`(`<var>`t`</var>`) = ``(`<var>`t`</var>`) + `**`1`**` 如果 ``(`<var>`t`</var>`) = `**`0`**
`   = ``(`<var>`t`</var>`) - `**`30`**` 如果 ``(`<var>`t`</var>`) = `**`1`**
`   = ``(`<var>`t`</var>`) - `**`58`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`2`**
`   = ``(`<var>`t`</var>`) - `**`89`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`3`**
`   = ``(`<var>`t`</var>`) - `**`119`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`4`**
`   = ``(`<var>`t`</var>`) - `**`150`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`5`**
`   = ``(`<var>`t`</var>`) - `**`180`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`6`**
`   = ``(`<var>`t`</var>`) - `**`211`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`7`**
`   = ``(`<var>`t`</var>`) - `**`242`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`8`**
`   = ``(`<var>`t`</var>`) - `**`272`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`9`**
`   = ``(`<var>`t`</var>`) - `**`303`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`10`**
`   = ``(`<var>`t`</var>`) - `**`333`**` - ``(`<var>`t`</var>`) 如果 ``(`<var>`t`</var>`) = `**`11`**

#### 星期数

特定时间值 <var>t</var> 对应的星期数的定义为：

` `**`WeekDay`**`(`<var>`t`</var>`) = (``(`<var>`t`</var>`) + `**`4`**`) `[`modulo`](ES5/notation#modulo "wikilink")` `**`7`**

星期数的值 **0** 指星期日；**1** 指星期一；**2** 指星期二；**3** 指星期三；**4** 指星期四；**5** 指星期五；**6** 指星期六。注：(**0**) = **4**，对应 **1970 年 1 月 01 日** 星期四。

#### 本地时区校准

期望一个 ECMAScript 的实现确定本地时区校准。本地时区校准是一个毫秒为单位的值 **LocalTZA**，它加上 UTC 代表本地标准时间。**LocalTZA** 不体现夏令时。**LocalTZA** 值不随时间改变，但只取决于地理位置。

#### 夏令时校准

期望一个 ECMAScript 的实现确定夏令时算法。确定夏令时校准的算法 **DaylightSavingTA**(<var>t</var>)，以毫秒为单位，必须只依赖下面四个项目：

（1）自本年开始以来的时间

` `<var>`t`</var>` - ``(``(`<var>`t`</var>`))`

（2）<var>t</var> 是否在闰年内

` ``(`<var>`t`</var>`)`

（3）本年第一天的星期数

` ``(``(``(`<var>`t`</var>`))`

（4）地理位置。

ECMAScript的实现不应该尝试确定精确时间是否是夏令时，如果当前的夏令时算法已经被用在了时间上也只是确定夏令时会不会一直影响。这样避免了冲突，例如考虑到本地观测全年的夏令时。 如果宿主环境提供确定夏令时的功能，ECMAScript的实现自由映射有问题的年份到一个同等的年（相同的闰日和开始的星期）来为宿主环境提供夏令时信息。唯一的限制是它应该在处理相同的年时候产生相同的结果。

#### 本地时间

从协调世界时到本地时间的转换，定义为

` `**`LocalTime`**`(`<var>`t`</var>`) = `<var>`t`</var>` + `` + ``(`<var>`t`</var>`)`

从本地时间到协调世界时的转换，定义为

` `**`UTC`**`(`<var>`t`</var>`) = `<var>`t`</var>` - `` - ``(`<var>`t`</var>` - ``)`

#### 小时、分钟、秒、毫秒

以下函数用于分解时间值：

` `**`HourFromTime`**`(`<var>`t`</var>`) = `[`floor`](ES5/notation#floor "wikilink")`(`<var>`t`</var>` / ``) `[`modulo`](ES5/notation#modulo "wikilink")` `
` `**`MinFromTime`**`(`<var>`t`</var>`) = `[`floor`](ES5/notation#floor "wikilink")`(`<var>`t`</var>` / ``) `[`modulo`](ES5/notation#modulo "wikilink")` `
` `**`SecFromTime`**`(`<var>`t`</var>`) = `[`floor`](ES5/notation#floor "wikilink")`(`<var>`t`</var>` / ``) `[`modulo`](ES5/notation#modulo "wikilink")` `
` `**`msFromTime`**`(`<var>`t`</var>`) = `<var>`t`</var>` `[`modulo`](ES5/notation#modulo "wikilink")` `

其中

` `**`HoursPerDay`**` = `**`24`**
` `**`MinutesPerHour`**` = `**`60`**
` `**`SecondsPerMinute`**` = `**`60`**
` `**`msPerSecond`**` = `**`1000`**
` `**`msPerMinute`**` = `**`60000`**` = `**`msPerSecond`**` × `**`SecondsPerMinute`**
` `**`msPerHour`**` = `**`3600000`**` = `**`msPerMinute`**` × `**`MinutesPerHour`**

#### MakeTime (hour, min, sec, ms)

**MakeTime** 抽象操作用它的四个参数算出一个毫秒数，参数必须是 ECMAScript 数字值。此抽象操作运行如下：

1.  如果 <var>hour</var> 不是有限的或 <var>min</var> 不是有限的或 <var>sec</var> 不是有限的或 <var>ms</var> 不是有限的，返回 **NaN**。
2.  令 <var>h</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>hour</var>)。
3.  令 <var>m</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>min</var>)。
4.  令 <var>s</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>sec</var>)。
5.  令 <var>milli</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>ms</var>)。
6.  令 <var>t</var> 为 <var>h</var> × + <var>m</var> × + <var>s</var> × + <var>milli</var>，执行的四则运算根据 IEEE 754 规则（这就像使用 ECMAScript 运算符 × 和 + 一样）。
7.  返回 <var>t</var>。

#### MakeDay (year, month, date)

**MakeDay** 抽象操作用它的三个参数算出一个天数，参数必须是 ECMAScript 数字值。此抽象操作运行如下：

1.  如果 <var>year</var> 不是有限的或 <var>month</var> 不是有限的或 <var>date</var> 不是有限的，返回 **NaN**。
2.  令 <var>y</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>year</var>)。
3.  令 <var>m</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>month</var>)。
4.  令 <var>dt</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>date</var>)。
5.  令 <var>ym</var> 为 <var>y</var> + [floor](ES5/notation#floor "wikilink")(<var>m</var> / **12**)。
6.  令 <var>mn</var> 为 <var>m</var> [modulo](ES5/notation#modulo "wikilink") **12**。
7.  找一个满足 (<var>t</var>) == <var>ym</var> 且 (<var>t</var>) == <var>mn</var> 且 (<var>t</var>) == **1** 的 <var>t</var> 值；但如果这些条件是不可能的（因为有些参数超出了范围），返回 **NaN**。
8.  返回 (<var>t</var>) + <var>dt</var> - **1**。

#### MakeDate (day, time)

**MakeDate** 抽象操作用它的两个参数算出一个毫秒数，参数必须是 ECMAScript 数字值。此抽象操作运行如下：

1.  如果 <var>day</var> 不是有限的或 <var>time</var> 不是有限的，返回 **NaN**。
2.  返回 <var>day</var> × + <var>time</var>。

#### TimeClip (time)

**TimeClip** 抽象操作用它的参数算出一个毫秒数，参数必须是 ECMAScript 数字值。此抽象操作运行如下：

1.  如果 <var>time</var> 不是有限的 , 返回 **NaN**。
2.  如果 [abs](ES5/notation#abs "wikilink")(<var>time</var>) \> **8.64×10<sup>15</sup>**, 返回 **NaN**。
3.  返回 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>time</var>) 和 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>time</var>) + (**+0**) 之一，这依赖于实现 ( 加正一是为了将 **-0** 转换成 **+0** )。

#### 日期时间字符串格式

ECMAScript 定义了一个基于简化的 ISO 8601 扩展格式的日期时间的字符串互换格式，格式为：**YYYY-MM-DDTHH:mm:ss.sssZ**

其中个字段为：

|---|---|
|**YYYY**|是公历中年的十进制数字。|
|**-**|在字符串中直接以**“-”**（连字符）出现两次。|
|**MM**|是一年中的月份，从 **01**（一月）到 **12**（十二月）。|
|**DD**|是月份中的日期，从 **01** 到 **31**。|
|**T**|在字符串中直接以**“T”**出现，用来表明时间元素的开始。|
|**HH**|是用两个十进制数字表示的，自 **午夜0点** 以来的小时数。|
|**:**|在字符串中直接以**“:”**（冒号）出现两次。|
|**mm**|是用两个十进制数字表示的，自小时开始以来的分钟数。|
|**ss**|是用两个十进制数字表示的，自分开始以来的秒数。|
|**.**|在字符串中直接以**“.”**（点）出现。|
|**sss**|是用三个十进制数字表示的，自秒开始以来的毫秒数。|
|**Z**|是时区偏移量，由（**“Z”**（指 UTC）或 **“+”** 或 **“-”**）和后面跟着的时间表达式 **hh:mm** 组成。|

这个格式包括只表示日期的形式：

` YYYY`
` YYYY-MM`
` YYYY-MM-DD`

这个格式还包括“日期时间”形式，它由上面的只表示日期的形式之一和紧跟在后面的“T”和以下时间形式之一和可选的时区偏移量组成：

` THH:mm`
` THH:mm:ss`
` THH:mm:ss.sss`

所有数字必须是十进制的。如果缺少 **MM** 或 **DD** 字段，用 **“01”** 作为它们的值。如果缺少 **mm** 或 **ss** 字段，用 **“00”** 作为它们的值，对于缺少的 **sss** 用 **“000”** 作为它的值。对于缺少的时区偏移量用 **“Z”**。

一个格式字符串里有非法值（越界以及语法错误），意味着这个格式字符串不是有效的本节描述格式的实例。

##### 扩展的年

ECMAScript 需要能表示6位数年份（扩展的年份）的能力；协调世界时 **1970年1月1日** 前后分别约 **285,616** 年。对于表示 **0年** 之前或 **9999年** 之后的年份，ISO 8601 允许对年的表示法进行扩展，但只能在发送和接受信息的双方有事先共同约定的情况下才能扩展。在已经简化的 ECMAScript 的格式中这样扩展的年份表示法有2个额外的数字和始终存在的前缀符号 **+** 或 **-** 。**0年** 被认为是正的，因此用 **+** 符号作为前缀。

### 作为函数调用 Date 构造器

当把 **Date** 作为函数来调用，而不作为构造器，它返回一个表示当前时间（协调世界时）的字符串。

#### Date ( [ year [, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ] ] ] )

所有参数都是可选的；接受提供的任何参数，但被完全忽略。返回一个仿佛是用表达式 **(new Date()).toString()** 创建的字符串，这里的 **Date** 是标准内置构造器，**toString** 是标准内置方法 **Date.prototype.toString**。

### Date 构造器

当把 **Date** 作为 **new** 表达式的一部分来调用，它是个构造器：它初始化新创建的对象。

#### new Date (year, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ] )

当用二到七个参数调用 **Date** 构造器，它用 <var>year</var>、<var>month</var> 还有（可选的）<var>date</var>、<var>hours</var>、<var>minutes</var>、<var>seconds</var>、<var>ms</var> 来计算时间。

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为原始的时间原型对象，它是 [Date.prototype](#x15.9.4.1 "wikilink") 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"Date"**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **ture**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性按照以下步骤设定：

1.  令 <var>y</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>year</var>)。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>month</var>)。
3.  如果提供了 <var>date</var>，则令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)；否则令 <var>dt</var> 为 **1**。
4.  如果提供了 <var>hours</var>，则令 <var>h</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>hours</var>)；否则令 <var>h</var> 为 **0**。
5.  如果提供了 <var>minutes</var>，则令 <var>min</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>minutes</var>)；否则令 <var>min</var> 为 **0**。
6.  如果提供了 <var>seconds</var>，则令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>seconds</var>)；否则令 <var>s</var> 为 **0**。
7.  如果提供了 <var>ms</var>，则令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)；否则令 <var>milli</var> 为 **0**。
8.  如果 <var>y</var> 不是 **NaN** 且 **0** ≤ [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>y</var>) ≤ **99**，则令 <var>yr</var> 为 **1900**+[ToInteger](ES5/conversion#ToInteger "wikilink")(<var>y</var>)；否则令 <var>yr</var> 为 <var>y</var>。
9.  令 <var>finalDate</var> 为 ((<var>yr</var>, <var>m</var>, <var>dt</var>), (<var>h</var>, <var>min</var>, <var>s</var>, <var>milli</var>))。
10. 设定新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 ((finalDate))。

#### new Date (value)

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为原始的时间原型对象，它是 [Date.prototype](#x15.9.4.1 "wikilink") 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"Date"**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **ture**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性按照以下步骤设定：

1.  令 <var>v</var> 为 [ToPrimitive](ES5/conversion#ToPrimitive "wikilink")(<var>value</var>)。
2.  如果 [Type](ES5/types#Type "wikilink")(<var>v</var>) 是 **String**，则
    1.  用与 **parse** 方法 ([15.9.4.2](#x15.9.4.2 "wikilink")) 完全相同的方式将 <var>v</var> 解析为一个日期时间；令 <var>V</var> 为这个日期时间的时间值。

3.  否则，令 <var>V</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>v</var>)。
4.  设定新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 (<var>V</var>)，并返回这个值。

#### new Date ( )

新构造对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性设定为原始的时间原型对象，它是 [Date.prototype](#x15.9.4.1 "wikilink") 的初始值。

新构造对象的 [[[Class]]](ES5/types#Class "wikilink") 内部属性设定为 **"Date"**。

新构造对象的 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性设定为 **ture**。

新构造对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性设定为表示当前时间的时间值（协调世界时）。

### Date 构造器的属性

**Date** 构造器的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值是 [Function 原型对象](#x15.3.4 "wikilink")。

除了内部属性和 **length** 属性 ( 值为 **7** ) 之外，**Date** 构造器还有以下属性：

#### Date.prototype

**Date.prototype** 的初始值是内置的 [Date''' 原型对象](#x15.9.5 "wikilink")。

此属性有特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### Date.parse (string)

**parse** 函数对它的参数应用 [ToString](ES5/conversion#ToString "wikilink") 操作并将结果字符串解释为一个日期和时间；返回一个数字值，是对应这个日期时间的 UTC 时间值。字符串可解释为本地时间，UTC 时间，或某个其他时区的时间，这取决于字符串里的内容。此函数首先尝试根据日期时间字符串格式（[15.9.1.15](#x15.9.1.15 "wikilink")）里的规则来解析字符串的格式。如果字符串不符合这个格式此函数可回退，用任意实现定义的试探方式或日期格式。无法识别的字符串或日期时间包含非法元素值，将导致 **Date.parse** 返回 **NaN**。

在所有属性都指向它们的初始值的情况下，如果 <var>x</var> 是一个在特定 ECMAScript 的实现里的毫秒数为零的任意 **Date** 对象，则在这个实现中以下所有表达式应产生相同数字值：

` x.valueOf()`
` Date.parse(x.toString())`
` Date.parse(x.toUTCString())`
` Date.parse(x.toISOString())`

然而，表达式

` Date.parse( x.toLocaleString())`

是不需要产生与前面三个表达参数相同的数字值。通常，在给定的字符串不符合日期时间字符串格式（[15.9.1.15](#x15.9.1.15 "wikilink")）时，**Date.parse** 的产生值是依赖于实现，并且在同一实现中 **toString** 或 **toUTCString** 方法不能产生不符合日期时间字符串格式的字符串。

#### Date.UTC (year, month [, date [, hours [, minutes [, seconds [, ms ] ] ] ] ])

当用少于两个的参数调用 **UTC** 函数时，它的行为是依赖于实现的。当用二到七个参数调用 **UTC** 函数，它从 <var>year</var>、<var>month</var> 和（可选的）<var>date</var>、<var>hours</var>、<var>minutes</var>、<var>seconds</var>、<var>ms</var> 计算出日期时间。采用以下步骤：

1.  令 <var>y</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>year</var>)。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>month</var>)。
3.  如果提供了 <var>date</var>，则令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)；否则令 <var>dt</var> 为 **1**。
4.  如果提供了 <var>hours</var>，则令 <var>h</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>hours</var>)；否则令 <var>h</var> 为 **0**。
5.  如果提供了 <var>minutes</var>，则令 <var>min</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>minutes</var>)；否则令 <var>min</var> 为 **0**。
6.  如果提供了 <var>seconds</var>，则令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>seconds</var>);；否则令 <var>s</var> 为 **0**。
7.  如果提供了 <var>ms</var>，则令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)；否则令 <var>milli</var> 为 **0**。
8.  如果 <var>y</var> 不是 **NaN** 且 **0** ≤ [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>y</var>) ≤ **99**，则令 <var>yr</var> 为 **1900** + [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>y</var>)；否则令 <var>yr</var> 为 <var>y</var>。
9.  返回 (((<var>yr</var>, <var>m</var>, <var>dt</var>), (<var>h</var>, <var>min</var>, <var>s</var>, <var>milli</var>)))。

**UTC** 函数的 **length** 属性是 **7**。

#### Date.now ( )

**now** 函数返回一个数字值，它表示调用 **now** 时的 **UTC** 日期时间的时间值。

### Date 原型对象的属性

**Date** 原型对象自身是一个 **Date** 对象（其 [[[Class]]](ES5/types#Class "wikilink") 是 **"Date"**），其 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 是 **NaN** 。

**Date** 原型对象的 [[[Prototype]]](ES5/types#Prototype "wikilink") 内部属性的值是标准内置 [Object''' 原型对象](#x15.2.4 "wikilink")。

在以下对 **Date** 原型对象的函数属性的描述中，短语**“this Date 对象”**指调用函数时的 **this** 值对象。除非另外说明，这些函数不是通用的；如果 this 值不是 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Date"** 的对象，则抛出一个 **TypeError** 异常。短语**“this 时间值”**指代表 **this Date 对象** 的时间值的数字值，它是 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性的值。

#### Date.prototype.constructor

**Date.prototype.constructor** 的初始值是内置 **Date** 构造器。

#### Date.prototype.toString ( )

此函数返回一个字符串值。字符串中内容是依赖于实现的，但目的是用一种方便，人类可读的形式表示当前时区的时间。

#### Date.prototype.toDateString ( )

此函数返回一个字符串值。字符串中内容是依赖于实现的，但目的是用一种方便，人类可读的形式表示当前时区时间的“日期”部分。

#### Date.prototype.toTimeString ( )

此函数返回一个字符串值。字符串中内容是依赖于实现的，但目的是用一种方便，人类可读的形式表示当前时区时间的“时间”部分。

#### Date.prototype.toLocaleString ( )

这个函数返回一个 String 值。String 的内容由实现决定，但它的目的是使用一种与宿主环境的语言习惯对应的人类可读形式来方便地表述当前时区中的 Date。

#### Date.prototype.toLocaleDateString ( )

这个函数返回一个 String 值。String 的内容由实现决定，但它的目的是使用一种与宿主环境的语言习惯对应的人类可读形式来方便地表述当前时区中的 Date 的日期部分。

#### Date.prototype.toLocaleTimeString ( )

这个函数返回一个 String 值。String 的内容由实现决定，但它的目的是使用一种与宿主环境的语言习惯对应的人类可读形式来方便地表述当前时区中的 Date 的时间部分。

#### Date.prototype.valueOf ( )

**valueOf** 函数返回一个数字值，它是 **this 时间值**。

#### Date.prototype.getTime ( )

1.  返回 **this 时间值**。

#### Date.prototype.getFullYear ( ) 

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCFullYear ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getMonth ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCMonth ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getDate ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCDate ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getDay ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCDay ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getHours ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCHours ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getMinutes ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCMinutes ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getSeconds ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCSeconds ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getMilliseconds ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ((<var>t</var>))。

#### Date.prototype.getUTCMilliseconds ( )

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 (<var>t</var>)。

#### Date.prototype.getTimezoneOffset ( )

返回本地时间和 UTC 时间之间相差的分钟数。

1.  令 <var>t</var> 为 **this 时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 ( <var>t</var> - (<var>t</var>) ) / )。

#### Date.prototype.setTime (time)

1.  令 <var>v</var> 为 ([ToNumber](ES5/conversion#ToNumber "wikilink")(<var>time</var>))。
2.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
3.  返回 <var>v</var>。

#### Date.prototype.setMilliseconds (ms)

1.  令 <var>t</var> 为 (**this 时间值**) 的结果。
2.  令 <var>time</var> 为 ((<var>t</var>), (<var>t</var>), (<var>t</var>), [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>))。
3.  令 <var>u</var> 为 ((((<var>t</var>), <var>time</var>)))。
4.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
5.  返回 <var>u</var>。

#### Date.prototype.setUTCMilliseconds (ms)

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>time</var> 为 ((<var>t</var>), (<var>t</var>), (<var>t</var>), [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>))。
3.  令 <var>v</var> 为 (((<var>t</var>), <var>time</var>))。
4.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
5.  返回 <var>v</var>。

#### Date.prototype.setSeconds (sec [, ms ] )

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getMilliseconds](#x15.9.5.24 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果。
2.  令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
3.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
4.  令 <var>date</var> 为 ((<var>t</var>), ((<var>t</var>), (<var>t</var>), <var>s</var>, <var>milli</var>))。
5.  令 <var>u</var> 为 ((<var>date</var>))。
6.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
7.  返回 <var>u</var>。

**setSeconds** 方法的 **length** 属性是 **2**。

#### Date.prototype.setUTCSeconds (sec [, ms ] )

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getUTCMilliseconds](#x15.9.5.25 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
3.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 milli 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
4.  令 <var>date</var> 为 ((<var>t</var>), ((<var>t</var>), (<var>t</var>), <var>s</var>, <var>milli</var>))。
5.  令 <var>v</var> 为 (<var>date</var>)。
6.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
7.  返回 <var>v</var>。

**setUTCSeconds** 方法的 **length** 属性是 **2**。

#### Date.prototype.setMinutes (min [, sec [, ms ] ] )

没指定 <var>sec</var> 参数时的行为是，仿佛 <var>sec</var> 被指定为调用 [getSeconds](#x15.9.5.22 "wikilink")() 的结果一样。

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getMilliseconds](#x15.9.5.24 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>min</var>)。
3.  如果没指定 <var>sec</var>，则令 <var>s</var> 为 (<var>t</var>)；否则，令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
4.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
5.  令 <var>date</var> 为 ((<var>t</var>)，((<var>t</var>), <var>m</var>, <var>s</var>, <var>milli</var>))。
6.  令 <var>u</var> 为 ((<var>date</var>))。
7.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
8.  返回 <var>u</var>。

**setMinutes** 方法的 **length** 属性是 **3**。

#### Date.prototype.setUTCMinutes (min [, sec [, ms ] ] )

没指定 <var>sec</var> 参数时的行为是，仿佛 <var>sec</var> 被指定为调用 [getUTCSeconds](#x15.9.5.23 "wikilink")() 的结果一样。

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getUTCMilliseconds](#x15.9.5.25 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>min</var>)。
3.  如果没指定 <var>sec</var>，则令 <var>s</var> 为 (<var>t</var>)；否则，令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
4.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
5.  令 <var>date</var> 为 ((<var>t</var>)，((<var>t</var>), <var>m</var>, <var>s</var>, <var>milli</var>))。
6.  令 <var>v</var> 为 (<var>date</var>)。
7.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
8.  返回 <var>v</var>。

**setUTCMinutes** 方法的 **length** 属性是 **3**。

#### Date.prototype.setHours (hour [, min [, sec [, ms ] ] ] )

没指定 <var>min</var> 参数时的行为是，仿佛 <var>min</var> 被指定为调用 [getMinutes](#x15.9.5.20 "wikilink")() 的结果一样。

没指定 <var>sec</var> 参数时的行为是，仿佛 <var>sec</var> 被指定为调用 [getSeconds](#x15.9.5.22 "wikilink")() 的结果一样。

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getMilliseconds](#x15.9.5.24 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果。
2.  令 <var>h</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>hour</var>)。
3.  如果没指定 <var>min</var>，则令 <var>m</var> 为 (<var>t</var>)；否则，令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>min</var>)。
4.  如果没指定 <var>sec</var>，则令 <var>s</var> 为 (<var>t</var>)；否则，令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
5.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
6.  令 <var>date</var> 为 ((<var>t</var>), (<var>h</var>, <var>m</var>, <var>s</var>, <var>milli</var>))。
7.  令 <var>u</var> 为 ((<var>date</var>))。
8.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
9.  返回 <var>u</var>。

**setHours** 方法的 **length** 属性是 **4**。

#### Date.prototype.setUTCHours (hour [, min [, sec [, ms ] ] ] )

没指定 <var>min</var> 参数时的行为是，仿佛 <var>min</var> 被指定为调用 [getUTCMinutes](#x15.9.5.21 "wikilink")() 的结果一样。

没指定 <var>sec</var> 参数时的行为是，仿佛 <var>sec</var> 被指定为调用 [getUTCSeconds](#x15.9.5.23 "wikilink")() 的结果一样。

没指定 <var>ms</var> 参数时的行为是，仿佛 <var>ms</var> 被指定为调用 [getUTCMilliseconds](#x15.9.5.25 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>h</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>hour</var>)。
3.  如果没指定 <var>min</var>，则令 <var>m</var> 为 (<var>t</var>)；否则，令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>min</var>)。
4.  如果没指定 <var>sec</var>，则令 <var>s</var> 为 (<var>t</var>)；否则，令 <var>s</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>sec</var>)。
5.  如果没指定 <var>ms</var>，则令 <var>milli</var> 为 (<var>t</var>)；否则，令 <var>milli</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>ms</var>)。
6.  令 <var>date</var> 为 ((<var>t</var>), (<var>h</var>, <var>m</var>, <var>s</var>, <var>milli</var>))。
7.  令 <var>v</var> 为 (<var>date</var>)。
8.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
9.  返回 <var>v</var>。

**setUTCHours** 方法的 **length** 属性是 **4**。

#### Date.prototype.setDate (date)

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果。
2.  令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)。
3.  令 <var>newDate</var> 为 (((<var>t</var>), (<var>t</var>), <var>dt</var>), (<var>t</var>))。
4.  令 <var>u</var> 为 ((<var>newDate</var>))。
5.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
6.  返回 <var>u</var>。

#### Date.prototype.setUTCDate (date)

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)。
3.  令 <var>newDate</var> 为 (((<var>t</var>), (<var>t</var>), <var>dt</var>), (<var>t</var>))。
4.  令 <var>v</var> 为 (<var>newDate</var>)。
5.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
6.  返回 <var>v</var>。

#### Date.prototype.setMonth (month [, date ] )

没指定 <var>date</var> 参数时的行为是，仿佛 <var>date</var> 被指定为调用 [getDate](#x15.9.5.14 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>month</var>)。
3.  如果没指定 <var>date</var>，则令 <var>dt</var> 为 (<var>t</var>)；否则，令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)。
4.  令 <var>newDate</var> 为 (((<var>t</var>), <var>m</var>, <var>dt</var>), (<var>t</var>))。
5.  令 <var>u</var> 为 ((<var>newDate</var>))。
6.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
7.  返回 <var>u</var>。

**setMonth** 方法的 **length** 属性是 **2**。

#### Date.prototype.setUTCMonth (month [, date ] )

没指定 date 参数时的行为是，仿佛 date 被指定为调用 [getUTCDate](#x15.9.5.15 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 **this 时间值**。
2.  令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>month</var>)。
3.  如果没指定 <var>date</var>，则令 <var>dt</var> 为 (t)；否则，令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)。
4.  令 <var>newDate</var> 为 (((<var>t</var>), <var>m</var>, <var>dt</var>), (<var>t</var>))。
5.  令 <var>v</var> 为 (<var>newDate</var>)。
6.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
7.  返回 <var>v</var>。

**setUTCMonth** 方法的 **length** 属性是 **2**。

#### Date.prototype.setFullYear (year [, month [, date ] ] ) 

没指定 <var>month</var> 参数时的行为是，仿佛 <var>month</var> 被指定为调用 [getMonth](#x15.9.5.12 "wikilink")() 的结果一样。

没指定 <var>date</var> 参数时的行为是，仿佛 <var>date</var> 被指定为调用 [getDate](#x15.9.5.14 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 ( **this 时间值** ) 的结果；但如果 **this 时间值** 是 **NaN**，则令 <var>t</var> 为 **+0**。
2.  令 <var>y</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>year</var>)。
3.  如果没指定 <var>month</var>，则令 <var>m</var> 为 (<var>t</var>)；否则，令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(month)。
4.  如果没指定 <var>date</var>，则令 <var>dt</var> 为 (<var>t</var>)；否则，令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(date)。
5.  令 <var>newDate</var> 为 ((<var>y</var>, <var>m</var>, <var>dt</var>), (t))。
6.  令 <var>u</var> 为 ((<var>newDate</var>))。
7.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>u</var>。
8.  返回 <var>u</var>。

**setFullYear** 方法的 **length** 属性是 **3**。

#### Date.prototype.setUTCFullYear (year [, month [, date ] ] )

没指定 <var>month</var> 参数时的行为是，仿佛 <var>month</var> 被指定为调用 [getUTCMonth](#x15.9.5.13 "wikilink")() 的结果一样。

没指定 <var>date</var> 参数时的行为是，仿佛 <var>date</var> 被指定为调用 [getUTCDate](#x15.9.5.15 "wikilink")() 的结果一样。

1.  令 <var>t</var> 为 **this 时间值**；但如果 **this 时间值** 是 **NaN**，则令 <var>t</var> 为 **+0**。
2.  令 <var>y</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>year</var>)。
3.  如果没指定 <var>month</var>，则令 <var>m</var> 为 (<var>t</var>)；否则，令 <var>m</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>month</var>)。
4.  如果没指定 <var>date</var>，则令 <var>dt</var> 为 (<var>t</var>)；否则，令 <var>dt</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>date</var>)。
5.  令 <var>newDate</var> 为 ((<var>y</var>, <var>m</var>, <var>dt</var>), (<var>t</var>))。
6.  令 <var>v</var> 为 (<var>newDate</var>)。
7.  设定 **this Date 对象** 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性为 <var>v</var>。
8.  返回 <var>v</var>。

**setUTCFullYear** 方法的 **length** 属性是 **3**。

#### Date.prototype.toUTCString ( ) 

此函数返回一个字符串值。字符串中内容是依赖于实现的，但目的是用一种方便，人类可读的形式表示 UTC 时间。

#### Date.prototype.toISOString ( )

此函数返回一个代表 **this Date 对象**表示的时间实例 的字符串。字符串的格式是 [15.9.1.15](#x15.9.1.15 "wikilink") 定义的日期时间字符串格式。字符串中包含所有的字段。字符串表示的时区总是 UTC，用后缀 **Z** 标记。如果 **this** 对象的时间值不是有限的数字值，抛出一个 **RangeError** 异常。

#### Date.prototype.toJSON ( key )

此函数为 **JSON.stringify** ([15.12.3](#x15.12.3 "wikilink")) 提供 **Date** 对象的一个字符串表示。

当用参数 <var>key</var> 调用 **toJSON** 方法，采用以下步骤：

1.  令 <var>O</var> 为 以 **this** 值为参数调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果。
2.  令 <var>tv</var> 为 [ToPrimitive](ES5/conversion#ToPrimitive "wikilink")(<var>O</var>, **暗示 Number**)。
3.  如果 <var>tv</var> 是一个数字值且不是有限的，返回 **null**。
4.  令 <var>toISO</var> 为以 **"toISOString"** 为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
5.  如果 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>toISO</var>) 是 **false**，抛出一个 **TypeError** 异常。
6.  <var>O</var> 作为以 **this** 值并用空参数列表调用 <var>toISO</var> 的 [[[Call]]](ES5/types#Call "wikilink") 内部方法，返回结果。

### Date 实例的属性

**Date** 实例从 **Date** 原型对象继承属性，**Date** 实例的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值是 **"Date"**。**Date** 实例还有一个 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性。

[[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性是代表 **this Date 对象** 的时间值。

RegExp 对象
-----------

一个 **RegExp** 对象包含一个正则表达式和关联的标志。

### 模式（Patterns）

**RegExp** 构造器对输入模式字符串应用以下文法。如果文法无法将字符串解释为 **Pattern** 的一个展开形式，则发生错误。

语法：

` `*<b id="Pattern">`Pattern`</b>*` :: `
`   `**

` `*<b id="Disjunction">`Disjunction`</b>*` :: `
`   `**
`   `**` `**`|`**` `**` `

` `*<b id="Alternative">`Alternative`</b>*` :: `
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

` `*<b id="Term">`Term`</b>*` ::`
`   `**
`   `**
`   `**` `**

` `*<b id="Assertion">`Assertion`</b>*` ::`
`   `**`^`**` `
`   `**`$`**` `
`   `**`\` `b`**` `
`   `**`\` `B`**` `
`   `**`(`**` `**`?`**` `**`=`**` `**` `**`)`**` `
`   `**`(`**` `**`?`**` `**`!`**` `**` `**`)`**` `

` `*<b id="Quantifier">`Quantifier`</b>*` ::`
`   `**
`   `**` `**`?`**` `

` `*<b id="QuantifierPrefix">`QuantifierPrefix`</b>*` ::`
`   `**`*`**` `
`   `**`+`**` `
`   `**`?`**` `
`   `**`{`**` `*[`DecimalDigits`](#ES5/lexical#DecimalDigits "wikilink")*` `**`}`**` `
`   `**`{`**` `*[`DecimalDigits`](#ES5/lexical#DecimalDigits "wikilink")*` `**`,`**` `**`}`**` `
`   `**`{`**` `*[`DecimalDigits`](#ES5/lexical#DecimalDigits "wikilink")*` `**`,`**` `*[`DecimalDigits`](#ES5/lexical#DecimalDigits "wikilink")*` `**`}`**` `

` `*<b id="Atom">`Atom`</b>*` ::`
`   `**
`   `**`.`**` `
`   `**`\`**` `**
`   `**` `
`   `**`(`**` `**` `**`)`**` `
`   `**`(`**` `**`?`**` `**`:`**` `**` `**`)`**` `

` `*<b id="PatternCharacter">`PatternCharacter`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not` `one` `of`**
`   `**`^` `$` `\` `.` `*` `+` `?` `(` `)` `[` `]` `{` `}` `|`**

` `*<b id="AtomEscape">`AtomEscape`</b>*` ::`
`   `**` `
`   `**
`   `**` `

` `*<b id="CharacterEscape">`CharacterEscape`</b>*` ::`
`   `**
`   `**`c`**` `**` `
`   `*[`HexEscapeSequence`](ES5/lexical#HexEscapeSequence "wikilink")*` `
`   `*[`UnicodeEscapeSequence`](ES5/lexical#UnicodeEscapeSequence "wikilink")*` `
`   `**` `

` `*<b id="ControlEscape">`ControlEscape`</b>*` :: `**`one` `of`**
`   `**`f` `n` `r` `t` `v`**` `` `

` `*<b id="ControlLetter">`ControlLetter`</b>*` :: `**`one` `of`**
`   `**`a` `b` `c` `d` `e` `f` `g` `h` `i` `j` `k` `l` `m` `n` `o` `p` `q` `r` `s` `t` `u` `v` `w` `x` `y` `z`**
`   `**`A` `B` `C` `D` `E` `F` `G` `H` `I` `J` `K` `L` `M` `N` `O` `P` `Q` `R` `S` `T` `U` `V` `W` `X` `Y` `Z`**

` `*<b id="IdentityEscape">`IdentityEscape`</b>*` ::`
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not`**` `*[`IdentifierPart`](ES5/lexical#IdentifierPart "wikilink")*
`   `<ZWJ>
`   `<ZWNJ>

` `*<b id="DecimalEscape">`DecimalEscape`</b>*` ::`
`   `*[`DecimalIntegerLiteral`](ES5/lexical#DecimalIntegerLiteral "wikilink")*` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `*[`DecimalDigit`](#ES5/lexical#DecimalDigit "wikilink")*`]`

` `*<b id="CharacterClassEscape">`CharacterClassEscape`</b>*` :: `**`one` `of`**
`   `**`d` `D` `s` `S` `w` `W`**` `

` `*<b id="CharacterClass">`CharacterClass`</b>*` :: `
`   `**`[`**` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` {`**`^`**`}] `**` `**`]`**
`   `**`[`**` `**`^`**` `**` `**`]`**` `

` `*<b id="ClassRanges">`ClassRanges`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**

` `*<b id="NonemptyClassRanges">`NonemptyClassRanges`</b>*` ::`
`   `**
`   `**` `**
`   `**` - `**` `**` `

` `*<b id="NonemptyClassRangesNoDash">`NonemptyClassRangesNoDash`</b>*` ::`
`   `**
`   `**` `**
`   `**` - `**` `**

` `*<b id="ClassAtom">`ClassAtom`</b>*` ::`
`   `**`-`**
`   `**

` `*<b id="ClassAtomNoDash">`ClassAtomNoDash`</b>*` :: `
`   `*[`SourceCharacter`](ES5#SourceCharacter "wikilink")*` `**`but` `not`**` `**`\`**`、`**`]`**`、'''- '''`
`   `**`\`**` `**

` `*<b id="ClassEscape">`ClassEscape`</b>*` ::`
`   `**
`   `**`b`**` `
`   `**
`   `**

### 模式语义（Pattern Semantics）

使用下面描述的过程来将一个正则表达式模式转换为一个内部程序。实现使用比下面列出的算法跟高效的算法是被鼓励的，只要结果是相同的。内部程序用作 **RegExp** 对象的 [[[Match]]](ES5/types#Match "wikilink") 内部属性的值。

#### 表示法（Notation）

后面的描述用到以下变量：

-   ，是正则表达式模式要匹配的字符串。符号 **Input[**<var>n</var>**]** 表示 **Input** 的第 <var>n</var> 个字符，这里的 <var>n</var> 可以是 **0**（包括）和 **InputLength**（不包括）之间的。

-   ，是 字符串里的字符数目。

-   <b id="NcapturingParens">NcapturingParens</b>，是在模式中左捕获括号的总数（即，** :: **(** ** **)** 产生式被展开的总次数）。一个左捕获括号是匹配产生式 ** :: **(** ** **)** 中的 终结符 **(** 的任意 **(** 模式字符。
-   <b id="IgnoreCase">IgnoreCase</b>，是 **RegExp** 对象的 **ignoreCase** 属性的设定值。
-   <b id="Multiline">Multiline</b>，是 **RegExp** 对象的 **multiline** 属性的设定值。

此外，后面的描述用到以下内部数据结构：

-   <b id="CharSet">CharSet</b>，是字符的一个数学上的集合。
-   <b id="State">State</b>，是一个有序对 (<var>endIndex</var>, <var>captures</var>) ，这里 <var>endIndex</var> 是一个整数，<var>captures</var> 是有 个值的内部数组。 **State** 用来表示正则表达式匹配算法里的局部匹配状态。<var>endIndex</var> 是到目前为止模式匹配的最后一个输入字符的索引值加上一，而 <var>captures</var> 持有捕获括号的捕获结果。<var>captures</var> 的第 <var>n</var> 个元素是一个代表第 <var>n</var> 个捕获括号对捕获值的字符串，或如果第 <var>n</var> 个捕获括号对未能达到目的，<var>captures</var> 的第 <var>n</var> 个元素是 **undefined**。由于回溯，很多 **State** 可能在匹配过程中的任何时候被使用。
-   <b id="MatchResult">MatchResult</b>，值为 或表示匹配失败特殊记号 **failure**。
-   <b id="Continuation">Continuation</b> 程序，是一个内部闭包（即，一些参数已经绑定了值的内部程序），它用一个 参数返回一个 结果。 如果一个内部闭包引用的变量是绑定在创建这个闭包的函数里 , 则闭包使用在创建闭包时的这些变量值。**Continuation** 尝试从其 参数给定的中间状态开始用模式的其余部分（由闭包的已绑定参数指定）匹配输入字符串。如果匹配成功，**Continuation** 返回最终的 ；如果匹配失败，**Continuation** 返回 **failure**。
-   <b id="Matcher">Matcher</b> 程序，是一个需要两个参数： 和 ，的内部闭包，它返回一个 结果。 **Matcher** 尝试从其 参数给定的中间状态开始用模式的一个中间子模式（由闭包的已绑定参数指定）匹配输入字符串。 参数是去匹配模式中剩余部分的闭包。用模式的子模式匹配之后获得一个新 ，之后 **Matcher** 用新 去调用 来测试模式的剩余部分是否能匹配成功。如果匹配成功，**Matcher** 返回 返回的 ；如果匹配失败，**Matcher** 尝试用不同的可选位置重复调用 ，直到 匹配成功或用尽所有的可选位置。
-   <b id="AssertionTester">AssertionTester</b> 程序，是需要一个 参数并返回一个布尔结果的内部闭包。 **AssertionTester** 测试输入字符串的当前位置是否满足一个特定条件 ( 由闭包的已绑定参数指定 ) ，如果匹配了条件，返回 **true**；如果不匹配，返回 **false**。
-   <b id="EscapeValue">EscapeValue</b>，是一个字符或一个整数。**EscapeValue** 用来表示 转移序列的解释结果：一个字符 <var>ch</var> 在转义序列里时，它被解释为字符 <var>ch</var>；而一个整数 <var>n</var> 在转义序列里时，它被解释为对第 <var>n</var> 个捕获括号组的反响引用。

#### 模式（）

产生式 ** :: ** 按照以下方式解释执行 :

1.  解释执行 ** ，获得一个 <var>m</var>。
2.  返回一个需要两个参数的内部闭包，一个字符串 <var>str</var> 和一个整数 <var>index</var>，执行方式如下：
    1.  令 为给定的字符串 <var>str</var>。[15.10.2](#x15.10.2 "wikilink") 中的算法都将用到此变量。
    2.  令 为 的长度。[15.10.2](#x15.10.2 "wikilink") 中的算法都将用到此变量。
    3.  令 <var>c</var> 为 一个 ，它始终对它的任何 参数都返回成功匹配的 。
    4.  令 <var>cap</var> 为一个有 个 **undefined** 值的内部数组，索引是从 **1** 到 。
    5.  令 <var>x</var> 为 (<var>index</var>, <var>cap</var>)。
    6.  调用 <var>m</var>(<var>x</var>, <var>c</var>)，并返回结果。

#### 析取（）

产生式 ** :: ** 的解释执行，是解释执行 ** 来获得 并返回这个 。

产生式 ** :: ** **|** ** 按照以下方式解释执行：

1.  解释执行 ** 来获得一个 <var>m1</var>。
2.  解释执行 ** 来获得一个 <var>m2</var>。
3.  返回一个需要两个参数的内部闭包 ，参数分别是一个 <var>x</var> 和一个 <var>c</var>，此内部闭包的执行方式如下：
    1.  调用 <var>m1</var>(<var>x</var>, <var>c</var>) 并令 <var>r</var> 为其结果。
    2.  如果 <var>r</var> 不是 **failure**，返回 <var>r</var>。
    3.  调用 <var>m2</var>(<var>x</var>, <var>c</var>) 并返回其结果。

#### 选择项（）

产生式 ** :: [[empty](ES5/notation#empty "wikilink")] 解释执行返回一个 ，它需要两个参数，一个 <var>x</var> 和 一个 <var>c</var>，并返回调用 <var>c</var>(<var>x</var>) 的结果。

产生式 ** :: ** ** 按照如下方式解释执行：

1.  解释执行 ** 来获得一个 <var>m1</var>。
2.  解释执行 ** 来获得一个 <var>m2</var>。
3.  返回一个内部闭包 ，它需要两个参数，一个 <var>x</var> 和一个 <var>c</var>，执行方式如下 :
    1.  创建一个 <var>d</var>，它需要一个 参数 <var>y</var>，返回调用 <var>m2</var>(<var>y</var>，<var>c</var>) 的结果。
    2.  调用 <var>m1</var>(<var>x</var>, <var>d</var>) 并返回结果。

#### 匹配项（）

产生式 ** :: ** 解释执行，返回一个需要两个参数 <var>x</var> 和 <var>c</var> 的内部闭包 ，它的执行方式如下：

1.  解释执行 ** 来获得一个 <var>t</var>。
2.  调用 <var>t</var>(<var>x</var>) 并令 <var>r</var> 为调用结果布尔值。
3.  如果 <var>r</var> 是 **false**，返回 **failure**。
4.  调用 <var>c</var>(<var>x</var>) 并返回结果。

产生式 ** :: ** 的解释执行方式是，解释执行 ** 来获得一个 并返回这个 。

产生式 ** :: ** ** 的解释执行方式如下 :

1.  解释执行 ** 来获得一个 <var>m</var>。
2.  解释执行 ** 来获得三个结果值：一个整数 <var>min</var>，一个整数（或 **∞**）<var>max</var>，和一个布尔值 <var>greedy</var>。
3.  如果 <var>max</var> 是有限的 且小于 <var>min</var>，则抛出一个 **SyntaxError** 异常。
4.  令 <var>parenIndex</var> 为整个正则表达式中在此产生式 ** 展开形式左侧出现的左匹配括号的数目。这是此产生式 ** 前面展开的 ** :: **(** ** **)** 产生式总数与此 ** 里面的 ** :: **(** ** **)** 产生式总数之和。
5.  令 <var>parenCount</var> 为在展开的 ** 产生式里的左捕获括号数目。这是 ** 产生式里面 ** :: **(** ** **)** 产生式的总数。
6.  返回一个需要两个参数 <var>x</var> 和 <var>c</var> 的内部闭包 ，执行方式如下：
    1.  调用 (<var>m</var>, <var>min</var>, <var>max</var>, <var>greedy</var>, <var>x</var>, <var>c</var>, <var>parenIndex</var>, <var>parenCount</var>)，并返回结果。

抽象操作 **RepeatMatcher** 需要八个参数，一个 <var>m</var>，一个整数 <var>min</var>，一个整数（或 **∞**）<var>max</var>，一个布尔值 <var>greedy</var>，一个 <var>x</var>，一个 <var>c</var>，一个整数 <var>parenIndex</var>，一个整数 <var>parenCount</var>，执行方式如下：

1.  如果 <var>max</var> 是零，则调用 <var>c</var>(<var>x</var>)，并返回结果。
2.  创建需要一个 参数 <var>y</var> 的内部 闭包 <var>d</var>，执行方式如下：
    1.  如果 <var>min</var> 是零 且 <var>y</var> 的 <var>endIndex</var> 等于 <var>x</var> 的 <var>endIndex</var>，则返回 **failure**。
    2.  如果 <var>min</var> 是零，则令 <var>min2</var> 为零；否则令 <var>min2</var> 为 <var>min</var>-**1**。
    3.  如果 <var>max</var> 是 **∞**，则令 <var>max2</var> 为 **∞**；否则令 <var>max2</var> 为 <var>max</var>-**1**。
    4.  调用 **RepeatMatcher**(<var>m</var>, <var>min2</var>, <var>max2</var>, <var>greedy</var>, <var>y</var>, <var>c</var>, <var>parenIndex</var>, <var>parenCount</var>)，并返回结果。

3.  令 <var>cap</var> 为 <var>x</var> 的捕获内部数组的一个拷贝。
4.  对所有满足条件 <var>parenIndex</var> \< <var>k</var> 且 <var>k</var> ≤ <var>parenIndex</var>+<var>parenCount</var> 的整数 <var>k</var>，设定 <var>cap</var>[<var>k</var>] 为 <var>undefined</var>。
5.  令 <var>e</var> 为 <var>x</var> 的 <var>endIndex</var>。
6.  令 <var>xr</var> 为 值 (<var>e</var>, <var>cap</var>)。
7.  如果 <var>min</var> 不是零，则调用 <var>m</var>(<var>xr</var>, <var>d</var>)，并返回结果。
8.  如果 <var>greedy</var> 是 <var>false</var>，则
    1.  令 <var>z</var> 为调用 <var>c</var>(<var>x</var>) 的结果。
    2.  如果 <var>z</var> 不是 **failure**，返回 <var>z</var>。
    3.  调用 <var>m</var>(<var>xr</var>, <var>d</var>)，并返回结果。

9.  令 <var>z</var> 为调用 <var>m</var>(<var>xr</var>, <var>d</var>) 的结果。
10. 如果 <var>z</var> 不是 **failure**，返回 <var>z</var>。
11. 调用 <var>c</var>(<var>x</var>)，并返回结果。

#### 断言（）

产生式 ** :: **\^** 解释执行返回一个 ，它需要1个参数 <var>x</var>，并按如下算法执行：

1.  使 <var>e</var> 为 <var>x</var>的 **endIndex**。
2.  若 <var>e</var> = **0**，返回 **true**。
3.  若 **Multiline** 为 **false**，返回 **false**。
4.  若 [<var>e</var> - **1**] 的字符为 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")*，返回 **true**。
5.  返回 **false**。

产生式 ** :: **\$** 解释执行返回一个 ，它需要1个参数 <var>x</var>，并按如下算法执行：

1.  使 <var>e</var> 为 <var>x</var> 的 **endIndex**
2.  若 <var>e</var> = ，返回 **true**。
3.  若 **Multiline** 为 **false**，返回 **false**。
4.  若 [<var>e</var>] 的字符为 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")*，返回 **true**。
5.  返回 **false**。

产生式 ** :: **\\ b** 解释执行返回一个 ，它需要1个参数 <var>x</var>，并按如下算法执行：

1.  使 <var>e</var> 为 <var>x</var> 的 **endIndex**。
2.  调用 (<var>e</var> - **1**)，返回 **Boolean** 值赋给 <var>a</var>。
3.  调用 (<var>e</var>)，返回 **Boolean** 值赋给 <var>b</var>。
4.  若 <var>a</var> 为 **true**，<var>b</var> 为 **false**，返回 **true**。
5.  若 <var>a</var> 为 **false**，<var>b</var> 为 **true**，返回 **true**。
6.  返回 **false**。

产生式 ** :: **\\ B** 解释执行返回一个 ，它需要1个参数 <var>x</var>，并按如下算法执行：

1.  使 <var>e</var> 为 <var>x</var> 的 **endIndex**。
2.  调用 (<var>e</var> - **1**)，返回 **Boolean** 值赋给 <var>a</var>。
3.  调用 (<var>e</var>)，返回 **Boolean** 值赋给 <var>b</var>。
4.  若 <var>a</var> 为 **true**，<var>b</var> 为 **false**，返回 **false**。
5.  若 <var>a</var> 为 **false**，<var>b</var> 为 **true**，返回 **false**。
6.  返回 **true**。

产生式 ** :: **(? =** ** **)** 按如下算法执行：

1.  执行 **，得到 <var>m</var>。
2.  返回一个需要两个参数的内部闭包 ，参数分别是一个 <var>x</var> 和一个 <var>c</var>，此内部闭包的执行方式如下：
    1.  使 <var>d</var> 为一个，它始终对它的任何 参数都返回成功匹配的 。
    2.  调用 <var>m</var>(<var>x</var>, <var>d</var>)，令 <var>r</var> 为其结果。
    3.  若 <var>r</var> 为 **failure**，返回 **failure**。
    4.  使 <var>y</var> 为 <var>r</var> 的 。
    5.  使 <var>cap</var> 为 <var>r</var> 的**captures**。
    6.  使 <var>xe</var> 为 <var>r</var> 的**endIndex**。
    7.  使 <var>z</var> 为 (<var>xe</var>, <var>cap</var>)。
    8.  调用 <var>c</var>(<var>z</var>)，返回结果。

产生式 ** :: **(? !** ** **)** 按如下算法执行：

1.  执行 **，得到 <var>m</var>。
2.  返回一个需要两个参数的内部闭包 ，参数分别是一个 <var>x</var> 和一个 <var>c</var>，此内部闭包的执行方式如下：
    1.  使 <var>d</var> 为一个 ，它始终对它的任何 参数都返回成功匹配的 。
    2.  调用 <var>m</var>(<var>x</var>, <var>d</var>)，令 <var>r</var> 为其结果。
    3.  若r为**failure**，返回 **failure**。
    4.  调用 <var>c</var>(<var>z</var>)，返回结果。

抽象操作 **IsWordChar**，拥有一个整数类型的参数 <var>e</var>，按如下方式执行：

1.  若 <var>e</var> == **-1** 或 <var>e</var> == ，返回 **false**。
2.  令 <var>c</var> 为 [<var>e</var>]。
3.  若 <var>c</var> 为 以下63个字符，返回 **true**
    **a b c d e f g h i j k l m n o p q r s t u v w x y z**
    **A B C D E F G H I J K L M N O P Q R S T U V W X Y Z**
    **0 1 2 3 4 5 6 7 8 9 \_**。
4.  返回 **false**。

#### 量词（）

产生式 ** :: ** 按如下方式执行：

1.  执行 ** 得到 **2** 个数 <var>min</var> 和 <var>max</var>（或 **∞**）。
2.  返回 <var>min</var>、<var>max</var>、**true**。

产生式 ** :: ** **?** 按如下方式执行：

1.  执行 ** 得到 **2** 个数 <var>min</var> 和 <var>max</var>（或 **∞**）。
2.  返回 <var>min</var>、<var>max</var>、**false**。

产生式 ** :: **\*** 返回 **0** 和 **∞**

产生式 ** :: **+** 返回 **1** 和 **∞**

产生式 ** :: **?** 返回 **0** 和 **1**

产生式 ** :: **{** *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* **}** 按如下方式执行：

1.  令 <var>i</var> 为 *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* 的数学值。
2.  返回 <var>i</var>、<var>i</var>。

产生式 ** :: **{** *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* **,** **}** 按如下方式执行：

1.  令 <var>i</var> 为 *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* 的数学值。
2.  返回 <var>i</var>、**∞**。

产生式 ** :: **{** *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* **,** *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* **}** 按如下方式执行：

1.  令 <var>i</var> 为 *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* 的数学值。
2.  令 <var>j</var> 为 *[DecimalDigits](#ES5/lexical#DecimalDigits "wikilink")* 的数学值。
3.  返回 <var>i</var>、<var>j</var>。

#### 原子（）

产生式 ** :: ** 执行方式如下：

1.  令 <var>ch</var> 为 ** 表示的字符。
2.  令 <var>A</var> 为单元素 ，包含 <var>ch</var>。
3.  调用 (<var>A</var>, **false**)，返回 。

产生式 :: **.** 执行方式如下

1.  令 <var>A</var> 为 除去 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")* 外的所有字符。
2.  调用 (<var>A</var>, **false**)，返回 。

产生式 ** :: **\\** ** 通过执行 ** 返回 。

产生式 ** :: ** 执行方式如下：

1.  执行 ** 得到 <var>A</var> 和 **Boolean** <var>invert</var>。
2.  调用 (<var>A</var>, **false**)，返回 。

产生式 ** :: **(** ** **)** 执行方式如下：

1.  执行 ** 得到 。
2.  令 **parenIndex** 为 在整个正则表达式中从产生式展开初始化左括号时，当前展开左捕获括号的索引。**parenIndex** 为在产生式的 ** 被展开之前，** :: **(** ** **)** 产生式被展开的次数，加上 ** :: **(** ** **)** 闭合 这个 ** 的次数。
3.  返回一个内部闭包 ，拥有2个参数：一个 <var>x</var> 和 <var>c</var>，执行方式如下：
    1.  创建内容闭包 <var>d</var>，参数为 <var>y</var>，并按如下方式执行：
        1.  令 <var>cap</var> 为 <var>y</var> 的 **capture** 数组的一个拷贝。
        2.  令 <var>xe</var> 为 x 的 **endIndex**。
        3.  令 <var>ye</var> 为 <var>y</var> 的 **endIndex**。
        4.  令 <var>s</var> 为 从索引 <var>xe</var>（包括）至 <var>ye</var>（不包括）范围的新创建的字符串。
        5.  令 <var>s</var> 为 <var>cap</var>[<var>parenIndex</var> + **1**]。
        6.  令 <var>z</var> 为 (<var>ye</var>, <var>cap</var>)。
        7.  调用 <var>c</var>(<var>z</var>)，返回其结果。

    2.  执行 <var>m</var>(<var>x</var>, <var>d</var>)，返回其结果。

产生式 ** :: **( ? :**'' '' **)** 通过执行 ** 得到并返回一个 。

抽象操作 **CharacterSetMatcher**，拥有2个参数：一个 <var>A</var> 和 **Boolean** <var>invert</var> 标志，按如下方式执行：

1.  返回一个内部闭包 ，拥有2个参数：一个 <var>x</var> 和 <var>c</var>，执行方式如下：
    1.  令 <var>e</var> 为 <var>x</var> 的 **endIndex**。
    2.  若 <var>e</var> == ，返回 **failure**。
    3.  令 <var>ch</var> 为字符[<var>e</var>]。
    4.  令 <var>cc</var> 为 (<var>ch</var>) 的结果。
    5.  若 <var>invert</var> 为**false**，如果 <var>A</var> 中不存在 <var>a</var> 使得 (<var>a</var>) == <var>cc</var>，返回**failure**。
    6.  若 <var>invert</var> 为**true**，如果 <var>A</var> 中存在 <var>a</var> 使得 (<var>a</var>) == <var>cc</var>，返回**failure**。
    7.  令 <var>cap</var> 为 <var>x</var> 的内部 **captures** 数组。
    8.  令 <var>y</var> 为 (<var>e</var> + **1**, <var>cap</var>)。
    9.  调用 <var>c</var>(<var>y</var>)，返回结果。

抽象操作 **Canonicalize**，拥有一个字符参数 <var>ch</var>，按如下方式执行：

1.  若 为 **false**，返回 <var>ch</var>。
2.  令 <var>u</var> 为 <var>ch</var> 转换为大写后的结果，仿佛通过调用标准内置方法 [String.prototype.toUpperCase](ES5/builtins#x15.5.4.18 "wikilink")。
3.  若 <var>u</var> 不含单个字符，返回 <var>ch</var>。
4.  令 <var>cu</var> 为 <var>u</var> 的字符。
5.  若 <var>ch</var> 的单位代码值 \>= **128** 且 <var>cu</var> 的单位代码值 \<= **128**，返回<var>ch</var>。
6.  返回 <var>cu</var>。

例如，

` /(?=(a+))/.exec("baaabac")`

会匹配第一个b后的空白字符串，得到：

` ["", "aaa"]`

为了说明预查不会回溯，

` /(?=(a+))a*b\1/.exec("baaabac")`

得到：

` ["aba", "a"]`

而不是：

` ["aaaba", "a"]`

例如，

` /(.*?)a(?!(a+)b\2c)\2(.*)/.exec("baaabaac")`

搜索 **a**，其后有 <var>n</var> 个 **a**，一个 **b**， <var>n</var> 个 **a**（**\\2** 指定）和一个 **c**。第二个 **\\2** 位于负向预查模式的外部，因此它匹配 **undefined**，且总是成功的。整个表达式返回一个数组：

` ["baaabaac", "ba", undefined, "abaac"]`

在大小写不敏感的匹配中，所有字符都在它们参与比较之前隐式转换成大写的。然而，如果把一个字符转换成大写会产生多个字符（例如 **"ß"**（**\\u00DF**） 转换到 **"SS"**），那么字符将保持不变。如果一个字符是非 ASCII 字符，但却会因大小写转换而变成 ASCII 字符，那么在匹配中它也会保持不变。这个规定阻止了一些如 **\\u0131** 和 **\\u017F** 之类的 Unicode 字符 被 **/[a-z]/i** 这样的正则表达式匹配，这样的正则表达式被故意设计成只匹配 ASCII 字符。此外，倘若从 Unicode 到 ASCII 的转换被允许，将会造成 **/[\^\\W]/i** 可以匹配 **a**、**b**、**…**、**h**，但无法匹配 **i** 或 **s**。

#### 转义原子（）

产生式 ** :: ** 执行方式如下：

1.  执行 ** 得到 ** <var>E</var>。
2.  如果 <var>E</var> 为一个字符，
    1.  令 <var>ch</var> 为 <var>E</var> 的字符。
    2.  令 <var>A</var> 为包含 <var>ch</var> 字符的单元素字符集 。
    3.  调用 (<var>A</var>, **false**) 返回 结果。

3.  <var>E</var> 必须是一个数。令 <var>n</var> 为该数。
4.  如果 <var>n</var> = **0** 或 <var>n</var> \> ，抛出 **SyntaxError** 异常。
5.  返回一个内部闭包 ，拥有2个参数：一个 <var>x</var> 和 <var>c</var>，执行方式如下：
    1.  令 <var>cap</var> 为 <var>x</var> 的 **captures** 内部数组。
    2.  令 <var>s</var> 为 <var>cap</var>[<var>n</var>]。
    3.  如果 <var>s</var> 为 **undefined**，调用 <var>c</var>(<var>x</var>)，返回结果
    4.  令 <var>e</var> 为 <var>x</var> 的 <var>endIndex</var>。
    5.  令 <var>len</var> 为 <var>s</var> 的 <var>length</var>。
    6.  令 <var>f</var> 为 <var>e</var> + <var>len</var>。
    7.  如果 <var>f</var> \> ，返回 **failure**。
    8.  如果存在位于 **0**（包括）到 <var>len</var>（不包括）的整数 <var>i</var> 使得 (<var>s</var>[<var>i</var>]) 等于 ([<var>e</var> + <var>i</var>])，那么返回**failure**。
    9.  令 <var>y</var> 为 (<var>f</var>, <var>cap</var>)。
    10. 调用 <var>c</var>(<var>y</var>)，返回结果。

产生式 ** :: ** 执行方式如下：

1.  执行 ** 得到一个 <var>ch</var> 字符。
2.  令 <var>A</var> 为包含 <var>ch</var> 字符的单元素字符集 。
3.  调用 (<var>A</var>, **false**) 返回 结果。

产生式 ** :: 执行方式如下：

1.  执行 ** 得到一个 <var>A</var>。
2.  调用 **(<var>A</var>, **false**) 返回 结果。

#### 转义字符（）

产生式 ** :: 执行返回一个根据 **表23** 定义的字符：

|ControlEscape|单位代码|名称|记号|
|-------------|--------|----|----|
|t|\\u0009|水平制表符|<HT>|
|n|\\u000A|换行符|<LF>|
|v|\\u000B|垂直制表符|<VT>|
|f|\\u000C|换页符|<FF>|
|r|\\u000D|回车符|<CR>|

产生式 ** :: **c** <var>ControlLetter</var> 执行过程如下：

1.  令 <var>ch</var> 为通过 <var>ControlLetter</var> 表示的字符
2.  令 <var>i</var> 为 <var>ch</var> 的单位代码值
3.  令 <var>j</var> 为 <var>i</var>/**32** 的余数
4.  返回 <var>j</var>

产生式 ** :: *[HexEscapeSequence](ES5/lexical#HexEscapeSequence "wikilink")* 执行 *[HexEscapeSequence](ES5/lexical#HexEscapeSequence "wikilink")* 的字符值，返回其字符结果。

产生式 ** :: *[UnicodeEscapeSequence](ES5/lexical#UnicodeEscapeSequence "wikilink")* 执行 *[UnicodeEscapeSequence](ES5/lexical#UnicodeEscapeSequence "wikilink")* 的字符值，返回其字符结果。

产生式 ** :: ** 执行返回由 ** 表示的字符。

#### 转义十进制（）

产生式 ** :: *[DecimalIntegerLiteral](ES5/lexical#DecimalIntegerLiteral "wikilink")* [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") *[DecimalDigit](#ES5/lexical#DecimalDigit "wikilink")*] 按如下方式执行：

1.  令 <var>i</var> 为 *[DecimalIntegerLiteral](ES5/lexical#DecimalIntegerLiteral "wikilink")* 的字符值
2.  如果 <var>i</var> 为 **0**，返回包含一个 **<NUL>** 字符（Unicode 值为 **0000**）的 **
3.  返回包含整数 <var>i</var> 的 **

*[DecimalIntegerLiteral](ES5/lexical#DecimalIntegerLiteral "wikilink")* 的数学值在 [7.8.3](ES5/lexical#x7.8.3 "wikilink") 节定义。

#### 转义字符类（）

产生式 ** :: **d** 执行返回包含**0**到**9**之间的十元素字符集。

产生式 ** :: **D** 执行返回不包括 :: **d** 的字符集。

产生式 ** :: **s** 执行返回包含 *[WhiteSpace](ES5/lexical#WhiteSpace "wikilink")* 或 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")* 产生式右部分字符的字符集。

产生式 ** :: **S** 执行返回不包括 :: **s** 的字符集。

产生式 ** :: **w** 执行返回包含如下63个字符的字符集：

` `**`a` `b` `c` `d` `e` `f` `g` `h` `i` `j` `k` `l` `m` `n` `o` `p` `q` `r` `s` `t` `u` `v` `w` `x` `y` `z`**
` `**`A` `B` `C` `D` `E` `F` `G` `H` `I` `J` `K` `L` `M` `N` `O` `P` `Q` `R` `S` `T` `U` `V` `W` `X` `Y` `Z`**
` `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9` `_`**

产生式 ** :: **W** 执行返回不包括 ** :: **w** 的字符集。

#### 字符类（）

产生式 ** :: **[** [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") {**\^**}] ** **]** 通过执行 ** 获得并返回这个 和 **Boolean false**。

产生式 ** :: **[ \^** ** **]** 通过执行 ** 获得并返回这个 和 **Boolean true**。

#### 字符范围集（）

产生式 ** :: [[empty](ES5/notation#empty "wikilink")] 执行返回一个空的 。

产生式 ** :: ** 通过执行 ** 获得并返回这个 。

#### 非空字符范围集（）

产生式 ** :: ** 通过执行 ** 获得一个 并返回这个。

产生式 ** :: ** ** 按如下方式执行：

1.  执行 ** 得到一个 <var>A</var>。
2.  执行 ** 得到一个 <var>B</var>。
3.  返回 <var>A</var> 与 <var>B</var> 的并集。

产生式 ** :: ** - ** ** 按如下方式执行：

1.  执行第一个 ** 得到一个 <var>A</var>。
2.  执行第二个 ** 得到一个 <var>B</var>。
3.  执行 ** 得到一个 <var>C</var>。
4.  调用 **(<var>A</var>, <var>B</var>)，令D为其结果 。
5.  返回 <var>D</var> 与 <var>C</var> 的并集。

抽象操作 **CharacterRange**，拥有2个 参数 <var>A</var> 和 <var>B</var>，执行方式如下：

1.  如果 <var>A</var> 或 <var>B</var> 为空，抛出 **SyntaxError** 异常。
2.  令 <var>a</var> 为 <var>A</var> 的一个字符。
3.  令 <var>b</var> 为 <var>B</var> 的一个字符。
4.  令 <var>i</var> 为 <var>a</var> 的单位代码值。
5.  令 <var>j</var> 为 <var>b</var> 的单位代码值。
6.  如果 <var>i</var> \> <var>j</var>，抛出 **SyntaxError** 异常。
7.  返回位于在 <var>i</var> 到 <var>j</var>（包括边界）之间的所有字符的字符集。

#### 无连接符非空字符范围集（）

产生式 ** :: ** 执行一个 ** 获取结果 并返回。

产生式 ** :: ** ** 的结果根据以下步骤:

1.  执行 ** 得到一个 <var>A</var>。
2.  执行 ** 得到一个 <var>B</var>。
3.  返回 <var>A</var> 和 <var>B</var> 的并集。

产生式 ** :: ** **-** ** ** 按下面的步骤执行:

1.  执行 ** 得到一个 <var>A</var>。
2.  执行 ** 得到一个 <var>B</var>。
3.  执行 ** 得到一个 <var>C</var>
4.  令 <var>D</var> 为调用方法 (<var>A</var>, <var>B</var>) 返回的 。
5.  返回 <var>D</var> 和 <var>C</var> 的并集。

#### 字符类原子（）

产生式 ** :: **-** 执行返回包含单个字符 **-** 的字符集。

产生式 ** :: ** 通过执行 ** 获得并返回这个 。

#### 非连接符字符类原子（）

产生式 ** :: *[SourceCharacter](ES5#SourceCharacter "wikilink")* 不包括 **\\**、**]**、**-** 执行返回包含由 [SourceCharacter](ES5#SourceCharacter "wikilink") 表示的字符的单元素字符集。

产生式 ** :: **\\** ** 通过执行 ** 得到并返回这个 。

#### 字符类可用转义（）

产生式 ** :: ** 按如下方式执行：

1.  执行 ** 得到 ** <var>E</var>
2.  如果 <var>E</var> 不是一个字符，抛出 **SyntaxError** 异常。
3.  令 <var>ch</var> 为 <var>E</var> 的字符。
4.  返回包含字符 <var>ch</var> 的单元素 。

产生式 ** :: **b** 执行返回包含一个 **<BS>** 字符（Unicode 值 **0008**）的字符集。

产生式 ** :: ** 通过执行 ** 获得一个字符 并返回包含该字符的单元素字符集 。

产生式 ** :: ** 通过执行 ** 获得并返回这个。

### RegExp 构造器作为函数调用

#### RegExp(pattern, flags)

如果 <var>pattern</var> 是一个对象 <var>R</var>，其内部属性 [[[Class]]](ES5/types#Class "wikilink") 为 **"RegExp"** 且 <var>flags</var> 为 **undefined**，返回 <var>R</var>。否则，调用内置**RegExp**构造器，通过表达式 **new RegExp(**<var>pattern</var>, <var>flags</var>**)** 返回由该构造器构造的对象。

### RegExp 构造器

当**RegExp**作为 **new** 表达式一部分调用时，它是一个构造器，用来初始化一个新创建的对象。

#### new RegExp(pattern, flags)

如果 <var>pattern</var> 是一个对象且它的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"RegExp"**，则令 <var>R</var> 为 <var>pattern</var>。接着，如果 <var>flags</var> 是 **undefined**，则令 <var>P</var> 为构造 <var>R</var> 时使用的 <var>pattern</var>，令 <var>F</var> 为构造 <var>R</var> 时使用的 <var>flags</var>，否则抛出**TypeError**异常。对于其它情况，如果 <var>pattern</var> 为 **undefined**，则令 <var>P</var> 为空字符串，否则令 <var>P</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>pattern</var>)，如果 <var>flags</var> 为 **undefined**，则令 <var>F</var> 为空字符串，否则令 <var>F</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>flags</var>)。

如果字符 <var>P</var> 不满足 ** 句法，那么抛出 **SyntaxError** 异常。否则，令新构造的对象拥有内部 [[[Match]]](ES5/types#Match "wikilink") 属性，该属性通过执行（编译）字符 <var>P</var> 作为在 [15.10.2](#15.10.2 "wikilink") 节描述的 **。

如果 <var>F</var> 含有除 **"g"**、**"i"**、**"m"** 外的任意字符，或者 <var>F</var> 中包括出现多次的字符，那么，抛出**SyntaxError**异常。

如果 **SyntaxError** 异常未抛出，那么：

令 <var>S</var> 为一个字符串，其等价于 <var>P</var> 表示的 **，<var>S</var> 中的字符按如下描述进行转义。这样，<var>S</var> 可能或者不会与 <var>P</var> 或者 ** 相同；然而，由执行 <var>S</var> 作为一个 ** 的内部处理程序必须和通过构造对象的内部 [[[Match]]](ES5/types#Match "wikilink") 属性的内部处理程序完全相同。

如果 ** 里存在字符 **/** 或者 **\\** ，那么这些字符应该被转义，以确保由 **"/"**、<var>S</var>、**"/"** 构成的字符串的 <var>S</var> 值有效，而且 <var>F</var> 能被解析（在适当的词法上下文中）为一个与构造的正则表达式行为完全相同的 *[RegularExpressionLiteral](ES5/lexical#RegularExpressionLiteral "wikilink")* 。例如，如果 <var>P</var> 是**"/"**，那么 <var>S</var> 应该为 **"\\/"** 或 **"\\u002F"**，而不是 **"/"**，因为 <var>F</var> 后的 **///** 会被解析为一个 *[SingleLineComment](ES5/lexical#SingleLineComment "wikilink")*，而不是一个 *[RegularExpressionLiteral](ES5/lexical#RegularExpressionLiteral "wikilink")*。 如果 <var>P</var> 为空字符串，那么该规范定义为令 <var>S</var> 为 **"(?:)"**。

这个新构造对象的如下属性为数据属性，其特性在 [15.10.7](#x15.10.7 "wikilink") 中定义。各属性的 [[[Value]]](ES5/types#Value "wikilink") 值按如下方式设置：

其 **source** 属性置为 <var>S</var>。

其 **global** 属性置为一个 **Boolean** 值。当 <var>F</var> 含有字符 **g** 时，为 **true**，否则，为 **false**。

其 **IgnoreCase** 属性置为一个 **Boolean** 值。当 <var>F</var> 含有字符 **i** 时，为 **true**，否则，为 **false**。

其 **multiline** 属性置为一个 **Boolean** 值。当 <var>F</var> 含有字符 **m** 时，为 **true**，否则，为 **false**。

其 **lastIndex** 属性置为 **0**。

其内部 [[[Prototype]]](ES5/types#Prototype "wikilink") 属性置为 [15.10.6](#x15.10.6 "wikilink") 中定义的内置 **RegExp** 原型对象。

其内部 [[[Class]]](ES5/types#Class "wikilink") 属性置为 **"RegExp"**。

### RegExp构造器的属性

**RegExp** 构造器的[[[Prototype]]值为内置](ES5/types#Prototype "wikilink") **Function** 的原型（[15.3.4](#x15.3.4 "wikilink")）。

除了内部的一些属性和 **length** 属性（其值为**2**），**RegExp** 构造器还有如下属性：

#### RegExp.prototype

**RegExp.prototype**的初始值为**RegExp**的原型（[15.10.6](#x15.10.6 "wikilink")）。

该属性有这些特性： { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### RegExp.Prototype的属性

**RegExp** 的原型的内部 [[[Prototype]]](ES5/types#Prototype "wikilink") 属性为 **Object** 的原型（[15.2.4](#x15.2.4 "wikilink")）。**RegExp** 的原型为其本身的一个普通的正则表达式对象；它的[[[Class]]](ES5/types#Class "wikilink") 为 **"RegExp"**。**RegExp** 的原型对象的数据式属性的初始值被设置为仿佛由内置 **RegExp** 构造器深生成的表达式 **new RegExp()** 创建的对象。

*'RegExp* 的原型本身没有 **valueOf** 属性；然而，该 **valueOf** 属性是继承至 **Object** 的原型。

在作为 **RegExp** 原型对象的属性的如下函数描述中，**"this RegExp object"** 是指函数激活时 **this** 对象；如果 **this** 值不是一个对象，或者一个其内部 [[[Class]]](ES5/types#Class "wikilink") 属性值不是 **"RegExp"** 的对象，那么一个 **TypeError** 会抛出。

#### RegExp.prototype.constructor

**RegExp.prototype.constructor** 的初始值为内置 **RegExp** 构造器。

#### RegExp.prototype.exec(string)

1.  令 <var>R</var> 为该 **RegExp** 对象。
2.  令 <var>S</var> 为[ToString](ES5/conversion#ToString "wikilink")(<var>string</var>)的值。
3.  令 <var>length</var> 为 <var>S</var> 的长度。
4.  令 <var>lastIndex</var> 为以参数 **"lastIndex"** 调用 <var>R</var> 的内部方法 [[[Get]]](ES5/types#Get "wikilink") 的结果。
5.  令 <var>i</var> 为 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>lastIndex</var>) 的值。
6.  令 <var>global</var> 为以参数 **"global"** 调用 <var>R</var> 的内部方法 [[[Get]]](ES5/types#Get "wikilink") 的结果。
7.  若 <var>global</var> 为 **false**，则令 <var>i</var> = **0**。
8.  令 <var>matchSucceeded</var> 为**false**。
9.  到 <var>matchSucceeded</var> 为**false** 前重复以下。
    1.  若 <var>i</var> \< **0** 或者 <var>i</var> \> <var>length</var>，则
        1.  以参数 **"lastIndex"**、**0** 和 **true** 调用 <var>R</var> 的内部方法[[[Put]]](ES5/types#Put "wikilink")。
        2.  返回 **null**。

    2.  以参数 <var>S</var> 和 <var>i</var> 调用 <var>R</var> 的内部方法[[[Match]]](ES5/types#Match "wikilink")。
    3.  若 [[[Match]]](ES5/types#Match "wikilink") 返回失败，则
        1.  令 <var>i</var> = <var>i</var> + **1**。

    4.  否则
        1.  令 <var>r</var> 为调用 [[[Match]]](ES5/types#Match "wikilink") 的结果 。
        2.  设 <var>matchSucceeded</var> 为 **true**。

10. 令 <var>e</var> 为 <var>r</var> 的 <var>endIndex</var> 值。
11. 若 <var>global</var> 为**true**,
12. 以参数 **"lastIndex"**、<var>e</var> 和 **true** 调用 <var>R</var> 的内部方法 [[[Put]]](ES5/types#Put "wikilink")。
13. 令 <var>n</var> 为 <var>r</var> 的捕获数组的长度。（这跟 [15.10.2.1](#x15.10.2.1 "wikilink") 的 是同一个值）
14. 令 <var>A</var> 为如同以表达式 **new Array** 创建的新数组，其中**Array**是这个名字的内置构造器。
15. 令 <var>matchIndex</var> 为匹配到的子串在整个字符串 <var>S</var> 中的位置。
16. 以参数 **"index"**，属性描述 {[[Value]]: <var>matchIndex</var>, [[Writable]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **true** 调用 <var>A</var> 的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。
17. 以参数 **"input"**，属性描述 {{[[Value]]: <var>S</var>, [[Writable]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **true** 调用 <var>A</var> 的内部方法[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。
18. 以参数**"length"**，属性描述 {[[Value]]: <var>n</var> + 1} 和 **true** 调用 <var>A</var> 的内部方法[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。
19. 令 <var>matchedSubstr</var> 为匹配到的子串（例如：<var>S</var> 中从 <var>i</var> 位置<包含>到 <var>e</var> 位置<不包含>的部分 )。
20. 以参数 **"0"**，属性描述 {{[[Value]]: <var>matchedSubstr</var>, [[Writable]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **true** 调用 <var>A</var> 的内部方法[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。
21. 对每一满足 <var>I</var> \> **0** 且 <var>I</var> ≤ <var>n</var> 的整数 <var>i</var>
    1.  令 <var>captureI</var> 为第 <var>i</var> 个捕获数组中的元素。
    2.  以参数 [ToString](ES5/conversion#ToString "wikilink")(<var>i</var>)，属性描述 {[[Value]]: <var>captureI</var>, [[Writable]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **true** 调用 <var>A</var> 的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。

22. 返回 <var>A</var>。

#### RegExp.prototype.test(string)

采用如下步骤：

1.  令 <var>match</var> 为在这个 **RegExp** 对象上使用 <var>string</var> 作为参数执行 [RegExp.prototype.exec](#x15.10.6.2 "wikilink") 的结果。

1.  如果 <var>match</var> 不为 **null**，返回 **true**；否则返回 **false**。

#### RegExp.prototype.toString()

返回一个 **String**，由 **"/"**、**RegExp** 对象的 **source** 属性值、**"/"** 与 **"g"**（如果 **global** 属性为 **true**），**"i"**（如果 **IgnoreCase** 为**true**），**"m"**（如果 **multiline** 为**true**）通过连接组成。

### RegExp实例的属性

**RegExp** 实例继承至 **RegExp** 原型对象，其 [[[Class]]](ES5/types#Class "wikilink") 内部属性值为 **"RegExp"**。**RegExp** 实例也拥有一个 [[[Match]]](ES5/types#Match "wikilink") 内部属性和一个 **length** 属性。

内部属性 [[[Match]]](ES5/types#Match "wikilink") 的值是正则表达式对象的 ** 的依赖实现的表示形式。

**RegExp**实例还有如下属性。

#### source

**source** 属性为构成正则表达式 ** 的字符串。该属性拥有这些特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### global

**global** 属性是一个 **Boolean** 值，表示正则表达式 **flags** 是否有 **"g"**。该属性拥有这些特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### ignoreCase

**ignoreCase** 属性是一个 **Boolean** 值，表示正则表达式 **flags** 是否有 **"i"**。该属性拥有这些特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### multiline

**multiline** 属性是一个 **Boolean** 值，表示正则表达式 **flags** 是否有 **"m"**。该属性拥有这些特性 { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### lastIndex

**lastIndex** 属性指定从何处开始下次匹配的一个字符串类型的位置索引。当需要时该值会转换为一个整型数。该属性拥有这些特性 { [[Writable]]: **true**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

Error对象
---------

**Error** 对象的实例在运行时遇到错误的情况下会被当做异常抛出。**Error** 对象也可以作为用户自定义异常类的基对象。

### Error构造器作为函数调用

当 **Error** 被作为函数而不是构造器调用时，它创建并初始化一个新的 **Error** 对象。这样函数调用 **Error(…)** 与同样参数的对象创建表达式 **new Error(…)** 是等效的。

#### Error (message)

新构造的对象内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 会被设为原本的 **Error** 原型对象，也就是 **Error.prototype** 的初始值。([15.11.3.1](#x15.11.3.1 "wikilink"))

新构造的对象内部属性 [[[Class]]](ES5/types#Class "wikilink") 会被设为 **"Error"**。

新构造的对象内部属性 [[[Extensible]]](ES5/types#Extensible "wikilink") 会被设为 **true**。

如果形参 <var>message</var> 不是 **undefined**，新构造的对象本身属性 <var>message</var> 则被设为 [ToString](ES5/conversion#ToString "wikilink")(<var>message</var>)。

### Error构造器

当 **Error** 作为 **new** 表达式的一部分被调用时，它是一个构造器：它初始化新创建的对象。

#### new Error (message)

新构造的对象内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 会被设为原本的 **Error** 原型对象，也就是 **Error.prototype** 的初始值。([15.11.3.1](#x15.11.3.1 "wikilink"))

新构造的对象内部属性 [[[Class]]](ES5/types#Class "wikilink") 会被设为**"Error"**。

新构造的对象内部属性 [[[Extensible]]](ES5/types#Extensible "wikilink") 会被设为**true**。

如果形参 <var>message</var> 不是**undefined**，新构造的对象本身属性 <var>message</var> 则被设为[ToString](ES5/conversion#ToString "wikilink")(<var>message</var>)。

### Error构造器的属性

**Error**构造器的内部属性[[[Prototype]]值为](ES5/types#Prototype "wikilink")**Function**原型对象([15.3.4](#x15.3.4 "wikilink"))。

除内部属性和 **length** 属性（其值为**1**）以外，**Error**构造器还有以下属性：

#### Error.prototype

**Error.prototype** 的初始值为 **Error** 原型对象([15.3.4](#x15.3.4 "wikilink"))。

此属性有以下特性： { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

### Error 原型对象的属性

**Error**原型对象本身是一个**Error**对象（其[[[Class]]为](ES5/types#Class "wikilink")**"Error"**）。

**Error**原型对象的内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 为标准内置的 [Object 原型对象](#x15.2.4 "wikilink")。

#### Error.prototype.constructor

**Error.prototype.constructor** 初始值为内置的 **Error** 构造器。

#### Error.prototype.name

**Error.prototype.name** 初始值为 **"Error"**。

#### Error.prototype.message

**Error.prototype.message** 初始值为空字符串。

#### Error.prototype.toString ( )

执行以下步骤

1.  令 <var>O</var> 为 **this** 值
2.  如果 [Type](ES5/types#Type "wikilink")(<var>O</var>) 不是对象，抛出一个**TypeError**异常。
3.  令 <var>name</var> 为以**"name"**为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内置方法的结果。
4.  如果 <var>name</var> 为**undefined**, 令 <var>name</var> 为 **"Error"**；否则令 <var>name</var> 为[ToString](ES5/conversion#ToString "wikilink")(<var>name</var>)。
5.  令 <var>msg</var> 为以**"message"**为参数调用 <var>O</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内置方法的结果。
6.  如果 <var>msg</var> 为 **undefined**，令 <var>msg</var> 为空字符串；否则令 <var>msg</var> 为[ToString](ES5/conversion#ToString "wikilink")(<var>msg</var>)。
7.  如果 <var>name</var> 与 <var>msg</var> 都是空字符串，返回**"Error"**。
8.  如果 <var>name</var> 为空字符串，返回 <var>msg</var>。
9.  如果 <var>msg</var> 为空字符串，返回 <var>name</var>。
10. 返回拼接 <var>name</var>、":"、一个空格字符，以及 <var>msg</var> 的结果。

### Error实例的属性

**Error** 实例从 **Error** 原型对象继承属性，且它们的内部属性 [[[Class]]](ES5/types#Class "wikilink") 值为**"Error"**。**Error**实例没有特殊属性。

### 用于本标准的内部错误类型

以下原生 **Error** 对象之一会在运行时错误发生时被抛出。所有这些对象共享同样的结构，如 [15.11.7](#x15.11.7 "wikilink") 所述。

#### EvalError

本规范现在已经不再使用这个异常，这个对象保留用于跟规范之前版本的兼容性。

#### RangeError

表示一个数值超出了允许的范围，见 [15.4.2.2](#x15.4.2.2 "wikilink"), [15.4.5.1](#x15.4.5.1 "wikilink"), [15.7.4.2](#x15.7.4.2 "wikilink"), [15.7.4.5](#x15.7.4.5 "wikilink"), [15.7.4.6](#x15.7.4.6 "wikilink"), [15.7.4.7](#x15.7.4.7 "wikilink"), [15.9.5.43](#x15.9.5.43 "wikilink")。

#### ReferenceError

表示一个不正确的引用值被检测到。见 [8.7.1](ES5/types#x8.7.1 "wikilink"), [8.7.2](ES5/types#x8.7.2 "wikilink"), [10.2.1](ES5/execution#x10.2.1 "wikilink"), [10.2.1.1.4](ES5/execution#x10.2.1.1.4 "wikilink"), [10.2.1.2.4](ES5/execution#x10.2.1.2.4 "wikilink"), [11.13.1](ES5/execution#x11.13.1 "wikilink")。

#### SyntaxError

表示一个解析错误发生。见 [11.1.5](ES5/expressions#x11.1.5 "wikilink"), [11.3.1](ES5/expressions#x11.3.1 "wikilink"), [11.3.2](ES5/expressions#x11.3.2 "wikilink"), [11.4.1](ES5/expressions#x11.4.1 "wikilink"), [11.4.4](ES5/expressions#x11.4.4 "wikilink"), [11.4.5](ES5/expressions#x11.4.5 "wikilink"), [11.13.1](ES5/expressions#x11.13.1 "wikilink"), [11.13.2](ES5/expressions#x11.13.2 "wikilink"), [12.2.1](ES5/statements#x12.2.1 "wikilink"), [12.10.1](ES5/statements#x12.10.1 "wikilink"), [12.14.1](ES5/statements#x12.14.1 "wikilink"), [13.1](ES5/functions#x13.1 "wikilink"), [15.1.2.1](ES5/builtins#x15.1.2.1 "wikilink"), [15.3.2.1](ES5/builtins#x15.3.2.1 "wikilink"), [15.10.2.2](ES5/builtins#x15.10.2.2 "wikilink"), [15.10.2.5](ES5/builtins#x15.10.2.5 "wikilink"), [15.10.2.9](ES5/builtins#x15.10.2.9 "wikilink"), [15.10.2.15](ES5/builtins#x15.10.2.15 "wikilink"), [15.10.2.19](ES5/builtins#x15.10.2.19 "wikilink"), [15.10.4.1](ES5/builtins#x15.10.4.1 "wikilink"), [15.12.2](ES5/builtins#x15.12.2 "wikilink")。

#### TypeError

表示一个操作数的真实类型与期望类型不符。见 [8.6.2](ES5/types#x8.6.2 "wikilink"), [8.7.2](ES5/types#x8.7.2 "wikilink"), [8.10.5](ES5/types#x8.10.5 "wikilink"), [8.12.5](ES5/types#x8.12.5 "wikilink"), [8.12.7](ES5/types#x8.12.7 "wikilink"), [8.12.8](ES5/types#x8.12.8 "wikilink"), [8.12.9](ES5/types#x8.12.9 "wikilink"), [9.9](ES5/conversion#x9.9 "wikilink"), [9.10](ES5/conversion#x9.10 "wikilink"), [10.2.1](ES5/execution#x10.2.1 "wikilink"), [10.2.1.1.3](ES5/execution#x10.2.1.1.3 "wikilink"), [10.6](ES5/execution#x10.6 "wikilink"), [11.2.2](ES5/expressions#x11.2.2 "wikilink"), [11.2.3](ES5/expressions#x11.2.3 "wikilink"), [11.4.1](ES5/expressions#x11.4.1 "wikilink"), [11.8.6](ES5/expressions#x11.8.6 "wikilink"), [11.8.7](ES5/expressions#x11.8.7 "wikilink"), [11.3.1](ES5/expressions#x11.3.1 "wikilink"), [13.2](ES5/functions#x13.2 "wikilink"), [13.2.3](ES5/functions#x13.2.3 "wikilink"), [15](ES5/builtins#x15 "wikilink"), [15.2.3.2](ES5/builtins#x15.2.3.2 "wikilink"), [15.2.3.3](ES5/builtins#x15.2.3.3 "wikilink"), [15.2.3.4](ES5/builtins#x15.2.3.4 "wikilink"), [15.2.3.5](ES5/builtins#x15.2.3.5 "wikilink"), [15.2.3.6](ES5/builtins#x15.2.3.6 "wikilink"), [15.2.3.7](ES5/builtins#x15.2.3.7 "wikilink"), [15.2.3.8](ES5/builtins#x15.2.3.8 "wikilink"), [15.2.3.9](ES5/builtins#x15.2.3.9 "wikilink"), [15.9.5.44](ES5/builtins#x15.9.5.44 "wikilink"), [15.2.3.11](ES5/builtins#x15.2.3.11 "wikilink"), [15.2.3.12](ES5/builtins#x15.2.3.12 "wikilink"), [15.2.3.13](ES5/builtins#x15.2.3.13 "wikilink"), [15.2.3.14](ES5/builtins#x15.2.3.14 "wikilink"), [15.2.4.3](ES5/builtins#x15.2.4.3 "wikilink"), [15.3.4.2](ES5/builtins#x15.3.4.2 "wikilink"), [15.3.4.3](ES5/builtins#x15.3.4.3 "wikilink"), [15.3.4.4](ES5/builtins#x15.3.4.4 "wikilink"), [15.3.4.5](ES5/builtins#x15.3.4.5 "wikilink"), [15.3.4.5.2](ES5/builtins#x15.3.4.5.2 "wikilink"), [15.3.4.5.3](ES5/builtins#x15.3.4.5.3 "wikilink"), [15.3.5](ES5/builtins#x15.3.5 "wikilink"), [15.3.5.3](ES5/builtins#x15.3.5.3 "wikilink"), [15.3.5.4](ES5/builtins#x15.3.5.4 "wikilink"), [15.4.4.3](ES5/builtins#x15.4.4.3 "wikilink"), [15.4.4.11](ES5/builtins#x15.4.4.11 "wikilink"), [15.4.4.16](ES5/builtins#x15.4.4.16 "wikilink"), [15.4.4.17](ES5/builtins#x15.4.4.17 "wikilink"), [11.4.1](ES5/builtins#x11.4.1 "wikilink"), [15.4.4.19](ES5/builtins#x15.4.4.19 "wikilink"), [15.4.4.20](ES5/builtins#x15.4.4.20 "wikilink"), [15.4.4.21](ES5/builtins#x15.4.4.21 "wikilink"), [15.4.4.22](ES5/builtins#x15.4.4.22 "wikilink"), [15.4.5.1](ES5/builtins#x15.4.5.1 "wikilink"), [15.5.4.2](ES5/builtins#x15.5.4.2 "wikilink"), [15.5.4.3](ES5/builtins#x15.5.4.3 "wikilink"), [15.6.4.2](ES5/builtins#x15.6.4.2 "wikilink"), [15.6.4.3](ES5/builtins#x15.6.4.3 "wikilink"), [15.7.4](ES5/builtins#x15.7.4 "wikilink"), [15.7.4.2](ES5/builtins#x15.7.4.2 "wikilink"), [15.7.4.4](ES5/builtins#x15.7.4.4 "wikilink"), [15.7.4.8](ES5/builtins#x15.7.4.8 "wikilink"), [15.9.5](ES5/builtins#x15.9.5 "wikilink"), [15.9.5.44](ES5/builtins#x15.9.5.44 "wikilink"), [15.10.4.1](ES5/builtins#x15.10.4.1 "wikilink"), [15.10.6](ES5/builtins#x15.10.6 "wikilink"), [15.11.4.4](ES5/builtins#x15.11.4.4 "wikilink"), [15.12.3](ES5/builtins#x15.12.3 "wikilink")。

#### URIError

表示全局 URI 处理函数被以不符合其定义的方式使用。见 [15.1.3](ES5/builtins#x15.1.3 "wikilink")。

### NativeError对象结构

当 ECMAScript 实现探测到一个运行时错误时，它抛出一个 [15.11.6](ES5/builtins#x15.11.6 "wikilink") 所定义的 **NativeError** 对象的实例。每个这些对象都有如下所述结构，不同仅仅是在 <var>name</var> 属性中以构造器名称替换掉 **NativeError**，以及原型对象由实现自定义的 <var>message</var> 属性。

对于每个错误对象，定义中到 **NativeError** 的引用应当用 [15.11.6](ES5/builtins#x15.11.6 "wikilink") 中具体的对象名替换。

#### NativeError构造器作为函数调用

当 **NativeError** 被作为函数而不是构造器调用时，它创建并初始化一个新的 **NativeError** 对象。这样函数调用 **NativeError(…)** 与同样参数的对象创建表达式 **new NativeError(…)** 是等效的。

#### NativeError (message)

新构造的对象内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 会被设为这一错误构造器附带的原型对象。（[15.11.3.1](ES5/builtins#15.11.3.1 "wikilink")）

新构造的对象内部属性 [[[Class]]](ES5/types#Class "wikilink") 会被设为 **"Error"**。

新构造的对象内部属性 [[[Extensible]]](ES5/types#Extensible "wikilink") 会被设为 **true**。

如果形参 <var>message</var> 不是 **undefined**，新构造的对象本身属性 <var>message</var> 则被设为[ToString](ES5/conversion#ToString "wikilink")(message)。

#### NativeError构造器

当 **NativeError** 作为 **new** 表达式的一部分被调用时，它是一个构造器：它初始化新创建的对象。

#### New NativeError (message)

新构造的对象内部属性[[[Prototype]]会被设为这一错误构造器附带的原型对象](ES5/types#Prototype "wikilink")。([15.11.3.1](ES5/builtins#15.11.3.1 "wikilink"))

新构造的对象内部属性[[[Class]]会被设为](ES5/types#Class "wikilink") **"Error"**。

新构造的对象内部属性[[[Extensible]]会被设为](ES5/types#Extensible "wikilink") **true**。

如果形参 <var>message</var> 不是**undefined**，新构造的对象本身属性 <var>message</var> 则被设为[ToString](ES5/conversion#ToString "wikilink")(<var>message</var>)。

#### NativeError构造器的属性

**NativeError**构造器的内部属性[[[Prototype]]值为](ES5/types#Prototype "wikilink")**Function**原型对象([15.3.4](ES5/builtins#x15.3.4 "wikilink"))。

除内部属性和 **length** 属性（其值为**1**）以外，**Error**构造器还有以下属性：

#### NativeError.prototype

**NativeError.prototype** 的初始值为一个 **Error**([15.11.4](ES5/builtins#x15.11.4 "wikilink"))。

此属性有以下特性： { [[Writable]]: **false**, [[Enumerable]]: **false**, [[Configurable]]: **false** }。

#### NativeError原型对象的属性

每个 **NativeError** 的 [[[Prototype]]](ES5/types#Prototype "wikilink") 的初始值为一个 **Error**（其[[[Class]]为](ES5/types#Class "wikilink")**"Error"**）。

**NativeError** 原型对象的内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 为标准内置的 **Error** 对象([15.2.4](ES5/builtins#x15.2.4 "wikilink"))。

#### NativeError.prototype.constructor

对于特定的 **NativeError**，其 **Error.prototype.constructor** 初始值为 **NativeError** 构造器本身。

#### NativeError.prototype.name

对于特定的 **NativeError，Error.prototype.name** 初始值为构造器的名字。

#### NativeError.prototype.message

对于特定的 **NativeError，NativeError.prototype.message** 初始值为空字符串。

#### NativeError 实例的属性

**NativeError** 实例从 **NativeError** 原型对象继承属性，且它们的内部属性 [[[Class]]](ES5/types#Class "wikilink") 值为 **"Error"**。**Error** 实例没有特殊属性。

JSON 对象
---------

**JSON** 对象是一个单一的对象，它包含两个函数，**parse** 和 **stringify**，是用于解析和构造 **JSON** 文本的。**JSON** 数据的交换格式在 [RFC4627](http://www.ietf.org/rfc/rfc4627.txt) 里进行了描述。本规范里面的 **JSON** 交换格式会使用 [RFC4627](http://www.ietf.org/rfc/rfc4627.txt) 里所描述的，以下两点除外：

-   ECMAScript **JSON** 文法中的顶级 ** 产生式是由 ** 构成，而不是 [RFC4627](http://www.ietf.org/rfc/rfc4627.txt) 中限制成的 ** 或者 **。
-   确认 **JSON.parse** 和 **JSON.stringify** 的实现，它们必须准确的支持本规范描述的交换格式，而不允许对格式进行删除或扩展。这一点要区别于 [RFC4627](http://www.ietf.org/rfc/rfc4627.txt)，它允许 **JSON** 解析器接受 **non-JSON** 的格式和扩展。

**JSON** 对象内部属性 [[[Prototype]]](ES5/types#Prototype "wikilink") 的值是标准内建的 **Object** 原型对象（[15.2.4](ES5/builtins#properties-of-the-object-prototype-object "wikilink")）。内部属性 [[[Class]]](ES5/types#Class "wikilink") 的值是 **"JSON"**。内部属性 [[[Extensible]]](ES5/types#Extensible "wikilink") 的值设置为 **true**。

**JSON** 对象没有内部属性 [[[Construct]]](ES5/types#Construct "wikilink")；不能把 **JSON** 对象当作构造器来使用 **new** 操作符。

**JSON** 对象没有内部属性 [[[Call]]](ES5/types#Call "wikilink")；不能把 **JSON** 对象当作函数来调用。

### JSON 语法

**JSON.stringify** 会产生一个符合 **JSON** 语法的字符串。**JSON.parse** 接受的是一个符合 **JSON** 语法的字符串。

#### JSON 词法

类似于 ECMAScript 源文本，**JSON** 是由一系列符合 [*SourceCharacter*](ES5#SourceCharacter "wikilink") 规则的字符构成的。**JSON** 词法定义的 [Token](ES5/lexical#Token "wikilink") 使得 **JSON** 文本类似于 ECMAScript 词法定义的 [Token](ES5/lexical#Token "wikilink") 得到的 ECMAScript 源文本。**JSON** 词法仅能识别由 [JSONWhiteSpace](#JSONWhiteSpace "wikilink") 产生式得到的空白字符。在语法上，所有非终止符均不是由 **"JSON"** 字符开始，而是由 ECMAScript 词法产生式定义的。

语法

`   `*<b id="JSONWhiteSpace">`JSONWhiteSpace`</b>*` :: `
`       `<TAB>
`       `<CR>
`       `<LF>
`       `<SP>

`   `*<b id="JSONString">`JSONString`</b>*` ::`
`       `**`"`**` `*[`JSONStringCharacters`](#JSONStringCharacters "wikilink")*` `**`"`**

`   `*<b id="JSONStringCharacters">`JSONStringCharacters`</b>*` ::`
`       `*[`JSONStringCharacter`](#JSONStringCharacter "wikilink")*` `*[`JSONStringCharacters`](#JSONStringCharacters "wikilink")*

`   `*<b id="JSONStringCharacter">`JSONStringCharacter`</b>*` ::`
`       `[*`SourceCharacter`*](ES5#SourceCharacter "wikilink")` `**`but` `not` `"` `or` `\` `U+0000` `or` `through` `U+001F`**
`       `**`\`**` `*[`JSONEscapeSequence`](#JSONEscapeSequence "wikilink")*

`   `*<b id="JSONEscapeSequence">`JSONEscapeSequence`</b>*` ::`
`       `*[`JSONEscapeCharacter`](#JSONEscapeCharacter "wikilink")*
`       `*[*`UnicodeEscapeSequence`*](ES5/lexical#UnicodeEscapeSequence "wikilink")*

`   `*<b id="JSONEscapeCharacter">`JSONEscapeCharacter`</b>*` :: 以下之一 `
`       `**`"`**` `**`/`**` `**`\`**` `**`b`**` `**`f`**` `**`n`**` `**`r`**` `**`t`**

`   `*<b id="JSONNumber">`JSONNumber`</b>*` ::`
`       `**`-`**` `[*`DecimalIntegerLiteral`*](ES5/lexical#DecimalIntegerLiteral "wikilink")` `*[`JSONFraction`](#JSONFraction "wikilink")*` `[*`ExponentPart`*](ES5/lexical#ExponentPart "wikilink")

`   `*<b id="JSONFraction">`JSONFraction`</b>*` ::`
`       `**`.`**` `[*`DecimalDigits`*](ES5/lexical#DecimalDigits "wikilink")

`   `*<b id="JSONNullLiteral">`JSONNullLiteral`</b>*` ::`
`       `[*`NullLiteral`*](ES5/lexical#NullLiteral "wikilink")

`   `*<b id="JSONBooleanLiteral">`JSONBooleanLiteral`</b>*` ::`
`       `[*`BooleanLiteral`*](ES5/lexical#BooleanLiteral "wikilink")

#### JSON 句法

根据 **JSON** 词法定义的 [Token](ES5/lexical#Token "wikilink")，**JSON** 句法定义了一个合法的 **JSON** 文本。语法的目标符号是 **JSONText**。

语法

`   `*<b id="JSONText">`JSONText`</b>*` :`
`       `*[`JSONValue`](#JSONValue "wikilink")*

`   `*<b id="JSONValue">`JSONValue`</b>*` :`
`       `[*`JSONNullLiteral`*](#JSONNullLiteral "wikilink")
`       `[*`JSONBooleanLiteral`*](#JSONBooleanLiteral "wikilink")
`       `*[`JSONObject`](#JSONObject "wikilink")*
`       `*[`JSONArray`](#JSONArray "wikilink")*
`       `[*`JSONString`*](#JSONString "wikilink")
`       `[*`JSONNumber`*](#JSONNumber "wikilink")

`   `*<b id="JSONObject">`JSONObject`</b>*` :`
`       `**`{`**` `**`}`**
`       `**`{`**` `*[`JSONMemberList`](#JSONMemberList "wikilink")*` `**`}`**

`   `*<b id="JSONMember">`JSONMember`</b>*` :`
`       `[*`JSONString`*](#JSONString "wikilink")` `**`:`**` `*[`JSONValue`](#JSONValue "wikilink")*

`   `*<b id="JSONMemberList">`JSONMemberList`</b>*` :`
`       `*[`JSONMember`](#JSONMember "wikilink")*
`       `*[`JSONMemberList`](#JSONMemberList "wikilink")*` `**`,`**` `*[`JSONMember`](#JSONMember "wikilink")*

`   `*<b id="JSONArray">`JSONArray`</b>*` :`
`       `**`[`**` `**`]`**
`       `**`[`**` `*[`JSONElementList`](#JSONElementList "wikilink")*` `**`]`**

`   `*<b id="JSONElementList">`JSONElementList`</b>*` :`
`       `*[`JSONValue`](#JSONValue "wikilink")*
`       `*[`JSONElementList`](#JSONElementList "wikilink")*` `**`,`**` `*[`JSONValue`](#JSONValue "wikilink")*

### parse ( text [ , reviver ] )

**parse** 函数解析一段 **JSON** 文本（**JSON** 格式字符串），生成一个 ECMAScript 值。**JSON** 格式是ECMAScript直接量的受限模式。**JSON** 对象可以被理解为 ECMAScript 对象。**JSON** 数组可以被理解为 ECMAScript 数组。**JSON** 的字符串、数字、布尔值以及 **null** 可以被认为是 ECMAScript 字符串、数字、布尔值以及 **null**。**JSON** 使用受限更多的空白字符集合，并且允许 Unicode 码点 **U+2028** 和 **U+2029**直 接出现在 **JSONString** 直接量当中而无需使用转义序列。解析流程与 [11.1.4](ES5/expressions#x11.1.4 "wikilink") 和 [11.1.5](ES5/expressions#x11.1.5 "wikilink") 一样，但是由 **JSON** 语法限定。

可选参数 <var>reviver</var> 是一个接受两个参数的函数（<var>key</var> 和 <var>value</var>）。它可以过滤和转换结果。它在每个 **key/value** 对产生时被调用，它的返回值可以用于替代原本的值。如果它原样返回接收到的，那么结构不会被改变。如果它返回 **undefined**，那么属性会被从结果中删除。

1.  令 <var>JText</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>text</var>)。
2.  以 [15.12.1](ES5/builtins#x15.12.1 "wikilink") 所述语法解析 <var>JText</var>。如果 <var>JText</var> 不能以 **JSON** 语法解析成 *[JSONText](#JSONText "wikilink")*，则抛出 **SyntaxError** 异常。
3.  令 <var>unfiltered</var> 为按 ECMAScript 程序（但是用 *[JSONString](#JSONString "wikilink")* 替换 *[StringLiteral](ES5/lexical#StringLiteral "wikilink")*）解析和执行 <var>JText</var> 的结果。注因 <var>JText</var> 符合**JSON**语法，这个结果要么是原始值类型要么是 *[inlineArrayLiteral](ES5/expressions#inlineArrayLiteral "wikilink")* 或者 *[ObjectLiteral](ES5/expressions#inlineObjectLiteral "wikilink")* 所定义的对象。
4.  若 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>reviver</var>) 为 **true** 则
    1.  令 <var>root</var> 为由表达式 **new Object()** 创建的新对象，其中 **Object** 是以 **Object** 为名的标准内置的构造器。
    2.  以空字符串和属性描述 {[[Value]]: <var>unfiltered</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 为参数调用 **root** 的 *[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")* 内置方法。
    3.  返回传入 <var>root</var> 和空字符串为参数调用抽象操作 [Walk](#JSON-Walk "wikilink") 的结果，抽象操作 [Walk](#JSON-Walk "wikilink") 如下文所定义。

5.  否则，返回 <var>unfiltered</var>。

抽象操作 **Walk** 是一个递归的抽象操作，它接受两个参数：一个 <var>holder</var> 对象和一个表示该对象的属性名的 **String** <var>name</var> 。**Walk** 使用最开始被传入 **parse** 函数的 <var>reviver</var> 的值。

1.  令 <var>val</var> 为以参数 <var>name</var> 调用 <var>holder</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
2.  若 <var>val</var> 为对象，则
    1.  若 <var>val</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Array"**
        1.  设 <var>I</var> 为 **0**。
        2.  令 <var>len</var> 为以参数 **"length"** 调用 <var>val</var> 的 [[[Get]]](ES5/types#Get "wikilink") 内部方法的结果。
        3.  当 <var>I</var> \< <var>len</var> 时重复
            1.  令 <var>newElement</var> 为调用抽象操作 [Walk](#JSON-Walk "wikilink") 的结果，传入 <var>val</var> 和 [ToString](ES5/conversion#ToString "wikilink")(<var>I</var>) 为参数。
            2.  若 <var>newElement</var> 为 **undefined**，则
                1.  以 [ToString](ES5/conversion#ToString "wikilink")(<var>I</var>) 和 **false** 做参数，调用 <var>val</var> 的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")。
                2.  否则，以[ToString](ES5/conversion#ToString "wikilink")(<var>I</var>)，属性描述 {[[Value]]: <var>newElement</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 以及 **false** 做参数调用 <var>val</var> 的内部方法[[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。

            3.  对 <var>I</var> 加 **1**。

    2.  否则
        1.  令 <var>keys</var> 为包含 <var>val</var> 所有的具有 [[[Enumerable]]](ES5/types#Enumerable "wikilink") 特征的属性名 **String** 值的内部类型 [List](ES5/types#List "wikilink")。字符串的顺序应当与内置函数 [Object.keys](#x15.2.3.14 "wikilink") 一致。
        2.  对每个 <var>keys</var> 中的字符串 <var>P</var> 做以下操作
            1.  令 <var>newElement</var> 为调用抽象操作 [Walk](#JSON-Walk "wikilink") 的结果，传入 <var>val</var> 和 <var>P</var> 为参数。
            2.  若 <var>newElement</var> 为 **undefined**，则
                1.  以 <var>P</var> 和 **false** 做参数，调用 <var>val</var> 的内部方法 [[[Delete]]](ES5/types#Delete "wikilink")。
                2.  否则，以 <var>P</var>，属性描述{[[Value]]: <var>newElement</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 做参数调用调用 <var>val</var> 的内部方法 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。

3.  返回传入 <var>holder</var> 作为 **this** 值以及以 <var>name</var> 和 <var>val</var> 构成的参数列表调用 <var>reviver</var> 的[[[Call]]内部属性的结果](ES5/types#Call "wikilink")。

实现不允许更改 **JSON.parse** 的实现以扩展 **JSON** 语法。如果一个实现想要支持更改或者扩展过的 **JSON** 交换格式它必须以定义一个不同的 **parse** 函数的方式做这件事。

### stringify ( value [ , replacer [ , space ] ] )

**stringify** 函数返回一个 **JSON** 格式的字符串，用以表示一个ECMAScript值。它可以接受三个参数。第一个参数是必选的。<var>value</var> 参数是一个ECMAScript 值，它通常是对象或者数组，尽管它也可以是 **String**、**Boolean**、**Number** 或者是 **null**。可选的 <var>replacer</var> 参数要么是个可以修改对象和数组字符串化的方式的函数，要么是个扮演选择对象字符串化的属性的白名单这样的角色的 **String** 和 **Number** 组成的数组。可选的 <var>space</var> 参数是一个 **String** 或者 **Number**，可以允许结果中插入空白符以改善人类可读性。

以下为字符串化一对象的步骤：

1.  令 <var>stack</var> 为空 [List](ES5/types#List "wikilink")。
2.  令 <var>indent</var> 为空 **String**。
3.  令 <var>PropertyList</var> 和 <var>ReplacerFunction</var> 为 **undefined**。
4.  若 [Type](ES5/types#Type "wikilink")(<var>replacer</var>) 为 **Object**，则
    1.  若 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>replacer</var>) 为 **true**，则
        1.  令 <var>ReplacerFunction</var> 为 <var>replacer</var>

    2.  否则若 <var>replacer</var> 的内部属性 [[[Class]]](ES5/types#Class "wikilink") 为 **"Array"**，则
        1.  令 <var>PropertyList</var> 为一空内部类型 [List](ES5/types#List "wikilink")
        2.  对于所有名是数组下标的 <var>replacer</var> 的属性 <var>v</var>。以数组下标递增顺序枚举属性
            1.  令 <var>item</var> 为**undefined**
            2.  若 [Type](ES5/types#Type "wikilink")(<var>v</var>) 为 **String** 则令 <var>item</var> 为 <var>v</var>。
            3.  否则若 [Type](ES5/types#Type "wikilink")(<var>v</var>) 为 **Number** 则令 <var>item</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>v</var>)。
            4.  否则若 [Type](ES5/types#Type "wikilink")(<var>v</var>) 为 **Object** 则，
                1.  若 <var>v</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"String"** 或 **"Number"** 则令 <var>item</var> 为[ToString](ES5/conversion#ToString "wikilink")(<var>v</var>)。

            5.  若 <var>item</var> 不是 **undefined** 且 <var>item</var> 不是 <var>PropertyList</var> 的元素。
                1.  把 <var>item</var> 添加到 <var>PropertyList</var> 中。

5.  若 [Type](ES5/types#Type "wikilink")(<var>space</var>) 为 **Object** 则，
    1.  若 <var>space</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Number"** 则，
        1.  令 <var>space</var> 为 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>space</var>)。

    2.  否则若 <var>space</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"String"** 则，
        1.  令 <var>space</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>space</var>)。

6.  若 [Type](ES5/types#Type "wikilink")(<var>space</var>) 为 **Number**。
    1.  令 <var>space</var> 为 [min](ES5/builtins#x15.8.2.12 "wikilink")(**10**, [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>space</var>))。
    2.  设 <var>gap</var> 为一包含 <var>space</var> 个空格的 **String**。这将会是空 **String** 加入 <var>space</var> 小于**1**。

7.  否则若 [Type](ES5/types#Type "wikilink")(<var>space</var>) 为**String**
    1.  若 <var>space</var> 中字符个数为 **10** 或者更小，设 <var>gap</var> 为 <var>space</var>，否则设 <var>gap</var> 为包含前 **10** 个 <var>space</var> 中字符的字符串。

8.  否则设 <var>gap</var> 为空 **String**。
9.  令 <var>wrapper</var> 为一个如同以表达式 **new Object()** 创建的新对象，其中 **Object** 是这个名字的标准内置构造器。
10. 以参数空 **String**，属性描述{[[Value]]: <var>value</var>, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**} 和 **false** 调用 <var>wrapper</var> 的[[[DefineOwnProperty]]内部方法](ES5/types#DefineOwnProperty "wikilink")。
11. 返回以空 **String** 和 <var>wrapper</var> 调用抽象方法 [Str](#JSON-Str "wikilink") 的结果。

抽象操作 **Str**(<var>key</var>, <var>holder</var>) 可以访问调用它的 **stringify** 方法中的 <var>ReplacerFunction</var>。其算法如下：

1.  令 <var>value</var> 为以 <var>key</var> 为参数调用 <var>holder</var> 的内部方法[[[Get]]](ES5/types#Get "wikilink")。
2.  若 [Type](ES5/types#Type "wikilink")(<var>value</var>) 为 **Object**，则
    1.  令 <var>toJSON</var> 为以 **"toJSON"** 为参数调用 <var>value</var> 的内部方法 [[[Get]]](ES5/types#Get "wikilink")。
    2.  若 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>toJSON</var>) 为 **true**
        1.  令 <var>value</var> 为以调用 <var>toJSON</var> 的内部方法 [[[Call]]](ES5/types#Call "wikilink") 的结果，传入 <var>value</var> 为**this**值以及由 <var>key</var> 构成的参数列表。

3.  若 <var>ReplacerFunction</var> 不为 **undefined**,则
    1.  令 <var>value</var> 为以调用 <var>ReplacerFunction</var> 的内部方法 [[[Call]]](ES5/types#Call "wikilink") 的结果，传入 <var>holder</var> 为 **this** 值以及由 <var>key</var> 和 <var>value</var> 构成的参数列表。

4.  若 [Type](ES5/types#Type "wikilink")(<var>value</var>) 为 **Object** 则，
    1.  若 <var>value</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Number"** 则，
        1.  令 <var>value</var> 为[ToNumber](ES5/conversion#ToNumber "wikilink")(<var>value</var>)。

    2.  否则若 <var>value</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"String"** 则，
        1.  令 <var>value</var> 为 [ToString](ES5/conversion#ToString "wikilink")(<var>value</var>)

    3.  否则若 <var>value</var> 的 [[[Class]]](ES5/types#Class "wikilink") 内部属性为 **"Boolean"** 则，
        1.  令 <var>value</var> 为 <var>value</var> 的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性值

5.  若 <var>value</var> 为 **null** 则 返回 **"null"**。
6.  若 <var>value</var> 为 **true** 则 返回 **"true"**。
7.  若 <var>value</var> 为 **false** 则 返回 **"false"**。
8.  若 [Type](ES5/types#Type "wikilink")(<var>value</var>) 为 **String**，则返回以value调用[Quote抽象操作的结果](#JONS-Quote "wikilink")。
9.  若 [Type](ES5/types#Type "wikilink")(<var>value</var>) 为 **Number**
    1.  若 <var>value</var> 是有限的数字则 返回 [ToString](ES5/conversion#ToString "wikilink")(<var>value</var>)。
    2.  否则，返回 **"null"**。

10. 若 [Type](ES5/types#Type "wikilink")(<var>value</var>) 为 **Object** 且 [IsCallable](ES5/conversion#IsCallable "wikilink")(<var>value</var>) 为 **false**
    1.  若 <var>value</var> 的[[[Class]]内部属性为](ES5/types#Class "wikilink") **"Array"** 则
        1.  返回以 <var>value</var> 为参数调用抽象方法 [JA](#JSON-JA "wikilink") 的结果。

    2.  否则，返回以 <var>value</var> 为参数调用抽象方法 [JO](#JSON-JO "wikilink") 的结果。

11. 返回 **undefined**。

抽象操作 **Quote**(<var>value</var>) 将一个 **String** 值封装在双引号中，并且对其中的字符转义。

1.  令 <var>product</var> 为双引号字符。
2.  对 <var>value</var> 中的每一个字符 <var>C</var>
    1.  若 <var>C</var> 为双引号字符或者反斜杠字符
        1.  令 <var>product</var> 为 <var>product</var> 和反斜杠连接的结果。
        2.  令 <var>product</var> 为 <var>product</var> 与 <var>C</var> 的连接。

    2.  否则若 <var>C</var> 为退格符、换页符、换行符、回车符或制表符
        1.  令 <var>product</var> 为 <var>product</var> 与反斜杠字符的连接。
        2.  令 <var>abbrev</var> 为如下表所示 <var>C</var> 对应的字符:
            退格符 **"b"**
            换页符 **"f"**
            换行符 **"n"**
            回车符 **"r"**
            制表符 **"t"**
        3.  令 <var>product</var> 为 <var>product</var> 与 <var>abbrev</var> 的连接。

    3.  否则若 <var>C</var> 为代码值小于 <var>space</var> 的控制字符
        1.  令 <var>product</var> 为 <var>product</var> 与反斜杠字符的连接。
        2.  令 <var>product</var> 为 <var>product</var> 与 **"u"** 的连接。
        3.  令 <var>hex</var> 为转换 <var>C</var> 代码值按十六进制转换到四位字符串的结果。
        4.  令 <var>product</var> 为 <var>product</var> 与 <var>hex</var> 的连接。

    4.  否则
        1.  令 <var>product</var> 为 <var>product</var> 与 <var>C</var> 的连接。

3.  令 <var>product</var> 为 <var>product</var> 与双引号字符的连接。
4.  返回 <var>product</var>。

抽象操作 **JO**(<var>value</var>) 序列化一个对象，它可以访问调用它的方法中的 <var>stack</var>、<var>indent</var>、<var>gap</var>、<var>PropertyList</var>、<var>ReplacerFunction</var> 以及 <var>space</var>。

1.  若 <var>stack</var> 包含 <var>value</var>，则抛出一个**TypeError**，因为对象结构中存在循环。
2.  将 <var>value</var> 添加到 <var>stack</var>。
3.  令 <var>stepback</var> 为 <var>indent</var>。
4.  令 <var>indent</var> 为 <var>indent</var> 与 <var>gap</var> 的连接。
5.  若 <var>PropertyList</var> 没有被定义,则
    1.  令 <var>K</var> 为 <var>PropertyList</var>

6.  否则
    1.  令 <var>K</var> 为以由所有 [[[Enumerable]]](ES5/types#Enumerable "wikilink") 特性为 **true** 的自身属性名构成的内部 **String** 列表类型。

7.  令 <var>partial</var> 为空 [List](ES5/types#List "wikilink")。
8.  对于 <var>K</var> 的每一个元素 <var>P</var>
    1.  令 <var>strP</var> 为以 <var>P</var> 和 <var>value</var> 为参数调用抽象操作 <var>Str</var> 的结果。
    2.  若 <var>strP</var> 没有被定义
        1.  令 <var>member</var> 为以 <var>P</var> 为参数调用抽象操作P的结果。
        2.  令 <var>member</var> 为 <var>member</var> 与冒号字符的连接。
        3.  若 <var>gap</var> 不为空 **String**。
        4.  令 <var>member</var> 为 <var>member</var> 与空格字符的连接。
        5.  令 <var>member</var> 为 <var>member</var> 与 <var>strP</var> 的连接。
        6.  将 <var>member</var> 添加到 <var>partial</var>。

9.  若 <var>partial</var> 为 <var>empty</var>，则
    1.  令 <var>final</var> 为**"{}"**。

10. 否则
    1.  若 <var>gap</var> 为空 **String**
        1.  令 <var>properties</var> 为一个连接所有 <var>partial</var> 中的字符串而成的字符串，键值对之间用逗号分隔。第一个字符串之前和最后一个字符串之后没有逗号。
        2.  令 <var>final</var> 为连接 **"{"**、<var>properties</var>、和 **"}"** 的结果。

    2.  否则 <var>gap</var> 不是空 **String**
        1.  令 <var>separator</var> 为连接 逗号字符，换行字符以及 <var>indent</var> 而成的字符串。
        2.  令 <var>properties</var> 为一个连接所有 <var>partial</var> 中的字符串而成的字符串，键值对之间用 <var>separator</var> 分隔。第一个字符串之前和最后一个字符串之后没有 <var>separator</var>。
        3.  令 <var>final</var> 为连接 **"{"**、换行符、<var>indent</var>、<var>properties</var>、换行符、<var>stepback</var> 和 **"}"** 的结果。

11. 移除 <var>stack</var> 中的最后一个元素。
12. 令 <var>indent</var> 为 <var>stepback</var>。
13. 返回 <var>final</var>。

抽象操作 **JA**(<var>value</var>) 序列化一个数组。它可以访问调用它的 **stringify** 方法中的 <var>stack</var>、<var>indent</var>、<var>gap</var>、<var>PropertyList</var>、<var>ReplacerFunction</var> 以及 <var>space</var>。数组的表示中仅包扩零到 **array.length** - **1**的区间。命名的属性将会被从字符串化操作中排除。数组字符串化成开头的左方括号，逗号分隔的元素，以及结束的右方括号。

1.  若 <var>stack</var> 包含 <var>value</var>，则抛出一个**TypeError**，因为对象结构中存在循环。
2.  将 <var>value</var> 添加到 <var>stack</var>。
3.  令 <var>stepback</var> 为 <var>indent</var>。
4.  令 <var>indent</var> 为 <var>indent</var> 与 <var>gap</var> 的连接。
5.  令 <var>partial</var> 为空 [List](ES5/types#List "wikilink")。
6.  令 <var>len</var> 为以 **"length"** 为参数调用 <var>value</var> 的内部方法 [[[Get]]](ES5/types#Get "wikilink")。
7.  令 <var>index</var> 为 **0**。
8.  当 <var>index</var> \< <var>len</var> 时重复以下
    1.  令 <var>strP</var> 为传入 [ToString](ES5/conversion#ToString "wikilink")(<var>index</var>) 与 <var>value</var> 作为参数调用抽象方法 [Str](#JSON-Str "wikilink") 的结果。
    2.  若 <var>strP</var> 是 **undefined**
        1.  添加 **null** 到 <var>partial</var>。

    3.  否则
        1.  添加 <var>strP</var> 到 <var>partial</var>。

    4.  使 <var>index</var> 增加**1**。

9.  若 <var>partial</var> 为空，则
    1.  令 <var>final</var> 为 **"[]"**。

10. 否则
    1.  若 <var>gap</var> 为空 **String**。
        1.  令 <var>properties</var> 为为一个连接所有 <var>partial</var> 中的字符串而成的字符串，键值对之间用逗号分隔。第一个字符串之前和最后一个字符串之后没有逗号。
        2.  令 <var>final</var> 为连接 **"["**、<var>properties</var> 和 **"]"** 的结果。

    2.  否则
        1.  令 <var>separator</var> 为逗号字符，换行字符以及 <var>indent</var> 而成的字符串。
        2.  令 <var>properties</var> 为一个连接所有 <var>partial</var> 中的字符串而成的字符串，键值对之间用 <var>separator</var> 分隔。第一个字符串之前和最后一个字符串之后没有 <var>separator</var>。
        3.  令 <var>final</var> 为连接 **"["**、换行符、<var>indent</var>、<var>properties</var>、换行符、<var>stepback</var> 和 **"]"** 的结果。

11. 移除 <var>stack</var> 中的最后一个元素。
12. 令 <var>indent</var> 为 <var>stepback</var>。
13. 返回 <var>final</var>。

