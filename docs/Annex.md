附录 A 文法摘要
---------------

### A.1 词法

` `*<b id="SourceCharacter">`SourceCharacter`</b>*` ::`
`   any Unicode code unit`

` `*<b id="InputElementDiv">`InputElementDiv`</b>*` ::`
`   `**
`   `**
`   `**
`   `**
`   `**

` `*<b id="InputElementRegExp">`InputElementRegExp`</b>*` ::`
`   `**
`   `**
`   `**
`   `**
`   `**

` `*<b id="WhiteSpace">`WhiteSpace`</b>*` ::`
`   `<TAB>
`   `<VT>
`   `<FF>
`   `<SP>
`   `<NBSP>
`   `<BOM>
`   `<USP>

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
`   `<CR><LF>

` `*<b id="Comment">`Comment`</b>*` ::`
`   `**
`   `**

` `*<b id="MultiLineComment">`MultiLineComment`</b>*` ::`
`   `**`/*`**` `**` `**`*/`**

` `*<b id="MultiLineCommentChars">`MultiLineCommentChars`</b>*` ::`
`   `**` `**
`   `**`*`**` `**

` `*<b id="PostAsteriskCommentChars">`PostAsteriskCommentChars`</b>*` ::`
`   `**` `**
`   `**`*`**` `**

` `*<b id="MultiLineNotAsteriskChar">`MultiLineNotAsteriskChar`</b>*` ::`
`   `**` `**`but` `not` `*`**

` `*<b id="MultiLineNotForwardSlashorAsteriskChar">`MultiLineNotForwardSlashorAsteriskChar`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `/` `or` `*`**

` `*<b id="SingleLineComment">`SingleLineComment`</b>*` ::`
`   `**`//`**` `**

` `*<b id="SingleLineCommentChars">`SingleLineCommentChars`</b>*` ::`
`   `**` `**

` `*<b id="SingleLineCommentChar">`SingleLineCommentChar`</b>*` ::`
`   `**` `**`but` `not`**` `**

` `*<b id="Token">`Token`</b>*` ::`
`   `**
`   `**
`   `**
`   `**

` `*<b id="Identifier">`Identifier`</b>*` ::`
`   `**` `**`but` `not`**` `**

` `*<b id="IdentifierName">`IdentifierName`</b>*` ::`
`   `**
`   `**` `**

` `*<b id="IdentifierStart">`IdentifierStart`</b>*` ::`
`   `**
`   `**`$`**
`   `**`_`**` `
`   `**`\`**` `**

` `*<b id="IdentifierPart">`IdentifierPart`</b>*` ::`
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

` `*<b id="ReservedWord">`ReservedWord`</b>*` ::`
`   `**
`   `**
`   `**
`   `**

` `*<b id="Keyword">`Keyword`</b>*` :: `**`one` `of`**
`   `**`break` `do` `instanceof` `typeof`**
`   `**`case` `else` `new` `var`**
`   `**`catch` `finally` `return` `void`**
`   `**`continue` `for` `switch` `while`**
`   `**`debugger` `function` `this` `with`**
`   `**`default` `if` `throw`**
`   `**`delete` `in` `try`**

` `*<b id="FutureReservedWord">`FutureReservedWord`</b>*` :: `**`one` `of`**
`   `**`class` `enum` `extends` `super`**` `
`   `**`const` `export` `import`**
` 在`[`严格模式下还会考虑以下保留字`](ES5/execution#strict-mode-code "wikilink")
`   `**`implements` `let` `private` `public`**
`   `**`interface` `package` `protected` `static`**
`   `**`yield`**` `

` `*<b id="Punctuator">`Punctuator`</b>*` :: `**`one` `of`**
`   `**`{` `}` `(` `)` `[` `]`**
`   `**`.` `;` `,` `<` `>` `<=`**
`   `**`>` `=` `==` `!=` `===` `!==`**
`   `**`+` `-` `*` `%` `++` `--`**
`   `**`<<` `>>` `>>>` `&` `|` `^`**
`   `**`!` `~` `&&` `||` `?` `:`**
`   `**`=` `+=` `-=` `*=` `%=` `<<=`**
`   `**`>>=` `>>>=` `&=` `|=` `^=`**` `

` `*<b id="DivPunctuator">`DivPunctuator`</b>*` ::`**`one` `of`**
`   `**`/` `/=`**

` `*<b id="Literal">`Literal`</b>*` ::`
`   `**
`   `**
`   `**
`   `**
`   `**

` `*<b id="NullLiteral">`NullLiteral`</b>*` ::`
`   `**`null`**

` `*<b id="BooleanLiteral">`BooleanLiteral`</b>*` ::`
`   `**`true`**
`   `**`false`**

` `*<b id="NumericLiteral">`NumericLiteral`</b>*` ::`
`   `**
`   `**

` `*<b id="DecimalLiteral">`DecimalLiteral`</b>*` ::`
`   `**` `**`.`**` `**` `**
`   `**`.`**` `**` `**
`   `**` `**

` `*<b id="DecimalIntegerLiteral">`DecimalIntegerLiteral`</b>*` ::`
`   `**`0`**` `
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

` `*<b id="ExponentIndicator">`ExponentIndicator`</b>*` :: `**`one` `of`**
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

` `*<b id="StringLiteral">`StringLiteral`</b>*` ::`
`   "`**` "`
`   `*`'`*` '`

` `*<b id="DoubleStringCharacters">`DoubleStringCharacters`</b>*` ::`
`   `**` `**

` `*<b id="SingleStringCharacters">`SingleStringCharacters`</b>*` ::`
`   `**` `**

` `*<b id="DoubleStringCharacter">`DoubleStringCharacter`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `"` `or` `\` `or`**` `**
`   `**`\`**` `**
`   `**

` `*<b id="SingleStringCharacter">`SingleStringCharacter`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `'` `or` `\` `or`**` `**
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
`   `* **`but` `not` `one` `of`** *` `**`or`**` `**

` `*<b id="EscapeCharacter">`EscapeCharacter`</b>*` ::`
`   `**
`   `**
`   `**`x`**
`   `**`u`**

` `*<b id="HexEscapeSequence">`HexEscapeSequence`</b>*` ::`
`   `**`x`**` `**` `**

` `*<b id="UnicodeEscapeSequence">`UnicodeEscapeSequence`</b>*` ::`
`   `**`u`**` `**` `**` `**` `**

` `*<b id="RegularExpressionLiteral">`RegularExpressionLiteral`</b>*` ::`
`   `**`/`**` `**` `**`/`**` `**

` `*<b id="RegularExpressionBody">`RegularExpressionBody`</b>*` ::`
`   `**` `**

` `*<b id="RegularExpressionChars">`RegularExpressionChars`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

` `*<b id="RegularExpressionFirstChar">`RegularExpressionFirstChar`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `*` `or` `\` `or` `/` `or` `[`**
`   `**
`   `**

` `*<b id="RegularExpressionChar">`RegularExpressionChar`</b>*` ::`
`   `**` `**`but` `not` `\` `or` `/` `or` `[`**` `
`   `**
`   `**

` `*<b id="RegularExpressionBackslashSequence">`RegularExpressionBackslashSequence`</b>*` ::`
`   `**`\`**` `**

` `*<b id="RegularExpressionNonTerminator">`RegularExpressionNonTerminator`</b>*` ::`
`   `**` `**`but` `not`**` `**

` `*<b id="RegularExpressionClass">`RegularExpressionClass`</b>*` ::`
`   `**`[`**` `**` `**`]`**

` `*<b id="RegularExpressionClassChars">`RegularExpressionClassChars`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

` `*<b id="RegularExpressionClassChar">`RegularExpressionClassChar`</b>*` ::`
`   `**` `**`but` `not` `]` `or` `\`**` `
`   `**

` `*<b id="RegularExpressionFlags">`RegularExpressionFlags`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**` `**

### A.2 数字转换

` `*<b id="StringNumericLiteral">`StringNumericLiteral`</b>*` :::`
`   `**
`   `**` `**` `**

` `*<b id="StrWhiteSpace">`StrWhiteSpace`</b>*` :::`
`   `**` `**

` `*<b id="StrWhiteSpaceChar">`StrWhiteSpaceChar`</b>*` :::`
`   `**
`   `**

` `*<b id="StrNumericLiteral">`StrNumericLiteral`</b>*` :::`
`   `**
`   `**

` `*<b id="StrDecimalLiteral">`StrDecimalLiteral`</b>*` :::`
`   `**
`   `**`+`**` `**
`   `**`-`**` `**

` `*<b id="StrUnsignedDecimalLiteral">`StrUnsignedDecimalLiteral`</b>*` :::`
`   `**`Infinity`**` `
`   `**` . `**` `**
`   `**`.`**` `**` `**
`   `**` `**

` `*<b id="DecimalDigits">`DecimalDigits`</b>*` :::`
`   `**
`   `**` `**

` `*<b id="DecimalDigit">`DecimalDigit`</b>*` :::`**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9`**

` `*<b id="ExponentPart">`ExponentPart`</b>*` :::`
`   `**` `**

` `*<b id="ExponentIndicator">`ExponentIndicator`</b>*` :::`**`one` `of`**
`   `**`e` `E`**

` `*<b id="SignedInteger">`SignedInteger`</b>*` :::`
`   `**
`   `**`+`**` `**
`   `**`-`**` `**

` `*<b id="HexIntegerLiteral">`HexIntegerLiteral`</b>*` :::`
`   `**`0x`**` `**
`   `**`0X`**` `**
`   `**` `**

` `*<b id="HexDigit">`HexDigit`</b>*` :::`**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7` `8` `9` `a` `b` `c` `d` `e` `f` `A` `B` `C` `D` `E` `F`**

### A.3 表达式

` `*<b id="PrimaryExpression">`PrimaryExpression`</b>*` :`
`   `**`this`**` `
`   `**
`   `**
`   `**
`   `**
`   `**`(`**` `**` `**`)`**

` `*<b id="ArrayLiteral">`ArrayLiteral`</b>*` :`
`   `**`[`**` `**` `**`]`**
`   `**`[`**` `**` `**`]`**
`   `**`[`**` `**` `**`,`**` `**` `**`]`**

` `*<b id="ElementList">`ElementList`</b>*` :`
`   `**` `**
`   `**` `**`,`**` `**` `**

` `*<b id="Elision">`Elision`</b>*` :`
`   `**`,`**
`   `**` `**`,`**

` `*<b id="ObjectLiteral">`ObjectLiteral`</b>*` :`
`   `**`{` `}`**` `
`   `**`{`**` `**` `**`}`**
`   `**`{`**` `**` `**`,`**` `**`}`**

` `*<b id="PropertyNameAndValueList">`PropertyNameAndValueList`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="PropertyAssignment">`PropertyAssignment`</b>*` :`
`   `**` : `**
`   `**`get`**` `****`()`**` `**`{`**` `**` `**`}`**
`   `**`set`**` `****`(`**` `**` `**`)` `{`**` `**` `**`}`**

` `*<b id="PropertyName">`PropertyName`</b>*` :`
`   `**
`   `**
`   `**

` `*<b id="PropertySetParameterList">`PropertySetParameterList`</b>*` :`
`   `**

` `*<b id="MemberExpression">`MemberExpression`</b>*` :`
`   `**
`   `**
`   `**` `**`[`**` `**` `**`]`**
`   `**` `**`.`**` `**
`   `**`new`**` `**` `**

` `*<b id="NewExpression">`NewExpression`</b>*` :`
`   `**
`   `**`new`**` `**

` `*<b id="CallExpression">`CallExpression`</b>*` :`
`   `**` `**
`   `**` `**
`   `**` `**`[`**` `**` `**`]`**
`   `**` `**`.`**` `**

` `*<b id="Arguments">`Arguments`</b>*` :`
`   `**`(` `)`**
`   `**`(`**` `**` `**`)`**

` `*<b id="ArgumentList">`ArgumentList`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="LeftHandSideExpression">`LeftHandSideExpression`</b>*` :`
`   `**
`   `**

` `*<b id="PostfixExpression">`PostfixExpression`</b>*` :`
`   `**
`   `**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`++`**` `
`   `**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**`--`**

` `*<b id="UnaryExpression">`UnaryExpression`</b>*` :`
`   `**
`   `**`delete`**` `**
`   `**`void`**` `**
`   `**`typeof`**` `**
`   `**`++`**` `**
`   `**`--`**` `**
`   `**`+`**` `**
`   `**`-`**` `**
`   `**`~`**` `**
`   `**`!`**` `**

` `*<b id="MultiplicativeExpression">`MultiplicativeExpression`</b>*` :`
`   `**
`   `**` `**`*`**` `**
`   `**` `**`/`**` `**
`   `**` `**`%`**` `**

` `*<b id="AdditiveExpression">`AdditiveExpression`</b>*` :`
`   `**
`   `**` `**`+`**` `**
`   `**` `**`-`**` `**

` `*<b id="ShiftExpression">`ShiftExpression`</b>*` :`
`   `**
`   `**` `**`<<`**` `**
`   `**` `**`>>`**` `**
`   `**` `**`>>>`**` `**

` `*<b id="RelationalExpression">`RelationalExpression`</b>*` :`
`   `**
`   `**` `**`<`**` `**
`   `**` `**`>`**` `**
`   `**` `**`<=`**` `**
`   `**` `**`>=`**` `**
`   `**` `**`instanceof`**` `**
`   `**` `**`in`**` `**

` `*<b id="RelationalExpressionNoIn">`RelationalExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`<`**` `**
`   `**` `**`>`**` `**
`   `**` `**`<=`**` `**
`   `**` `**`>=`**` `**
`   `**` `**`instanceof`**` `**

` `*<b id="EqualityExpression">`EqualityExpression`</b>*` :`
`   `**
`   `**` `**`==`**` `**
`   `**` `**`!=`**` `**
`   `**` `**`===`**` `**
`   `**` `**`!==`**` `**

` `*<b id="EqualityExpressionNoIn">`EqualityExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`==`**` `**
`   `**` `**`!=`**` `**
`   `**` `**`===`**` `**
`   `**` `**`!==`**` `**

` `*<b id="BitwiseANDExpression">`BitwiseANDExpression`</b>*` :`
`   `**
`   `**` `**`&`**` `**

` `*<b id="BitwiseANDExpressionNoIn">`BitwiseANDExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`&`**` `**

` `*<b id="BitwiseXORExpression">`BitwiseXORExpression`</b>*` :`
`   `**
`   `**` `**`^`**` `**

` `*<b id="BitwiseXORExpressionNoIn">`BitwiseXORExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`^`**` `**

` `*<b id="BitwiseORExpression">`BitwiseORExpression`</b>*` :`
`   `**
`   `**` `**`|`**` `**

` `*<b id="BitwiseORExpressionNoIn">`BitwiseORExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`|`**` `**

` `*<b id="LogicalANDExpression">`LogicalANDExpression`</b>*` :`
`   `**
`   `**` `**`&&`**` `**

` `*<b id="LogicalANDExpressionNoIn">`LogicalANDExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`&&`**` `**

` `*<b id="LogicalORExpression">`LogicalORExpression`</b>*` :`
`   `**
`   `**` `**`||`**` `**

` `*<b id="LogicalORExpressionNoIn">`LogicalORExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`||`**` `**

` `*<b id="ConditionalExpression">`ConditionalExpression`</b>*` :`
`   `**
`   `**` `**`?`**` `**` `**`:`**` `**

` `*<b id="ConditionalExpressionNoIn">`ConditionalExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`?`**` `**` `**`:`**` `**

` `*<b id="AssignmentExpression">`AssignmentExpression`</b>*` :`
`   `**
`   `**` `**` `**

` `*<b id="AssignmentExpressionNoIn">`AssignmentExpressionNoIn`</b>*` :`
`   `**
`   `**` `**` `**

` `*<b id="AssignmentOperator">`AssignmentOperator`</b>*` :`**`one` `of`**
`   `**`=` `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `>>>=` `&=` `^=` `|=`**` `
`   `
` `*<b id="Expression">`Expression`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="ExpressionNoIn">`ExpressionNoIn`</b>*` :`
`   `**
`   `**` `**`,`**` `**

### A.4 语句

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

` `*<b id="Block">`Block`</b>*` :`
`   `**`{`**` `**` `**`}`**

` `*<b id="StatementList">`StatementList`</b>*` :`
`   `**
`   `**` `**

` `*<b id="VariableStatement">`VariableStatement`</b>*` :`
`   `**`var`**` `**` `**`;`**

` `*<b id="VariableDeclarationList">`VariableDeclarationList`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="VariableDeclarationListNoIn">`VariableDeclarationListNoIn`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="VariableDeclaration">`VariableDeclaration`</b>*` :`
`   `**` `**

` `*<b id="VariableDeclarationNoIn">`VariableDeclarationNoIn`</b>*` :`
`   `**` `**

` `*<b id="Initialiser">`Initialiser`</b>*` :`
`   `**`=`**` `**

` `*<b id="InitialiserNoIn">`InitialiserNoIn`</b>*` :`
`   `**`=`**` `**

` `*<b id="EmptyStatement">`EmptyStatement`</b>*` :`
`   `**`;`**

` `*<b id="ExpressionStatement">`ExpressionStatement`</b>*` :`
`   [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` {`**`{`**`, `**`function`**`}] `**` ;`

` `*<b id="IfStatement">`IfStatement`</b>*` :`
`   `**`if` `(`**` `**` `**`)`**` `**` `**`else`**` `**
`   `**`if` `(`**` `**` `**`)`**` `**

` `*<b id="IterationStatement">`IterationStatement`</b>*` :`
`   `**`do`**` `**` `**`while` `(`**` `**` `**`);`**` `
`   `**`while` `(`**` `**` `**`)`**` `**
`   `**`for` `(`**` `**` `**`;`**` `**` `**`;`**` `**` `**`)`**` `**
`   `**`for` `(` `var`**` `**` `**`;`**` `**` `**`;`**` `**` `**`)`**` `**
`   `**`for` `(`**` `**` `**`in`**` `**` `**`)`**` `**
`   `**`for` `(` `var`**` `**` `**`in`**` `**` `**`)`**` `**

` `*<b id="ContinueStatement">`ContinueStatement`</b>*` :`
`   `**`continue`**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**` `**`;`**

` `*<b id="BreakStatement">`BreakStatement`</b>*` :`
`   `**`break`**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**` `**`;`**

` `*<b id="ReturnStatement">`ReturnStatement`</b>*` :`
`   `**`return`**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**` `**`;`**

` `*<b id="WithStatement">`WithStatement`</b>*` :`
`   `**`with`**` `**`(`**` `**` `**`)`**` `**

` `*<b id="SwitchStatement">`SwitchStatement`</b>*` :`
`   `**`switch`**` `**`(`**` `**` `**`)`**` `**

` `*<b id="CaseBlock">`CaseBlock`</b>*` :`
`   { `**` } `
`   { `****` `**` }`

` `*<b id="CaseClauses">`CaseClauses`</b>*` :`
`   `**
`   `**` `**

` `*<b id="CaseClause">`CaseClause`</b>*` :`
`   `**`case`**` `**` `**`:`**` `**

` `*<b id="DefaultClause">`DefaultClause`</b>*` :`
`   `**`default` `:`**` `**

` `*<b id="LabelledStatement">`LabelledStatement`</b>*` :`
`   `**` : `**

` `*<b id="ThrowStatement">`ThrowStatement`</b>*` :`
`   `**`throw`**` [`[`no` *`LineTerminator`* `here`](ES5/notation#restricted-production "wikilink")`] `**` ;`

` `*<b id="TryStatement">`TryStatement`</b>*` :`
`   `**`try`**` `**` `**
`   `**`try`**` `**` `**
`   `**`try`**` `**` `**` `**

` `*<b id="Catch">`Catch`</b>*` :`
`   `**`catch` `(`**` `**` `**`)`**` `**

` `*<b id="Finally">`Finally`</b>*` :`
`   `**`finally`**` `**

` `*<b id="DebuggerStatement">`DebuggerStatement`</b>*` :`
`   `**`debugger` `;`**

### A.5 函数和程序

` `*<b id="FunctionDeclaration">`FunctionDeclaration`</b>*` :`
`   `**`function`**` `**` `**`(`**` `**` `**`)` `{`**` `**` `**`}`**

` `*<b id="FunctionExpression">`FunctionExpression`</b>*` :`
`   `**`function`**` `**` `**`(`**` `**` `**`)` `{`**` `**` `**`}`**

` `*<b id="FormalParameterList">`FormalParameterList`</b>*` :`
`   `**
`   `**` `**`,`**` `**

` `*<b id="FunctionBody">`FunctionBody`</b>*` :`
`   `**

` `*<b id="Program">`Program`</b>*` :`
`   `**

` `*<b id="SourceElements">`SourceElements`</b>*` :`
`   `**
`   `**` `**

` `*<b id="SourceElement">`SourceElement`</b>*` :`
`   `**
`   `**

### A.6 统一资源定位符字符分类

` `*<b id="uri">`uri`</b>*` :::`
`   `**

` `*<b id="uriCharacters">`uriCharacters`</b>*` :::`
`   `**` `**

` `*<b id="uriCharacter">`uriCharacter`</b>*` :::`
`   `**
`   `**
`   `**

` `*<b id="uriReserved">`uriReserved`</b>*` ::: `**`one` `of`**
`   `**`;` `/` `?` `:` `@` `&` `=` `+` `$` `,`**

` `*<b id="uriUnescaped">`uriUnescaped`</b>*` :::`
`   `**
`   `**
`   `**

` `*<b id="uriEscaped">`uriEscaped`</b>*` :::`
`   `**`%`**` `**` `**

` `*<b id="uriAlpha">`uriAlpha`</b>*` ::: `**`one` `of`**
`   `**`a` `b` `c` `d` `e` `f` `g` `h` `i` `j` `k` `l` `m` `n` `o` `p` `q` `r` `s` `t` `u` `v` `w` `x` `y` `z`**
`   `**`A` `B` `C` `D` `E` `F` `G` `H` `I` `J` `K` `L` `M` `N` `O` `P` `Q` `R` `S` `T` `U` `V` `W` `X` `Y` `Z`**

` `*<b id="uriMark">`uriMark`</b>*` ::: `**`one` `of`**
`   `**`-` `_` `.` `!` `~` `*` `‘` `(` `)`**

### A.7 正则表达式

` `*<b id="Pattern">`Pattern`</b>*` ::`
`   `**

` `*<b id="Disjunction">`Disjunction`</b>*` ::`
`   `**
`   `**` `**`|`**` `**

` `*<b id="Alternative">`Alternative`</b>*` ::`
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
`   `**`(` `?` `=`**` `**` `**`)`**` `
`   `**`(` `?` `!`**` `**` `**`)`**

` `*<b id="Quantifier">`Quantifier`</b>*` ::`
`   `**
`   `**` `**`?`**

` `*<b id="QuantifierPrefix">`QuantifierPrefix`</b>*` ::`
`   `**`*`**
`   `**`+`**` `
`   `**`?`**` `
`   `**`{`**` `**` `**`}`**` `
`   `**`{`**` `**` `**`,` `}`**` `
`   `**`{`**` `**` `**`,`**` `**` `**`}`**

` `*<b id="Atom">`Atom`</b>*` ::`
`   `**
`   `**`.`**
`   `**`\`**` `**
`   `**
`   `**`(`**` `**` `**`)`**` `
`   `**`(` `?` `:`**` `**` `**`)`**

` `*<b id="PatternCharacter">`PatternCharacter`</b>*` :: `
`   `**` `**`but` `not` `one` `of`**` :`
`   `**`^` `$` `\` `.` `*` `+` `?` `(` `)` `[` `]` `{` `}` `|`**

` `*<b id="AtomEscape">`AtomEscape`</b>*` ::`
`   `**
`   `**
`   `**

` `*<b id="CharacterEscape">`CharacterEscape`</b>*` ::`
`   `**
`   `**`c`**` `**
`   `**
`   `**
`   `**

` `*<b id="ControlEscape">`ControlEscape`</b>*` :: `**`one` `of`**
`   `**`f` `n` `r` `t` `v`**

` `*<b id="ControlLetter">`ControlLetter`</b>*` :: `**`one` `of`**
`   `**`a` `b` `c` `d` `e` `f` `g` `h` `i` `j` `k` `l` `m` `n` `o` `p` `q` `r` `s` `t` `u` `v` `w` `x` `y` `z`**
`   `**`A` `B` `C` `D` `E` `F` `G` `H` `I` `J` `K` `L` `M` `N` `O` `P` `Q` `R` `S` `T` `U` `V` `W` `X` `Y` `Z`**

` `*<b id="IdentityEscape">`IdentityEscape`</b>*` ::`
`   `**` but not `**
`   `<ZWJ>
`   `<ZWNJ>

` `*<b id="DecimalEscape">`DecimalEscape`</b>*` ::`
`   `**` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `**`]`

` `*<b id="CharacterClassEscape">`CharacterClassEscape`</b>*` ::`**`one` `of`**
`   `**`d` `D` `s` `S` `w` `W`**

` `*<b id="CharacterClass">`CharacterClass`</b>*` ::`
`   `**`[`**` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` {`**`^`**`}] `**` `**`]`**` `
`   `**`[` `^`**` `**` `**`]`**

` `*<b id="ClassRanges">`ClassRanges`</b>*` ::`
`   [`[`empty`](ES5/notation#empty "wikilink")`]`
`   `**

` `*<b id="NonemptyClassRanges">`NonemptyClassRanges`</b>*` ::`
`   `**
`   `**` `**
`   `**` `**`–`**` `**` `**

` `*<b id="NonemptyClassRangesNoDash">`NonemptyClassRangesNoDash`</b>*` ::`
`   `**
`   `**` `**
`   `**` `**`–`**` `**` `**

` `*<b id="ClassAtom">`ClassAtom`</b>*` ::`
`   `**`-`**` `
`   `**

` `*<b id="ClassAtomNoDash">`ClassAtomNoDash`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `\` `or` `]` `or` `-`**` `
`   `**`\`**` `**

` `*<b id="ClassEscape">`ClassEscape`</b>*` ::`
`   `**
`   `**`b`**` `
`   `**
`   `**

### A.8 JSON

#### A.8.1 JSON 词法

` `*<b id="JSONWhiteSpace">`JSONWhiteSpace`</b>*` ::`
`   `<TAB>
`   `<CR>
`   `<LF>
`   `<SP>

` `*<b id="JSONString">`JSONString`</b>*` ::`
`   `**`"`**` `**` `**`"`**

` `*<b id="JSONStringCharacters">`JSONStringCharacters`</b>*` ::`
`   `**` `**

` `*<b id="JSONStringCharacter">`JSONStringCharacter`</b>*` ::`
`   `**` `**`but` `not` `one` `of` `"` `or` `\` `or` `U+0000` `or` `U+001F`**
`   `**`\`**` `**

` `*<b id="JSONEscapeSequence">`JSONEscapeSequence`</b>*` ::`
`   `**
`   `**

` `*<b id="JSONEscapeCharacter">`JSONEscapeCharacter`</b>*` :: `**`one` `of`**
`   `**`"` `/` `\` `b` `f` `n` `r` `t`**

` `*<b id="JSONNumber">`JSONNumber`</b>*` ::`
`   `**`-`**` `**` `**` `**

` `*<b id="JSONFraction">`JSONFraction`</b>*` ::`
`   `**`.`**` `**

` `*<b id="JSONNullLiteral">`JSONNullLiteral`</b>*` ::`
`   `**

` `*<b id="JSONBooleanLiteral">`JSONBooleanLiteral`</b>*` ::`
`   `**

#### A.8.2 JSON 句法

` `*<b id="JSONText">`JSONText`</b>*` :`
`   `**

` `*<b id="JSONValue">`JSONValue`</b>*` :`
`   `**
`   `**
`   `**
`   `**
`   `**
`   `**

` `*<b id="JSONObject">`JSONObject`</b>*` :`
`   `**`{` `}`**` `
`   `**`{`**` `**` `**`}`**

` `*<b id="JSONMember">`JSONMember`</b>*` :`
`   `**` `**`:`**` `**

` `*<b id="JSONMemberList">`JSONMemberList`</b>*` :`
`   `**` `
`   `**` `**`,`**` `**

` `*<b id="JSONArray">`JSONArray`</b>*` :`
`   `**`[` `]`**` `
`   `**`[`**` `**` `**`]`**

` `*<b id="JSONElementList">`JSONElementList`</b>*` :`
`   `**
`   `**` `**`,`**` `**

附录 B 兼容性
-------------

### 附加语法

ECMAScript 的过去版本中还包含了说明八进制直接量和八进制转义序列的额外语法、语义。在此版本中已将这些附加语法、语义移除。这个非规范性的附录给出与八进制直接量和八进制转义序列一致的语法、语义，以兼容某些较老的 ECMAScript 程序。

#### 数字直接量

[7.8.3](ES5/lexical#numeric-literals "wikilink") 中的语法、语义可以做如下扩展，但在[严格模式代码里不允许做这样的扩展](ES5/execution#strict-mode-code "wikilink")。

语法

` `*<b id="NumericLiteral">`NumericLiteral`</b>*` ::`
`   `*[`DecimalLiteral`](ES5/lexical#DecimalLiteral "wikilink")*
`   `*[`HexIntegerLiteral`](ES5/lexical#HexIntegerLiteral "wikilink")*
`   `**

` `*<b id="OctalIntegerLiteral">`OctalIntegerLiteral`</b>*` ::`
`   `**`0`**` `**
`   `**` `**

` `*<b id="OctalDigit">`OctalDigit`</b>*` :: `**`one` `of`**
`   `**`0` `1` `2` `3` `4` `5` `6` `7`**

语义

-   ** :: ** 的数学值是 ** 的数学值。
-   ** :: **0** 的数学值是 **0**。
-   ** :: **1** 的数学值是 **1**。
-   ** :: **2** 的数学值是 **2**。
-   ** :: **3** 的数学值是 **3**。
-   ** :: **4** 的数学值是 **4**。
-   ** :: **5** 的数学值是 **5**。
-   ** :: **6** 的数学值是 **6**。
-   ** :: **7** 的数学值是 **7**。
-   ** :: **0** ** 的数学值是 ** 的数学值。
-   ** :: ** ** 的数学值是 ** 的数学值乘以 **8** 再加上 ** 的数学值。

#### 字符串直接量

[7.8.4](ES5/lexical#string-literals "wikilink") 中的语法、语义可以做如下扩展，但在[严格模式代码里不允许做这样的扩展](ES5/execution#strict-mode-code "wikilink")。

语法

` `*<b id="EscapeSequence">`EscapeSequence`</b>*` ::`
`   `*[`CharacterEscapeSequence`](ES5/lexical#CharacterEscapeSequence "wikilink")*
`   `**
`   `*[`HexEscapeSequence`](ES5/lexical#HexEscapeSequence "wikilink")*
`   `*[`UnicodeEscapeSequence`](ES5/lexical#UnicodeEscapeSequence "wikilink")*

` `*<b id="OctalEscapeSequence">`OctalEscapeSequence`</b>*` ::`
`   `*[`OctalDigit`](#OctalDigit "wikilink")*` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `*[`DecimalDigit`](ES5/lexical#DecimalDigit "wikilink")*`]`
`   `**` `*[`OctalDigit`](#OctalDigit "wikilink")*` [`[`lookahead` `?`](ES5/notation#lookahead-not-in "wikilink")` `*[`DecimalDigit`](ES5/lexical#DecimalDigit "wikilink")*`]`
`   `**` `*[`OctalDigit`](#OctalDigit "wikilink")*
`   `**` `*[`OctalDigit`](#OctalDigit "wikilink")*` `*[`OctalDigit`](#OctalDigit "wikilink")*

` `*<b id="ZeroToThree">`ZeroToThree`</b>*` :: `**`one` `of`**
`   `**`0` `1` `2` `3`**

` `*<b id="FourToSeven">`FourToSeven`</b>*` :: `**`one` `of`**
`   `**`4` `5` `6` `7`**

语义

-   ** :: ** 的字符值是 ** 的字符值。
-   ** :: ** [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") *[DecimalDigit](ES5/lexical#DecimalDigit "wikilink")*] 的字符值是个字符，它的 unicode 代码单元值是 ** 的数学值。
-   ** :: ** ** [[lookahead ?](ES5/notation#lookahead-not-in "wikilink") *[DecimalDigit](ES5/lexical#DecimalDigit "wikilink")*] 的字符值是个字符，它的 unicode 代码单元值是 ** 的数学值乘以 **8** 再加上 ** 的数学值。
-   ** :: ** ** 的字符值是个字符，它的 unicode 代码单元值是 ** 的数学值乘以 **8** 再加上 ** 的数学值。
-   ** :: ** ** ** 的字符值是个字符，它的 unicode 代码单元值是（** 的数学值乘以 **8<sup>2</sup>**）加上（第一个 ** 的数学值乘以 **8**）加上 ** 的数学值。
-   ** :: **0** 的数学值是 **0**。
-   ** :: **1** 的数学值是 **1**。
-   ** :: **2** 的数学值是 **2**。
-   ** :: **3** 的数学值是 **3**。
-   ** :: **4** 的数学值是 **4**。
-   ** :: **5** 的数学值是 **5**。
-   ** :: **6** 的数学值是 **6**。
-   ** :: **7** 的数学值是 **7**。

### 附加属性

ECMAScript的某些实现给某些标准内置对象加入了额外属性。这个非规范性的附录为这些没有在本标准中提到的属性或它们的语义给出了一致的语义。

#### escape (string)

**escape** 函数是全局对象的一个属性。它通过将一些字符替换成十六进制转义序列，计算出一个新字符串值。

对于代码单元小于等于 **0xFF** 的被替换字符，使用 **%xx** 格式的两位数转义序列。对于代码单元大于 **0xFF** 的被替换字符，使用 **%uxxxx** 格式的四位数转义序列。

用一个参数 <var>string</var> 调用 **escape** 函数，采用以下步骤：

1.  调用 [ToString](ES5/conversion#ToString "wikilink")(<var>string</var>)。
2.  计算 <var>Result(1)</var> 的字符数。
3.  令 <var>R</var> 为空字符串。
4.  令 <var>k</var> 为 **0**。
5.  如果 <var>k</var> 等于 <var>Result(2)</var>, 返回 <var>R</var>。
6.  获得 <var>Result(1)</var> 中 <var>k</var> 位置的字符（表示为16位无符号整数）。
7.  如果 <var>Result(6)</var> 是69个非空字符 **"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789@\*\_+-./"** 之一，则转到 **步骤13**。
8.  如果 <var>Result(6)</var> 小于 **256**，则转到 **步骤11**。
9.  令 <var>S</var> 为包含六个字符 **"%u wxyz"** 的字符串，其中 <var>wxyz</var> 是用四个十六进制数字编码的 <var>Result(6)</var> 值。
10. 转到 **步骤14**。
11. 令 <var>S</var> 为包含三个字符 **"% xy"** 的字符串，其中 <var>xy</var> 是用两个十六进制数字编码的 <var>Result(6)</var> 值。
12. 转到 **步骤14**。
13. 令 <var>S</var> 为包含单个字符 <var>Result(6)</var> 的字符串。
14. 令 <var>R</var> 为将之前的 <var>R</var> 和 <var>S</var> 值连起来组成的新字符串。
15. <var>k</var> 递增 **1**。
16. 转到 **步骤5**。

#### unescape (string)

**unescape** 函数是全局对象的一个属性。它通过将每个可能是 **escape** 函数导入的转义序列，分别替换成代表这些转义序列的字符， 计算出一个新字符串值。

用一个参数 <var>string</var> 调用 **unescape** 函数，采用以下步骤：

1.  调用 [ToString](ES5/conversion#ToString "wikilink")(<var>string</var>)。
2.  计算 <var>Result(1)</var> 的字符数。
3.  令 <var>R</var> 为空字符串。
4.  令 <var>k</var> 为 **0**。
5.  如果 <var>k</var> 等于 <var>Result(2)</var>，返回 <var>R</var>。
6.  令 <var>c</var> 为 <var>Result(1)</var> 中 <var>k</var> 位置的字符。
7.  如果 <var>c</var> 不是 **%** ，转到 **步骤18**。
8.  如果 <var>k</var> 大于 <var>Result(2)</var> - **6**，转到 **步骤14**。
9.  如果 <var>Result(1)</var> 中 <var>k</var> + **1** 位置的字符不是 <b>u</b>，转到 **步骤14**。
10. 如果 <var>Result(1)</var> 中分别在 <var>k</var> + **2**、<var>k</var> + **3**、<var>k</var> + **4**、<var>k</var> + **5** 位置的四个字符不全是十六进制数字，转到 **步骤14**。
11. 令 <var>c</var> 为一个字符，它的代码单元值是 <var>Result(1)</var> 中 <var>k</var> + **2**、<var>k</var> + **3**、<var>k</var> + **4**、<var>k</var> + **5** 位置的四个十六进制数字代表的整数。
12. <var>k</var> 递增 **5**。
13. 转到 **步骤18**。
14. 如果 <var>k</var> 大于 <var>Result(2)</var> - **3**，转到 **步骤18**。
15. 如果 <var>Result(1)</var> 中分别在 <var>k</var> + **1**、<var>k</var> + **2** 位置的两个字符不都是十六进制数字，转到 **步骤18**。
16. 令 <var>c</var> 为一个字符，它的代码单元值是两个零加上 <var>Result(1)</var> 中 <var>k</var> + **1**、<var>k</var> + **2** 位置的两个十六进制数字代表的整数。
17. <var>k</var> 递增 **2**。
18. 令 <var>R</var> 为将之前的 <var>R</var> 和 <var>c</var> 值连起来组成的新字符串。
19. <var>k</var> 递增 **1**。
20. 转到 **步骤5**。

#### String.prototype.substr (start, length)

**substr** 方法有两个参数 <var>start</var> 和 <var>length</var>，将 **this** 对象转换为一个字符串，并返回这个字符串中从 <var>start</var> 位置一直到 <var>length</var> 位置（或如果 <var>length</var> 是 **undefined**，就一直到字符串结束位置）的字符组成的子串。如果 <var>start</var> 是负数，那么它就被当作是 (<var>sourceLength</var> + <var>start</var>)，这里的 <var>sourceLength</var> 是字符串的长度。返回结果是一个字符串值，不是 **String** 对象。采用以下步骤：

1.  将 **this** 值作为参数调用 [ToString](ES5/conversion#ToString "wikilink")。
2.  调用 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>start</var>)。
3.  如果 <var>length</var> 是 **undefined**，就用 **+∞**；否则调用 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>length</var>)。
4.  计算 <var>Result(1)</var> 的字符数。
5.  如果 <var>Result(2)</var> 是正数或零，就用 <var>Result(2)</var>；否则使用 [max](ES5/builtins#x15.8.2.11 "wikilink")(<var>Result(4)</var> + <var>Result(2)</var>, **0**)。
6.  计算 [min](ES5/builtins#x15.8.2.12 "wikilink")([max](ES5/builtins#x15.8.2.11 "wikilink")(<var>Result(3)</var>, **0**), <var>Result(4)</var> - <var>Result(5)</var>)。
7.  如果 <var>Result(6)</var> ≤ **0**, 返回空字符串 "" 。
8.  返回一个由 <var>Result(1)</var> 中的 <var>Result(5)</var> 位置的字符开始的连续的 <var>Result(6)</var> 个字符组成的字符串。

<var>substr</var> 方法的 **length** 属性是 **2**。

#### Date.prototype.getYear ( )

无参数方式调用 **getYear** 方法，采用以下步骤：

1.  令 <var>t</var> 为 **this时间值**。
2.  如果 <var>t</var> 是 **NaN**，返回 **NaN**。
3.  返回 [YearFromTime](ES5/builtins#YearFromTime "wikilink")([LocalTime](ES5/builtins#LocalTime "wikilink")(<var>t</var>)) - **1900**。

#### Date.prototype.setYear (year)

用一个参数 <var>year</var> 调用 **setYear** 方法，采用以下步骤：

1.  令 <var>t</var> 为 [LocalTime](ES5/builtins#LocalTime "wikilink")(**this时间值**) 的结果；但如果 **this时间值** 是 **NaN**，那么令 <var>t</var> 为 **+0**。
2.  调用 [ToNumber](ES5/conversion#ToNumber "wikilink")(<var>year</var>)。
3.  如果 <var>Result(2)</var> 是 **NaN**，将 **this** 值的 [[PrimitiveValue]] 内部属性设为 **NaN**，并返回 **NaN**。
4.  如果 <var>Result(2)</var> 不是 **NaN** 并且 **0** ≤ [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>Result(2)</var>) ≤ **99**，则 <var>Result(4)</var> 是 [ToInteger](ES5/conversion#ToInteger "wikilink")(<var>Result(2)</var>) + **1900**。否则，<var>Result(4)</var> 是 <var>Result(2)</var>。
5.  计算 [MakeDay](ES5/builtins#MakeDay "wikilink")(<var>Result(4)</var>, [MonthFromTime](ES5/builtins#MonthFromTime "wikilink")(<var>t</var>), [DateFromTime](ES5/builtins#DateFromTime "wikilink")(<var>t</var>))。
6.  计算 [UTC](ES5/builtins#UTC "wikilink")([MakeDate](ES5/builtins#MakeDate "wikilink")(<var>Result(5)</var>, [TimeWithinDay](ES5/builtins#TimeWithinDay "wikilink")(<var>t</var>)))。
7.  将 **this** 值的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性设为 [TimeClip](ES5/builtins#TimeClip "wikilink")(<var>Result(6)</var>)。
8.  返回 **this** 值的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 内部属性值。

#### Date.prototype.toGMTString ( )

**Date.prototype.toGMTString** 的初始值是与 **Date.prototype.toUTCString** 的初始值相同的函数对象。

附录 C ECMAScript 的严格模式
----------------------------

**严格模式下的限制和异常**

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink"),"**implements**"、"**interface**"、"**let**"、"**package**"、"**private**"、"**protected**"、"**public**"、"**static**"、和 "**yield**" 这些标识符都属于 *[FutureReservedWord](ES5/lexical#FutureReservedWord "wikilink")*。

-   符合规范的实现中，当处理[严格模式下的代码时](ES5/execution#x10.1.1 "wikilink")，不应该像 中描述地那样将 ** 扩展到 *[NumericLiteral](ES5/lexical#NumericLiteral "wikilink")* 的语法中。

-   符合规范的实现中，当处理[严格模式下的代码时](ES5/execution#x10.1.1 "wikilink")，不应该像 中描述地那样将 ** 扩展到 *[EscapeSequence](ES5/lexical#EscapeSequence "wikilink")* 的语法中。

-   对一个未定义的标识符或其他[无法解析的引用赋值时不会在全局对象上创建属性](ES5/types#IsUnresolvableReference "wikilink")。在[严格模式下](ES5/execution#x10.1.1 "wikilink")，出现一个简单的赋值时，其 *[LeftHandSideExpression](ES5/expressions#LeftHandSideExpression "wikilink")* 不能解析为一个[无法解析的引用](ES5/types#IsUnresolvableReference "wikilink")。如果是那样，将抛出一个 **ReferenceError** 异常。同时，*[LeftHandSideExpression](ES5/expressions#LeftHandSideExpression "wikilink")* 不该引用到一个特性为 { [[Writable]]: **false** } 的数据属性上，也不该引用到一个特性为 { [[Set]]: **undefined** } 的访问器属性上，还不该引用到一个 [[[Extensible]]](ES5/types#Extensible "wikilink") 内部属性值为 **false** 的不可扩对象上。这些情况同样会抛出一个 **TypeError**。

-   **eval** 或 **arguments** 不能出现在[赋值运算符或](ES5/expressions#x11.13 "wikilink")[后缀表达式的](ES5/expressions#x11.3 "wikilink") *[LeftHandSideExpression](ES5/expressions#LeftHandSideExpression "wikilink")* 中，也不能作为[前自增运算符或](ES5/expressions#x11.4.4 "wikilink")[前自减运算符的](ES5/expressions#x11.4.5 "wikilink") *[UnaryExpression](ES5/expressions#UnaryExpression "wikilink")*。

-   [严格模式下](ES5/execution#x10.1.1 "wikilink")，[Arguments](ES5/execution#x10.6 "wikilink") 对象定义了不可配置的存取属性，包括“**caller**”和“**callee**”，如果访问这两个对象则会抛出一个 **TypeError**。

-   [严格模式下](ES5/execution#x10.1.1 "wikilink")，[Arguments](ES5/execution#x10.6 "wikilink") 对象不于其对应的函数形参列表动态共享参数数组索引的值（[10.6](ES5/execution#x10.6 "wikilink")）。

-   [严格模式下](ES5/execution#x10.1.1 "wikilink")，在 [Arguments](ES5/execution#x10.6 "wikilink") 被创建后，局部标识符 **arguments** 将指向这个对象。它是不可改变的，之后也不能对其做赋值操作。（[10.5](ES5/execution#x10.5 "wikilink")）

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，如果 *[ObjectLiteral](ES5/expressions#ObjectLiteral "wikilink")* 中的任何同名数据属性定义超过一次，那么这就是一个语法错误（[11.1.5](ES5/expressions#x11.1.5 "wikilink")）。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，如果 **eval** 或者 **arguments** 出现在属性参数列表中，那么这就是一个语法错误（[11.1.5](ES5/expressions#x11.1.5 "wikilink")）。

-   如果在[严格模式下执行](ES5/execution#x10.1.1 "wikilink") [this](ES5/expressions#x11.1.1 "wikilink") 相关的代码，而且 [this](ES5/expressions#x11.1.1 "wikilink") 的值没有强制指向一个对象。如果 [this](ES5/expressions#x11.1.1 "wikilink") 的值是 **null** 或者 **undefined**，那么 [this](ES5/expressions#x11.1.1 "wikilink") 就不会被转换成全局对象并且静态值不会被转换成包装对象。在[函数调用的操作中](ES5/execution#x10.4.3 "wikilink")（包括 [Function.prototype.apply](ES5/builtins#x15.3.4.3 "wikilink") 和 [Function.prototype.call](ES5/builtins#x15.3.4.4 "wikilink")）传入的 [this](ES5/expressions#x11.1.1 "wikilink") 值不会被强制将传入的 [this](ES5/expressions#x11.1.1 "wikilink") 值指向一个对象。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，使用 [delete](ES5/expressions#x11.4.1 "wikilink") 运算符时，如果 [delete](ES5/expressions#x11.4.1 "wikilink") 后面的值是一个变量的直接引用、函数的参数或函数名，那么就会抛出一个 **SyntexError**。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，使用 [delete](ES5/expressions#x11.4.1 "wikilink") 运算符删除特性为“{ [[Configurable]]:**false** }”的属性时，会抛出一个 **TypeError**。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，*[VariableDeclaration](ES5/statements#VariableDeclaration "wikilink")* 或 *[VariableDeclarationNoIn](ES5/statements#VariableDeclarationNoIn "wikilink")* 中的 *[Identifier](ES5/lexical#Identifier "wikilink")* 出现 **eval** 或 **arguments** 时，抛出一个 **SyntaxError**。

-   [严格模式下的代码不应该含有](ES5/execution#x10.1.1 "wikilink") *[WithStatement](ES5/statements#WithStatement "wikilink")*，如果存在则抛出一个 **SyntexError**。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，使用 *[TryStatement](ES5/statements#TryStatement "wikilink")* 语句时，如果 *[Catch](ES5/statements#Catch "wikilink")* 产生式中的 *[Identifier](ES5/lexical#Identifier "wikilink")* 是 **eval** 或 **arguments**，则抛出一个 **SyntexError**。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，*[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")* 或 *[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 中的 *[FormalParameterList](ES5/functions#FormalParameterList "wikilink")* 里面包含 **eval** 或 **arguments** 标识符，则抛出一个 **SyntexError**。

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，函数的形参列表中不能含有两个或两个以上的同名参数。当试图使用 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")*、*[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 或 [Function构造器](ES5/builtins#x15.3.2 "wikilink") 来创建一个这样的函数时将抛出一个 **SyntexError**。

-   浏览器具体实现不会在当前规范下进行扩展，这也意味着包括[严格模式下函数的](ES5/execution#x10.1.1 "wikilink") **caller** 或其实例的 **arguments** 属性。[严格模式下](ES5/execution#x10.1.1 "wikilink")，ECMAScript代码不能创建或者修改函数上的这些属性。（[10.6](ES5/execution#x10.6 "wikilink")、[13.2](ES5/functions#x13.2 "wikilink")、[15.3.4.5.3](ES5/builtins#x15.3.4.5.3 "wikilink")）

-   在[严格模式下](ES5/execution#x10.1.1 "wikilink")，使用 **eval** 或 **arguments** 标识符作为 *[FunctionDeclaration](ES5/functions#FunctionDeclaration "wikilink")* 或 *[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 或 *[FormalParameterList](ES5/functions#FormalParameterList "wikilink")* 的名字，都会导致 **SyntexError**。试图使用 [Function构造器](ES5/builtins#x15.3.2 "wikilink") 动态定义一个这样的严格模式函数也会抛出一个 **SyntexError**。

附录 D 第5版 中可能会对 第3版 产生兼容性影响的更正及澄清
--------------------------------------------------------

全体：在 **第3版** 规范中像“就像用表达式 **new Array()** 一样”这样的短语的意思受到了误解。 **第5版** 规范中，对标准内置对象、属性的所有内部引用和内部调用相关文本描述，都做了澄清：应使用实际的内置对象，而不是对应命名属性的当前动态值。

[11.8.2](ES5/expressions#x11.8.2 "wikilink")、[11.8.3](ES5/expressions#x11.8.3 "wikilink")、[11.8.5](ES5/expressions#x11.8.5 "wikilink")：ECMAScript 总体上是以从左到右的顺序解释执行，但是 **第3版** 规范中 **\>** 和 **\<=** 运算符的描述语言导致了局部从右到左的顺序。本规范已经更正了这些运算符，现在完全是从左到右的顺序解释执行。然而，这个对顺序的修改，如果在解释执行过程期间产生副作用，就有可能被观察到。

[11.1.4](ES5/expressions#x11.1.4 "wikilink")：**第5版** 澄清了[数组初始化结束位置的尾端逗号不计入数组长度](ES5/expressions#x11.1.4 "wikilink")。这不是对 **第3版** 语义的修改，但有些实现在之前可能对此有误解。

[11.2.3](ES5/expressions#x11.2.3 "wikilink")：**第5版** 调换了算法 **第2步** 和 **第3步** 的顺序。**第1版** 一直到 **第3版** 规定的顺序是错误的，原来的顺序在解释执行 [Arguments](ES5/execution#x10.6 "wikilink") 时有副作用，可能影响到 *[MemberExpression](ES5/expressions#MemberExpression "wikilink")* 的解释执行结果。

[12.14](ES5/statements#x12.14 "wikilink")：在 **第3版** 中，对于传给 [try语句](ES5/statements#x12.14 "wikilink") 的 **catch** 子句的异常参数的名称解析，用与 **new Object()** 一样的方式创建一个对象来作为解析这个名称的作用域。如果实际的异常对象是个函数并且在 **catch** 子句中调用了它，那么作用域对象将会作为 **this** 值传给这个调用。在函数体里可以给它的 **this** 值定义新属性，并且这些属性名将在函数返回之后在 **catch** 子句的作用域内变成可见的标识符绑定。在 **第5版** 中，如果把异常参数作为函数来调用，传入的 **this** 值是 **undefined**。

[13](ES5/functions "wikilink")：在 **第3版** 中，有 *[Identifier](ES5/lexical#Identifier "wikilink")* 的 *[FunctionExpression](ES5/functions#FunctionExpression "wikilink")* 产生式的算法，用与 **new Object()** 一样的方式创建一个对象并加入到作用域链中，用来提供函数名查找的作用域。标识符解析规则（**第3版** 里的 [10.1.4](ES5/expressions#x10.1.4 "wikilink")）会作用在这样的对象上，如果需要，还会用对象的原型链来尝试解析标识符。这种方式使得 **Object.prototype** 的所有属性以标识符的形式在这个作用域里可见。实践中，大多数 **第3版** 的实现都没有实行这个语义。**第5版** 更改了这里的语义，用一个声明式环境记录项来绑定了函数名。

[14](ES5/program "wikilink")：在 **第3版** 中，产生式 *[SourceElements](ES5/program#SourceElements "wikilink")* : *[SourceElements](ES5/program#SourceElements "wikilink")* *[SourceElement](ES5/program#SourceElement "wikilink")* 的算法不像相同形式的 *[Block](ES5/statements#Block "wikilink")* 对语句的结果值做正确的传递。这可导致 **eval** 函数解释执行一个 *[Program](ES5/program#Program "wikilink")* 文本时产生错误的结果。实践中，大多数 **第3版** 的实现都做了正确的传递，而不关心 **第5版** 规定了什么。

[15.10.6](ES5/builtins#15.10.6 "wikilink")：**RegExp.prototype** 现在是一个 **RegExp** 对象，而不是 **Object** 的一个实例。用 **Object.prototype.toString** 可看到它的 [[[Class]]](ES5/types#Class "wikilink") 内部属性值现在是 "**RegExp**"，不是 "**Object**"。

附录 E 第5版 内容的增加与变化，介绍 第3版 不兼容问题
----------------------------------------------------

[7.1](ES5/lexical#x7.1 "wikilink")：Unicode 格式控制字符在受到处理之前不再从 ECMAScript 源文本中剥离。在 **第5版** 中，如果这样一个字符在字符串字面量或者正则表达式字面量中出现，这个字符会被合并到字面量中，而在 **第3版** 里，这个字符不会被合并。

[7.2](ES5/lexical#x7.2 "wikilink")：Unicode 字符 **<BOM>** 现在是作为空格使用，如果它出现在本该是一个标识符的位置的中间，则会产生一个语法错误，而在 **第3版** 里不会。

[7.3](ES5/lexical#x7.3 "wikilink")：换行符以前是作为转义字符处理，而现在允许换行符被包含在字符串字面量标记中。这在 **第3版** 中会产生一个语法错误。

[7.8.5](ES5/lexical#x7.8.5 "wikilink")：现在的正则表达式字面量在字面量解析执行的时候都会返回一个唯一的对象。这个改变可以被任意测试字面量值的对象标识符或者一些敏感的副作用的程序检测到。

[7.8.5](ES5/lexical#x7.8.5 "wikilink")：**第5版** 要求从 *[RegularExpressionLiteral](ES5/lexical#RegularExpressionLiteral "wikilink")* 转换到 **RegExp** 对象时可能的错误作为[早期错误抛出](ES5/errors#early-error "wikilink")。在 **第5版** 之前的实现允许延迟抛出 **TypeError**，直到真正执行到这个对象。

[7.8.5](ES5/lexical#x7.8.5 "wikilink")：在 **第5版** 中，未转义的 "**/**" 字符可以作为 *[CharacterClass](ES5/lexical#x7.8.5 "wikilink")* 存在于正则表达式字面量中。在 **第3版** 里，这样的字符是作为字面量的最后一个字符存在。

[10.4.2](ES5/execution#x10.4.2 "wikilink")：在 **第5版** 中，间接调用 **eval** 函数会将全局对象作为 [eval代码](ES5/execution#eval-code "wikilink") 的变量环境和 [词法环境](ES5/execution#x10.2 "wikilink")。在 **第3版** 中，**eval** 函数的间接调用者的变量和[词法环境是作为](ES5/execution#x10.2 "wikilink") [eval代码](ES5/execution#eval-code "wikilink") 的环境使用。

[15.4.4](ES5/builtins#x15.4.4 "wikilink")：在 **第5版** 中，所有 [Array.prototype](ES5/builtins#x15.4.3.1 "wikilink") 下的方法都是通用的。在 **第3版** 中，**toString** 和 **toLocaleString** 方法不是通用的，如果被非 **Array** 实例调用时会抛出一个 **TypeError** 的异常。

[10.6](ES5/execution#x10.6 "wikilink")：在 **第5版** 中，**arguments** 对象与实际的参数符合，它的数组索引属性是可枚举的。在 **第3版** 中，这些属性是不可枚举的。

[10.6](ES5/execution#x10.6 "wikilink")：在 **第5版** 中，**arguments** 对象的 [[[Class]]](ES5/types#Class "wikilink") 内置属性值是“**Arguments**”。在 **第3版** 中，它是“**Object**”。当对 **arguments** 对象调用 **toString** 的时候

[12.6.4](ES5/statements#x12.6.4 "wikilink")：当 **in** 表达式执行一个 **null** 或者 **undefined** 时，[for-in 语句不再抛出](ES5/statements#12.6.4 "wikilink") **TypeError**。取而代之的是将其作为不包含可枚举属性的对象执行。

[15](ES5/builtins "wikilink")：在 **第5版** 中，下面的新属性都是在第三种中已存在的内建对象中定义，**Object.getPrototypeOf, Object.getOwnPropertyDescriptor, Object.getOwnPropertyNames, Object.create, Object.defineProperty, Object.defineProperties, Object.seal, Object.freeze, Object.preventExtensions, Object.isSealed, Object.isFrozen, Object.isExtensible, Object.keys, Function.prototype.bind, Array.prototype.indexOf, Array.prototype.lastIndexOf, Array.prototype.every, Array.prototype.some, Array.prototype.forEach, Array.prototype.map, Array.prototype.filter, Array.prototype.reduce, Array.prototype.reduceRight, String.prototype.trim, Date.now, Date.prototype.toISOString, Date.prototype.toJSON**。

[15](ES5/builtins "wikilink")：实现现在要求忽略内建方法中的额外参数，除非明确指定。在 **第3版** 中，并没有规定额外参数的处理方式，实现中明确允许抛出一个 **TypeError** 错误。

[15.1.1](ES5/builtins#x15.1.1 "wikilink")：全局对象的值属性 **NaN**、**Infinity** 和 **Undefined** 改为只读属性。

[15.1.2.1](ES5/builtins#x15.1.2.1 "wikilink")：实现不再允许约束非直接调用 **eval** 的方式。另外间接调用 **eval** 会使用全局对象作为变量环境，而不是使用调用者的变量环境作为变量环境。

[15.1.2.2](ES5/builtins#x15.1.2.2 "wikilink")：**parseInt** 的规范不再允许实现将 **0** 开头的字符串作为8进制值。

[15.3.4.3](ES5/builtins#x15.3.4.3 "wikilink")：在 **第3版** 中，如果传入 [Function.prototype.apply](ES5/builtins#x15.3.4.3 "wikilink") 的第二个参数不是一个数组对象或者一个 **arguments** 对象，就会抛出一个 **TypeError**。在 **第5版** 中，参数也可以是任意类型的含有 **length** 属性的类数组对象。

[15.3.4.3](ES5/builtins#x15.3.4.3 "wikilink")，[15.3.4.4](ES5/builtins#x15.3.4.4 "wikilink")：在 **第3版** 中，在 [Function.prototype.apply](ES5/builtins#x15.3.4.3 "wikilink") 或者 [Function.prototype.call](ES5/builtins#x15.3.4.4 "wikilink") 中传入 **undefined** 或者 **null** 作为第一个参数会导致[全局对象被作为一个个参数传入](ES5/builtins#x15.1 "wikilink")，间接导致目标函数的 **this** 会指向全局变量环境。如果第一个参数是一个原始值，在原始值上调用 [ToObject](ES5/conversion#ToObject "wikilink") 的结果会作为 **this** 的值。在 **第5版** 中，这些转换不会出现，目标函数的 **this** 会指向真实传入的参数。这个不同点一般情况下对已存在的遵循 ECMAScript **第3版** 的代码来说不太明显，因为相应转换会在目标函数生效之前执行。然而，基于不同的实现，如果使用 **apply** 或者 **call** 调用函数时，这个不同点就会很明显。另外，用这个方法调用一个标准的内建函数，并使用 **null** 或者 **undefined** 作为参数时，很可能会导致 **第5版** 标准下的实现与 **第3版** 标准下的实现不同。特别是 **第5版** 中代表性地规定了需要将实际调用的传入的 **this** 值作为对象的内建函数，在传入 **null** 或者 **undefined** 作为 **this** 值时，会抛出一个 **TypeError** 异常。

[15.3.5.2](ES5/builtins#x15.3.5.2 "wikilink")：在 **第5版** 中，函数实例的 **prototype** 属性是不可枚举的。在 **第3版** 中，是可以枚举的。

[15.5.5.2](ES5/builtins#x15.5.5.2 "wikilink")：在 **第5版** 中，一个字符串对象的 [[[PrimitiveValue]]](ES5/types#PrimitiveValue "wikilink") 的单个字符可以作为字符串对象的数组索引属性访问。这些属性是不可泄也不可配置的，并会影响任意名字相同的继承属性。在 **第3版** 中，这些属性不会存在，ECMAScript 代码可以通过这些名字动态添加和移除可写的属性并访问以这些名字继承的属性。

[15.9.4.2](ES5/builtins#x15.9.4.2 "wikilink")：[Date.parse](ES5/builtins#x15.9.4.2 "wikilink") 方法现在不要求第一个参数首先作为 ISO 格式字符串解析。使用这个格式但是基于特定行为实现（包括未来的一些行为）或许会表现的不太一样。

[15.10.2.12](ES5/builtins#x15.10.2.12 "wikilink")：在 **第5版** 中，**\\s** 现在可以匹配 **<BOM>** 了。

[15.10.4.1](ES5/builtins#x15.10.4.1 "wikilink")：在 **第3版** 中，由 **RegExp** 构造器创建的对象的 **source** 字符串的精确形式由实现定义。在 **第5版** 中，字符串必须符合确定的指定条件，因此会和 **第3版** 标准的实现的结果不一样。

[15.10.6.4](ES5/builtins#x15.10.6.4 "wikilink")：在 **第3版** 中，[RegExp.prototype.toString](ES5/builtins#x15.10.6.4 "wikilink") 的规则不需要由 **RegExp** 对象的 **source** 属性决定。在 **第5版** 中，结果必须由 **source** 属性经由一个指定的规则，因此会和 **第3版** 实现的结果不一样。

[15.11.2.1](ES5/builtins#x15.11.2.1 "wikilink")，[15.11.4.3](ES5/builtins#x15.11.4.3 "wikilink")：在 **第5版** 中，如果一个错误对象的 **message** 属性原始值没有通过 **Error** 构造器指定，那么这个原始值就是一个空的字符串。在 **第3版** 中，这个原始值由实现决定。

[15.11.4.4](ES5/builtins#x15.11.4.4 "wikilink")：在 **第3版** 中，[Error.prototype.toString](ES5/builtins#x15.11.4.4 "wikilink") 的结果是由实现定义的。在 **第5版** 中，有完整的规范指定，因此可能会和 **第3版** 的实现不同。

[15.12](ES5/builtins#x15.12 "wikilink")： 在 **第5版** 中，**JSON** 是在全局环境中定义的。 **第3版** 中，测试这个名词的存在会发现它是 **undefined**，除非这个程序或者实现定义了这个名词。

附录 F 5.1 版中技术上的重大更正和阐明
-------------------------------------

[7.8.4](ES5/lexical#x7.8.4 "wikilink")：字符值定义追加了 *[DoubleStringCharacter](ES5/lexical#DoubleStringCharacter "wikilink")* :: *[LineContinuation](ES5/lexical#LineContinuation "wikilink")* 与 *[SingleStringCharacter](ES5/lexical#SingleStringCharacter "wikilink")* :: *[LineContinuation](ES5/lexical#LineContinuation "wikilink")*。

[10.2.1.1.3](ES5/execution#x10.2.1.1.3 "wikilink")：参数 <var>S</var> 是不能被忽略的。它控制着试图设置一个不可改变的绑定时是否抛出异常。

[10.2.1.2.2](ES5/execution#x10.2.1.2.2 "wikilink")：在算法的 **第5步**，真被传递后最后一个参数为 [[[DefineOwnProperty]]](ES5/types#DefineOwnProperty "wikilink")。

[10.5](ES5/execution#x10.5 "wikilink")：当重定义全局函数使，原算法 **第5.5步** 调整为现在的 **第5.6步**，并加入一个新的 **第5.5步** 用来还原与第三版的兼容性。

[11.5.3](ES5/expressions#x11.5.3 "wikilink")：在最后符号项，指定使用 IEEE754 舍入到最接近模式。

[12.6.3](ES5/statements#x12.6.3 "wikilink")：在 **第3.1.2步** 的两种算法中修复缺失的 [ToBoolean](ES5/conversion#ToBoolean "wikilink")。

[12.6.4](ES5/statements#x12.6.4 "wikilink")：在最后两段的额外最后一句中，阐明某些属性枚举的规定。

[12.7](ES5/statements#x12.7 "wikilink")、[12.8](ES5/statements#x12.8 "wikilink")、[12.9](ES5/statements#x12.9 "wikilink")：BNF 的修改为阐明 [continue](ES5/statements#x12.7 "wikilink") 或 [break](ES5/statements#x12.8 "wikilink") 语句没有一个 [Identifier](ES5/lexical#Identifier "wikilink") 或一个 [return](ES5/statements#x12.9 "wikilink") 语句没有一个表达式时，在分号之前可以有一个 *[LineTerminator](ES5/lexical#LineTerminator "wikilink")*。

[12.14](ES5/statements#x12.14 "wikilink")：**算法1** 的 **第3步**，**算法3** 的 **第2.1步** 中，纠正这样的值 <var>B</var> 是作为参数传递而不是 <var>B</var> 本身。

[15.1.2.2](ES5/builtins#x15.1.2.2 "wikilink")：在算法的 **第2步** 中阐明 <var>S</var> 可能是空字符串。

[15.1.2.3](ES5/builtins#x15.1.2.3 "wikilink")：在算法的 **第2步** 中阐明 <var>trimmedString</var> 可以是空字符串。

[15.1.3](ES5/builtins#x15.1.3 "wikilink")：添加注释阐明 ECMAScript 中的 URI 语法基于 RFC 2396 和较新的 RFC 3986。

[15.2.3.7](ES5/builtins#x15.2.3.7 "wikilink")：在算法 **第5步** 和 **第6步** 中更正使用变量 <var>P</var>。

[15.2.4.2](ES5/builtins#x15.2.4.2 "wikilink")：**第5版** 处理 **undefined** 和 **null** 值导致现有代码失败。规范修改为保持这样的代码的兼容性。在算法中加入新的 **第1步** 和 **第2步**。

[15.3.4.3](ES5/builtins#x15.3.4.3 "wikilink")：**第5版** 中的 **第5步** 和 **第7步** 已被删除，因为它们规定要求 <var>argArray</var> 参数与泛数组状对象的其它用法不一致。

[15.4.4.12](ES5/builtins#x15.4.4.12 "wikilink")：在 **第9.1步**，用 <var>actualStart</var> 替换不正确 <var>relativeStart</var> 引用。

[15.4.4.15](ES5/builtins#x15.4.4.15 "wikilink")：阐明 <var>fromIndex</var> 的默认值是数组的长度减去 **1**。

[15.4.4.18](ES5/builtins#x15.4.4.18 "wikilink")：在算法的 **第9步**，**undefined** 是现在指定的返回值。

[15.4.4.22](ES5/builtins#x15.4.4.22 "wikilink")：在 **第9.3.2步**，第一个参数的 [[[Call]]](ES5/types#Call "wikilink") 内部方法已经改变为 **undefined**，保持与 **Array.prototype.reduce** 定义的一致性。

[15.4.5.1](ES5/builtins#x15.4.5.1 "wikilink")：在算法 **第3.12.2步** 和 **第3.12.3步** 中，变量的名字是相反的，导致一个不正确的相反测试。

[15.5.4.9](ES5/builtins#x15.5.4.9 "wikilink")：规范要求每有关规范等效字符串删除，算法从每一个段落都承接，因为它在 **注2** 中被列为建议的。

[15.5.4.14](ES5/builtins#x15.5.4.14 "wikilink")：在 **split** 算法 **第11.1步** 和 **第13.1步**，[SplitMatch](ES5/builtins#SplitMatch "wikilink") 参数的位置顺序已修正为匹配 [SplitMatch](ES5/builtins#SplitMatch "wikilink") 的实际参数特征。在 **第13.1.3.7.4步**，<var>lengthA</var> 取代 <var>A</var>.<var>length</var>。

[15.5.5.2](ES5/builtins#x15.5.5.2 "wikilink")：在首段中，删除的单个字符属性访问“**array index**”语义的含义。改进算法 **第3步** 和 **第5步**，这样它们不执行“**array index**”的要求。

[15.9.1.15](ES5/builtins#x15.9.1.15 "wikilink")：为缺失字段指定了合法值范围。淘汰“**time-only**”格式。所有可选字段指定默认值。

[15.10.2.2](ES5/builtins#x15.10.2.2 "wikilink")：算法步骤编号为 **第2步** 所产生的内部闭包被错误的编号，它们是额外的算法步骤。

[15.10.2.6](ES5/builtins#x15.10.2.6 "wikilink")：在 **第3步** 中的列表中抽象运算符 [IsWordChar](ES5/builtins#IsWordChar "wikilink") 的第一个字符是“**a**”而不是“**A**”。

[15.10.2.8](ES5/builtins#x15.10.2.8 "wikilink")：在闭包算法返回抽象运算符 [CharacterSetMatcher](ES5/builtins#CharacterSetMatcher "wikilink") 中，为了避免与一个闭包的形参名称冲突，**第3步** 中定义的变量作为参数传递在 **第4步** 更名为 <var>ch</var>。

[15.10.6.2](ES5/builtins#x15.10.6.2 "wikilink")：**第步9.5步** 被删除，因为它执行了 <var>I</var> 的额外增量。

[15.11.1.1](ES5/builtins#x15.11.1.1 "wikilink")：当 <var>message</var> 参数是 **undefined** 时，撤销 <var>message</var> 自身属性设置为空字符串的要求。

[15.11.1.2](ES5/builtins#x15.11.1.2 "wikilink")：当 <var>message</var> 参数是 **undefined** 时，撤销 <var>message</var> 自身属性设置为空字符串的要求。

[15.11.4.4](ES5/builtins#x15.11.4.4 "wikilink")：**第6步** 到 **第10步** 修改 **/** 添加正确处理缺少或空的 <var>message</var> 属性值。

[15.12.3](ES5/builtins#x15.12.3 "wikilink")：在 [JA](ES5/builtins#JSON-JA "wikilink") 的内部操作的 **第10.2.3步**，串联的最后一个元素是 “]”。

[B.2.1](ES5/annex#B.2.1 "wikilink")：追加注释，说明编码是基于 RFC 1738 而不是新的 RFC 3986。

附录 [C](ES5/annex#C "wikilink")：增加了 **FutureReservedWords** 在标准模式下的相应内容到 [7.6.1.2](ES5/lexical#x7.6.12 "wikilink") 节。

