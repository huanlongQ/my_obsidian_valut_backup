# C++ and C++&Python counterpart

- [cpp-python counterpart](https://gemini.google.com/share/a5fda5cdc739)  

## Core differences 

- 动态静态类型(dynamic typing&static typing)
- 内存管理(automatic garbage collection&manual memory managementor smart ptr)
- 编译(解释型语言interpreter&编译型语言compiler)

## Syntax

- comment `#` `//, /*comment*/`
- var declaration `int someint = 1;`
	- `const int someint = 100`
- std lib `#include <somelib> ; std::cout<<"sometext"<<std::endl`
- if else ```if (some bool) {}```

## Data structure

![[Pasted image 20250808180901.png]] 

## Keywords

|                      |                                      |             |
| -------------------- | ------------------------------------ | ----------- |
| **Python**           | **C++**                              | **类别**      |
| class                | class, struct                        | 面向对象        |
| def                  | (无直接对应)                              | 函数定义        |
| return               | return                               | 函数          |
| if, elif, else       | if, else if, else                    | 控制流         |
| for, in              | for                                  | 循环          |
| while                | while                                | 循环          |
| break                | break                                | 循环控制        |
| continue             | continue                             | 循环控制        |
| and, or, not         | &&, `                                |             |
| is                   | (无直接对应, 通常用 == 或指针比较)                | 对象身份        |
| None                 | nullptr                              | 空值          |
| True, False          | true, false                          | 布尔值         |
| try, except, finally | try, catch, ... (通过 RAII 模拟 finally) | 异常处理        |
| import               | #include                             | 模块/库导入      |
| del                  | delete                               | 内存管理 (概念相关) |
| with                 | (无直接对应, RAII 设计模式)                   | 资源管理        |
| global, nonlocal     | (无直接对应, 通过引用/指针/类成员实现)               | 作用域         |
| assert               | assert                               | 断言          |
| lambda               | [](){}                               | 匿名函数        |
| yield                | co_yield (C++20 Coroutines)          | 生成器/协程      |

## `::` `->` `.` `&` `*` `(Type)Obj` 

![[Pasted image 20250808181216.png]] 

### python's `.`

- 成员访问: 用于访问`class & struct`的内部成员
	- `.` & `->` 
	- `.` for real `obj` instance or `obj` refence while `->` for `obj` as a ptr. 
- 作用域(scope)与命名空间(namespace)访问
	- `::`
- 内存地址与值(memory address value)
	- `&` `*` 

### 特别注意：`&` 和 `*` 的双重身份

您需要特别注意 `&` 和 `*` 在C++中有两种截然不同的含义，这取决于它们出现的位置：

**关键在于, `ptr`是个可变对象, 而`ref`是个不变对象, `ref`与`instance`在性质上没有质的区别.** 具体到业务实例上, 员工的mentor可变, 而company不可变(只有一个). 

- **`*`永远与`ptr`在同一侧, 而`&`永远与`ref`或`instance`在同一侧.** 

1. **在声明 (Declaration) 中**：它们是**类型修饰符**。
    
    - `int& ref = x;` // `&` 在这里表示 “`ref` 是一个 `int` 类型的**引用**”
        **引用(ref) $==$ 别名(alias)**
    - `int* ptr;` // `*` 在这里表示 “`ptr` 是一个 `int` 类型的**指针**”
        
2. **在表达式 (Expression) 中**：它们是**运算符**。
    
    - `ptr = &x;` // `&` 在这里是**取地址**运算符
        
    - `y = *ptr;` // `*` 在这里是**解引用**运算符 

## `(Type)Obj` 

#### **`(ViString)"*RST\n"` 里面的 `()` 是什么意思？**

这里的 `(ViString)` 是一种**强制类型转换 (Type Casting)**，具体来说是**C风格的类型转换**。

**核心作用**：明确地告诉编译器：“请把后面这个东西，当作 `ViString` 这种类型来处理。”

让我们分解来看：

- **`"*RST\n"`**: 这是一个**字符串字面量 (string literal)**。在C++中，它的原始类型是 `const char*`（指向一个常量字符的指针）。
    
- **`ViString`**: 这是NI-VISA库自己定义的一种类型。如果我们查看 `visa.h` 头文件，会发现它的定义类似于 `typedef char* ViString;`。它本质上就是一个 `char*`（指向字符的指针）。
    
- **`(ViString)"*RST\n"`**: 整个表达式的意思就是，将 `const char*` 类型的字符串字面量，强制转换为VISA函数所期望的 `ViString` (即 `char*`) 类型。

#### **为什么需要这样做？**

主要是为了**匹配函数签名**和**消除编译器警告**。

`viPrintf` 函数的第二个参数被定义为 `ViString` 类型。虽然 `const char*` 和 `char*` 非常接近，但它们在C++的类型系统中是不同的（一个指向常量，一个指向变量）。为了确保函数调用严格匹配其声明，并抑制编译器可能发出的关于“从`const char*`到`char*`的转换是不安全的”之类的警告，代码的作者在这里进行了显式的强制类型转换。

# 对象 Class

## public & private

在cpp中, `public`与`private`对`class`的`method`与`attr`进行了分类: 
- `public`: 可以由外部代码调用. 
- `private`: 不可由外部代码调用, 只能在`class {  }`内调用以构建该类. 
- [‎`public` and `private` - Gemini - C++ 连接 UTG932E 指南](https://g.co/gemini/share/b430840ed9e0) 

## 成员初始化列表(Member Initializer List) 

```cpp
MVCamera::MVCamera()
    : m_hDeviceHandle(nullptr),
    m_bIsGrabbing(false)
{
    // 构造函数中仅初始化变量
}
```

**核心作用**：在**构造函数的主体（即 `{}` 内部的代码）开始执行之前**，对类的成员变量进行**初始化 (Initialization)**。

让我们分解来看：

- **`:` (冒号)**: 在构造函数的参数列表 `(...)` 之后、函数体 `{` 之前，这个冒号是启动“成员初始化列表”的标志。
    
- **`resourceName(visa_address)`**: 这句的意思是：请用构造函数的输入参数 `visa_address` 来**直接初始化**成员变量 `resourceName`。
    
- **`defaultRM(VI_NULL)`**: 这句的意思是：请用 `VI_NULL` 这个值来**初始化**成员变量 `defaultRM`。
    
- **`instr(VI_NULL)`**: 同上，用 `VI_NULL` 来**初始化**成员变量 `instr`。
    
- **`,` (逗号)**: 当有多个成员需要初始化时，它们之间用逗号隔开。

#### **为什么这种写法更好？(初始化 vs. 赋值)**

您可能会想，为什么不这样写呢？

```cpp
// 另一种写法（赋值）
InstrumentControl::InstrumentControl(const std::string& visa_address) {
    resourceName = visa_address; // 赋值
    defaultRM = VI_NULL;         // 赋值
    instr = VI_NULL;             // 赋值
}
```

这两种写法看起来效果一样，但有着本质的区别：

- **成员初始化列表 (我们的代码)**: 执行的是**初始化**。这就像在造房子打地基时，就直接用“高强度混凝土”（`visa_address`）来浇筑地基（`resourceName`）。一步到位，效率最高。
    
- **在 `{}` 内赋值**: 执行的是**赋值 (Assignment)**。这就像先用“普通混凝土”（默认构造函数）把地基浇筑好，然后再把地基敲掉，重新用“高强度混凝土”（`visa_address`）浇筑一遍。多了一步不必要的操作。

对于 `std::string` 这样的复杂对象，使用初始化列表可以避免一次不必要的默认构造和一次赋值操作，效率更高。对于 `const` 成员或引用成员，则**必须**在初始化列表中进行初始化。因此，使用成员初始化列表是C++中公认的、更专业、更高效的编程实践。

# 典型cpp项目文件结构:

一个C++项目的文件结构，我们可以从两个不同的视角来看待：

- 库的引用逻辑是: `.h` $\to$ `.lib` $\to$ `.dll`
	- `.h`是header文件, 用于通知`.cpp`哪些函数可用. 它可以放在物理文件结构的`\external\include`中, 也可以放在其他`Path`. 
	- `.lib`是linker用于链接`.dll`的文件. 它可以放在物理文件结构的`\external\lib`中, 也可以放在其他`Path`. 
	- `.dll`是实际的代码库. 它一般放在某个`Path`中. 从`.lib` $\to$ `.dll`的寻址过程是由Windows按照特定搜索顺序完成的, 一般搜索空间包括当前目录`current working dir`(可以用`SetCurrentDirectory`修改)、`C:\Windows\System32`、`C:\Windows`, 也可以由VS的Linker加入`Delay Loaded DLLs`, 并用`SetDllDirectory / AddDllDirectory`在代码里动态添加`.dll`搜索路径. 

1. **物理结构 (Physical Structure)**: 文件和文件夹在您硬盘上的真实存储布局（您在Windows文件资源管理器里看到的样子）。
    
2. **逻辑结构 (Logical Structure)**: 您在Visual Studio的“解决方案资源管理器”中看到的虚拟组织结构。

这两者有关联，但**不一定完全相同**。

---

### 0. C++项目的配置

go to `.sln` **property,** set include and linker. 
![[Pasted image 20250812140431.png|295]] 

### **1. 典型C++项目的物理结构 (在文件资源管理器中)**

一个组织良好、可扩展的C++项目的物理目录结构，通常遵循“关注点分离”的原则。这样做的好处是让项目清晰、易于维护、方便团队协作和版本控制。

这是一个非常经典且推荐的结构：

```
MyProject/
│
├─── build/
│      # 这个文件夹用来存放所有编译生成的文件 (.obj, .exe, .dll等)。
│      # 源代码目录将保持干净。
│
├─── docs/
│      # 存放项目相关的文档，如需求文档、设计文档、用户手册等。
│
├─── external/  (或者叫 third_party, vendor)
│   │
│   ├─── include/
│   │      # 存放所有第三方库的头文件 (.h, .hpp)，例如 visa.h
│   │
│   └─── lib/
│          # 存放所有第三方库的链接文件 (.lib, .a)，例如 visa64.lib
│
├─── src/  (或者叫 source)
│   │
│   ├─── main.cpp
│   ├─── QtWidgetsApplication1.cpp
│   └─── QtWidgetsApplication1.h
│      # 项目的核心，存放所有您自己编写的源代码。
│
├─── .gitignore
│      # 如果使用Git进行版本控制，这个文件会告诉Git忽略哪些文件（比如整个build文件夹）。
│
└─── MyProject.sln
       # Visual Studio的解决方案文件，位于项目的根目录。
```

**这个结构的优点：**

- **清晰**: 您自己的代码 (`src`)、第三方依赖 (`external`)、生成产物 (`build`) 和文档 (`docs`) 完全分开，一目了然。
    
- **干净**: 编译时产生的大量中间文件都被隔离在 `build` 目录中，不会污染您的源代码区。
    
- **可移植**: 当您需要将项目发给别人或在另一台电脑上编译时，`external` 文件夹可以跟着一起走，对方不需要再单独安装这些依赖库。

---

### **2. Visual Studio的逻辑结构 (在“解决方案资源管理器”中)**

现在，我们来看看Visual Studio是如何“看待”这些文件的。VS的“解决方案资源管理器”提供的是一个**逻辑视图**，它使用**“筛选器”(Filter)** 来组织文件，主要是为了方便开发者查找。

**关键点：** VS中的“筛选器”文件夹**不一定**与硬盘上的物理文件夹一一对应。

一个典型的逻辑结构可能看起来是这样的：

```
解决方案 'MyProject' (1 个项目)
└─── MyProject
     │
     ├─── ▷ 外部依赖项 (External Dependencies)
     │      # VS自动识别并显示系统级的include文件
     │
     ├─── ▷ 头文件 (Header Files)  <- 这是一个筛选器
     │    │
     │    ├─── QtWidgetsApplication1.h   (来自物理目录 src/)
     │    └─── visa.h                    (来自物理目录 external/include/)
     │
     ├─── ▷ 源文件 (Source Files)  <- 这是一个筛选器
     │    │
     │    ├─── main.cpp                  (来自物理目录 src/)
     │    └─── QtWidgetsApplication1.cpp   (来自物理目录 src/)
     │
     └─── ▷ 资源文件 (Resource Files) <- 这是一个筛选器
```

**逻辑结构与物理结构的关系：**

- **分离**: 您可以看到，在逻辑结构中，`QtWidgetsApplication1.h` 和 `visa.h` 都被归类到了“头文件”这个筛选器下，尽管它们在硬盘上的物理位置完全不同。这纯粹是为了方便您查看。
    
- **桥梁**: 那么，编译器是如何知道去哪里找这些文件的呢？**桥梁就是我们之前一直在配置的项目属性！**
    
    - **`VC++目录 -> 包含目录`**: 您在这里添加 `external/include` 路径，就是告诉编译器：“除了默认路径，也请去这个物理文件夹里找头文件。”
        
    - **`VC++目录 -> 库目录`**: 您在这里添加 `external/lib` 路径，就是告诉链接器：“请去这个物理文件夹里找库文件。”

### **总结**

|方面|物理结构 (File Explorer)|逻辑结构 (Visual Studio)|
|---|---|---|
|**目的**|文件的**实际磁盘存储**和物理隔离|代码的**组织、分类与可视化**|
|**组织方式**|真实的文件夹 (Folder)|虚拟的“筛选器” (Filter)|
|**关系**|是项目的基础，决定了文件真实存在哪里|是项目的一种表现形式，方便开发者查看和管理|
|**如何连接**|**通过项目属性（包含目录、库目录等设置）将物理路径告知给逻辑项目**||
