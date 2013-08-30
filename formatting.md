# 格式 #
	代码风格和格式确实比较随意, 但一个项目中所有人遵循同一风格是非常容易的.
	个体未必同意下述每一处格式规则, 但整个项目服从统一的编程风格是很重要的,
	只有这样才能让所有人能很轻松的阅读和理解代码.
	此文档同时提供了代码格式模板文件.

## cpplint ##
	Google提供了代码检查工具 `cpplint` , 我们对此工具进行了修改.
	所有代码提交前都需要使用此工具进行检查.
	此工具使用python编写, 随此文档提供.

## 行长度 ##
	每一行代码字符数不超过 80.

优点:
:	提倡该原则的人主张强迫他们调整编辑器窗口大小很野蛮.
	很多人同时并排开几个代码窗口, 根本没有多余空间拉伸窗口.
	大家都把窗口最大尺寸加以限定, 并且 80 列宽是传统标准.
	为什么要改变呢?

缺点:
:	反对该原则的人则认为更宽的代码行更易阅读. 80 列的限制是上个世纪 60
	年代的大型机的古板缺陷; 现代设备具有更宽的显示屏,
	很轻松的可以显示更多代码.

结论:
:	80 个字符是最大值.

	特例:

	-   如果一行注释包含了超过 80 字符的命令或 URL,
		出于复制粘贴的方便允许该行超过 80 字符.
	-	包含长路径的 `#include` 语句可以超出80列. 但应该尽量避免.
	-	头文件保护 \<define\_guard\> 可以无视该原则.

## 非 ASCII 字符 ##
	尽量不使用非 ASCII 字符, 使用时必须使用 UTF-8 编码.

即使是英文, 也不应将用户界面的文本硬编码到源代码中, 因此非 ASCII
字符要少用. 特殊情况下可以适当包含此类字符. 如, 代码分析外部数据文件时,
可以适当硬编码数据文件中作为分隔符的非 ASCII 字符串; 更常见的是
(不需要本地化的) 单元测试代码可能包含非 ASCII 字符串. 此类情况下, 应使用
UTF-8 编码, 因为很多工具都可以理解和处理 UTF-8 编码. 十六进制编码也可以,
能增强可读性的情况下尤其鼓励 —— 比如 `"\xEF\xBB\xBF"` 在 Unicode 中是
*零宽度 无间断* 的间隔符号, 如果不用十六进制直接放在 UTF-8 格式的源文件中, 是看不到的.

## 空格还是制表位 ##
	只使用空格, 每次缩进 2 个空格.

我们使用空格缩进. 不要在代码中使用制符表.
你应该设置编辑器将制符表转为空格.

## 函数声明与定义 ##
	返回类型和函数名在同一行, 参数也尽量放在同一行.

函数看上去像这样:

	ReturnType ClassName::FunctionName(Type par_name1, Type par_name2)
	{
		DoSomething();
		...
    }

如果同一行文本太多, 放不下所有参数:

	ReturnType ClassName::ReallyLongFunctionName(Type par_name1,
												Type par_name2,
												Type par_name3)
	{
		DoSomething();
		...
	}

甚至连第一个参数都放不下:

	ReturnType LongClassName::ReallyReallyReallyLongFunctionName(
		Type par_name1,  // 4 space indent
		Type par_name2,
		Type par_name3)
	{
		DoSomething();  // 2 space indent
		...
	}

注意以下几点:

-	返回值总是和函数名在同一行;
-	左圆括号总是和函数名在同一行;
-	函数名和左圆括号间没有空格;
-	圆括号与参数间没有空格;
-	左大括号总在最后一个参数同一行的末尾处;
-	右大括号总是单独位于函数最后一行;
-	右圆括号和左大括号间总是有一个空格;
-	函数声明和实现处的所有形参名称必须保持一致;
-	所有形参应尽可能对齐;
-	缺省缩进为 2 个空格;
-	换行后的参数保持 4 个空格的缩进;

如果函数声明成 `const`, 关键字 `const` 应与最后一个参数位于同一行:=

	// Everything in this function signature fits on a single line
	ReturnType FunctionName(Type par) const
	{
		...
	}

	// This function signature requires multiple lines, but
	// the const keyword is on the line with the last parameter.
	ReturnType ReallyLongFunctionName(Type par1,
									Type par2) const
	{
		...
	}

## 函数调用 ##
	尽量放在同一行, 否则, 将实参封装在圆括号中.

函数调用遵循如下形式:

	bool retval = DoSomething(argument1, argument2, argument3);

如果同一行放不下, 可断为多行, 后面每一行都和第一个实参对齐, 左圆括号后和右圆括号前不要留空格:

	bool retval = DoSomething(averyveryveryverylongargument1,
							argument2, argument3);

如果函数参数很多, 出于可读性的考虑可以在每行只放一个参数:

	bool retval = DoSomething(argument1,
							argument2,
							argument3,
							argument4);

## 条件语句 ##

	倾向于不在圆括号内使用空格. 关键字 `else` 另起一行.

示例代码如下:

	if (condition)// no spaces inside parentheses
	{// new line
		...
	}
	else// new line
	{// new line
		...
	}


## 循环和开关选择语句 ##
-	`switch` 语句可以使用大括号分段. 空循环体应使用 `{}` 或 `continue`.
-	`switch` 语句中的 `case` 块可以使用大括号也可以不用, 取决于你的个人喜好.
示例代码如下
	switch (var)
	{
		case 0:
			...
			break;
		case 1:
			...
			break;
		default:
			assert(false);
			break;
	}

## 指针和引用表达式 ##
	句点或箭头前后不要有空格. 指针/地址操作符 (`*, &`) 之后不能有空格.

示例如下:

	x = *p;
	p = &x;
	x = r.y;
	x = r->y;

注意:

-	在访问成员时, 句点或箭头前后没有空格.
-	指针操作符 `*` 或 `&` 后没有空格.

## 函数返回值 ##

	`return` 表达式中不要用圆括号包围.

8.11. 变量及数组初始化
	用 `=` 或 `()` 均可.

在二者中做出选择; 下面的方式都是正确的:

	int x = 3;
	int x(3);
	string name("Some Name");
	string name = "Some Name";

## 预处理指令 ##
	预处理指令不要缩进, 从行首开始.
	即使预处理指令位于缩进代码块中, 指令也应从行首开始.

示例如下

		// Good - directives at beginning of line
		if (lopsided_score)
		{
	#if DISASTER_PENDING      // Correct -- Starts at beginning of line
			DropEverything();
	#endif
			BackToNormal();
		}

## 类格式 ##
	访问控制块的声明依次序是 `public:`, `protected:`, `private:`, 每次缩进 1 个空格.

示例如下:

	class MyClass : public OtherClass
	{
	 public:      // Note the 1 space indent!
	  MyClass();  // Regular 2 space indent.
	  explicit MyClass(int var);
	  ~MyClass() {}

	  void SomeFunction();
	  void SomeFunctionThatDoesNothing() 

	  void setSome_var(int var) { some_var_ = var; }
	  int getSome_var() const { return some_var_; }

	 private:
	  bool SomeInternalFunction();

	  int some_var_;
	  int some_other_var_;
	  DISALLOW_COPY_AND_ASSIGN(MyClass);
	};

注意事项:

-	所有基类名应在 80 列限制下尽量与子类名放在同一行.
-	关键词 `public:`, `protected:`, `private:` 要缩进 1 个空格.
-	除第一个关键词 (一般是 `public`) 外, 其他关键词前要空一行.
	如果类比较小的话也可以不空.
-	这些关键词后不要保留空行.
-	`public` 放在最前面, 然后是 `protected`, 最后是 `private`.
-	关于声明顺序的规则请参考 声明顺序一节.

## 初始化列表 ##
	构造函数初始化列表放在同一行或按四格缩进并排几行.
下面两种初始化列表方式都可以接受:

	// When it all fits on one line:
	MyClass::MyClass(int var) : some_var_(var), some_other_var_(var + 1)
	{
		...
	}

	// When it requires multiple lines, indent 4 spaces, putting the colon on
	// the first initializer line:
	MyClass::MyClass(int var) :
	    some_var_(var),             // 4 space indent
	    some_other_var_(var + 1)    // lined up
	{	
		...
	}

## 名字空间格式化 ##
	名字空间内容执行标准缩进(2个空格).

示例如下:

	namespace abc
	{

		void foo()
		{
			...
    	}
    } // namespace abc

## 水平留白 ##

-	水平留白的使用因地制宜. 永远不要在行尾添加没意义的留白.
-	添加冗余的留白会给其他人编辑时造成额外负担. 因此, 行尾不要留空格.
-	如果确定一行代码已经修改完毕, 将多余的空格去掉, 或者在专门清理空格时去掉（确信没有其他人在处理). 

## 垂直留白 ##
	垂直留白越少越好.

-	这不仅仅是规则而是原则问题了: 不在万不得已, 不要使用空行. 尤其是:
两个函数定义之间的空行不要超过 2 行, 函数体首尾不要留空行,
函数体中也不要随意添加空行.
-	基本原则是: 同一屏可以显示的代码越多, 越容易理解程序的控制流. 当然,
过于密集的代码块和过于疏松的代码块同样难看, 取决于你的判断.
但通常是垂直留白越少越好.

