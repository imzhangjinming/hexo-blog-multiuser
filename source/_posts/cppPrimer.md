---
title: 'Cpp Primer,5th edition  -- 读书摘抄&随想'
categories:
  - notes
date: 2021-07-24 13:57:33
tags:
---

{% asset_img 1.jpg %}
<!-- more -->

# 第二章 变量和基本类型  
* 不要混用有符号和无符号类型  
* 整型字面值  
	|进制|格式|  
	|:---:|:---:|  
	|十进制||  
	|八进制|以0开头|  
	|十六进制|以0x开头|  
* `nullptr` 是指针字面值  
* 列表初始化（list initialization）  
* 引用在**声明**的时候必须**初始化**  
* 引用即别名  
* 默认情况下，`const` 对象仅在文件内有效  
* 不初始化 `const` 变量是非法的  
* 允许使用常量引用引用非常量对象，不允许使用非常量引用引用常量对象  
* 常量表达式是指值不会改变并且在**编译过程**中就能得到计算结果的表达式。C++11允许将变量声明为 `constexpr` 类型以便由编译器来验证变量的值是否是一个常量表达式。  
* 一个 `constexpr` 指针的初始值必须是 `nullptr` 或者 `0`，或者是存储于某个固定地址中的对象  
* 别名声明（alias declaration）  
	`using SI = Sales_item;`  
* `auto` 一般会忽略顶层 `const` ，保留底层 `const`  
* `decltype` 类型指示符
	`decltype` 用来获得一个表达式的类型,  
	如 `decltype(f()) sum = x;` `sum` 是 `f()` 返回值的类型  
* `decltype((variable))`  双层括号的结果永远是引用  
	`decltype(variable)`  结果只有当variable本身就是一个引用时才是引用  

# 第三章 字符串、向量和数组  
*  `using namespace::space`  
*  头文件中不应包含 `using` 声明  
*  使用等号初始化对象，实际上执行是是拷贝初始化（copy initialization）,不使用等号，执行直接初始化（direct initialization）  
*  如果想读取一整行，包括空白符，应该使用 `getline` 函数  
*  如果一条表达式中已经有了 `size()` 函数就不要在使用 `int` 了，这样可以避免混用 `int` 和 `unsigned` 可能带来的问题  
* 标准库允许把字符字面值和字符串字面值转换成 `string` 对象  
* 字符串字面值和 `string` 是**不同的类型**  
* `string` 类的输入运算符 `>>` 在遇到**空白符**的时候结束读取  
	`getline` 不会在空白符处停止读取  
* 使用下标访问空 `string` 会引发不可预知的后果  
* 理解数组声明的关键是从数组的名字开始按照**由内向外**的顺序阅读  
* `strlen` 函数返回字符串长度，不包含空字符  

# 第四章 表达式
* `cout << i << ++i <<endl; should never appear in your code.`  
* **溢出**，计算的结果超出该类型所能表达的范围时就会产生溢出  
* 环绕（wrapped around）  
* 赋值运算满足**右结合律**  
* 递增/递减运算符  
	前置版本将对象本身作为**左值**返回，后置版本则将对象原始值的副本作为**右值**返回  
* `*ptr++` 输出 `ptr` 当前指向的值并将 `ptr` 向前移动一个元素  
* `sizeof` **不会**把数组名当作指针来处理  
* `sizeof` 对 `string` 对象或 `vector` 对象执行 `sizeof` 操作只返回该类型固定部分的大小，不会计算对象中的元素占了多少空间  
* 隐式类型转换，在大多数表达式中，比 `int` 类型小的整型值首先提升为较大的整数类型  
* 整型提升(integral promotion)负责把小整数类型转换成较大的整数类型  
* 强制类型转换  
	* `static_cast`  
	* `dynamic_cast`  
	* `const_cast`
	* `reinterpret_cast`

# 第五章 语句  
* `switch` 中的 `case` 标签必须是整型常量表达式  
* 任何两个标签的值不能相同  
* 一般不要省略 `case` 分支最后的 `break` 语句  
* 想到利用 `switch` 语句特性的一种可能的场景  
	需要统计某个范围内的数字出现的次数，比如要统计小于5、6、7、8、9的数字出现的次数，显然，并分别以less_5 、less_6 、less_7 、less_8 、less_9计数，那么可以用switch语句这样写：  

	```	C++
	switch(value)
	{
		case 5:
			++less_6;
		case 6:
			++less_7;
		case 7:
			++less_8;
		case 8:
			++less_9;
		break;
	}
	```
	这个语句可能并没有什么用，是突然想到的，记录一下  
* `switch` 语句内部不应该定义并初始化变量，因为 `switch` 语句可能会跳过它的初始化  
* `do while` 语句不允许在条件部分定义变量  
* **不要**在程序中使用 `goto` 语句，因为它使得程序既难理解又难修改  
* 
	* `throw` 表达式  
	异常检测部分使用 `throw` 表达式来表示它遇到了无法处理的问题，`throw` 语句引发异常  
	* `try` 语句块，使用 `try` 语句块处理异常。`try` 语句块以 `try` 关键字开始，后接一个或多个 `catch` 子句，`catch` 子句处理异常（exception handler）  
	* 异常类（exception class），用于在 `throw` 和相关 `catch` 子句之间传递异常信息  

# 第六章 函数  
* 调用运算符（call operator）  
* 函数调用完成两项工作：一是用实参初始化形参，二是将控制权转移给被调函数。此时，主调函数(calling function)的执行被暂时中断，被调函数(called function)开始执行  
* C++中，名字由作用域，对象有生命周期  
* 函数声明也称为函数原型（function prototype）  
* 常量引用可以使用字面值初始化  
	`const int &r2 = 42;`  
* C++允许将变量定义成**数组的引用**  
	`int (&arr)[10]; //数组的引用，数组长度为10`  
	`int &arr[10];	//arr是一个长度为10的数组，每一个数组元素都是int&`  
* 在讲到含有可变形参的函数时提到的一个应用是输出错误信息的程序  
* C++11提供两种方法实现变参数函数，一是 `initializer_list` 的标准库类型，但是它只适用于**所有实参类型**相同的情况，二是使用可变参数模板  
* `initializer_list` 对象中的元素永远是常量值，**无法改变** `initializer_list` 对象中元素的值  
* 不要返回局部对象的引用或指针  
* 如果同一作用域内的几个函数名字相同但形参列表不同，我们称之为重载函数  
* 不允许两个函数除了返回类型外其他所有的要素都相同  
* 在C++中，名字查找发生在类型检查之前  
* 内联说明只是向编译器发出的一个请求，编译器**可以选择忽略**这个请求  
* `assert(expr)`  
	首先对 `expr` 求值，如果表达式为假，`assert` 输出信息并终止程序的执行。如果表达式为真，则什么也不做  
* `assert` 是预处理宏，它由预处理器而**非编译器管理**，所以无需使用using声明  
* |预处理指令|作用|  
  |:---:|:---:|  
  |__FILE__|存放文件名的字符串字面值|  
  |__LINE__|存放当前行号的字面值|  
  |__TIME__|存放文件编译时间的字符串字面值|  
  |__DATE__|存放文件编译日期的字符串字面值|  
 

# 第七章 类
* 不同的编程角色
	提及用户时，不同的语境决定了不同的含义  
* 定义在类内部的函数是隐式的 `inline` 函数  
* 成员函数通过一个名为 `this` 的额外的隐式参数来访问调用它的那个对象。当我们调用一个成员函数时，用请求该函数的对象地址初始化 `this` 
* IO类属于不能被拷贝的类型，因此只能通过引用来传递它们  
* 默认构造函数**无需任何**实参  
* 如果不能使用类内初始值，则所有构造函数都应该显式地初始化每个内置类型的成员  
* 使用 `class` 和 `struct` 定义类的唯一区别是**默认的访问权限**  
* 可变数据成员 （mutable data member）永远不会是 `const` ，即使它是 `const` 对象的成员。一个 `const` 成员函数可以改变一个可变成员的值  
* 类允许包含指向它自己类型的**引用**或**指针**  
* 编译器处理完类中的全部声明后才会处理成员函数的定义  
* `::var` 表示全局作用域中的变量 `var`  

* 构造和赋值是两个不同的概念

* 构造函数的初始值有时候必不可少，因为有些成员，如**const**、**引用**等，必须进行初始化。

* 成员初始化的顺序是它们在类中出现的顺序

* 如果一个构造函数为**所有**的参数都提供了默认实参，则它实际上也定义了默认构造函数

* exercise 7.36
	```C++
	MyClass(std::istream& c = std::cin);
	```

* 委托构造函数(delegating constructor)

* 隐式的类类型转换只允许进行一步
* 将构造函数声明为`explicit`可以阻止隐式类类型转换，`explicit`只对一个实参的构造函数有效，只能在类内声明构造函数时使用，在类外定义的时候就不需要重复了
* 可以用`static`关键字声明类的静态成员，静态成员由类拥有，而不是为对象所拥有
* 即使一个常量静态数据成员在类内部被初始化了，通常情况下也应该在类的外部定义一下该成员
* 静态成员可以是不完全类型

	```C++
	class Bar{
	public:
		//...
	private:
		static Bar mem1;	//正确：静态成员可以是不完全类型
		Bar *mem2;			//正确：指针成员可以是不完全类型
		Bar mem3;			//错误：数据成员必须是完全类型
	};
	```

* 静态成员可以作为默认实参

# 第八章 IO库  

* IO库类型和头文件   

	|头文件 | 类型|
	|:---: | :---: |
	|iostream | istream ostream iostream|
	|fstream | iftream ofstream fstream|
	|sstream | istringstream ostringstream stringstream|

* IO对象无**拷贝**或**赋值**  
* 由于IO对象无法进行拷贝或赋值，所以不能将形参或返回类型设置为流类型。通常以**引用**方式传递和返回流。读写一个IO对象会改变其状态，因此传递和返回的引用不能是`const`的。  
* 一个流一旦发生错误，其上后续的IO操作也会失败。  
* 每个输出流管理一个缓冲区，缓冲技术主要是为了提升效率，因为单一的写操作可能会很费时，将多个写操作合并成一个会节省很多开销。  
* `std::endl` 可以显式刷新缓冲区  
* `std::endl` `std::flush` `std::ends`都可以显式刷新缓冲区，但是它们的附加符号不同  
* `unitbuf` 和 `nounitbuf`  
* `tie` 可以用来关联流  
* 一个`fstream`对象被销毁时，`close`会被自动调用  
* 保留被`ofstream`打开的文件中已有的数据的唯一方法是显式指定`app`或`in`模式  

# 第九章 顺序容器  
* 顺序容器类型  
	`vector` `deque` `list` `forward_list` `array` `string`  
* `string` 和 `vector` 的元素保存在连续的内存空间中  
* 通常，使用  **`vector`**是最好的选择，除非有很好的理由选择其他容器  
* exercise 9.2  
	`list<deque<int>> L;`  
* `forward_list`迭代器不支持递减运算符  
* 构成迭代器范围的迭代器的限制  
	* `begin` 与 `end` 相等，则范围为空  
	* `begin` 与 `end` 不等，则范围至少包含一个元素，且`begin` 指向该范围中的第一个元素  
	* 可以对`begin` 递增若干次，使得 `begin == end`   
* exercise 9.7  
	`vector<int>::sizetype i;`  
* exercise 9.8  
	`list<string>::const_iterator i;`  
	`list<string>::iterator i;`  
* 当 `auto` 与 `begin` 或 `end` 结合使用时，获得的迭代器类型依赖于容器类型  
* exercise 9.10
	`it1 : iterator`  
	`it2 : const_iterator`  
	`it3 : const_iterator`  
	`it4 : const_iterator`  
* 只有顺序容器的构造函数才接受大小参数，关联容器并不支持  
* 需要交换两个相同类型的容器的内容时，`swap`通常比拷贝快得多  
* 顺序容器（ `array`  除外）定义了一个名为`assign`的成员，允许我们从一个不同但相容的类型赋值，或者从容器的一个子序列赋值。  
* 传递给`assign`的迭代器不能指向调用`assign`的容器（即不能指向它自身？）  
* 除了`string`外，指向容器的迭代器、引用和指针在`swap`操作后不会失效，但是它们指向的元素已经属于不同的容器。  
* 统一使用非成员版本的`swap`是一个好习惯  
* 比较两个容器实际上是进行元素的逐对比较。所以容器的关系运算符使用元素的关系运算符完成比较  
* 向一个`vector`、`string`、`deque`插入元素会使所有指向容器的迭代器、引用和指针都失效  
* `emplace`成员使用传递给它的参数在容器管理的内存中直接构造元素，省去了使用`push`或`insert`时拷贝对象所花费的时间  
* 不能递减`forward_list`迭代器  
* `string` `vector` `deque` `array` 都提供下标运算符  
* `forward_list`部分没有仔细看  
* 使用迭代器添加元素或者删除元素可能会使迭代器失效，因此必须保证每次操作完成后迭代器被**重新定位**  
* `end`返回的迭代器很容易失效，所以最好不要保存`end`返回的迭代器，或者记得实时更新保存`end`返回值的迭代器  
* `vector` `string` `deque` 支持 `shrink_to_fit` 操作，将 `capacity` 减少为与 `size` 相同的大小  
* `string` 的额外操作部分没有细看，需要用到时再回来查吧  
* 容器**适配器**（`adaptor`）
* 每个容器适配器都基于底层容器类型的操作定义了自己的特殊操作，我们**只能**使用适配器操作，不能使用底层容器的操作  

# 第十章 泛型算法（generic algorithm）  

* 泛型算法永远不会改变底层容器的大小。算法可能改变容器中保存的元素的值，也可能在容器内移动元素，但永远不会直接添加或删除元素。（因为这些操作可能会使迭代器失效）  

* 对书中提到的算法做一个简单记录  

	|算法名称|功能|
	|:---:|:---:|
	|find|在一个未排序的元素序列中查找一个特定元素|
	|count|返回指定元素序列中指定值出现的次数|
	|accumulate|计算指定元素序列中所有元素的和|
	|equal|用于确定两个序列是否保存相同的值|
	|fill  fill_n|将范围内的元素赋为给定值|
	|copy|复制|
	|replace|替换|
	|sort|排序|

* 只接受一个单一迭代器来表示第二个序列的算法，都假定第二个序列至少与第一个序列一样长  
* 向目的位置迭代器写入数据的算法假定目的位置足够大，能容纳要写入的元素  
* **可调用对象** （callable object）。
* 四种可调用对象
	* 函数  
	* 函数指针  
	* 重载了函数调用运算符的类  
	* lambda表达式  
* 一个lambda表达式表示一个可调用的代码单元，可以将其理解为一个未命名的内联函数  
* lambda必须使用尾置返回类型  
* lambda可以省略参数列表和返回类型，但必须永远包含捕获列表和函数体  
* 只对lambda所在函数中定义的非static变量使用捕获列表，在lambda函数体中可以直接使用局部static变量和在它所在函数之外声明的名字  
* 捕获列表可以使用值捕获或者引用捕获，值捕获在lambda创建时拷贝变量，而不是调用时  
* **尽量保持lambda的变量捕获简单化**  
* 混合使用隐式和显示捕获变量时，显示捕获的变量必须使用与隐式捕获不同的方式  
* 默认情况下，如果一个lambda体包含 `return` 之外的任何语句，则编译器自动推断其返回值为  `void` ，需要定义返回类型时，必须使用**尾置返回类型**  
* 对于那种只在**一两个地方**使用的**简单操作**，lambda表达式是最有用的。  
* 标准库 **bind** 函数，定义在头文件 `functional` 中  
* `bind` 接受一个可调用对象，返回一个可调用对象  
* placeholders 占位符
* 使用占位符应该声明一个命名空间 `using namespace std::placeholders`  
* 插入迭代器  

	|类型|特点|
	|:---:|:---:|
	|back_inserter|创建一个使用push_back的迭代器|
	|front_inserter|创建一个使用push_front的迭代器|
	|inserter|创建一个使用insert的迭代器，第二个参数指向想要操作的容器，inserter创建的迭代器会向其参数位置之前插入元素|

* 根据算法对迭代器操作的要求可以把迭代器分成5类  

	|类别|特点|
	|:---:|:---:|
	|输入迭代器|只读，不写；单遍扫描，只递增|
	|输出迭代器|只写，不读；单遍扫描，只递增|
	|前向迭代器|可读写；多遍扫描（？？），只递增|
	|双向迭代器|可读写；多遍扫描，可递增递减|
	|随机访问迭代器|可读写；多遍扫描，支持全部迭代器运算|

# 第十一章 关联容器  
* `map` 是键值对的集合，`set` 是关键字的集合  
* `pair` 定义在头文件 `utility` 中  
* `pair` 的默认构造函数对数据成员进行值初始化  
* 关联容器的额外类型别名  

	|别名|特点|
	|:---:|:---:|
	|key_type|此容器类型的关键字类型|
	|mapped_type|每个关键字关联的类型|
	|value_type|对于 set ，即 key_type ; 对于 map ，即 pair<const key_type,mapped type>|

* 我们不能改变一个元素的关键字  
* 一个 map 的 value_type 是一个 pair  
* set 的 迭代器是 const 的  
* 通常不对关联容器使用泛型算法  
* map的下标运算符和普通下标运算不太一样，当索引的值不在map中时，下标运算会为它创建一个元素并插入到map中  

	> 由于下标运算符可能插入一个新元素，我们只能对非 `const` 的 `map` 使用下标操作  

* 对于 `map` 来说，解引用迭代器和使用下标操作的返回值不同，解引用迭代器返回 `value_type` 对象，下标操作返回 `mapped_type` 对象  
* >有时只是想知道一个元素是否已经在 `map` 中，但在不存在时并不想添加元素，在这种情况下就不能使用下标运算符  

	这种情况下应该使用 `find` 方法  
* 关联容器查找指定元素，有 `find` 和 `count` 方法可以用  
* 无序关联容器使用哈希函数和关键字类型的 `==` 运算符来组织元素  
* 无序容器在存储上组织为一组桶，每个桶保存零个或多个元素  
* 哈希函数负责将指定元素映射到对应的桶，我的理解：哈希函数就是个”垃圾分类工“  
* 对于相同的参数，哈希函数必须产生相同的结果  
* 无序容器对关键字类型有要求  
	具体来说，无序容器的关键字类型可以是内置类型、`string` 和智能指针  
	但是不能直接定义关键字类型为自定义类型的无序容器，原因应该是没有为自定义类型服务的哈希函数吧，这样的哈希函数必须自己提供  

# 第十二章 动态内存  
* 管理动态内存是非常**棘手**的  
* 智能指针（smart pointer） 定义在 memory 头文件中   

	|智能指针类型|特点|
	|:---:|:---:|
	|shared_ptr|允许多个指针指向同一个对象|
	|unique_ptr|独占所指向的对象|

* 引用计数（reference count）  
* 当一个 `shared_ptr` 的计数器变为0，他就会自动释放指向的内存  
* >如果将 `shared_ptr` 存放在一个容器中，而后不再需要全部元素，而只使用其中的一部分，要记得用 `erase` 删除不再需要的那些元素  
* 定位 `new` (placement new)  
* `delete` 表达式执行两个动作：销毁给定的指针指向的对象；释放对应的内存  
* 通常情况下，编译器不能分辨一个指针是指向静态还是动态内存，所以请**确保**传递给 `delete` 的指针是指向动态内存的指针或者一个空指针  
* 不能进行内置指针向智能指针的隐式转换，所以类似下面这样的初始化是错误的  
	`shared_ptr<double> p1 = new int(1024);`  
	这样声明并初始化是正确的  
	`shared_ptr<double> p1(new int(1024)); //相当于直接调用构造函数了`  
* 智能指针默认使用 `delete` 释放关联的对象，所以智能指针一般指向动态内存；当然，也可以将智能指针绑定到一个指向其他类型的资源的指针上，前提是我们要提供自己的操作（删除器 `deleter` ）替代 `delete`  
* 尽量不要混合使用内置指针和智能指针  
* 不要使用智能指针的 `get` 方法初始化或为另一个智能指针赋值，因为那有可能造成空悬指针，即指向已经被释放的内存的指针  
* 为了正确使用智能指针，我们必须坚持一些基本规范：  
	* 不使用**相同**的内置指针初始化（或 `reset` ）多个智能指针  
	* 不 `delete` `get` 返回的指针  
	* 不适用 `get()` 初始化或 `reset` 另一个智能指针  
	* 如果使用 `get()` 返回的指针，记住当最后一个对应的那个指针销毁后，你使用的指针就变为无效了（空悬指针）  
	* 如果使用智能指针管理的资源不是 `new` 分配的内存，记住传递给它一个删除器（`deleter`）  

* `unique_ptr` 没有类似 `shared_ptr` 的 `make_shared` 那样的库函数，当我们定义一个 `unique_ptr` 时，必须将其绑定到一个 `new` 返回的指针上，同样的， `unique_ptr` 也必须使用直接初始化，而不能使用隐式转换初始化  
* `unique_ptr` 不支持普通的拷贝或赋值操作  
* `u = nullptr` 释放 u 指向的对象，将 u 置为空  
* 可以使用 `release` 或 `reset` 将指针的所有权从一个 `unique_ptr` 转移给另一个 `unique_ptr`  
* `allocator`  类允许我们将内存分配和初始化分离  
* `allocator` 通常会提供更好的性能和更灵活的内存管理能力  
* 大多数应用应该使用标准库容器而不是动态分配数组。  
* `new int[size]` 方括号中的大小必须是整型，但**不必是常量**  
* 动态分配一个数组时，得到的实际上是一个数组元素类型的指针  
* **不能**使用范围 `for` 语句来处理所谓的动态数组  
* 默认初始化和值初始化  
	`int *pia = new int[10]; //10个默认初始化的int`  
    `int *pia = new int[10](); //10个值初始化的int`  
* `new char[0]` 是合法的，但是不能解引用它返回的指针  
* `unique_ptr<int[]> up(new int[10]);` 使用 `unique_ptr` 指向一个动态分配的数组，指向数组的 `unique_ptr` 不支持成员访问运算符（点和箭头运算符）  
* 由于 `shared_ptr` 默认使用 `delete` 释放关联的对象，所以如果想用 `shared_ptr` 管理动态数组，必须提供自己的删除器  
* `new & delete` 的组合有灵活性的局限，具体来说就是 `new` 将内存分配和对象构造组合在一起，`delete` 将对象析构和内存释放组合在一起  
* `allocator` 类将内存分配和对象构造分开  
* `allocator` 是一个模板类  
* `allocate -> construct -> destroy -> deallocate`  
* 传递给 `deallocate` 的指针不能为空，必须是 `allocate` 返回的指针  
* `uninitialized_copy` `uninitialized_fill` 用来在未初始化的内存中创建对象  

# 第十三章 拷贝控制  
* 析构函数不接受任何参数，所以不能被重载，每个类只有唯一一个析构函数  
* 构造函数和析构函数初始化/销毁的顺序  
	构造函数先按成员在类中出现的顺序对成员进行初始化，然后执行函数体  
	析构函数先执行函数体，然后按成员初始化的逆序销毁成员  
* 隐式销毁一个内置的指针类型的成员不会delete它所指向的对象  
* 注意成员并不是在析构函数体里被销毁的，它们是在析构函数体运行完之后的**销毁阶段**被销毁的  
* 有三个基本操作可以控制**类的拷贝操作**：拷贝构造函数、拷贝赋值运算符和析构函数  
* 一个经验是：需要析构函数的类通常也需要拷贝构造函数和拷贝赋值运算符。需要析构函数说明类中定义了自动执行销毁过程时候无法彻底“清理干净”的成员，那么当使用拷贝构造和赋值运算的时候自然也不能自动完成相应的操作，所以自然需要自定义拷贝构造函数和拷贝赋值运算符  
* 使用拷贝操作的类也需要赋值操作，反之亦然  
* 大多数类应该定义**默认构造函数**、**拷贝构造函数**和**拷贝赋值运算符**，无论是显式的还是隐式的  
* 对于**析构函数已删除**的类型，**不能定义**该类型的变量或释放指向该类型对象的指针；对于这种类，不能定义它的对象，但是可以动态分配这种类型的对象，即 `new`  
* 本质上来说，当不可能拷贝、赋值或销毁类的成员时，类的合成拷贝控制成员就被定义为删除的  
* 希望阻止拷贝的类应该使用 `=delete` 来定义它们自己的拷贝构造函数和拷贝赋值运算符  
* 定义拷贝控制操作时有两种选择，一种是使类的**行为像值**，另一种是使类的**行为像指针**  
* 实现类的类值拷贝行为  
	注意要在拷贝赋值运算符内释放对象之前动态分配的内存，而拷贝构造函数不需要，因为拷贝构造函数负责对象初始化，在调用它的时候对象还没有已经初始化的成员，自然就不会有已经动态分配的内存；  
* 编写赋值运算符时有两点需要记住：  
1.如果将一个对象**赋予它自身**，赋值运算符必须能正常工作  
2.大多数赋值运算符组合了**析构函数**和**拷贝构造函数**的工作  
编写赋值运算符时，一个好的模式是先将右侧运算对象先拷贝到一个局部临时对象中，当拷贝完成后销毁左侧运算对象的现有成员就是安全的了。然后将临时对象拷贝到左侧运算对象的成员中  

* 引用计数  
	除了拷贝构造函数，每个构造函数创建一个引用计数。  
	拷贝构造函数递增对象的计数器  
	拷贝赋值运算符递增右侧对象的计数器，递减左侧对象的计数器  
	析构函数递减计数器  
这其实类似智能指针的实现思路了  

* 交换操作 `swap` 在需要进行排序的类中特别有用  
* 拷贝赋值运算符通常执行拷贝构造函数和析构函数中的工作，这种情况下，公共的工作应该放在  `private` 的工具函数中完成  
* `move` 函数定义在 `utility` 头文件  
* `vector` 预先分配足够的内存来保存可能需要的更多元素，我曾测试过，在我的环境下，分配内存的大小依次是1，1，2，4，8 ...个元素内存  
* 使用 `allocator` 类分配的内存是**未构造**的，谨记  
* 移动构造函数 `std::move` ，定义在 `utility` 头文件中   
* 我们通常**不为** `move` 提供一个 `using` 声明，书中这里卖了一个关子，说在第十八章会解释  
* 记录一个错误  
	在编译13.5节的 `StrVec` 程序时，老是会报一个奇怪的错误：

	`C:\Users\Neymar\AppData\Local\Temp\ccGF08ER.o:StrVec.cpp:(.rdata$.refptr._ZN6StrVec5allocB5cxx11E[.refptr._ZN6StrVec5allocB5cxx11E]+0x0):undefined reference to `StrVec::alloc[abi:cxx11]' `  

	经过查资料才记起来，一个类内的静态成员在类内只是被声明了，并没有被定义，所以要在类外（也就是实现文件），定义一遍改成员，具体就是：  
	`std::allocator<std::string> StrVec::alloc;`   
加上之后就能正常编译运行了  

* 新标准（指C++11）有一个重要特征，即可以移动而非拷贝对象的能力。主要是为了提升性能吧  
* 标准库容器、`string` 和 `shared_ptr` 类**既支持移动也支持拷贝**。IO类和 `unique_ptr`类**可以移动但不能拷贝**  
* **右值引用**：必须绑定到右值的引用  
* 右值引用有一个很重要的性质，它只能绑定到一个将要销毁的对象  
* 右值引用不过是某个对象的另一个名字而已  
* 可以将一个 `const` 引用绑定到一个右值上  
* 左值持久；右值短暂  
* **变量**可以看作只有一个运算对象而没有运算符的表达式  
* `std::move()` 可以返回一个绑定在左值上的右值引用，但是执行完这个操作后，对移后源允许的操作就很有限了  
* **移动构造函数**第一个参数是该类型的一个**右值引用**，它的任何额外的参数必须有**默认实参**  
* 移动构造函数必须确保移后源对象处于“销毁无害” 的状态  
* 移动操作窃取资源，通常不分配资源  
* `noexcept` 通知编译器，我们的函数**不抛出**任何异常，使用这一个特性时，必须在类头文件的声明和定义中都指定 `noexcept`  
* 移动赋值运算符主要完成两个工作，一是释放原来的内存，二是接管 rhs 的值，并确保 rhs 原来的成员与资源不再关联  
* 在移动操作之后，移后原对象必须保持**有效、可析构**的状态，但是用户**不能**对其值进行任何假设  
* 只有当一个类**没有定义任何自己版本的拷贝控制成员**，且它的所有数据成员都**能移动构造**或**移动赋值**时，编译器才会为它合成移动构造函数或移动赋值运算符  
* 定义了一个移动构造函数或移动赋值运算符的类必须也定义自己的拷贝操作，否则拷贝操作成员会被默认地定义为删除的  
* 如果一个类同时定义了拷贝构造函数和移动构造函数，则编译器使用普通的函数匹配规则来确定使用哪个构造函数，一般是**拷贝左值**，**移动右值**；如果没有定义移动构造函数，则右值也被拷贝  
* 所有**五个**拷贝控制成员应该看作一个整体：一般来说，如果一个类定义了任何一个拷贝操作，它就应该定义所有五个操作。（五个拷贝控制成员：拷贝构造函数、拷贝赋值运算符、移动构造函数、移动赋值运算符和析构函数）  
* 移动迭代器（move iterator）适配器  
	移动迭代器通过改变给定迭代器的解引用运算符的行为来适配此迭代器  
	普通迭代器的解引用运算符返回一个左值；移动迭代器的解引用运算符生成一个右值引用。  
* `make_move_iterator` 函数将一个普通迭代器转换为一个移动迭代器  
* 可以将移动迭代器传递给 `unintialized_copy`   
* 标准库不保证哪些算法使用移动迭代器，哪些不适用  

# 第十四章 重载运算与类型转换  
* 重载运算符函数的参数数量与该运算符作用的运算对象数量一样多  
* 除了重载的函数调用运算符operator()之外，其他重载运算符不能含有默认实参  
* 如果一个运算符函数**是成员函数**，则它的第一个运算对象绑定到隐式的 `this` 指针上  
* 当一个重载的运算符是成员函数时，`this` 绑定到左侧的运算对象，**成员运算符函数**的参数数量比运算对象少一个  
* 只能重载已有的运算符，不能发明新的运算符号  
* 对于一个重载的运算符来说，其优先级和结合律与**对应的内置运算符**保持一致  
* `::`、 `.*`、 `.`、 `?:` **不能**被重载  
* 关于运算对象求值顺序的规则**无法**应用到重载的运算符上 （逻辑与运算符、逻辑或运算符、逗号运算符等）  
* 一般**不重载逗号运算符**和**取地址运算符**  
* 通常情况下**不重载**逗号、取地址、逻辑与和逻辑或运算符  
* 定义重载的运算符时应该首先考虑是将其声明为成员还是非成员函数 ，有下面几条准则可以帮助我们选择：
	* 赋值（=）、下标（[]）、调用（()）、和成员访问箭头（->）运算符**必须是成员**  
	* 复合赋值运算符一般来说应该是成员，但非必须  
	* 改变对象状态的运算符或者与给定类型密切相关的运算符，如递增、递减和解引用运算符，通常应该是成员  
	* 具有**对称性**的运算符可能转换任意一端的运算对象，例如算术、相等性、关系和位运算等，因此它们通常应该是非成员函数  
* 通常情况下输出运算符的第一个形参是一个**非常量** `ostream` 对象的引用，之所以是非常量是因为向流写入内容会改变其状态，而引用是因为无法直接复制一个 `ostream`对象  
* 输出运算符尽量**减少**格式化操作，一般输出运算符**不应该打印**换行符  
* 输入输出运算符必须是**非成员**运算符  
* 通常情况下，重载的输入运算符只设置输入流的 `failbit` 类  
* 如果类同时定义了算术运算符和相关的复合赋值运算符，则通常情况下应该**使用复合赋值运算符来实现算术运算符**  
* 通常情况下**关系运算符**应该：
	* 定义顺序关系，令其与**关联容器**中对**关键字**的要求一致  
	* 如果类同时含有 `==` 运算符的话，则定义一种关系令其与 `==` 保持一致，特别是如果两个对象是不等的，那么一个对象应该 < 另一个  
* `std::lexicographical_compare` 可以执行**词典比较 **  
* 除了拷贝赋值运算符，类还可以定义其他赋值运算符以使用**别的类型作为右侧运算对象**  
* 不论形参的类型是什么，**赋值运算符**都必须定义为**成员函数**  
* **下标运算符**必须是**成员函数**  
* 最好同时定义下标运算符的**常量版本**和**非常量版本**  
* 定义递增和递减运算符的类应该**同时**定义**前置版本**和**后置版本**  
* **箭头运算符**对**返回值**有限定，必须返回**类的指针**或者**自定义了箭头运算符**的某个类对象  
* **函数调用运算符**必须是**成员函数**  
* **函数对象类**通常含有一些数据成员，这些成员被用于**定制**调用运算符中的**操作**  
* 函数对象常常作为泛型算法的实参  
* lambda 表达式产生的类不含默认构造函数、赋值运算符及默认析构函数；它是否含有默认的拷贝/移动构造函数则通常要视捕获的数据成员类型确定  
* 标准库定义了一组表示算术运算符、关系运算符和逻辑运算符的类。这些类型定义在 `functional` 头文件中，但是我暂时不知道它们发挥用处的特定情境  
* 接上面这一条，它们常传递给标准库算法  
* 再一次：C++语言中有几种**可调用对象**：函数、函数指针、lambda表达式和重载的函数调用运算符的类  
* `function` 是一个新的标准库类型，它可以存储可调用对象  
* 类型转换运算符（conversion operator）是类的一种特殊成员函数，它负责将一个类类型的值转换成其他类型  
* **类型转换运算符**既没有显式的返回类型，也没有形参，而且必须定义成类的**成员函数**。类型转换运算符通常不应该改变待转换对象的内容，因此一般被定义成 `const` 成员  
*  尽管类型转换函数不负责指定返回类型，但实际上每个类型转换函数都会返回一个对应类型的值  
*  在实践中，类**很少提供**类型转换运算符，但是定义向 `bool` 的类型转换还是比较普遍的现象  

# 第十五章 面向对象程序设计  
* 面向对象程序设计（OOP）的核心思想是**数据抽象**、**继承**和**动态绑定**  
* C++11 新标准允许在派生类中显式地注明它将使用哪个成员函数改写基类的虚函数，具体措施是在该函数的形参列表后增加一个 `override` 关键字  
* 在C++语言中，当我们使用**基类的引用或指针**调用一个**虚函数**时将发生**动态绑定**  
* 关键字 `virtual` 只能出现在**类内部**的声明语句之前而不能用于类外部的函数定义  
* 派生列表中的**访问说明符**的作用是为了说明派生类从基类继承来的成员**是否对*派生类的用户*可见**  
* 如果派生类不重写基类的虚函数，则它将继承基类的版本  
* 在一个对象中，继承自基类的部分和派生类自定义的部分**不一定连续存储**  
* 可以把派生类对象的引用或指针用在需要基类对象引用或指针的地方  
* 每个类控制它**自己的成员的初始化**过程  
* 派生类初始化过程：首先初始化基类的部分，然后按照声明的顺序依次初始化派生类的成员  
* 如果基类定义了一个**静态成员**，则在**整个继承体系**中只存在该成员的**唯一定义**  
* 如果一个类想被用作基类，那么它必须已经定义，而非仅仅声明  
* 为了防止继承发生，可以在类名后面跟一个关键字 `final`  
* 静态类型 (static type) 与 动态类型 (dynamic type)  
	表达式的**静态**类型在**编译时**就是已知的；  
	**动态**类型往往是变量或表达式表示的内存中的对象的模型  
* 从派生类向基类的类型转换只对指针或引用类型有效；基类向派生类不存在隐式类型转换  
* 当使用基类的引用或指针调用一个虚成员函数是会执行**动态绑定**；当通过一个普通类型的表达式调用虚函数时，在编译的时候就能确定到底调用 哪一个版本的虚函数  
* polymorphism 多态性，即“多种形式”  
* 当且仅当对通过**指针或引用调用虚函数**时，才会在运行期间解析该调用，也只有在这种情况下对象的动态类型才有可能与静态类型不同  
* 派生类在重写虚函数的时候可以在函数声明前加注 `virtual` 关键字，当然，也可以不加，这其中的区别在于，如果加注了 `virtual`，则这个函数在所有它的派生类中都是虚函数  
* 虽然不能创建**抽象基类**的对象，但是必须为它定义构造函数，因为它的派生类指望着用它来**初始化虚基类**的成员呢  
* 含有**纯虚函数**的类就是**抽象基类**了  
* 保护继承有一条特别的性质，即在派生类中只能通过派生类的对象访问该对象包含的基类部分的受保护成员  
* 某个类对其继承而来的成员的**访问权限**受到两个因素影响：一是该成员在基类中的访问权限说明符，二是在派生类的派生列表中的访问说明符  
* 派生访问说明符对于派生类的成员及友元能否访问其直接基类的成员没什么影响。对基类成员的访问权限只与基类中的访问说明符有关。注意是**派生类的成员和友元对基类成员的访问权限只与基类中的访问说明符有关**  
* 派生访问说明符是为了控制派生类用户对基类成员的访问权限。注意是派生类用户（派生类对象、派生类的派生类等）的访问权限  
* **公有派生**，则派生类用户的访问权限就是基类中声明的那样  
* 派生类向基类转换的可访问性  
	总的来说，对于代码中的某个给定节点，如果基类的公有成员是可访问的，则派生类向基类的类型转换也是可访问的  
* 类的设计与受保护的成员  
	基类应该将其接口成员声明为公有的；同时将属于其实现部分分成两组：一组可供派生类访问，声明为 `protected`;另一组只能由基类及基类的友元访问，声明为 `private`  
* 友元与继承  
	**友元关系不能继承**。基类的友元在访问派生类成员时不具有特殊性；派生类的友元也不能随意访问基类的成员  
* 判断友元访问权限时，分清要访问的对象属于哪个类，然后根据该友元对于这个类的访问权限判断能否访问  
* 不能继承友元关系；每个类负责控制各自成员的访问权限  
* 默认的继承保护级别  
	使用 `class` 关键字定义的派生类是私有继承的  
* 使用 `struct` 和 `class` 定义的类的差别（**仅有两个差别**）
	* `struct` 成员默认访问说明符是 `public` ; `class` 成员默认访问说明符是 `private`  
	* 使用 `struct` 定义派生类时，默认派生访问说明符是 `public` ，`class` 则是 `private`  
* **派生类向基类转换的可访问性**  
	首先应该分清访问的主体，即谁来访问  
	我将主体分为三类：类的成员或友元 、类的对象 、 派生类  
	对于**派生类的对象**来说，只有派生类是 `public`  继承自基类时，才能使用派生类对象向基类的转换  
	对于**派生类的派生类**来说（派生类的派生类也是派生类的用户），只有派生类是 `public` 继承自基类时，派生类的派生类的对象才能使用向基类的转换  
	无论派生类如何继承自基类，**派生类的成员及友元**都能使用向基类的转换  
	对于**派生类的派生类的成员和友元**来说，是否能向基类转换取决于派生类的继承方式，如果派生类 `public` 或 `protected` 继承自基类，那么派生类的派生类的成员和友元仍然可以访问基类的保护和公有成员，就可以向基类转换  
	如果派生类 `private` 继承自基类，那么派生类的派生类的成员或友元就不能访问基类的任何成员了，自然不能向基类转换  
	总的来说，如果想在某个代码节点使用向基类的转换，应该判断在当前节点（派生类对象、派生类成员或友元、派生类的派生类的对象、派生类的派生类的成员或友元）是否能够访问基类的公有成员，下面来一一分析：  
	* 派生类的对象  
	由于派生类对象对基类的访问权限由派生访问说明符控制，所以当且仅当派生类是 `public` 继承自基类时，派生类的对象才能访问基类的公有成员，才能向基类转换。  
	* 派生类的成员或友元  
	派生类的成员或友元对基类的访问权限不受派生访问说明符控制，所以无论派生类如何继承自基类，派生类的成员或友元总能访问基类的公有成员，也总能向基类转换  
	* 派生类的派生类的对象  
	这时候，这个对象对基类的访问权限由两个派生访问说明符控制，所以只有派生类 `public` 继承自基类，派生类的派生类 `public` 继承自派生类，派生类的派生类的对象才能向基类转换  
	* 派生类的派生类的成员和友元  
	此时，这些成员和友元对基类的访问权限仅由派生类如何继承自基类决定，当派生类 `public` 或 `protected` 继承自基类时，基类的公有成员对于派生类的派生类的成员和友元来说是可访问的，因此可以使用向基类的转换  
* 继承中的类作用域  
	只需记住一点：派生类的作用域嵌套在基类作用域之中，通俗理解就是基类作用域包含派生类的作用域。  
	使用基类指针指向派生类对象时，**不能**通过这个指针直接调用派生类的成员  
# 第十六章 模板与泛型编程  
* 在模板定义中，模板参数列表**不能为空**  
* 可以将类型参数看作类型说明符，可以用来指定返回类型或函数的参数类型，以及在函数体内用于变量声明或类型转换  
* 除了定义类型参数，还可以在模板中定义非类型参数（nontype parameter）  
* **非类型模板参数**的模板**实参**必须是**常量表达式**  
* 编写泛型代码的两个原则：  
	模板中的函数参数是 `const`	 引用  
	函数体中的条件判断仅使用 `<` 比较运算  
* 模板程序应该尽量减少对实参类型的要求  
* 当编译器遇到一个模板定义时并不生成代码，只有当**实例化**出模板的一个特定版本时，编译器才会生成代码  
* 模板的头文件通常既包括声明也包括定义  
* **函数模板**和**类模板成员函数**的定义通常放在**头文件**中  
* 模板的设计者应该提供一个头文件，包含模板定义以及在类模板或成员定义中用到的所有名字的声明  
* 模板程序的大多数编译**错误在实例化期间报告**  
* 保证传递给模板的实参支持模板所要求的操作，以及这些操作在模板中能正确工作，是**调用者**的责任  
* 类模板是用来生成类的蓝图的  
* 一个类模板的每个实例都形成一个**独立**的类  
* 定义在类模板之外的成员函数必须以关键字 `template` 开始，后接类模板参数列表  
* 默认情况下，一个类模板的成员函数只有当程序用到它时才会实例化  
* 在类模板自己的作用域中，我们可以直接使用模版名而不提供实参  
* 当一个类包含一个友元声明时，类与友元各自是否是模板是相互无关的。如果一个类包含一个**非模板友元**，则该友元被授权可以访问**所有**模板的**实例**  
* 与函数参数相同，模板声明中的参数名称不必与定义时相同  
* 一个特定文件所需要的所有模板的声明通常一起放置在文件开始位置，出现于任何使用这些模板的代码之前  
* 当我们希望通知编译器一个名字表示类型时，必须使用关键字 `typename` ，而不能使用 `class`  
* 对于一个模板参数，只有当它右侧的所有参数都有默认实参时，它才可以有默认实参  
* 无论是普通类还是模板类，都可以包含本身是模板的成员函数，这种成员被称为成员模板，成员模板**不能是虚函数**  
* **显式实例化**可以避免因为在多个文件中生成同一模板的同一实例化时产生的不必要的开销  
* 实例化定义会实例化所有成员  、
* 之前学过，类模板的成员只有**在使用时**才会被实例化，所以用来实例化类模板的类型不一定要适用于类模板的所有成员，只要用某一类型实例化后，不使用那些不符合的成员就行。但是当使用显式实例化（也就是使用 `extern` 和集中实例化的方法）时，编译器并不知道我们会使用那些成员，所以它会将全部成员实例化，所以，当使用显式实例化时，所使用的类型必须能用于模板的所有成员  
* `shared_ptr` 不是将删除器直接保存为一个成员，因为删除器的类型知道运行时才知道。在一个 `shared_ptr` 的生存期中，我们可以随时改变其删除器的类型，通常，类成员的类型在运行时是不能改变的。因此，`shared_ptr` ** 不能直接保存删除器**  
* `unique_ptr`的删除器类型在编译时就知道，所以 `unique_ptr` 的删除器可以直接保存在其对象中  
* 从函数实参来确定模板实参的过程被称为**模板实参推断**  
* 模板函数通常不执行形参的类型转换，编译器通常会选择生成一个新的实例  
* 能在调用中应用于函数模板的类型转换包括如下两项  
	* `const` 转换：可以将一个非 `const` 对象的引用（或指针）传递给一个 `const` 的引用（或指针）形参  
	* 数组或函数指针转换  
* 将实参传递给带模板类型的函数形参时，能够自动应用的类型转换只有 **`const` 转换**及**数组或函数到指针的转换**  
* 如果函数参数类型不是模板类型，则对实参进行正常的类型转换  
* 显式模板实参  
* 如果模板函数的返回类型需要根据实参类型来推断，可以使用尾置返回类型 。首先说说为什么使用正常的返回形式不行，使用下面这个例子  
	`template<typename T> ??? &fcn(It beg,It end){return *beg;}`  
`???` 代表未知的返回类型，一个比较自然的想法是使用 `decltype(*beg)` ，可是在编译器遇到参数列表之前，`beg` 都是不存在的，因此不能用它来推断返回类型。使用尾置返回类型可以解决这个问题，因为尾置返回类型在参数列表之后，它可以使用函数的参数  

* 类型转换（type transformation）模板定义在 `type_traits` 头文件中  
* `remove_reference` 模板可以获得引用的类型  
* 当我们用函数模板初始化一个函数指针或者为一个函数指针赋值时，编译器使用**指针的类型来推算模板实参**  
* 引用折叠只能用于间接创建的引用的引用，如类型别名或模板参数  
* 关于中译版中的 **顶层** 和 **底层** `const`  
	* top-level const 顶层 ：`char *const x;` 即变量 `x` 本身不能改变  
	* low-level const 底层 :  `char const* x;` 指针指向的那个 `char` 型变量不能改变  
	top-level const 负责自己，low-level const 负责他人，合理 :-)  
* 当一个函数参数是模板类型参数的一个**左值引用**时（ `T&` ），则只能传递给它一个**左值**。实参可以是 `const` 类型，也可以不是，如果实参是 `const` 的，则 `T` 将被推断为 `const` 类型  
* 如果一个函数参数的类型是 `const T&` ，则我们可以传递给它任何类型的实参：一个对象、一个临时对象或是一个字面常量值。当函数参数本身是 `const` 时，`T` 的类型推断结果不会是一个 `const` 类型。  
* 当一个函数参数是一个**右值引用** （ `T&&` ）时，可以传递给它一个**右值**  

>假定 `i` 是一个 `int` 对象，我们可能认为 `f3(i)` (`template <typename T>void f3(T&&);`) 这样的调用是不合法的。毕竟，`i` 是一个左值，而通常我们不能将一个右值引用绑定到一个左值上。但是，C++语言在正常的绑定规则之外又定义了两个例外规则，允许这种绑定。这两个例外规则是 `move` 这种标准库设施正确工作的基础。  

* **第一个例外**规则影响右值引用参数的推断如何进行  
	当我们将一个**左值**传递给**右值引用参数**，且此右值引用指向模板类型参数时，编译器推断模板类型参数为实参的**左值引用类型**。因此调用 `f3(i)` 编译器推断 `T` 的类型为 `int&` ，而非 `int`  
* 通常，我们不能直接定义一个引用的引用。但是，通过类型别名或通过**模板类型参数**间接定义是可以的  
* **第二个例外**的绑定规则  
	如果我们间接创建一个引用的引用，则这些引用形成了“折叠”。**除了右值引用的右值引用**，所有引用会折叠成一个普通的**左值引用类型**  
	`X& &`、 `X& &&`、 `X&& &` 都折叠成类型 `X&`  
	`X&& &&` 折叠成 `X&&`  
* 这两个例外的引用规则导致了两个重要结果：  
	* 如果一个函数参数是一个指向模板类型参数的右值引用（如 `T&&` ），则它可以被绑定到一个左值上；且  
	* 如果实参是一个左值，则推断出来的模板实参类型将是一个左值引用，且函数参数将被实例化为一个左值引用参数（ `T&` ）  
* 以上两个规则暗示，我们可以将**任意类型的实参**传递给 `T&&` 类型的参数。
* 右值引用通常用于两种情况：**模板转发其实参**或**模板被重载**  
* 从一个左值 `static_cast` 到一个右值引用是允许的  
* 转发  
	某些函数需要将其一个或多个实参连同类型**不变地**转发给其他函数。在此情况下，我们需要保持被转发实参的**所有性质**  
* 通过将一个函数参数定义为一个指向模板类型参数的**右值引用**，我们可以保持其对应实参的所有类型信息。
	* 使用引用参数使得我们可以保持 `const` 属性，因为在引用类型中的 `const` 是 low-level const  ；
	* 使用右值引用，通过引用折叠就可以保持实参的左值/右值属性  
* 如果一个函数参数是指向模板类型参数的右值引用，它对应的实参的 `const` 属性和左值/右值属性将得到保持  
* 使用 `std::forward` 保持类型信息。其定义在utility头文件中。`forward` 必须通过显式模板实参来调用。`forward` 返回该类型的右值引用 。即，`forward<T>` 的返回类型是 `T&&`  
* 通常情况下，使用 `forward` 传递那些定义为模板类型参数的右值引用的函数参数  
* 通常不对 `std::move` 和 `std::forward` 使用 `using` 声明  
* 可变参数模板就是一个接受参数数目可变的模板函数或模板类  
* 可变数目的参数被称为参数包（parameter packet）  
	* 模板参数包（template parameter packet）  
	* 函数参数包（function parameter packet）  
* 对于可变参数模板，编译器会推断包中参数的数目  
* 使用 `sizeof...` 运算符可以得到参数包中参数的数目  
* 可变参数函数通常是**递归**的  
* 对于一个参数包，除了获取其大小外，我们能对它做的唯一的事情就是**扩展**（expand），这里应该理解为”展开“   
* 转发参数包的一个例子  

	```C++
	template<typename... Args>   
	void fun(Args&&... args)  
	{  
		work(std::forward<Args>(args)...);     
	}  
	```
	
    在这段代码里函数 `fun` 将参数包转发给 `work` ，`work` 调用中的扩展既扩展了模板参数包也扩展了函数参数包  


# 第十七章 标准库特殊设施  
* `tuple` 是类似 `pair` 的**模板**  
* 当我们希望将一些数据组合成单一对象，但又不想麻烦地定义一个新数据结构来表示这些数据， `tuple` 非常有用。（但是使用新建数据类型也不失为一种好方法，那样数据结构中的每个成员都有意义明确的名字）  
* >我们可以将 `tuple` 看作一个“快速而随意”的数据结构  
* 要访问一个 `tuple` 的成员，就要使用一个名为 `get` 的标准库函数模板  
* `auto book = get<0>(item);` 返回 `item` 的第一个成员，其它成员以此类推  
* `bitset` 类是用来处理位运算的  
* 正则表达式（regular expression）是一种描述字符序列的方法，是一种极其强大的计算工具  
* C++正则表达式库（RE库）定义在头文件regex中  
* `regex` 类表示一个正则表达式  
* 默认情况下，`regex` 使用的正则表达式语言是 ECMAScript  
* 在C++正则表达式中如果想要查询 `.` ，则需要写成 `\\.`  
* >需要意识到的非常重要的一点是，一个正则表达式的语法是否正确是在**运行时**解析的  
* 一个正则表达式是在运行时而非编译时编译的。该编译过程是一个非常慢的操作，因此应该避免使用不必要的正则表达式。特别是，如果在循环中使用正则表达式，则应该在循环外定义它，而不是每次循环都编译它  
* C++程序不应该使用库函数 `rand` ，而应使用 `default_random_engine` 类和恰当的分布类对象  
* 在C++中，使用随机数引擎（random-numbers engines）和随机数分布类（random-number distribution）生成随机数。引擎类可以生成 `unsigned` 随机数序列，一个分布类使用一个引擎类生成指定类型的、在给定范围内的、服从特定概率分布的随机数  
* 随机数引擎是**函数对象类**  
* 当我们说**随机数发生器**时，是指分布对象和引擎对象的组合  
* >一个给定的随机数发生器一直会产生相同的随机数序列。一个函数如果定义的局部的随机数发生器，应该将其（包括引擎和分布对象）定义为 `static` 的。否则，每次调用函数都会生成相同的随机数序列  
* `bernoulli_distrubution` 类是一个普通类，不是模板。此分布返回 `bool` 值，它返回 `true` 的概率默认是0.5，这个概率可以更改  
* 当操纵符（manipulator）改变流的格式状态时，通常改变后的状态对所有后续 `IO` 都生效  
* 操纵符 `boolalpha` 可以更改布尔值的输出形式（0/1 or false/true），`noboolalpha` 恢复默认状态  
* 操纵符 `hex` `oct` `dec` 可以更改整型值输入输出的格式（分别是十六进制、八进制和十进制）  
* 操纵符 `setprecision` 和其它接受参数的操纵符都定义在头文件 iomanip 中  
* 未格式化IO（unformatted IO）允许我们将一个流当作一个无解释的字节序列来处理  

# 第十八章 用于大型程序的工具  
* 异常处理（exception handling）  
* **栈展开**（stack unwinding）  
	当抛出一个异常后，程序暂停当前函数的执行过程并立即开始寻找与异常匹配的 `catch` 子句。当 `throw` 出现在一个 `try` 语句块内时，检查与该 `try` 块关联的 `catch` 子句。  如果找到了，就使用该 `catch` 语句处理异常。如果这一步没有找到，则退出当前的函数，在调用当前函数的外层函数中继续寻找。如果仍然没有找到匹配的 `catch` 语句，则退出当前这个主调函数，继续在调用了刚刚退出的这个函数的其他函数中寻找，以此类推。以上这个过程称为**栈展开**。如果一直没有找到匹配的 `catch` 语句，则程序退出主程序后终止。  
	当找不到匹配的 `catch` 子句，程序将退出并调用标准库函数 `terminate`   
* 栈展开过程中对象被**自动销毁**  
* >在栈展开的过程中，运行类类型的**局部对象**的**析构函数**。因为这些析构函数是自动执行的，所以它们不应该抛出异常。一旦在栈展开的过程中析构函数抛出异常，并且析构函数自身没能捕获到该异常，则程序将被终止  
* 编译器使用异常抛出表达式来对异常对象进行拷贝初始化  
* 当我们抛出一条表达式的时候，该表达式的静态编译时类型决定了异常对象的类型。这意味着如果一条 `throw` 表达式解引用一个基类指针，而该指针实际指向的是派生类对象，则抛出的对象将被切掉一部分，只有**基类部分被抛出**  
* 抛出指针要求在任何对应的处理代码存在的地方，指针所指的对象都必须存在  
* `catch` 子句的异常声明中声明的类型决定了处理代码所能捕获的异常类型，这个类型必须是**完全类型**  
* >通常情况下，如果 `catch` 接受的异常与某个继承体系有关，则最好将该 `catch` 的参数定义成引用类型  
* >如果在多个 `catch` 语句的类型之间存在着继承关系，则我们应该把继承链最低端的类（most derived type）放在前面，而将继承链最顶端的类（least derived type）放在后面  
* 一个重新抛出（rethrowing）语句并不指定新的表达式，而是将当前的异常对象沿着调用链向上传递  
* `catch(...)` 语句捕获**所有异常**  
* 处理**构造函数初始值异常**的唯一方法是将构造函数写成**函数 `try` 语句块**  
* **`noexcept`** 说明指定某个函数不会抛出异常  
* 命名空间（namespace）是为防止名字冲突提供的机制  
* 命名空间作用域后面**无须**分号  
* 命名空间可以定义在几个不同的地方  
