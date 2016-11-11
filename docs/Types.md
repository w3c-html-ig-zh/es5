本规范的算法会处理每个关联了类型的值，所有可能出现的值的类型都定义在本条目中。这些类型又再细分为 [ECMAScript语言类型](#language-type "wikilink") 和 [规范类型](#specification-type "wikilink")。

<b id="language-type" title="ECMAScript language Type">ECMAScript语言类型</b> 对应的是程序员使用 ECMAScript 语言直接操作的值。**ECMAScript语言类型** 包括 、、、、、。

<b id="specification-type" title="Specification Type">规范类型</b> 对应的是 <b title="Meta Value">元值</b>，它被用于在算法中描述 ECMAScript 语言结构的语义和 **ECMAScript语言类型**。**规范类型**包括[引用](#Reference "wikilink")、[列表](#List "wikilink")、[完结](#Completion "wikilink")、[属性描述式](#property-descriptor "wikilink")、[属性标示](#property-identifier "wikilink")、[词法环境](ES5/execution#lexical-environment "wikilink")、[ 环境纪录](ES5/execution#environment-record "wikilink")。**规范类型**的值是规范自造的，在 ECMAScript 的实现中不必对应到特定的实体上。**规范类型**可用来描述 ECMAScript 表达式运算的中间结果，但这样的值不能储存为对象的属性或 ECMAScript 语言的变量值。

在本规范中，记法 <b id="Type">Type(<var>x</var>)</b> 表示 “<var>x</var> 的类型”，而“类型”指的就是上述的 [ECMAScript语言类型](#language-type "wikilink") 与[规范类型](#specification-type "wikilink")。

Undefined类型
-------------

**Undefined类型** 有且只有一个值，称为 **undefined** 。任何没有被赋值的变量值为 **undefined** 。

Null类型
--------

**Null类型** 有且只有一个值，称为 **null** 。

Boolean类型
-----------

**Boolean类型** 表示逻辑实体，有两个值，称为 **true** 和 **false**。

String类型
----------

字符串类型是所有有限的零个或多个16位无符号整数值（“**元素**”）的有序序列。在运行的 ECMAScript 程序中，字符串类型常被用于表示文本数据，此时字符串中的每个**元素**都被视为一个 **代码单元**（参看 [章节 6](ES5#x6 "wikilink")）。 每个**元素**都被认为占有此序列中的一个位置，用非负整数索引这些位置。任何时候，第一个**元素**（若存在）在位置0，下一个**元素**（若存在）在位置1，依此类推。字符串的长度即其中**元素**（即16位的值）的个数。空字符串长度为零，因而不包含任何**元素**。

若一个字符串包含实际的文本数据，每个**元素**都被认为是一个单独的 UTF-16 **代码单元**。无论这是不是 **String** 实际的存储格式，**String** 中的字符都被当作表示为 UTF-16 来计数。除非特别声明，作用在字符串上的所有操作都视它们为无差别的 16 位无符号整数；这些操作不保证结果字符串仍为正规形式，也不保证语言敏感结果。

Number 类型
-----------

精确地描述，数值类型拥有 **18437736874454810627**（即，**2<sup>64</sup>-2<sup>53</sup>+3**）个值，表示为 IEEE-754 格式 64 位双精度数值（IEEE 二进制浮点数算术中描述了它），除了 IEEE 标准中的 **9007199254740990**（即，**2<sup>53</sup>-2**）个明显的“**非数字**”值；在 ECMAScript 中，它们被表示为一个单独的特殊值：**NaN**。（请注意，**NaN** 值由程序表达式 **NaN** 产生，并假设执行程序不能调整定义的全局变量 **NaN**。） 在某些实现中，外部代码也许有能力探测出众多**非数字**值之间的不同，但此类行为依赖于具体实现；对于 ECMAScript 代码而言，**NaN** 值相互之间无法区别。

还有另外两个特殊值，称为正无穷和负无穷。为简洁起见，在说明目的时，用符号 **+∞** 和 **-∞** 分别代表它们。（请注意，两个无限数值由程序表达式 **+Infinity**（简作 **Infinity**） 和 **-Infinity** 产生，并假设执行程序不能调整定义的全局变量 **Infinity**。）

另外 **18437736874454810624**（即，**2<sup>64</sup>-2<sup>53</sup>**） 个值被称为有限数值。其中的一半是正数，另一半是负数，对于每个正数而言，都有一个与之对应的、相同规模的负数。

请注意，还有一个正零和一个负零。为简洁起见，类似地，在说明目的时，分别用用符号 **+0** 和 **-0** 代表这些值。（请注意，这两个数字零由程序表达式 **+0**（简作 **0**） 和 **-0** 产生。）

这 **18437736874454810622**（即，**2<sup>64</sup>-2<sup>53</sup>-2**） 个有限非零值分为两种：

其中 **18428729675200069632**（即，**2<sup>64</sup>-2<sup>54</sup>**） 个是常规值，形如

`   `<var>`s`</var>`×`<var>`m`</var>`×2`<sup><var>`e`</var></sup>

这里的 <var>s</var> 是 **+1** 或 **-1**，<var>m</var> 是一个小于 **2<sup>53</sup>** 但不小于 **2<sup>52</sup>** 的正整数，<var>s</var> 是一个闭区间 **-1074** 到 **971** 中的整数。

剩下的 **9007199254740990**（即，**2<sup>53</sup>-2**）个值是非常规的，形如

`   `<var>`s`</var>`×`<var>`m`</var>`×2`<sup><var>`e`</var></sup>

这里的 <var>m</var> 是 **+1** 或 **-1**，<var>m</var> 是一个小于 **2<sup>52</sup>** 的 正整数，<var>e</var> 为 **-1074**

请注意，所有规模不超过 **2<sup>53</sup>** 的正整数和负整数都可被数值类型表示（不过，整数 **0** 有两个呈现形式，**+0** 和 **0**）。

如果一个有限的数值非零且用来表达它（上文两种形式之一）的整数 <var>m</var> 是奇数，则该数值有 <b title="odd significand">奇数标记</b>。否则，它有 <b title="even significand">偶数标记</b>。

在本规范中，当 <var>x</var> 表示一个精确的非零实数数学量（甚至可以是无理数，比如 **π**）时，短语 "**<var>x</var> 的 Number 值**" 意为，以下面的方式选择一个 **Number** 值。考虑数值类型的所有有限值的集合（不包括 **-0** 和两个被加入在数值类型中但不可呈现的值，即 **2<sup>1024</sup>**（即 **+1×2<sup>53</sup>×2<sup>971</sup>**）和 **-2<sup>1024</sup>** （即 **-1×2<sup>53</sup>×2<sup>971</sup>**）。选择此集合 中值最接近 <var>x</var> 的一员，若集合中的两值近似相等，那么选择有偶数标记的那个；为此，**2<sup>1024</sup>** 和 **-2<sup>1024</sup>** 这两个超额值被认为有偶数标记。最终，若选择 **2<sup>1024</sup>** ，用 **+∞** 替换它；若选择 **-2<sup>1024</sup>** ，用 **-∞** 替换它；若选择 **+0**，有且只有 <var>x</var> 小于零时，用 **-0** 替换它；其它任何被选取的值都不用改变。结果就是 **<var>x</var> 的 Number 值**。（此过程正是 IEEE-754 的四舍五入模式对应的行为。）

某些 ECMAScript 运算符仅涉及闭区间 **-2<sup>31</sup>** 到 **2<sup>31</sup>-1** 的整数，或闭区间 **0** 到 **2<sup>32</sup>-1**。这些运算符接受任何数值类型的值，不过，数值首先被转换为 **2<sup>32</sup>** 个整数值中的一个。参见 [ToInt32](ES5/conversion#to-int32 "wikilink") 和 [ToUint32](ES5/conversion#to-uint32 "wikilink") 的描述，分别在[章节 9.5](ES5/conversion#to-int32 "wikilink") 和 [9.6](ES5/conversion#to-uint32 "wikilink") 中。

Object 类型
-----------

**Object** 是一个属性的集合。每个属性既可以是一个**命名数据属性**，也可以是一个**命名访问器属性**，或是一个**内部属性**：

-   <b title="Named Data Property">命名数据属性</b> 由一个名字与一个 [ECMAScript语言类型](#language-type "wikilink") 值和一个 **Boolean** 属性集合组成。

-   <b title="Named Accessor Property">命名访问器属性</b> 由一个名字与一个或两个访问器函数，和一个 **Boolean** 属性集合组成。访问器函数用于存取一个与该属性相关联的 [ECMAScript语言类型](#language-type "wikilink") 值。

-   <b title="Internal Property">内部属性</b> 没有名字，且不能直接通过 ECMAScript 语言操作。内部属性的存在纯粹为了规范的目的。

有两种带名字的访问器属性（非内部属性）：**get** 和 **put**，分别对应取值和赋值。

### 属性的特性

本规范中的<b title="Attributes">特性</b>用于定义和解释命名<b title="Property">属性</b>的状态。**命名的数据属性**由一个名字关联到一个下表中列出的<b title="Attributes">特性</b>。

|特性名称|取值范围|描述|
|--------|--------|----|
|**[[Value]]**|任何 [ECMAScript语言类型](#language-type "wikilink")|通过读<b title="Property">属性</b>来取到该值|
|**[[Writable]]**|**Boolean**|如果为 **false**，试图通过 ECMAScript 代码 [[[Put]]](#Put "wikilink") 去改变该属性的 **[[Value]]**，将会失败|
|**[[Enumerable]]**|**Boolean**|如果为 **true**，则该属性可被 [for-in](ES5/statements#x12.6.4 "wikilink") 枚举出来，否则，该属性不可枚举。|
|**[[Configurable]]**|**Boolean**|如果为 **false**，试图删除该属性或改变该属性为访问器属性，或改变它的<b title="Attributes">特性</b>（除了 **[[Value]]**），都会失败。|

**命名访问器属性**由一个名字关联到一个下表中列出的<b title="Attributes">特性</b>。

|特性名称|取值范围|描述|
|--------|--------|----|
|**[[Get]]**|**Object** 或 **Undefined**|如果该值为一个 **Object** 对象，那么它必须是一个函数对象。每次有对属性进行 **get** 访问时，该函数的内部方法 [[[Call]]](#Call "wikilink") 会伴随着一个空参数列表被调用，并返回该属性值。|
|**[[Set]]**|**Object** 或 **Undefined**|如果该值为一个 **Object** 对象，那么它必须是一个函数对象。每次有对属性进行 **set** 访问时，该函数的内部方法 [[[Call]]](#Call "wikilink") 会伴随着一个参数列表被调用，这个参数列表包含了指定值作为唯一的参数。<b title="Property">属性</b>的内部方法 **[[Set]]** 可能会对随后的 <b title="Property">属性</b> 内部方法 **[[Get]]** 的调用返回结果产生影响。|
|**[[Enumerable]]**|**Boolean**|如果为 **true**，则该属性可被 [for-in](ES5/statements#x12.6.4 "wikilink") 枚举出来，否则，该属性不可枚举。|
|**[[Configurable]]**|**Boolean**|如果为 **false**，试图删除该属性，改变该属性为数据属性，或改变它的<b title="Attributes">特性</b>，都会失败。|

如果在此规范中没有对某个命名属性的<b title="Attributes">特性</b>做出明确指定，那么它的默认值将使用下表的定义。

|名称|默认值|
|----|------|
|**[[Value]]**|**undefined**|
|**[[Get]]**|**undefined**|
|**[[Set]]**|**undefined**|
|**[[Writable]]**|**false**|
|**[[Enumerable]]**|**false**|
|**[[Configurable]]**|**false**|

### Object的内部属性及方法

本规范使用各种内部属性来定义对象值的语义。这些内部属性不是 ECMAScript 语言的一部分。本规范中纯粹是以说明为目的定义它们。ECMAScript 实现需要保持和这里描述的内部属性产生和操作的结果一致。内部属性的名字用闭合双方括号“**[[ ]]**”括起来。如果一个算法使用一个对象的一个内部属性，而此对象并没有实现需要的内部属性，那么就抛出 **TypeError** 异常。

**表8** 总结了本规范中适用于所有 ECMAScript 对象的内部属性。**表9** 总结了本规范中适用于某些 ECMAScript 对象的内部属性。这些表中的描述如果没有特别指出是特定的原生 ECMAScript 对象，那么就说明了其在原生 ECMAScript 对象中的行为。宿主对象的内部属性可以支持任何依赖于实现的行为，只要其与本文档说的宿主对象的个别限制一致。

下面表的 “**值的类域**” 一列定义了内部属性关联值的类型。类型名称参考[第 8 章定义的类型](#types "wikilink")，作为增强添加了一下名称：<b id="any">“任意”</b> 指值可以是任何 [ECMAScript语言类型](#language-type "wikilink")；<b id="primitive">“**原始类型**”</b> 指 **Undefined**、**Null**、**Boolean**、**String**、**Number**；<b id="SpecOp">“**SpecOp**”</b> 指内部属性是一个内部方法，一个抽象操作规范定义一个实现提供它的步骤。“**SpecOp**” 后面跟着描述性参数名的列表。如果参数名和类型名一致那么这个名字用于描述参数的类型。如果 “**SpecOp**” 有返回值，那么这个参数列表后跟着 “→” 符号和返回值的类型。

|内部属性|值的类型范围|说明|
|--------|------------|----|
|[[[Prototype]]](#Prototype-desc "wikilink")|**Object** 或 **Null**|此对象的原型|
|[[[Class]]](#Class-desc "wikilink")|**String**|说明规范定义的对象分类的一个字符串值|
|[[[Extensible]]](#Extensible-desc "wikilink")|**Boolean**|如果是 **true**，可以向对象添加自身属性。|
|[[[Get]]](#Get-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>) → [任意](#any "wikilink")|返回命名属性的值|
|nowrap | [[[GetOwnProperty]]](#GetOwnProperty-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>) → **Undefined** 或 [属性描述](#property-descriptor "wikilink")|返回此对象的自身命名属性的[属性描述](#property-descriptor "wikilink")，如果不存在返回 **undefined**|
|[[[GetProperty]]](#GetProperty-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>) → **Undefined** 或 [属性描述](#property-descriptor "wikilink")|返回此对象的完全填入的自身命名属性的[属性描述](#property-descriptor "wikilink")，如果不存在返回 **undefined**|
|[[[Put]]](#Put-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>, [任意](#any "wikilink"), **Boolean**)|将指定命名属性设为第二个参数的值。flag 控制失败处理。|
|[[[CanPut]]](#CanPut-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>) → **Boolean**|返回一个 **Boolean** 值，说明是否可以在 <var>属性名</var> 上执行 [[[Put]]](#Put "wikilink") 操作。|
|[[[HasProperty]]](#HasProperty-impl "wikilink")|[SpecOp](#SpecOp "wikilink") (<var>属性名</var>) → **Boolean**|返回一个 **Boolean** 值，说明对象是否含有给定名称的属性。|
|[[[Delete]]](#Delete-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>, **Boolean**) → **Boolean**|从对象上删除指定的自身命名属性。flag 控制失败处理。|
|[[[DefaultValue]]](#DefaultValue-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>暗示</var>) → [原始类型](#primitive "wikilink")|<var>暗示</var> 是一个字符串 {{question|这里想表达“暗示”认这个参数的默值为String还是它自身的类型是String？从其它部分来看，这个“暗示”本身并不是String类型的，而是一个类型的标识符。所以我觉得理解为前者比较合理。其它意见？}}。返回对象的默认值|
|[[[DefineOwnProperty]]](#DefineOwnProperty-impl "wikilink")|[SpecOp](#SpecOp "wikilink")(<var>属性名</var>, <var>属性描述</var>, **Boolean**) → **Boolean**|创建或修改自身命名属性为拥有[属性描述里描述的状态](#property-descriptor "wikilink")。flag 控制失败处理。|

所有对象（包括宿主对象）必须实现 **表8** 中列出的所有内部属性。然而，对某些对象的 [[[DefaultValue]]](#DefaultValue "wikilink") 内部方法，可以简单的抛出 **TypeError** 异常。

所有对象都有一个叫做 [[[Prototype]]](#Prototype "wikilink") 的内部属性。此对象的值是 **null** 或一个对象，并且它用于实现继承。一个原生属性是否可以把宿主对象作为它的 [[[Prototype]]](#Prototype "wikilink") 取决于实现。所有 [[[Prototype]]](#Prototype "wikilink") 链必须是有限长度（即，从任何对象开始，递归访问 [[[Prototype]]](#Prototype "wikilink") 内部属性必须最终到头，并且值是 **null**）。从 [[[Prototype]]](#Prototype "wikilink") 对象继承来的**命名数据属性**（作为子对象的属性可见）可以通过 **get** 获取，但无法用于 通过 **put** 写入。命名访问器属性会把 **get** 和 **put** 请求都继承。

所有 ECMAScript对象 都有一个 **Boolean** 类型的 [[[Extensible]]](#Extensible "wikilink") 内部属性，它决定了 是否可以给对象添加命名属性。如果 [[[Extensible]]](#Extensible "wikilink") 内部属性的值是 **false** 就不得给对象添加命名属性。此外，如果 [[[Extensible]]](#Extensible "wikilink") 是 **false** 那么不得更改对象的 [[[Class]]](#Class "wikilink") 和 [[[Prototype]]](#Prototype "wikilink") 内部属性的值。一旦 [[[Extensible]]](#Extensible "wikilink") 内部属性的值设为 **false** 之后无法再更改为 **true**。

本规范的每种内置对象都定义了 [[[Class]]](#Class "wikilink") 内部属性的值。宿主对象的 [[[Class]]](#Class "wikilink") 内部属性的值可以是除了 **"Arguments"**、**"Array"**、**"Boolean"**、**"Date"**、**"Error"**、**"Function"**、**"JSON"**、**"Math"**、**"Number"**、**"Object"**、**"RegExp"**、**"String"** 的任何字符串。[[[Class]]](#Class "wikilink") 内部属性的值用于内部区分对象的种类。注，本规范中除了通过 [Object.prototype.toString](ES5/builtins#x14.2.4.2 "wikilink") 没有提供任何手段使程序访问此值。

除非特别指出，原生 ECMAScrpit 对象的公共内部方法的行为描述在 [8.12](#object-internal-methods "wikilink")。**Array** 对象的 [[[DefineOwnProperty]]](ES5/builtins#x15.4.5.1 "wikilink") 内部方法有稍不同的实现，又有 **String** 对象的 [[[GetOwnProperty]]](ES5/builtins#x15.5.5.2 "wikilink") 内部方法有稍不同的实现。[Arguments](ES5/execution#x10.6 "wikilink") 对象的 [[[Get]]](ES5/execution#arguments-Get "wikilink")，[[[GetOwnProperty]]](ES5/execution#arguments-GetOwnProperty "wikilink")，[[[DefineOwnProperty]]](ES5/execution#arguments-DefineOwnProperty "wikilink")，[[[Delete]]](ES5/execution#arguments-Delete "wikilink") 有不同的实现。**Function** 对象的 [[[Get]]](ES5/builtins#x15.3.5.4 "wikilink") 有不同的实现。

除非特别指出，宿主对象可以以任何方式实现这些内部方法，一种可能是一个特别的宿主对象的 [[[Get]]](#Get "wikilink") 和 [[[Put]]](#Put "wikilink") 确实可以存取属性值，但 [[[HasProperty]]](#HasProperty "wikilink") 总是产生 **false**。然而，如果任何对宿主对象内部属性的操作不被实现支持，那么当试图操作时必须抛出 **TypeError** 异常。

宿主对象的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法必须符合宿主对象每个属性的以下不变量 ：

-   如果属性被作为数据属性来描述，并随着时间的推移，它可能返回不同的值，那么即使没有暴露提供更改值机制的其他内部方法，[[[Writable]]](#Writable "wikilink") 和 [[[Configurable]]](#Configurable "wikilink") 之一或全部必须是 **true**。
-   如果属性被作为数据属性来描述，并且其 [[[Writable]]](#Writable "wikilink") 和 [[[Configurable]]](#Configurable "wikilink") 都是 **false**。那么所有对 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 的调用，必须返回作为属性 [[[Value]]](#table5-Value "wikilink") 特性的 [SameValue](ES5/conversion#SameValue "wikilink")。
-   如果 [[[Writable]]](#Writable "wikilink") 特性可以从 **false** 更改为 **true**，那么 [[[Configurable]]](#Configurable "wikilink") 特性必须是 **true**。
-   当 ECMAScript 代码监测到宿主对象的 [[[Extensible]]](#Extensible "wikilink") 内部属性值是 **false**。那么如果调用 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 描述一个属性是不存在，那么接下来所有调用这个属性必须也描述为不存在。

如果 ECMAScript 代码监测到宿主对象的 [[[Extensible]]](#Extensible "wikilink") 内部属性是 **false**，那么这个宿主对象的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法不允许向宿主对象添加新属性。

如果 ECMAScript 代码监测到宿主对象的 [[[Extensible]]](#Extensible "wikilink") 内部属性是 **false**，那么它以后必须不能再改为 **true**。

|内部属性|值的类型范围|说明|
|--------|------------|----|
|**[[PrimitiveValue]]**|[原始类型](#primitive "wikilink")|与此对象的内部状态信息关联。对于标准内置对象只能用 **Boolean**、**Date**、**Number**、**String** 对象实现 **[[PrimitiveValue]]**。|
|[[[Construct]]](ES5/functions#x13.2.2 "wikilink")|[SpecOp](#SpecOp "wikilink") ([任意类型的](#any "wikilink")[列表](#List "wikilink")) → **Object**|通过 **new** 运算符调，创建对象。[SpecOp](#SpecOp "wikilink") 的参数是通过 **new** 运算符传的参数。实现了这个内部方法的对象叫做<b>构造器</b>。|
|[[[Call]]](ES5/functions#x13.2.1 "wikilink")|[SpecOp](#SpecOp "wikilink") ([任意](#any "wikilink"), [任意类型的](#any "wikilink")[列表](#List "wikilink")) → [任意](#any "wikilink") 或 [引用](#Reference "wikilink")|运行与此对象关联的代码。通过函数调用表达式调用。[SpecOp](#SpecOp "wikilink") 的参数是一个 **this** 对象和函数调用表达式传来的参数组成的列表。实现了这个内部方法的对象是<b>可调用</b>的。只有作为宿主对象的可调用对象才可能返回[引用值](#Reference "wikilink")。|
|[[[HasInstance]]](ES5/builtins#x15.3.5.3 "wikilink")|[SpecOp](#SpecOp "wikilink") ([任意](#any "wikilink")) → **Boolean**|返回一个表示参数对象是否可能是由本对象构建的布尔值。在标准内置 ECMAScript 对象中只有 **Function** 对象实现 **[[HasInstance]]**。|
|**[[Scope]]**|[词法环境](ES5/execution#lexical-environment "wikilink")|一个定义了函数对象执行的环境的[词法环境](ES5/execution#lexical-environment "wikilink")。在标准内置 ECMAScript 对象中只有 **Function** 对象实现 **[[Scope]]**。|
|**[[FormalParameters]]**|**Strings** 的[列表](#List "wikilink")|一个包含 **Function** 的 *[FormalParameterList](ES5/functions#FormalParameterList "wikilink")* 的标识符字符串的可能是空的[列表](#List "wikilink")。在标准内置 ECMAScript 对象中只有 **Function** 对象实现 **[[FormalParameterList]]** {{question|原作中这里是[[FormalParameters]]的笔误吗？}}。|
|**[[Code]]**|ECMAScript 代码|函数的 ECMAScript 代码。在标准内置 ECMAScript 对象中只有 **Function** 对象实现 **[[Code]]**。|
|**[[TargetFunction]]**|**Object**|使用标准内置的 [Function.prototype.bind](ES5/builtins#x15.3.4.5 "wikilink") 方法创建的函数对象的目标函数。只有使用 [Function.prototype.bind](ES5/builtins#x14.3.4.5 "wikilink") 创建的 ECMAScript 对象才有 **[[TargetFunction]]** 内部属性。|
|**[[BoundThis]]**|[任意](#any "wikilink")|使用标准内置的 [Function.prototype.bind](ES5/builtins#x14.3.4.5 "wikilink") 方法创建的函数对象的预绑定的 **this** 值。只有使用 [Function.prototype.bind](ES5/builtins#x14.3.4.5 "wikilink") 创建的 ECMAScript 对象才有 **[[BoundThis]]** 内部属性。|
|nowrap | **[[BoundArguments]]** {{extra note|其它章节中出现的[[BoundArgs]]也指这个。}}|[任意类型的](#any "wikilink")[列表](#List "wikilink")|使用标准内置的 [Function.prototype.bind](ES5/builtins#x14.3.4.5 "wikilink") 方法创建的函数对象的预绑定的参数值。只有使用 [Function.prototype.bind](ES5/builtins#x14.3.4.5 "wikilink") 创建的 ECMAScript 对象才有 **[[BoundArguments]]** 内部属性。|
|**[[Match]]**|[SpecOp](#SpecOp "wikilink") (**String**, <var>index</var >) → [MatchResult](ES5/builtins#MatchResult "wikilink")|测试正则匹配并返回一个 [MatchResult](ES5/builtins#MatchResult "wikilink") 值。在标准内置 ECMAScript 对象中只有 **RegExp** 对象实现 **[[Match]]**。|
|**[[ParameterMap]]**|**Object**|提供[参数对象的属性和函数关联的形式参数之间的映射](ES5/execution#CreateArgumentsObject "wikilink")。只有参数对象才有 **[[ParameterMap]]** 内部属性。|

引用规范类型
------------

引用类型用来说明 **delete**、**typeof**、赋值运算符这些运算符的行为。例如，在赋值运算中左边的操作数期望产生一个引用。通过赋值运算符左侧运算子的语法案例分析可以但不能完全解释赋值行为，还有个难点：函数调用允许返回引用。承认这种可能性纯粹是为了宿主对象。本规范没有定义返回引用的内置 ECMAScript 函数，并且也不提供返回引用的用户定义函数。（另一个不使用语法案列分析的原因是，那样将会影响规范的很多地方，冗长并且别扭。）

一个<b title="Reference">引用</b>是个已解析的命名绑定。它由三部分组成：<b title="Base">基</b>值、<b title="Referenced Name">引用名称</b>和一个<b title="Strict Reference">严格引用</b>标志（布尔值）。 <b title="Base">基</b>值是 **undefined**、**Object**、**Boolean**、**String**、**Number**、[环境记录项中的任意一个](ES5/execution#environment-record "wikilink")。<b title="Base">基</b>值是 **undefined** 表示此引用不可以解析为一个绑定。<b title="Referenced Name">引用名称</b>是一个字符串。

本规范中使用以下抽象操作接近引用的部分：

-   <b id="GetBase">GetBase(<var>V</var>)</b>：返回<b title="Reference">引用</b>值 <var>V</var> 的<b title="Base">基</b>值部分。
-   <b id="GetReferencedName ">GetReferencedName(<var>V</var>)</b>：返回<b title="Reference">引用</b>值 <var>V</var> 的<b title="Referenced Name">引用名称</b>部分。
-   <b id="IsStrictReference">IsStrictReference(<var>V</var>)</b>：返回<b title="Reference">引用</b>值 <var>V</var> 的<b title="Strict Reference">严格引用</b>部分。
-   <b id="HasPrimitiveBase">HasPrimitiveBase(<var>V</var>)</b>：如果<b title="Base">基</b>值是 **Boolean**、**String**、**Number**，那么返回 **true**。
-   <b id="IsPropertyReference">IsPropertyReference(<var>V</var>)</b>：如果<b title="Base">基</b>值是个 **Object** 或 **HasPrimitiveBase**(<var>V</var>) 是 **true**，那么返回 **true**；否则返回 **false**。
-   <b id="IsUnresolvableReference">IsUnresolvableReference(<var>V</var>)</b>：如果<b title="Base">基</b>值是 **undefined** 那么返回 **true**，否则返回 **false**。

本规范使用以下抽象操作来操作引用：

### GetValue(V)

1.  如果 (<var>V</var>) 不是[引用](#Reference "wikilink")，返回 <var>V</var>。
2.  令 <var>base</var> 为调用 (<var>V</var>) 的返回值。
3.  如果 (<var>V</var>)，抛出一个 **ReferenceError** 异常。
4.  如果 (<var>V</var>)，那么
    1.  如果 (<var>V</var>) 是 **false**，那么令 <var>get</var> 为 <var>base</var> 的 [[[Get]]](#Get "wikilink") 内部方法 , 否则令 <var>get</var> 为下面定义的特殊的 **[[Get]]** 内部方法。
    2.  将 <var>base</var> 作为 **this** 值，传递 (<var>V</var>) 为参数，调用 <var>get</var> 内部方法，返回结果。

5.  否则，<var>base</var> 必须是一个[环境记录项](ES5/execution#environment-record "wikilink")。
6.  传递 (<var>V</var>) 和 (<var>V</var>) 为参数调用 <var>base</var> 的 [GetBindingValue](ES5/execution#GetBindingValue "wikilink") 具体方法，返回结果。

**GetValue** 中的 <var>V</var> 是原始基值的[属性引用时使用下面的](#IsPropertyReference "wikilink") **[[Get]]** 内部方法。它用 <var>base</var> 作为他的 **this** 值，其中属性 <var>P</var> 是它的参数。采用以下步骤：

1.  令 <var>O</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>base</var>)。
2.  令 <var>desc</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的返回值。
3.  如果 <var>desc</var> 是 **undefined**，返回 **undefined**。
4.  如果 (<var>desc</var>) 是 **true**，返回 <var>desc</var>。[[[Value]]](#Value "wikilink")。
5.  否则 (<var>desc</var>) 必须是 **true**，令 <var>getter</var> 为 <var>desc</var>。[[[Get]]](#descriptor-Get "wikilink")。
6.  如果 <var>getter</var> 是 **undefined**，返回 **undefined**。
7.  提供 <var>base</var> 作为 **this** 值，无参数形式调用 <var>getter</var> 的 [[[Call]]](#Call "wikilink") 内部方法，返回结果。

### PutValue(V, W)

1.  如果 (<var>V</var>) 不是引用，抛出一个 **ReferenceError** 异常。
2.  令 <var>base</var> 为调用 (<var>V</var>) 的结果。
3.  如果 (<var>V</var>)，那么
    1.  如果 (<var>V</var>) 是 **true**，那么
        1.  抛出 **ReferenceError** 异常。

    2.  用 (<var>V</var>)、<var>W</var>、**false** 作为参数调用[全局对象的](ES5/builtins#the-global-object "wikilink") [[[Put]]](#Put "wikilink") 内部方法。

4.  否则如果 (<var>V</var>)，那么
    1.  如果 (<var>V</var>) 是 **false**，那么令 <var>put</var> 为 <var>base</var> 的 [[[Put]]](#Put "wikilink") 内部方法，否则令 <var>put</var> 为下面定义的特殊的 **[[Put]]** 内部方法。
    2.  用 <var>base</var> 作为 **this** 值，用 (<var>V</var>)、<var>W</var>、(<var>V</var>) 作为参数调用 <var>put</var> 内部方法。

5.  否则 <var>base</var> 必定是[环境数据作为](ES5/execution#environment-record "wikilink") <var>base</var> 的引用。所以，
    1.  用 (<var>V</var>)、<var>W</var>、(<var>V</var>) 作为参数调用 <var>base</var> 的 [SetMutableBinding](ES5/execution#SetMutableBinding "wikilink") 具体方法。

6.  返回。

**PutValue** 中的 <var>V</var> 是原始基值的[属性引用时使用下面的](#property-reference "wikilink") **[[Put]]** 内部方法。用 <var>base</var> 作为 **this** 值，用属性 <var>P</var>，值 <var>W</var>，布尔标志 <var>Throw</var> 作为参数调用它。采用以下步骤：

1.  令 <var>O</var> 为 [ToObject](ES5/conversion#to-object "wikilink")(<var>base</var>)。
2.  如果用 <var>P</var> 作为参数调用 <var>O</var> 的 [[[CanPut]]](#CanPut "wikilink") 内部方法的结果是 **false**，那么
    1.  如果 <var>Throw</var> 是 **true**，那么抛出一个 **TypeError** 异常。
    2.  否则返回。

3.  令 <var>ownDesc</var> 为用 <var>P</var> 作为参数调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法的结果。
4.  如果 (<var>ownDesc</var>) 是 **true**，那么
    1.  如果 <var>Throw</var> 是 **true**，那么抛出一个 **TypeError** 异常。
    2.  否则返回。

5.  令 <var>desc</var> 为用 <var>P</var> 作为参数调用 <var>O</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的结果。这可能是一个自身或继承的[访问器属性描述或是一个继承的](#accessor-property-descriptor "wikilink")[数据属性描述](#data-property-descriptor "wikilink")。
6.  如果 (<var>desc</var>) 是 **true**，那么
    1.  令 <var>setter</var> 为 <var>desc</var>。[[[Set]]](#descriptor-Set "wikilink")，他不会是 **undefined**。
    2.  用 <var>base</var> 作为 **this** 值，用只由 <var>W</var> 组成的列表作为参数调用 <var>setter</var> 的 [[[Call]]](#Call "wikilink") 内部方法。

7.  否则，这是要在临时对象 <var>O</var> 上创建自身属性的请求。
    1.  如果 <var>Throw</var> 是 **true**，抛出一个 **TypeErroe** 异常。

8.  返回。

列表规范类型
------------

列表类型用于说明 **new** 表达式、函数调用，和其他需要值的简单列表的算法中的参数列表的计算。列表类型的值是简单排序的一些值的序列，此序列可以是任意长度。

完结规范类型
------------

**完结类型**用于说明执行将控制转移到外部的声明（**break**、**continue**、**return**、**throw**）的行为。**完结类型**的值是由三部分组成，形如 (<var>type</var>,<var>value</var>,<var>target</var>)，其中 <var>type</var> 是 **normal**、**break**、**continue**、**return**、**throw** 之一，<var>value</var> 是任何 [ECMASCript语言值](#language-type "wikilink") 或 **empty**，<var>target</var> 是任何 ECMAScript 的 [Identifier](ES5/lexical#Identifier "wikilink") 或 **empty**。如果 <var>cv</var> 是一个**完结类型**的值，那么 <var>cv.type</var>、<var>cv.value</var>、<var>cv.target</var> 可以被用来明确地表示其成员值。

术语 “<b id="abrupt completion">非常规完结</b>” 是指任何 <var>type</var> 不是 **normal** 的完结。

属性描述符及属性标识符规范类型
------------------------------

<b title="Property Descriptor">属性描述符</b>类型是用来解释命名属性具体操作的特性集。属性描述符类型的值是记录项，由命名字段组成，每个字段的名称是一个特性名并且它的值是一个相应的特性值，这些特性指定在 [8.6.1](#property-attributes "wikilink")。此外，任何字段都可能存在或不存在。

根据是否存在或使用了某些字段，属性描述符的值可进一步划分为<b id="data-property-descriptor">数据属性描述符</b>和<b id="accessor-property-descriptor">访问器属性描述符</b>。一个数据属性描述符里包括叫做 [[[Value]]](#table5-Value "wikilink") 或 [[[Writable]]](#table5-Writable "wikilink") 的字段。一个访问器属性描述符里包括叫做 [[[Get]]](#table6-Get "wikilink") 或 [[[Set]]](#table6-Set "wikilink") 的字段。任何属性描述都可能有名为 <b id="Enumerable">[[Enumerable]]</b> 和 <b id="Configurable">[[Configurable]]</b> 的字段。一个属性描述符不能同时是数据属性描述符和访问器属性描述符；但是，它可能二者都不是。一个通用属性描述符是，既不是数据属性描述符也不是访问器属性描述符的属性描述符值。一个<b id="fully-populated">完全填充</b>属性描述符是访问器属性描述符或数据属性描述符，并且拥有 [表5](#table5 "wikilink") 或 [表6](#tabl6 "wikilink") 里定义的所有属性特性对应的字段。

本规范中为了便于标记，使用一种类似对象字面量的语法来定义属性描述符。例如，属性描述符 {[[Value]]: **42**, [[Writable]]: **false**, [[Configurable]]: **true**}，就定义了一个**数据属性描述符**。字段名称的顺序并不重要。任何没有明确列出的字段被认为是不存在的。

在规范中的文本和算法里，可用点符号来指明一个属性描述符的特定字段。例如，如果 <var>D</var> 是一个属性描述符，那么 <var>D</var>.[[Value]] 是“<var>D</var> 的 [[Value]] 字段”的简写。

<b title="Property Identifier">属性标识符</b>类型用于关联属性名称与属性描述符。<b title="Property Identifier">属性标识符</b>类型的值是 (<var>name</var>, <var>descriptor</var>) 形式的一对值，其中 <var>name</var> 是一个字符串和 <var>descriptor</var> 是一个属性描述符值。

在本规范中使用以下的抽象操作来操作属性描述符值：

### IsAccessorDescriptor(Desc)

当用[属性描述符](#property-descriptor "wikilink") <var>Desc</var> 调用抽象操作 **IsAccessorDescriptor**，采用以下步骤：

1.  如果 <var>Desc</var> 是 **undefined**，那么返回 **false**。
2.  如果<var>Desc</var>.[[[Get]]](#descriptor-Get "wikilink") 和 <var>Desc</var>.[[[Set]]](#descriptor-Set "wikilink") 都不存在，则返回 **false**。
3.  返回 **true**。

### IsDataDescriptor(Desc)

当用[属性描述符](#property-descriptor "wikilink") <var>Desc</var> 调用抽象操作 **IsDataDescriptor**，采用以下步骤：

1.  如果 <var>Desc</var> 是 **undefined**，那么返回 **false**。
2.  如果 <var>Desc</var>.[[[Value]]](#table5-Value "wikilink") 和 <var>Desc</var>.[[[Writable]]](#table5-Writable "wikilink") 都不存在，则返回 **false**。
3.  返回 **true**。

### IsGenericDescriptor(Desc)

当用[属性描述符](#property-descriptor "wikilink") <var>Desc</var> 调用抽象操作 **IsGenericDescriptor**，采用以下步骤：

1.  如果 <var>Desc</var> 是 **undefined**，那么返回 **false**。
2.  如果 (<var>Desc</var>) 和 (<var>Desc</var>) 都是 **false**，则返回 **true**。
3.  返回 **false**。

### FromPropertyDescriptor(Desc)

当用[属性描述符](#property-descriptor "wikilink") <var>Desc</var> 调用抽象操作 **FromPropertyDescriptor**，采用以下步骤：

假定以下算法的 <var>Desc</var> 是 [[[GetOwnProperty]]](#GetOwnProperty-impl "wikilink") 返回的[完全填充的](#fully-populated "wikilink")[属性描述符](#property-descriptor "wikilink")。

1.  如果 <var>Desc</var> 是 **undefined**，那么返回 **undefined**。
2.  令 <var>obj</var> 为仿佛使用 **new Object()** 表达式创建的新对象，这里的 **Object** 是[标准内置构造器名](ES5/builtins#object-objects "wikilink")。
3.  如果 (<var>Desc</var>) 是 **true**，则
    1.  用参数 **"value"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Value]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。
    2.  用参数 **"writable"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Writable]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。

4.  否则，(<var>Desc</var>) 必定是 **true**，所以
    1.  用参数 **"get"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Get]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。
    2.  用参数 **"set"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Set]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。

5.  用参数 **"enumerable"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Enumerable]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。
6.  用参数 **"configurable"**、[属性描述符](#property-descriptor "wikilink") {[[Value]]: <var>Desc</var>.[[Configurable]], [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}、**false** 调用 <var>obj</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。
7.  返回 <var>obj</var>。

### ToPropertyDescriptor(Obj)

当用对象 <var>Obj</var> 调用抽象操作 **ToPropertyDescriptor**，采用以下步骤：

1.  如果 (<var>Obj</var>) 不是 **Object**，抛出一个 **TypeError** 异常。
2.  令 <var>desc</var> 为创建初始不包含字段的新[属性描述的结果](#property-descriptor "wikilink")。
3.  如果用参数 **"enumerable"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>enum</var> 为用参数 **"enumerable"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  设定 <var>desc</var> 的 [[[Enumerable]]](#Enumerable "wikilink") 字段为 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>enum</var>)。

4.  如果参数 **"configurable"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>conf</var> 为用参数 **"configurable"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  设定 <var>desc</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段为 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>conf</var>)。

5.  如果参数 **"value"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>value</var> 为用参数 **"value"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  设定 <var>desc</var> 的 [[[Value]]](#table5-Value "wikilink") 字段为 <var>value</var>。

6.  如果参数 **"writable"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>writable</var> 为用参数 **"writable"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  设定 <var>desc</var> 的 [[[Writable]]](#table5-Writable "wikilink") 字段为 [ToBoolean](ES5/conversion#to-boolean "wikilink")(<var>writable</var>)。

7.  如果参数 **"get"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>getter</var> 为用参数 **"get"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>getter</var>) 是 **false** 并且 <var>getter</var> 不是 **undefined**，则抛出一个 **TypeError** 异常。
    3.  设定 <var>desc</var> 的 [[[Get]]](#table6-Get "wikilink") 字段为 <var>getter</var>。

8.  如果参数 **"set"** 调用 <var>Obj</var> 的 [[[HasProperty]]](#HasProperty "wikilink") 内部方法的结果是 **true**，则
    1.  令 <var>setter</var> 为用参数 **"set"** 调用 <var>Obj</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
    2.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>setter</var>) 是 **false** 并且 <var>setter</var> 不是 **undefined**，则抛出一个 **TypeError** 异常。
    3.  设定 <var>desc</var> 的 [[[Set]]](#table6-Set "wikilink") 字段为 <var>setter</var>。

9.  如果存在 <var>desc</var>.[[[Get]]](#table6-Get "wikilink") 或 <var>desc</var>.[[[Set]]](#table6-Set "wikilink")，则
    1.  如果存在 <var>desc</var>.[[[Value]]](#table5-Value "wikilink") 或 <var>desc</var>.[[[Writable]]](#table5-Writable "wikilink")，则抛出一个 **TypeError** 异常。

10. 返回 <var>desc</var>。

词法环境和环境记录项规范类型
----------------------------

[词法环境和](ES5/execution#lexical-environment "wikilink")[环境记录项类型用于说明在嵌套的函数或块中的名称解析行为](ES5/execution#environment-record "wikilink")。这些类型和他们的操作定义在[第 10 章](ES5/execution "wikilink")。

对象内部方法的算法
------------------

在以下算法说明中假定 <var>O</var> 是一个原生 ECMAScript 对象，<var>P</var> 是一个字符串，<var>Desc</var> 是一个属性说明记录，<var>Throw</var> 是一个布尔标志。

### [[GetOwnProperty]] (P)

当用属性名 <var>P</var> 调用 <var>O</var> 的 <b>[[GetOwnProperty]]</b> 内部方法，采用以下步骤：

1.  如果 <var>O</var> 不包含名为 <var>P</var> 的自身属性，返回 **undefined**。
2.  令 <var>D</var> 为无字段的新建[属性描述](#property-descriptor "wikilink")。
3.  令 <var>X</var> 为 <var>O</var> 的名为 <var>P</var> 的自身属性。
4.  如果 <var>X</var> 是[数据属性](#data-property-descriptor "wikilink")，则
    1.  设定 <var>D</var>.[[[Value]]](#Value "wikilink") 为 <var>X</var> 的 [[[Value]]](#Value "wikilink") 特性。
    2.  设定 <var>D</var>.[[[Writable]]](#Writable "wikilink") 为 <var>X</var> 的 [[[Writable]]](#Writable "wikilink") 特性。

5.  否则 <var>X</var> 是[访问器属性](#accessor-property-descriptor "wikilink")，所以
    1.  设定 <var>D</var>.[[[Get]]](#descriptor-Get "wikilink") 为 <var>X</var> 的 [[[Get]]](#descriptor-Get "wikilink") 特性。
    2.  设定 <var>D</var>.[[[Set]]](#descriptor-Set "wikilink") 为 <var>X</var> 的 [[[Set]]](#descriptor-Set "wikilink") 特性。

6.  设定 <var>D</var>.[[[Enumerable]]](#Enumerable "wikilink") 为 <var>X</var> 的 [[[Enumerable]]](#Enumerable "wikilink") 特性。
7.  设定 <var>D</var>.[[[Configurable]]](#Configurable "wikilink") 为 <var>X</var> 的 [[[Configurable]]](#Configurable "wikilink") 特性。
8.  返回 <var>D</var>。

然而，如果 <var>O</var> 是一个 **String** 对象，它就具有一个更细致的 [[[GetOwnProperty]]](ES5/builtins#x15.5.5.2 "wikilink") 内部方法。

### [[GetProperty]] (P)

当用属性名 <var>P</var> 调用 <var>O</var> 的 <b>[[GetProperty]]</b> 内部方法，采用以下步骤：

1.  令 <var>prop</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法的结果。
2.  如果 <var>prop</var> 不是 **undefined**，返回 <var>prop</var>。
3.  令 <var>proto</var> 为 <var>O</var> 的 [[[Prototype]]](#Prototype "wikilink") 内部属性值。
4.  如果 <var>proto</var> 是 **null**，返回 **undefined**。
5.  用参数 <var>P</var> 调用 <var>proto</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法，返回结果。

### [[Get]] (P)

当用属性名 <var>P</var> 调用 <var>O</var> 的 <b>[[Get]]</b> 内部方法，采用以下步骤：

1.  令 <var>desc</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的结果。
2.  如果 <var>desc</var> 是 **undefined**，返回 **undefined**。
3.  如果 (<var>desc</var>) 是 **true**，返回 <var>desc</var>.[[[Value]]](#Value "wikilink")。
4.  否则，(<var>desc</var>) 必定是真，所以，令 <var>getter</var> 为 <var>desc</var>.[[[Get]]](#descriptor-Get "wikilink")。
5.  如果 <var>getter</var> 是 **undefined**，返回 **undefined**。
6.  用 <var>O</var> 作为 **this**，无参数调用 <var>getter</var> 的 [[[Call]]](#Call "wikilink") 内部方法，返回结果。

### [[CanPut]] (P)

当用属性名 <var>P</var> 调用 <var>O</var> 的 <b>[[CanPut]]</b> 内部方法，采用以下步骤：

1.  令 <var>desc</var> 为用参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法的结果。
2.  如果 <var>desc</var> 不是 **undefined**，则
    1.  如果 (<var>desc</var>) 是 **true**，则
        1.  如果 <var>desc</var>.[[[Set]]](#descriptor-Set "wikilink") 是 **undefined**，则返回 **false**。
        2.  否则返回 **true**。

    2.  否则，<var>desc</var> 必定是[数据属性](#data-property-descriptor "wikilink")，所以返回 <var>desc</var>.[[[Writable]]](#Writable "wikilink") 的值。

3.  令 <var>proto</var> 为 <var>O</var> 的 [[[Prototype]]](#Prototype "wikilink") 内部属性。
4.  如果 <var>proto</var> 是 **null**，则返回 <var>O</var> 的 [[[Extensible]]](#Extensible "wikilink") 内部属性的值。
5.  令 <var>inherited</var> 为用属性名 <var>P</var> 调用 <var>proto</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的结果。
6.  如果 <var>inherited</var> 是 **undefined**，返回 <var>O</var> 的 [[[Extensible]]](#Extensible "wikilink") 内部属性的值。
7.  如果 (<var>inherited</var>) 是 **true**，则
    1.  如果 <var>inherited</var>.[[[Set]]](#descriptor-Set "wikilink") 是 **undefined**，则返回 **false**。
    2.  否则返回 **true**。

8.  否则，<var>inherited</var> 必定是[数据属性](#data-property-descriptor "wikilink")。
    1.  如果 <var>O</var> 的 [[[Extensible]]](#Extensible "wikilink") 内部属性是 **false**，返回 **false**。
    2.  否则返回 <var>inherited</var>.[[[Writable]]](#Writable "wikilink") 的值。

宿主对象可以定义受额外约束的 [[[Put]]](#Put "wikilink") 操作。如果可能，宿主对象不应该在 [[[CanPut]]](#CanPut "wikilink") 返回 **false** 的情况下允许 [[[Put]]](#Put "wikilink") 操作。

### [[Put]] (P, V, Throw)

当用属性名 <var>P</var>，值 *V*，布尔值 <var>Throw</var> 调用 <var>O</var> 的 <b>[[Put]]</b> 内部方法，采用以下步骤：

1.  如果用参数 <var>P</var> 调用 <var>O</var> 的 [[[CanPut]]](#CanPut "wikilink") 内部方法的结果是 **false**，则
    1.  如果 <var>Throw</var> 是 **true**，则抛出一个 **TypeError** 异常。
    2.  否则返回。

2.  令 <var>ownDesc</var> 为用参数 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法的结果。
3.  如果 (<var>ownDesc</var>) 是 **true**，则
    1.  令 <var>valueDesc</var> 为[属性描述](#property-descriptor "wikilink") {[[Value]]: *V*}。
    2.  用参数 <var>P</var>、<var>valueDesc</var>、<var>Throw</var> 调用 <var>O</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。
    3.  返回。

4.  令 <var>desc</var> 为用参数 <var>P</var> 调用 <var>O</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的结果。这可能是自身或继承的访问器属性描述或者是继承的数据属性描述。
5.  如果 (<var>desc</var>) 是 **true**，则
    1.  令 <var>setter</var> 为 <var>desc</var>.[[[Set]]](#descriptor-Set "wikilink")（不会是 **undefined**）。
    2.  用 <var>O</var> 作为 **this**，*V* 作为唯一参数调用 <var>setter</var> 的 [[[Call]]](#Call "wikilink") 内部方法。

6.  否则，按照以下步骤在对象 <var>O</var> 上创建名为 <var>P</var> 的命名数据属性。
    1.  令 <var>newDesc</var> 为[属性描述](#property-descriptor "wikilink") {[[Value]]: *V*, [[Writable]]: **true**, [[Enumerable]]: **true**, [[Configurable]]: **true**}。
    2.  用参数 <var>P</var>、<var>newDesc</var>、<var>Throw</var> 调用 <var>O</var> 的 [[[DefineOwnProperty]]](#DefineOwnProperty "wikilink") 内部方法。

7.  返回。

### [[HasProperty]] (P)

当用属性名 <var>P</var> 调用 <var>O</var> 的 <b>[[HasProperty]]</b> 内部方法，采用以下步骤：

1.  令 <var>desc</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetProperty]]](#GetProperty "wikilink") 内部方法的结果。
2.  如果 <var>desc</var> 是 **undefined**，则返回 **false**。
3.  否则返回 **true**。

### [[Delete]] (P, Throw)

当用属性名 <var>P</var> 和布尔值 <var>Throw</var> 调用 <var>O</var> 的 <b>[[Delete]]</b> 内部方法，采用以下步骤：

1.  令 <var>desc</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部方法的结果。
2.  如果 <var>desc</var> 是 **undefined**，则返回 **true**。
3.  如果 <var>desc</var>.[[[Configurable]]](#Configurable "wikilink") 是 **true**，则
    1.  在 <var>O</var> 上删除名为 <var>P</var> 的自身属性。
    2.  返回 **true**。

4.  否则如果 <var>Throw</var>，则抛出一个 **TypeError** 异常。
5.  返回 **false**。

### [[DefaultValue]] (暗示)

当 <var>暗示</var> **String** 时调用 <var>O</var> 的 **[[DefaultValue]]** 内部方法，采用以下步骤：

1.  令 <var>toString</var> 为用参数 **"toString"** 调用对象 <var>O</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
2.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>toString</var>) 是 **true**，则
    1.  令 <var>str</var> 为用 <var>O</var> 作为 **this** 值，空参数列表调用 <var>toString</var> 的 [[[Call]]](#Call "wikilink") 内部方法的结果。
    2.  如果 <var>str</var> 是[原始值](#primitive "wikilink")，返回 <var>str</var>。

3.  令 <var>valueOf</var> 为用参数 **"valueOf"** 调用对象 <var>O</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
4.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>valueOf</var>) 是 **true**，则
    1.  令 <var>val</var> 为用 <var>O</var> 作为 **this** 值，空参数列表调用 <var>valueOf</var> 的 [[[Call]]](#Call "wikilink") 内部方法的结果。
    2.  如果 <var>val</var> 是[原始值](#primitive "wikilink")，返回 <var>val</var>。

5.  抛出一个 **TypeError** 异常。

当 <var>暗示</var> **Number** 时调用 <var>O</var> 的 **[[DefaultValue]]** 内部方法，采用以下步骤：

1.  令 <var>valueOf</var> 为用参数 **"valueOf"** 调用对象 <var>O</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
2.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>valueOf</var>) 是 **true**，则
    1.  令 <var>val</var> 为用 <var>O</var> 作为 **this** 值，空参数列表调用 <var>valueOf</var> 的 [[[Call]]](#Call "wikilink") 内部方法的结果。
    2.  如果 <var>val</var> 是[原始值](#primitive "wikilink")，返回 <var>val</var>。

3.  令 <var>toString</var> 为用参数 **"toString"** 调用对象 <var>O</var> 的 [[[Get]]](#Get "wikilink") 内部方法的结果。
4.  如果 [IsCallable](ES5/conversion#is-callable "wikilink")(<var>toString</var>) 是 **true**，则
    1.  令 <var>str</var> 为用 <var>O</var> 作为 **this** 值，空参数列表调用 <var>toString</var> 的 [[[Call]]](#Call "wikilink") 内部方法的结果。
    2.  如果 <var>str</var> 是[原始值](#primitive "wikilink")，返回 <var>str</var>。

5.  抛出一个 **TypeError** 异常。

当没有指定 <var>暗示</var> 时调用 <var>O</var> 的 **[[DefaultValue]]** 内部方法，除了 **Date** 对象的行为用 <var>暗示</var> **String** 来处理以外，其它情况的行为都作为 <var>暗示</var> **Number** 来处理。

上面说明的 **[[DefaultValue]]** 在原生对象中只能返回[原始值](#primitive "wikilink")。如果一个宿主对象实现了它自身的 **[[DefaultValue]]** 内部方法，那么必须确保其 **[[DefaultValue]]** 内部方法只能返回[原始值](#primitive "wikilink")。

### [[DefineOwnProperty]] (P, Desc, Throw)

在以下算法中，术语 <b id="reject-DefineOwnProperty">“拒绝”</b> 是指 “如果 <var>Throw</var> 是 **true**，则抛出 **TypeError** 异常，否则返回 **false**”。算法包含测试具体值的[属性描述](#property-descriptor "wikilink") <var>Desc</var> 的各种字段的步骤。这种方式测试的字段事实上不需要真的在 <var>Desc</var> 里。如果一个字段不存在则将其值看作是 **false**。

当用属性名 <var>P</var>，[属性描述](#property-descriptor "wikilink") <var>Desc</var>，布尔值 <var>Throw</var> 调用 <var>O</var> 的 <b>[[DefineOwnProperty]]</b> 内部方法，采用以下步骤：

1.  令 <var>current</var> 为用属性名 <var>P</var> 调用 <var>O</var> 的 [[[GetOwnProperty]]](#GetOwnProperty "wikilink") 内部属性的结果。
2.  令 <var>extensible</var> 为 <var>O</var> 的 [[[Extensible]]](#Extensible "wikilink") 内部属性值。
3.  如果 <var>current</var> 是 **undefined** 并且 <var>extensible</var> 是 **false**，则[拒绝](#reject-DefineOwnProperty "wikilink")。
4.  如果 <var>current</var> 是 **undefined** 并且 <var>extensible</var> 是 **true**，则
    1.  如果 (<var>Desc</var>) 或 (<var>Desc</var>) 是 **true**，则
        1.  在 <var>O</var> 上创建名为 <var>P</var> 的自身数据属性，<var>Desc</var> 描述了它的 [[[Value]]](#Value "wikilink")、[[[Writable]]](#Writable "wikilink")、[[[Enumerable]]](#Enumerable "wikilink")、[[[Configurable]]](#Configurable "wikilink") 特性值。如果 <var>Desc</var> 的某特性字段值不存在，那么设定新建属性的此特性为默认值。

    2.  否则，<var>Desc</var> 必定是[访问器属性描述](#accessor-property-descriptor "wikilink")，所以
        1.  在 <var>O</var> 上创建名为 <var>P</var> 的自身访问器属性，<var>Desc</var> 描述了它的 [[[Get]]](#descriptor-Get "wikilink")、[[[Set]]](#descriptor-Set "wikilink")、[[[Enumerable]]](#Enumerable "wikilink")、[[[Configurable]]](#Configurable "wikilink") 特性值。如果 <var>Desc</var> 的某特性字段值不存在，那么设定新建属性的此特性为默认值。

5.  如果 <var>Desc</var> 不存在任何字段，返回 **true**。
6.  如果 <var>Desc</var> 的任何字段都出现在 <var>current</var> 中，并且用 [SameValue](ES5/conversion#SameValue "wikilink") 算法比较 <var>Desc</var> 中每个字段值和 <var>current</var> 里对应字段值，结果相同，则返回 **true**。
7.  如果 <var>current</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **false**，则
    1.  如果 <var>Desc</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **true**，则[拒绝](#reject-DefineOwnProperty "wikilink")。
    2.  如果 <var>Desc</var> 有 [[[Enumerable]]](#Enumerable "wikilink") 字段，并且 <var>current</var> 和 Desc 的 [[[Enumerable]]](#Enumerable "wikilink") 字段相互布尔否定，则[拒绝](#reject-DefineOwnProperty "wikilink")。

8.  (<var>Desc</var>) 是 **true**，则不需要进一步验证。

9.  否则，如果 (<var>current</var>) 和 (<var>Desc</var>) 的结果不同，则
    1.  如果 <var>current</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **false**，则[拒绝](#reject-DefineOwnProperty "wikilink")。
    2.  如果 (<var>current</var>) 是 **true**，则
        1.  将对象 <var>O</var> 的名为 <var>P</var> 的数据属性转换为访问器属性。保留转换属性的 [[[Configurable]]](#Configurable "wikilink") 和 [[[Enumerable]]](#Enumerable "wikilink") 特性的现有值，并且设定属性的其余特性为其默认值。

    3.  否则
        1.  将对象 <var>O</var> 的名为 <var>P</var> 的访问器属性转换为数据属性。保留转换属性的 [[[Configurable]]](#Configurable "wikilink") 和 [[[Enumerable]]](#Enumerable "wikilink") 特性的现有值，并且设定属性的其余特性为其默认值。

10. 否则，如果 (<var>current</var>) 和 (<var>Desc</var>) 都是 **true**，则
    1.  如果 <var>current</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **false**，则
        1.  如果 <var>current</var> 的 [[[Writable]]](#Writable "wikilink") 字段是 **false** 并且 <var>Desc</var> 的 [[[Writable]]](#Writable "wikilink") 字段是 **true**，则[拒绝](#reject-DefineOwnProperty "wikilink")。
        2.  如果 <var>current</var> 的 [[[Writable]]](#Writable "wikilink") 字段是 **false**，则
            1.  如果 <var>Desc</var> 有 [[[Value]]](#Value "wikilink") 字段，并且 [SameValue](ES5/conversion#SameValue "wikilink")(<var>Desc</var>. [[[Value]]](#Value "wikilink"), <var>current</var>. [[[Value]]](#Value "wikilink")) 是 **false**，则[拒绝](#reject-DefineOwnProperty "wikilink")。

    2.  否则，<var>current</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **true**，所以可接受任何更改。

11. 否则 (<var>current</var>) 和 (<var>Desc</var>) 都是 **true**，所以
    1.  如果 <var>current</var> 的 [[[Configurable]]](#Configurable "wikilink") 字段是 **false**，则
        1.  如果 <var>Desc</var> 有 [[[Set]]](#descriptor-Set "wikilink") 字段，并且 [SameValue](ES5/conversion#SameValue "wikilink")(<var>Desc</var>. [[[Set]]](#descriptor-Set "wikilink"), <var>current</var>. [[[Set]]](#descriptor-Set "wikilink")) 是 **false**，则[拒绝](#reject-DefineOwnProperty "wikilink")。
        2.  如果 <var>Desc</var> 有 [[[Get]]](#descriptor-Get "wikilink") 字段，并且 [SameValue](ES5/conversion#SameValue "wikilink")(<var>Desc</var>. [[[Get]]](#descriptor-Get "wikilink"), <var>current</var>. [[[Get]]](#descriptor-Get "wikilink")) 是 **false**，则[拒绝](#reject-DefineOwnProperty "wikilink")。

12. <var>Desc</var> 拥有所有特性字段，设定对象 <var>O</var> 的名为 <var>P</var> 的属性的对性特性为这些字段值。
13. 返回 **true**。

然而，如果 <var>O</var> 是一个 **Array** 对象，它就具有一个更细致的 [[[DefineOwnProperty]]](ES5/builtins#x15.4.5.1 "wikilink") 内部方法。

