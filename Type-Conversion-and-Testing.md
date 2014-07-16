ECMAScript运行环境会在需要时执行自动类型转换。定义一套关于转换的抽象操作有助于阐明某些结构的语义。这些抽象操作不是语言本身的一部分；它们被定义在这里是为了协助语言的语义规范。这些关于转换的抽象操作是多态的，它们可以接受任何[ECMAScript语言类型](ES5/types#language-type "wikilink")，但不能接受[规范类型](ES5/types#specification-type "wikilink")。

ToPrimitive
-----------

**ToPrimitive** 抽象操作接受一个值，和一个可选的<var>期望类型</var>作参数。**ToPrimitive** 运算符把其值参数转换为非对象类型。如果对象有能力被转换为不止一种原语类型，可以使用可选的<var>期望类型</var>来暗示那个类型。根据下表完成转换：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|结果等于输入的参数（不转换）。|
|空值|结果等于输入的参数（不转换）。|
|布尔值|结果等于输入的参数（不转换）。|
|数值|结果等于输入的参数（不转换）。|
|字符串|结果等于输入的参数（不转换）。|
|对象|返回该对象的默认值。调用该对象的内部方法 [[[DefaultValue]]](ES5/types#DefaultValue "wikilink") 来恢复这个默认值，调用时传递暗示<var>期望类型</var>（所有 ECAMScript 本地对象的 [[[DefaultValue]]](ES5/types#DefaultValue "wikilink") 一樣）。|

ToBoolean
---------

**ToBoolean** 抽象操作根据下表将其参数转换为布尔值类型的值：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|**false**|
|空值|**false**|
|布尔值|结果等于输入的参数（不转换）。|
|数值|如果参数是 **+0**, **-0**, 或 **NaN**，结果为 **false** ；否则结果为 **true**。|
|字符串|如果参数是空字符串（其长度为零），结果为 **false**，否则结果为 **true**。|
|对象|**true**|

ToNumber
--------

**ToNumber** 抽象操作根据下表将其参数转换为数值类型的值：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|**NaN**|
|空值|**+0**|
|布尔值|如果参数是 **true**，结果为 **1**。如果参数是 **false**，此结果为 **+0**。|
|数字|结果等于输入的参数（不转换）。|
|字符串|参见下文的文法和注释。|
|对象|应用下列步骤：

1.  令<var>primValue</var>为 (<var>输入参数</var>, 暗示<var>数值类型</var>)。
2.  返回 **ToNumber**(<var>primValue</var>)。|

### 对字符串类型应用 ToNumber

对字符串应用 **ToNumber** 时，对输入字符串应用如下文法。如果此文法无法将字符串解释为 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 的扩展，那么 **ToNumber** 的结果为 **NaN**。

` `*<b id="ToNumber-StringNumericLiteral">`StringNumericLiteral`</b>*` :::`
`   `*[`StrWhiteSpace`](#ToNumber-StrWhiteSpace "wikilink")<sub>`opt`</sub>*
`   `*[`StrWhiteSpace`](#ToNumber-StrWhiteSpace "wikilink")<sub>`opt`</sub>*` `*[`StringNumericLiteral`](#ToNumber-StringNumericLiteral "wikilink")<sub>`opt`</sub>*` `*[`StrWhiteSpace`](#ToNumber-StrWhiteSpace "wikilink")<sub>`opt`</sub>*

` `*<b id="ToNumber-StrWhiteSpace">`StrWhiteSpace`</b>*` :::`
`   `*[`StrWhiteSpaceChar`](#ToNumber-StrWhiteSpaceChar "wikilink")*` `*[`StrWhiteSpace`](#ToNumber-StrWhiteSpace "wikilink")<sub>`opt`</sub>*

` `*<b id="ToNumber-StrWhiteSpaceChar">`StrWhiteSpaceChar`</b>*` :::`
`   `*[`WhiteSpace`](ES5/lexical#white-space "wikilink")*
`   `*[`LineTerminator`](ES5/lexical#line-terminator "wikilink")*

` `*<b id="ToNumber-StrNumericLiteral">`StrNumericLiteral`</b>*` :::`
`   `*[`StrDecimalLiteral`](#ToNumber-StrDecimalLiteral "wikilink")*
`   `*[`HexIntegerLiteral`](#ToNumber-HexIntegerLiteral "wikilink")*

` `*<b id="ToNumber-StrDecimalLiteral">`StrDecimalLiteral`</b>*` :::`
`   `*[`StrUnsignedDecimalLiteral`](#ToNumber-StrUnsignedDecimalLiteral "wikilink")*
`   `**`+`**` `*[`StrUnsignedDecimalLiteral`](#ToNumber-StrUnsignedDecimalLiteral "wikilink")*
`   `**`-`**` `*[`StrUnsignedDecimalLiteral`](#ToNumber-StrUnsignedDecimalLiteral "wikilink")*

` `*<b id="ToNumber-StrUnsignedDecimalLiteral">`StrUnsignedDecimalLiteral`</b>*` :::`
`   `**`Infinity`**
`   `*[`DecimalDigits`](#ToNumber-DecimalDigits "wikilink")*` `**`.`**` `*[`DecimalDigits`](#ToNumber-DecimalDigits "wikilink")<sub>`opt`</sub> [`ExponentPart`](#ToNumber-ExponentPart "wikilink")<sub>`opt`</sub>*
`   `**`.`**` `*[`DecimalDigits`](#ToNumber-DecimalDigits "wikilink")*` `*[`ExponentPart`](#ToNumber-ExponentPart "wikilink")<sub>`opt`</sub>*
`   `*[`DecimalDigits`](#ToNumber-DecimalDigits "wikilink")*` `*[`ExponentPart`](#ToNumber-ExponentPart "wikilink")<sub>`opt`</sub>*

` `*<b id="ToNumber-DecimalDigits">`DecimalDigits`</b>*` :::`
`   `*[`DecimalDigit`](#ToNumber-DecimalDigit "wikilink")*
`   `*[`DecimalDigits`](#ToNumber-DecimalDigits "wikilink")*` `*[`DecimalDigit`](#ToNumber-DecimalDigit "wikilink")*

` `*<b id="ToNumber-DecimalDigit">`DecimalDigit`</b>*` ::: `**`one` `of`**
`   `**`0`**` `**`1`**` `**`2`**` `**`3`**` `**`4`**` `**`5`**` `**`6`**` `**`7`**` `**`8`**` `**`9`**

` `*<b id="ToNumber-ExponentPart">`ExponentPart`</b>*` :::`
`   `*[`ExponentIndicator`](#ToNumber-ExponentIndicator "wikilink")*` `*[`SignedInteger`](#ToNumber-SignedInteger "wikilink")*

` `*<b id="ToNumber-ExponentIndicator">`ExponentIndicator`</b>*` ::: `**`one` `of`**
`   `**`e`**` `**`E`**

` `*<b id="ToNumber-SignedInteger">`SignedInteger`</b>*` :::`
`   `*[`DecimalDigit`](#ToNumber-DecimalDigit "wikilink")*
`   `**`+`**` `*[`DecimalDigit`](#ToNumber-DecimalDigit "wikilink")*
`   `**`-`**` `*[`DecimalDigit`](#ToNumber-DecimalDigit "wikilink")*

` `*<b id="ToNumber-HexIntegerLiteral">`HexIntegerLiteral`</b>*` :::`
`   `**`0x`**` `*[`HexDigit`](#ToNumber-HexDigit "wikilink")*
`   `**`0X`**` `*[`HexDigit`](#ToNumber-HexDigit "wikilink")*
`   `*[`HexIntegerLiteral`](#ToNumber-HexIntegerLiteral "wikilink")*` `*[`HexDigit`](#ToNumber-HexDigit "wikilink")*

` `*<b id="ToNumber-HexDigit">`HexDigit`</b>*` ::: `**`one` `of`**
`   `**`0`**` `**`1`**` `**`2`**` `**`3`**` `**`4`**` `**`5`**` `**`6`**` `**`7`**` `**`8`**` `**`9`**` `**`a`**` `**`b`**` `**`c`**` `**`d`**` `**`e`**` `**`f`**` `**`A`**` `**`B`**` `**`C`**` `**`D`**` `**`E`**` `**`F`**

需要注意到 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 和 *[NumericLiteral](ES5/lexical#numeric-literals "wikilink")* 语法上的不同：

-   *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 的前后可以有若干的[空白字符或](ES5/lexical#white-space "wikilink")[行终止符](ES5/lexical#line-terminator "wikilink")。
-   十进制的 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 可有任意位数的 **0** 在前头。
-   十进制的 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 可有指示其符号的 **+** 或 **-** 前缀。
-   空的，或只包含空白的 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 會被转换为 **+0**。

字符串到[数字值的转换](ES5/types#Number "wikilink")，大体上类似于判定 *[NumericLiteral](ES5/lexical#numeric-literals "wikilink")* 的[数字值](ES5/types#Number "wikilink")，不过有些细节上的不同，所以，这里给出了把 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 转换为数值类型的值的全部过程。这个值分两步来判定：首先，从 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 中导出数学值；第二步，以下面所描述的方式对该数学值进行舍入。

-   *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* ::: *[empty]* 的数学值是 **0**。
-   *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* ::: *[StrWhiteSpace](#ToNumber-StrWhiteSpace "wikilink")* 的数学值是 **0**。
-   *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* ::: *[StrWhiteSpace](#ToNumber-StrWhiteSpace "wikilink")<sub>opt</sub>* *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* *[StrWhiteSpace](#ToNumber-StrWhiteSpace "wikilink")<sub>opt</sub>* 的数学值是里面的 *[StringNumericLiteral](#ToNumber-StringNumericLiteral "wikilink")* 部分，无论前后是否存在空白。
-   *[StrNumericLiteral](#ToNumber-StrNumericLiteral "wikilink")* ::: *[StrDecimalLiteral](#ToNumber-StrDecimalLiteral "wikilink")* 的数学值是 *[StrDecimalLiteral](#ToNumber-StrDecimalLiteral "wikilink")* 的数学值。
-   *[StrNumericLiteral](#ToNumber-StrNumericLiteral "wikilink")* ::: *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* 的数学值是 *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* 的数学值。
-   *[StrDecimalLiteral](#ToNumber-StrDecimalLiteral "wikilink")* ::: *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值是 *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值。
-   *[StrDecimalLiteral](#ToNumber-StrDecimalLiteral "wikilink")* ::: **+** *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值是 *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值。
-   *[StrDecimalLiteral](#ToNumber-StrDecimalLiteral "wikilink")* ::: **-** *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值是 *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值的负数。 （需要注意的是，如果 *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 的数学值是 **0**, 其负数也是 **0**。下面中描述的舍入规则会合适地处理小于数学零到浮点数 **+0** 或 **-0** 的变换。）
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: **Infinity** 的数学值是 '''10<sup>10000'''</sup>（一个大到会舍入为 **+∞** 的值）。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* **.** 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* **.** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值是第一个 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值加（第二个 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10<sup>-<var>n</var></sup>**），这里的 <var>n</var> 是第二个 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的字符数量。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* **.** *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10<sup><var>e</var></sup>**, 这里的 <var>e</var> 是 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* **.** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值是（第一个 [DecimalDigits](#ToNumber-DecimalDigits "wikilink") 的数学值加（第二个 [DecimalDigits](#ToNumber-DecimalDigits "wikilink") 的数学值乘以 **10<sup>-<var>n</var></sup>**））乘以 **10<sup><var>e</var></sup>**，这里的 <var>n</var> 是 第二个 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 中的字符个数，<var>e</var> 是 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: **.** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10<sup>-<var>n</var></sup>**，这里的 <var>n</var> 是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 中的字符个数。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: **.** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10<sup><var>e</var>-<var>n</var></sup>**，这里的 <var>n</var> 是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 中的字符个数，<var>e</var> 是 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值。
-   *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10<sup><var>e</var></sup>**，这里的 <var>e</var> 是 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的数学值。
-   *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* ::: *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* 是 *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* 的数学值。
-   *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* 的数学值。是（ *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值乘以 **10**）加 *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* 的数学值。
-   *[ExponentPart](#ToNumber-ExponentPart "wikilink")* ::: ''[ExponentIndicator](#ToNumber-ExponentIndicator "wikilink") *[SignedInteger](#ToNumber-SignedInteger "wikilink")* 的数学值是 *[SignedInteger](#ToNumber-SignedInteger "wikilink")* 的数学值。
-   *[SignedInteger](#ToNumber-SignedInteger "wikilink")* ::: *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值。
-   *[SignedInteger](#ToNumber-SignedInteger "wikilink")* ::: **+** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值。
-   [SignedInteger](#ToNumber-SignedInteger "wikilink") ::: **-** *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 是 *[DecimalDigits](#ToNumber-DecimalDigits "wikilink")* 的数学值的负数。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **0** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **0** 的数学值是 **0**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **1** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **1** 的数学值是 **1**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **2** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **2** 的数学值是 **2**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **3** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **3** 的数学值是 **3**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **4** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **4** 的数学值是 **4**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **5** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **5** 的数学值是 **5**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **6** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **6** 的数学值是 **6**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **7** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **7** 的数学值是 **7**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **8** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **8** 的数学值是 **8**。
-   *[DecimalDigit](#ToNumber-DecimalDigit "wikilink")* ::: **9** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **9** 的数学值是 **9**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **a** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **A** 的数学值是 **10**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **b** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **B** 的数学值是 **11**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **c** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **C** 的数学值是 **12**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **d** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **D** 的数学值是 **13**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **e** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **E** 的数学值是 **14**。
-   *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **f** 或 *[HexDigit](#ToNumber-HexDigit "wikilink")* ::: **F** 的数学值是 **15**。
-   *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* ::: **0x** *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值是 *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值。
-   *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* ::: **0X** *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值是 *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值。
-   *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* ::: *[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")* *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值是（*[HexIntegerLiteral](#ToNumber-HexIntegerLiteral "wikilink")*　的数学值乘以 **16**）加 *[HexDigit](#ToNumber-HexDigit "wikilink")* 的数学值。

一旦字符串数值常量的数学值被精确地确定，接下来就会被舍入为数值类型的一个值。如果数学值是 **0**，那么舍入值为 **+0**，否则如果字符串数值常量中第一个非空白字符是 ‘**-**’，舍入值为 **-0**。对于其它情况，舍入后的值必须是其数学值的[数字值](ES5/types#Number "wikilink")。如果该字面量包含一个 *[StrUnsignedDecimalLiteral](#ToNumber-StrUnsignedDecimalLiteral "wikilink")* 且该字面量大于 **20** 位<b title="significant digit">有效数字</b>，则此数字的值是下面两种之一：一是将其 **20** 位之后的每个数位用 **0** 替换，产生此字符串解析出的数学值的[数字值](ES5/types#Number "wikilink")；二是将其 **20** 位之后的每个数位用 **0** 替换，并在第 **20** 位<b title="significant digit">有效数字</b>加一，产生此字符串解析出的数学值的[数字值](ES5/types#Number "wikilink")。判断一个数位是否为有效数位，首先它不能是 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 的一部分，且

-   它不是 **0**；或
-   它的左边是一个非零值，右边是一个不在 *[ExponentPart](#ToNumber-ExponentPart "wikilink")* 中的非零值。

ToInteger
---------

**ToInteger** 抽象操作将其参数转换为整数值。

此运算符功能如下所示：

1.  令 <var>number</var> 为对输入的参数调用 [ToNumber](#to-number "wikilink") 的结果。
2.  如果 <var>number</var> 是 **NaN** 则返回 **+0**。
3.  如果 <var>number</var> 是 **+0**、 **-0**、 **+∞** 或 **-∞** 则返回 <var>number</var>。
4.  返回计算 [sign](ES5/notation#sign "wikilink")(<var>number</var>)×[floor](ES5/notation#floor "wikilink")([abs](ES5/notation#abs "wikilink")(<var>number</var>)) 的结果。

ToInt32：（32 位有符号整数）
----------------------------

**ToInt32** 抽象操作将其参数转换为 在 **-2<sup>31</sup>** 到 **2<sup>31</sup>-1** 闭区间内的 **2<sup>32</sup>** 个整数中的任意一个。

此运算符功能如下所示：

1.  令 <var>number</var> 为对输入的参数调用 [ToNumber](#to-number "wikilink") 的结果。
2.  如果 <var>number</var> 是 **NaN**、 **+0**、 **-0**、 **+∞** 或 **-∞** 则返回 **+0**。
3.  令 <var>posInt</var> 为 [sign](ES5/notation#sign "wikilink")(<var>number</var>)×[floor](ES5/notation#floor "wikilink")([abs](ES5/notation#abs "wikilink")(<var>number</var>)) 的结果。
4.  令 <var>int32bit</var> 为 <var>posInt</var> [modulo](ES5/notation#modulo "wikilink") **2<sup>32</sup>**；也就是说，假如有一个数值类型的有限正整数 <var>k</var> ，它小于 **2<sup>32</sup>** ，那么 <var>posInt</var> 与 <var>k</var> 在数学上可能相差 **2<sup>32</sup>** 的整数倍。
5.  如果 <var>int32bit</var> 大于或等于 **2<sup>31</sup>** 则返回 <var>int32bit</var>-**2<sup>32</sup>** 否则返回 <var>int32bit</var>。

ToUint32：（32 位无符号整数）
-----------------------------

**ToUint32** 抽象操作将其参数转换为 在 **0** 到 **2<sup>32</sup>-1** 闭区间内的 **2<sup>32</sup>** 个整数中的任意一个。

此运算符功能如下所示：

1.  令 <var>number</var> 为对输入的参数调用 [ToNumber](#to-number "wikilink") 的结果。
2.  如果 <var>number</var> 是 **NaN**、 **+0**、 **-0**、 **+∞** 或 **-∞** 则返回 **+0**。
3.  令 <var>posInt</var> 为 [sign](ES5/notation#sign "wikilink")(<var>number</var>)×[floor](ES5/notation#floor "wikilink")([abs](ES5/notation#abs "wikilink")(<var>number</var>)) 的结果。
4.  令 <var>int32bit</var> 为 <var>posInt</var> [modulo](ES5/notation#modulo "wikilink") **2<sup>32</sup>**；也就是说，假如有一个数值类型的有限正整数 <var>k</var> ，它小于 **2<sup>32</sup>** ，那么 <var>posInt</var> 与 <var>k</var> 在数学上可能相差 **2<sup>32</sup>** 的整数倍。
5.  返回 <var>int32bit</var>。

ToUint16：（16 位无符号整数）
-----------------------------

**ToUint16** 抽象操作将其参数转换为 在 **0** 到 **2<sup>16</sup>-1** 闭区间内的 **2<sup>16</sup>** 个整数中的任意一个。

此运算符功能如下所示：

1.  令 <var>number</var> 为对输入的参数调用 [ToNumber](#to-number "wikilink") 的结果。
2.  如果 <var>number</var> 是 **NaN**、 **+0**、 **-0**、 **+∞** 或 **-∞** 则返回 **+0**。
3.  令 <var>posInt</var> 为 [sign](ES5/notation#sign "wikilink")(<var>number</var>)×[floor](ES5/notation#floor "wikilink")([abs](ES5/notation#abs "wikilink")(<var>number</var>)) 的结果。
4.  令 <var>int16bit</var> 为 <var>posInt</var> [modulo](ES5/notation#modulo "wikilink") **2<sup>16</sup>**；也就是说，假如有一个数值类型的有限正整数 <var>k</var> ，它小于 **2<sup>16</sup>** ，那么 <var>posInt</var> 与 <var>k</var> 在数学上可能相差 **2<sup>16</sup>** 的整数倍。
5.  返回 <var>int16bit</var>。

ToString
--------

**ToString** 运算符根据下表将其参数转换为字符串类型的值：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|**"undefined"**|
|空值|**"null"**|
|布尔值|如果参数是 **true**，那么结果为 **"true"**。

如果参数是 **false**，那么结果为 **"false"**。|
|数值|见 [9.8.1](#x9.8.1 "wikilink")。|
|字符串|返回输入的参数（不转换）。|
|对象|应用下列步骤：

1.  令 <var>primValue</var> 为 [ToPrimitive](#to-primitive "wikilink")(<var>输入参数</var>, 暗示<var>字符串类型</var>)。
2.  返回 **ToString**(<var>primValue</var>)。|

### 对数值类型应用 ToString

[ToString](#to-string "wikilink") 抽象操作将数字 <var>m</var> 转换为字符串格式的给出如下所示：

1.  如果 <var>m</var> 是 **NaN**，返回字符串 **"NaN"**。
2.  如果 <var>m</var> 是 **+0** 或 **-0**，返回字符串 **"0"**。
3.  如果 <var>m</var> 小于零，返回连接 **"-"** 和 [ToString](#to-string "wikilink")(-<var>m</var>) 的字符串。
4.  如果 <var>m</var> 无限大，返回字符串 **"Infinity"**。
5.  否则，令 <var>n</var>、<var>k</var> 和 <var>s</var> 皆为整数，且满足 <var>k</var> ≥ **1** 且 **10<sup><var>k</var>-1</sup>** ≤ <var>s</var> \< **10<sup><var>k</var></sup>** 、 <var>s</var>×**10<sup><var>n</var>-<var>k</var></sup>** 的数字值为 <var>m</var> 且 <var>k</var> 足够小。注意 <var>k</var> 是 <var>s</var> 的十进制位数。<var>s</var> 不能被 **10** 整除，且 <var>s</var> 的至少要求的有效数字位数不一定要被这些标准唯一确定。
6.  如果 <var>k</var> ≤ <var>n</var> ≤ **21**，返回由 <var>k</var> 个 <var>s</var> 在十进制表示中的数字组成的字符串（有序的，开头没有零），后面连接 <var>n</var>-<var>k</var> 个 **"0"** 字符。
7.  如果 **0** \< <var>n</var> ≤ **21**，返回由 <var>s</var> 在十进制表示中的、最多 <var>n</var> 个有效数字组成的字符串，后面跟随一个小数点 **"."**，再后面是余下的 <var>k</var>-<var>n</var> 个 <var>s</var> 在十进制表示中的数字。
8.  如果 **-6** \< <var>n</var> ≤ **0**，返回由字符 **"0"** 组成的字符串，后面跟随一个小数点 **"."**，再后面是 -<var>n</var> 个 **"0"** 字符，最后是 <var>k</var> 个 <var>s</var> 在十进制表示中的数字。
9.  否则，如果 <var>k</var> = **1**，返回由单个数字 <var>s</var> 组成的字符串，后面跟随小写字母 **"e"**，根据 <var>n</var>-**1** 是正或负，再后面是一个加号 **"+"** 或减号 **"-"** ，再往后是整数 [abs](ES5/notation#abs "wikilink")(<var>n</var>-**1**) 的十进制表示（没有前置的零）。
10. 返回由 <var>s</var> 在十进制表示中的、最多的有效数字组成的字符串，后面跟随一个小数点 **"."**，再后面是余下的是 <var>k</var>-**1** 个 <var>s</var> 在十进制表示中的数字，再往后是小写字母 **"e"**，根据 <var>n</var>-**1** 是正或负，再后面是一个加号 **"+"** 或减号 **"-"** ，再往后是整数 [abs](ES5/notation#abs "wikilink")(<var>n</var>-**1**) 的十进制表示（没有前置的零）。

ToObject
--------

**ToObject** 抽象操作根据下表将其参数转换为对象类型的值：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|抛出 **TypeError** 异常。|
|空值|抛出 **TypeError** 异常。|
|布尔值|创建一个新的 [Boolean](ES5/builtins#x15.6 "wikilink") 对象，其 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 属性被设为该参数的值。|
|数值|创建一个新的 [Number](ES5/builtins#x15.7 "wikilink") 对象，其 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 属性被设为该参数的值。|
|字符串|创建一个新的 [String](ES5/builtins#x15.8 "wikilink") 对象，其 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 属性被设为该参数的值。|
|对象|结果是输入的参数（不转换）。|

CheckObjectCoercible
--------------------

根据 **表15** 定义，抽象操作 <b>CheckObjectCoercible</b> 在其参数无法用 [ToObject](#to-object "wikilink") 转换成对象的情况下抛出一个异常：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|抛出一个 **TypeError** 异常|
|空值|抛出一个 **TypeError** 异常|
|布尔值|返回|
|数值|返回|
|字符串|返回|
|对象|返回|

IsCallable
----------

根据 **表16**，抽象操作 **IsCallable** 确定其必须是 ECMAScript 语言值的参数是否是一个可调用对象：

|nowrap| 输入类型|结果|
|----------------|----|
|未定义|返回 **false**。|
|空值|返回 **false**。|
|布尔值|返回 **false**。|
|数值|返回 **false**。|
|字符串|返回 **false**。|
|对象|如果参数对象包含一个 [[[Call]]](ES5/types#Call "wikilink") 内部方法，则返回 **true**，否则返回 **false**。|

SameValue 算法
--------------

内部严格比较操作 **SameValue**(<var>x</var>,<var>y</var>)，<var>x</var> 和 <var>y</var> 为 ECMAScript [语言中的值](ES5/types#language-type "wikilink")，需要产出 **true** 或 **false**。

比较过程如下：

1.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 与 [Type](ES5/types#Type "wikilink")(<var>y</var>) 的结果不一致，返回 **false**，否则
2.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Undefined**，返回 **true**
3.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Null**，返回 **true**
4.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Number**，则
    1.  如果 <var>x</var> 为 **NaN**，且 <var>y</var> 也为 **NaN**，返回 **true**
    2.  如果 <var>x</var> 为 **+0**，<var>y</var> 为 **-0**，返回 **false**
    3.  如果 <var>x</var> 为 **-0**，<var>y</var> 为 **+0**，返回 **false**
    4.  如果 <var>x</var> 与 <var>y</var> 为同一个数字，返回 **true**
    5.  返回 **false**

5.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **String**，如果 <var>x</var> 与 <var>y</var> 为完全相同的字符序列（相同的长度和相同的字符对应相同的位置），返回 **true**，否则，返回 **false**
6.  如果 [Type](ES5/types#Type "wikilink")(<var>x</var>) 结果为 **Boolean**，如果 <var>x</var> 与 <var>y</var> 都为 **true** 或 **false**，则返回 **true**，否则，返回 **false**
7.  如果 <var>x</var> 和 <var>y</var> 引用到同一个 **Object** 对象，返回 **true**，否则，返回 **false**

