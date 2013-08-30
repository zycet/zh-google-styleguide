# C++保留字使用分类 #

## 标准使用 ##
	基础类型
		bool
		true
		false
		char
		signed
		unsigned
		short
		int
		long
		float
		double
		void
	流程控制
		if
		else
		for
		while
		switch
		case
		break
		continue
		default(1)
		return
	类型定义
		enum
		struct
		class
		template
	访问控制
		const
		static
		virtual
		private
		protected
		public
		namespace
		using(1)
	内存管理
		new
		delete(1)
	其他
		inline
		this
		static_cast

## 有限使用 ##
	汇编操作
		asm
	变量位置
		register
		volatile
	访问控制
		extern
		explicit
	类型转换
		const_cast
		reinterpret_cast
		typedef
	特殊类型
		union
		wchar_t
	高级操作
		sizeof
		operator

## 无需使用 ##
	默认定义
		auto(1)
	可替换
		and
		and_eq
		bitand
		bitor
		compl
		not
		not_eq
		or
		or_eq
		xor
		xor_eq 

## 禁止使用 ##
	流程控制
		do
		goto
	访问控制
		friend
		mutable
	异常处理
		catch
		throw
		try
	动态类型
		typeid
		typename
		dynamic_cast

## 无法使用##
	编译器支持不确定
		export(1)
	C++11新命令字
		alignas
		alignof
		char16_t
		char32_t
		constexpr
		decltype
		noexcept
		nullptr
		static_assert
		thread_local
		override
		final
