# Others

- [大佬们编程一直是这样吗？？](https://www.zhihu.com/question/640637395) 先天编程圣体的思路. 
- [你的编程能力从什么时候开始突飞猛进?](https://www.zhihu.com/question/356351510/answer/111955045382?share_code=12KySEdAJpZj8&utm_psn=1938641334824067232) 各类**编程思想小汇总**. 
- [‎Gemini - Functional Programming](https://g.co/gemini/share/6ff4f0d80145)
- [Code Review](https://www.zhihu.com/question/41089988/answer/1947781098454123225?share_code=xgRSGmeymx8J&utm_psn=1947815802477744215)

# 面向对象 Object Oriented Programming

-  [为什么拥有C语言基础的人，依然学不会C++](https://www.zhihu.com/question/647517330/answer/1941522151241941686?share_code=2OKCoCdTfPg7&utm_psn=1941618348803733059)  
	**第一个坎：从“上帝视角”到“放权让对象自己管自己”, 一切操作通知对象来执行.**  
- [面向对象中的继承真的几乎“一无是处”吗？](https://www.zhihu.com/question/547885140/answer/2623928543?share_code=Y82VVMUGrzrM&utm_psn=1938751088653210101) 
	1) 继承过于强大, 过于奇异, 难以把握. 可能出现编译器无法完成类型检查的继承关系. 
	2) **面向组件编程**是解决面向对象中继承的方法. 
		Distinction from Object-Oriented Programming (OOP):
		While COP builds upon OOP principles, it differs in its level of abstraction and focus. OOP typically focuses on the design and interaction of individual objects and classes, often **emphasizing inheritance and polymorphism at a granular level**. COP, on the other hand, deals with **larger, more abstract units (components) that may be composed of multiple classes and objects**, with an **emphasis on loose coupling and independent deployment**.

# 函数书写

- 保证一个函数只做一件事, 避免内部步骤. 
	e.g.
	下面这个函数实现了输入调制函数及其系数、实空间array、中心频率、高斯系数、batch_size并输出生成信号频谱. 
	它内部做了两件事: 
	1) 生成信号
	2) 生成信号的频域分布
	这是不好的. 
	
	另外, **它的接口依赖于具体而不是依赖于抽象**, 这也是不好的. 
    ```python    
	# --- 1. 信号生成函数 (基本无需改动) ---
	def generate_spectrum_torch_batched(mod_func, poly_coeffs, x, f0, alpha_envelope, batch_size):
	    """根据指定的调制函数和系数，并行生成一批信号的频谱"""
	    num_samples = len(x)
	    y_mod = mod_func(x, poly_coeffs) # Use the passed modulation function
	    env = envelopeFunc(alpha_envelpoe=alpha_envelope, x=x)
	    freq = f0 + y_mod
	    noise = torch.randn(batch_size, num_samples, device=device) * error_distance
	    sig = torch.cos(2 * torch.pi * freq * (x + noise)) * env
	
	    x_freq = torch.fft.fftfreq(num_samples, d=x[1]-x[0], device=device)
	    x_freq = torch.fft.fftshift(x_freq)
	    
	    freq_sig_batch = torch.fft.fft(sig, dim=1)
	    freq_sig_batch = torch.fft.fftshift(freq_sig_batch, dim=1)
	    freq_sig_batch = torch.abs(freq_sig_batch)
	    
	    max_vals = torch.max(freq_sig_batch, dim=1, keepdim=True).values
	    freq_sig_batch = freq_sig_batch / (max_vals.detach() + 1e-9)
	    
	    return x_freq, freq_sig_batch
    ```
- **接口传参依赖于抽象, 而不应该依赖于具体.** [[6A proj management|@6A proj management]] 's Architecture step. 
	依赖于抽象的点有:
	1) 数值计算中, 应当把整个数据结构(如Gaussian函数ndarray)传输出来, 而不是数据结构的参数(Gaussian $\sigma$)传输出来, 以便于更换函数.  
	2) 使用`dict[string->types.FunctionType]`传输函数时, 换函数不需要换一大堆具体参数`arg`. 
	e.g.
	**它的接口依赖于具体而不是依赖于抽象**, 这也是不好的. 
    ```python    
	# --- 1. 信号生成函数 (基本无需改动) ---
	def generate_spectrum_torch_batched(mod_func, poly_coeffs, x, f0, alpha_envelope, batch_size):
	    """根据指定的调制函数和系数，并行生成一批信号的频谱"""
	    num_samples = len(x)
	    y_mod = mod_func(x, poly_coeffs) # Use the passed modulation function
	    env = envelopeFunc(alpha_envelpoe=alpha_envelope, x=x)
	    freq = f0 + y_mod
	    noise = torch.randn(batch_size, num_samples, device=device) * error_distance
	    sig = torch.cos(2 * torch.pi * freq * (x + noise)) * env
	
	    x_freq = torch.fft.fftfreq(num_samples, d=x[1]-x[0], device=device)
	    x_freq = torch.fft.fftshift(x_freq)
	    
	    freq_sig_batch = torch.fft.fft(sig, dim=1)
	    freq_sig_batch = torch.fft.fftshift(freq_sig_batch, dim=1)
	    freq_sig_batch = torch.abs(freq_sig_batch)
	    
	    max_vals = torch.max(freq_sig_batch, dim=1, keepdim=True).values
	    freq_sig_batch = freq_sig_batch / (max_vals.detach() + 1e-9)
	    
	    return x_freq, freq_sig_batch
	```
- 参数`arg`应该控制输出端, 而不是控制输入端. 
	这里的参数`amp_noise:ndarray`的`amp`直接控制了输出端的`amp`, 因而我不需要多次调试`amp_noise`的`amp`来实现对`amplitude_norm_noise: ndarray`的精确控制. 
	```python
	def amplitude_norm_noise(amp_noise: np.ndarray, cutoff_freq: float, sample_rate: float) -> np.ndarray:
	    """
	    Filters noise, conserving its original maximum absolute amplitude.
	    """
	    filtered_signal = direct_filter_noise(amp_noise, cutoff_freq, sample_rate)
	    
	    original_max_amplitude = np.std(np.abs(amp_noise), axis=-1, keepdims=True)
	    filtered_max_amplitude = np.max(np.abs(filtered_signal), axis=-1, keepdims=True)
	    
	    normalization_factor = original_max_amplitude / (filtered_max_amplitude + 1e-9)
	    
	    return filtered_signal * normalization_factor
	```

# Functional Programming (FP)

- [‎Gemini - Functional Programming](https://g.co/gemini/share/6ff4f0d80145) 

函数式编程（Functional Programming, FP）是一种编程范式，它将计算视为数学函数的求值，并强调**无副作用**和**不可变性**。它的核心理念是使用一系列纯粹、独立的函数来处理数据，从而让代码更可预测、更易于测试。

---

### 1. 纯函数（Pure Functions）

这是函数式编程的基石。一个纯函数必须同时满足以下两个严格条件：

- **引用透明（Referential Transparency）**：对于相同的输入，它总是产生相同的输出。这意味着它不依赖任何外部状态，例如全局变量、用户输入或系统时间。
    
- **无副作用（No Side Effects）**：它不修改任何外部状态。常见的副作用包括：
    
    - 改变全局变量。
        
    - 修改传入的参数。
        
    - 执行 I/O 操作（例如打印到控制台、读写文件或网络请求）。
        
    - 依赖或改变数据库状态。

纯函数的优点在于其可预测性，这让代码像数学公式一样稳定可靠，极大地简化了调试和测试过程。

---

### 2. 不可变性（Immutability）

函数式编程的核心原则之一是数据一旦创建就不能被修改。如果需要“更改”数据，你必须创建一个新的、修改过的数据副本。这种做法消除了程序中**可变状态**带来的复杂性，而可变状态是大多数程序 bug 的根源。不可变性尤其适用于并发编程，因为它允许多个线程安全地访问相同的数据，而不用担心数据被意外修改。

---

### 3. 一等公民函数（First-Class Functions）

在函数式编程中，函数被视为“一等公民”，与任何其他数据类型（如整数、字符串、列表）具有相同的地位。这意味着你可以像对待任何变量一样处理函数：

- **将函数赋值给变量**。
    
- **将函数作为参数传递给其他函数**。
    
- **将函数作为另一个函数的返回值**。

这个特性为构建高度抽象和灵活的程序提供了基础，使得**高阶函数**成为可能。

---

### 4. 高阶函数（Higher-Order Functions）

高阶函数是函数式编程中一种强大的抽象工具，它能将函数的行为作为参数进行传递。一个高阶函数满足以下两个条件之一：

- **接受一个或多个函数作为参数**：这种模式能将核心数据处理逻辑（如迭代）与具体操作（如平方或过滤）分离开来。例如，Python 中的 `map()`, `filter()`, `sorted()` 都是典型的高阶函数。
    
- **返回一个函数**：这种模式通常用于创建**函数工厂**(函数工厂创建一个闭包)，根据给定的参数动态地生成新的、可配置的函数。

---

### 5. 闭包（Closures）⭐

**闭包与类高度相似.**
**`closures are the poor man's object`**

闭包是一种特殊的高阶函数，它能**记住外部函数作用域中的变量**，即使外部函数已经执行完毕并返回。

- **实现机制**：闭包由一个内部函数构成，这个内部函数引用了外部函数作用域的变量，并由外部函数返回。
    
- **主要作用**：闭包能将 **数据（外部变量）** 和 **行为（内部函数）** 封装在一起，提供了一种无需使用类的轻量级**依赖注入**方式。**这使得你可以预先配置一个函数，并在需要时调用它，而不用重复传递配置参数**。

```python
import time
# A simple class with an internal, mutable state
class Counter:
    def __init__(self, initial_value):
        self.value = initial_value

    def increment(self):
        self.value += 1
        return self.value

def create_counter_step_closure(counter_instance: Counter): # -> 这是一个"函数工厂"⭐ 这里的Counter Type annotation用于使IDE理解Counter的attr与method. ⭐
    """
    A function factory that returns a closure.
    The closure depends on the 'counter_instance' passed to the factory.
    """
    def count_and_log():
        """
        The closure function. It accesses the state of 'counter_instance'.
        """
        # The inner function can directly access the outer function's
        # parameter, which is the specific instance of Counter.
        current_time = time.strftime("%H:%M:%S")
        
        # Access and modify the instance's attribute directly.
        new_value = counter_instance.increment()

        print(f"[{current_time}] Counter's value is now: {new_value}")
    
    return count_and_log # -> 这里return的是一个闭包⭐




# --- Main Program ---
if __name__ == '__main__':
    # 1. Create a specific instance of the Counter class
    my_counter = Counter(initial_value=10)

    # 2. Pass the instance to the function factory to create a closure ⭐⭐⭐
    # The returned 'my_count_step' remembers this specific 'my_counter' object.
    my_count_step = create_counter_step_closure(my_counter)

    # 3. Call the closure multiple times.
    # It will use and update the *same* 'my_counter' instance each time.
    print("Executing the closure...")
    my_count_step()  # Output: [HH:MM:SS] Counter's value is now: 11
    time.sleep(1)
    my_count_step()  # Output: [HH:MM:SS] Counter's value is now: 12
    time.sleep(1)
    my_count_step()  # Output: [HH:MM:SS] Counter's value is now: 13
```

```python
import torch
from typing import Callable

# Assuming SimConfig class is defined elsewhere, for example purposes:
class SimConfig:
    def __init__(self, mod_func_type: str, x_length: float, grating_domain_length: float):
        self.mod_func_type = mod_func_type
        self.x_length = x_length
        self.grating_domain_length = grating_domain_length


def make_mod_func(config: SimConfig) -> Callable[[torch.Tensor, torch.Tensor], torch.Tensor]: #⭐⭐⭐这个函数实在写得是太好啦!!!
    """
    一个函数工厂，根据配置类型返回一个预配置的调制函数闭包。
    
    这个函数封装了所有调制函数，并利用闭包将配置参数绑定到内部函数中，
    从而简化了外部调用接口。
    """
    if config.mod_func_type == 'polynomial':
        # 多项式函数不依赖于 config 的特定数值参数，可以直接返回一个纯函数。
        return lambda x, coeffs: torch.matmul(torch.vander(x, N=len(coeffs), increasing=True), coeffs)

    elif config.mod_func_type == 'chebyshev':
        # 闭包会捕获并使用 config.x_length 的值
        x_length = config.x_length
        def chebyshev_mod_func(x: torch.Tensor, coeffs: torch.Tensor) -> torch.Tensor:
            x_scaled = x / (x_length / 2.0)
            n = len(coeffs)
            cheby_basis = torch.zeros(len(x_scaled), n, device=x.device)
            if n > 0: cheby_basis[:, 0] = torch.ones_like(x_scaled)
            if n > 1: cheby_basis[:, 1] = x_scaled
            for i in range(2, n):
                cheby_basis[:, i] = 2 * x_scaled * cheby_basis[:, i-1] - cheby_basis[:, i-2]
            return torch.matmul(cheby_basis, coeffs)
        return chebyshev_mod_func

    elif config.mod_func_type == 'rbf_bspline':
        # 闭包会捕获并使用 config.grating_domain_length 的值
        grating_domain_length = config.grating_domain_length
        def rbf_mod_func(x: torch.Tensor, coeffs: torch.Tensor) -> torch.Tensor:
            num_basis_funcs = len(coeffs)
            centers = torch.linspace(-0.5 * grating_domain_length, 0.5 * grating_domain_length, num_basis_funcs, device=x.device)
            width = 2 * (grating_domain_length / num_basis_funcs)
            basis_funcs = torch.exp(-((x.unsqueeze(1) - centers) / width)**2)
            return torch.matmul(basis_funcs, coeffs)
        return rbf_mod_func

    elif config.mod_func_type == 'fourier':
        x_length = config.x_length
        def fourier_mod_func(x: torch.Tensor, coeffs: torch.Tensor) -> torch.Tensor:
            x_scaled = (x / (x_length / 2.0)) * torch.pi
            num_pairs = (len(coeffs) - 1) // 2
            y = coeffs[0] * torch.ones_like(x_scaled)
            for n in range(1, num_pairs + 1):
                a_n = coeffs[2*n - 1]
                b_n = coeffs[2*n]
                y = y + a_n * torch.cos(n * x_scaled) + b_n * torch.sin(n * x_scaled)
            return y
        return fourier_mod_func

    else:
        raise ValueError(f"Unknown modulation function type: {config.mod_func_type}")
```

### **闭包vs类**:

#### 核心区别：设计理念

**`closures are the poor man's object`**
- **闭包** 的设计理念是 **"行为与环境的绑定"**。它主要用于将一个函数与其创建时的特定数据（环境）打包在一起。闭包更侧重于功能，常用于一次性的、轻量级的任务或作为其他函数的配置工具。
    
- **类** 的设计理念是 **"数据与行为的封装"**。它是一个蓝图，用于创建对象。类通过属性来表示数据（状态），通过方法来表示行为，并将它们组织在一个单一的、可实例化的实体中。类更适合描述具有复杂状态和多种交互行为的实体。

#### 主要功能对比 (都不重要)

---

###### 1. 状态管理

- **闭包**：闭包通过捕获外部函数的局部变量来管理状态。这些状态对外部是不可见的，但可以被闭包内部的函数访问和修改。这种方式非常适合管理单一或少量状态变量。
    
- **类**：类通过实例属性（`self.variable`）来管理状态。这些状态是对象的一部分，可以在多个方法之间共享。类天然地支持管理复杂、多样的状态。

##### 2. 继承与多态

- **闭包**：闭包不支持继承。如果你想创建一个行为相似但有细微差别的闭包，你需要重新创建一个新的函数工厂。
    
- **类**：类是面向对象编程的基础，支持继承、多态和接口。这让你可以轻松地创建具有共享基类的新对象类型，并重用或扩展其行为。

##### 3. 代码组织

- **闭包**：通常作为函数内部的局部函数存在，代码结构相对扁平，易于理解其作用域。它们更适合作为轻量级的、一次性使用的工具。
    
- **类**：将相关的数据和方法封装在一个独立的命名空间（类）中。这种结构非常适合构建大型、复杂的程序，因为它能有效组织代码并防止全局命名空间的污染。

##### 4. 性能与内存

- **闭包**：创建闭包的开销通常比实例化类要小。然而，每个闭包都会在内存中保留对其捕获变量的引用，如果创建大量闭包，可能会占用更多内存。
    
- **类**：创建类的实例时，Python 会为每个实例分配内存来存储其属性。对于大量实例，类的内存管理通常更高效。

##### 结论

选择闭包还是类，取决于你的具体需求：

- **用闭包**：当你需要一个轻量级的、功能单一的函数，并且该函数需要记住一两个配置值或状态时。典型的例子是装饰器、函数工厂和回调函数。
    
- **用类**：当你需要描述一个具有复杂状态和多种相关行为的实体，并且希望利用继承、多态等面向对象特性来组织代码时。

总而言之，闭包是**行为的封装**，而类是**状态和行为的封装**。理解这个核心差异，能帮助你做出更明智的设计选择。

---

### 6. 其他高级概念

- **声明式编程（Declarative Programming）**：这种编程风格侧重于描述**做什么**，而不是**如何做**。它更关注结果而非过程，通常通过高阶函数来描述数据转换。
    
- **递归（Recursion）**：在没有可变循环状态的情况下，递归（函数调用自身）是实现迭代和处理数据的主要方式。
    
- **惰性求值（Lazy Evaluation）**：仅在真正需要时才进行计算。这能优化程序的性能和内存使用，尤其是在处理大型或无限数据集时。Python 中的生成器和迭代器就是惰性求值的例子。
