# 2. Linux Comm
# 4. git

git is a version control and collaborative tool for projects. I do not need git now. 

# 5. TeNPy

[Introduction Overview of tenpy](https://tenpy.readthedocs.io/en/latest/intro/overview.html)
~~~
simulations: run the below. 
algotithms: like DMRG, TEBD, TDVP
models: like Hubbard, TFIM, Heisenberg
networks: like MPS, MPO
linalg
~~~

# 6. GPU and CPU

Absolutely — understanding **what GPUs _can’t_ do efficiently** is _crucial_ when writing high-performance code, especially for algorithms like the Wolff cluster update. Let’s break it down precisely and clearly.

---

## ✅ What GPUs _are great_ at:

GPUs excel at **SIMD** (Single Instruction, Multiple Data) workloads:

- Regular, large-scale numerical computation
    
- Uniform operations on arrays (e.g., matrix multiplication, CNNs)
    
- No or minimal branching (everyone does the same thing)
    
- High memory _throughput_ when access is **contiguous and aligned**

---

## ❌ What GPUs **cannot do efficiently**

### 1. **Irregular control flow (branching logic)**

- When threads in a warp (usually 32 threads) **diverge** (e.g., some go into `if`, others don't), the GPU **serializes** the branches.
    
- Example: `if spin == old_spin and rand < p_add:` — some threads might pass, some won’t → warp divergence → slow

🧠 Analogy: Like a group of people crossing a street together, but each one deciding to take a different path.

---

### 2. **Recursive or dynamic-sized operations**

- Cluster growth (like Wolff or BFS-style algorithms) grows **dynamically**.
    
- GPUs **prefer fixed-size operations** — anything like:
    
    - Growing lists
        
    - Variable iteration loops (`while len(queue) > 0:`)
        
    - Recursion ...is **bad fit**.

---

### 3. **Random memory access (non-contiguous loads/stores)**

- GPUs are fast when accessing data like: `spins[:, :, :]`
    
- But **scattered access** (e.g. using `nonzero` or `advanced indexing`) breaks memory coalescing.
    
- `spins[boundary_indices]` is **random** access — slow!

---

### 4. **Sparse and conditional updates**

- GPU excels at dense tensor operations.
    
- Updating just a subset of pixels (`spins[mask] = new_spin`) is inherently **serial** if:
    
    - the `mask` varies per item
        
    - the value depends on nontrivial logic

---

### 5. **Dynamic allocation inside GPU kernels**

- Python-side dynamic lists (like `cluster = [(x, y)]`) don’t exist on the GPU.
    
- You can’t just `.append()` inside a GPU kernel.
    
- Preallocating large enough buffers = wasteful and error-prone.

---

### 6. **Small workloads or small batches**

- If your tensor is small (e.g., `L = 32`) or `N` (batch size) is low, the overhead of launching GPU kernels can outweigh the benefits.
    
- CPU may win here, especially for irregular logic.

---

## Real Example: Wolff Algorithm Bottlenecks on GPU

|Step|Good for GPU?|Why?|
|---|---|---|
|Seed spin selection|✅|Uniform random access, easy to batch|
|Cluster mask + visited updates|❌|Irregular shape, dynamic growth|
|Roll for neighbors|⚠️|Causes memory shuffling|
|Conditional inclusion (rand < p)|❌|Branching logic per lattice site|
|torch.nonzero() + advanced index|❌|Non-contiguous, dynamic-size tensor|
|Spin flipping via mask|❌|Sparse write + mismatch in shape|

---

## TL;DR

> **GPUs are awesome at doing the same thing over a big regular grid.** But if your algorithm has **irregular paths, dynamic growth, or sparse updates**, it’ll probably be faster on **CPU**, unless you rework it into a form that hides these patterns.

---

If you want to extract more speed from the Wolff algorithm, you're much better off:

- Using per-lattice loops (batch-level parallelism)
    
- Or porting the cluster update logic to a C++/CUDA extension or Numba

Want to try a Numba version next to compare?

# 7. numba

# 8. Parallelization Scheme

## 8.1 `concurrent.futures.ProcessPoolExecutor`

~~~python 
from concurrent.futures import ProcessPoolExecutor

def my_task(i):
    # 任意复杂代码
    return i + 42

task_num = 100
core_num = 28

with ProcessPoolExecutor(max_workers=core_num) as executor:
    results = list(executor.map(my_task, range(task_num)))
~~~

## 8.2 `joblib.Parallel`

~~~python 
from joblib import Parallel, delayed

def my_task(i):
    # 你的复杂逻辑
    return i * i  # 示例

results = Parallel(n_jobs=100)(delayed(my_task)(i) for i in range(100))
~~~

# 9. code trick

## 9.1 工作文件调制与管理

* 旧有方案
	`name_head + bools`
	使用name_head命名相应文件, 以保证文件可管理. 
	使用bools来选择运行配置和缩放大块code. 
	工作文件调制与管理.
0. 一般而言, 一个project可以被分为几个部分. 因而我们需要global和local分立的管理模式
1. 这几个部分所调用的包、具体函数、类等, 我们放入一个proj_tools.py.
	使用下列code将该.py文件内的所有名字引用, 一般这里会是引用进一个.ipynb文件.
~~~python
import importlib
importlib.reload(proj_tools)
from proj_tools import *
~~~
2. 在.ipynb的第一个block内, 应该区分global的config variables和local的config variables. 
	global config: 
		date = '20250416'
		project_name = 'filearrangement'
		d = 
		L = 
		...
		name_head = f'{data}{project_name}d{d}L{L}_'
	
	part1 config:
		part1trialidx = 1
		config_variables = 
		part1name_head = f'{name_head}{part1trialidx}{config_variables}' 

## 9.2 读`help(obj)`

20250411, 今天学习了一下阅读help文档, 发现还是有一些用处的.
`help(obj)` 返回的是`__doc__`attribute, 即为docstring, """ """内的内容.  
具体而言, 阅读了`tenpy`的`TwoSiteDMRGEngine`的`help`文档. 
发现它的结构是: 
- parameters: 对象的传入直接参数. 
- options: 对象的传入间接参数, 用于配置整个obj. 
- returns: 返回值.  

## 9.3 debug方向

coding过程中, 极大一部分问题来自于各个理论之间细节config的对齐. 举例而言, fft的norm. 

# 10. openMP问题

## 一、问题现象

- 在运行包含 `torch` 与 `matplotlib.pyplot` 的脚本时，报错：
    
    vbnet
    
    复制
    
    `OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized.`
    
- 错误提示多个 OpenMP 运行时被加载，可能导致性能下降或结果不正确。

---

## 二、初步排查

1. **查看加载的 DLL**  
    在脚本中打印进程已加载的 DLL，筛选包含 `iomp` 或 `omp` 的条目。  
    结果发现：
    
    vbnet
    
    复制
    
    `…\torch\lib\cudnn_engines_precompiled64_9.dll   …\torch\lib\cudnn_engines_runtime_compiled64_9.dll   …\torch\lib\libiomp5md.dll   …\torch\lib\libiompstubs5md.dll`
    
    其中后两者均属于 Intel OpenMP 运行时。
    ![[Pasted image 20250416123103.png]]
    将第二个存根dll改名后仍旧没有解决问题
2. **确认 Matplotlib 后端**
    
    python
    
    复制
    
    `import matplotlib print(matplotlib.get_backend())  # 输出 tkagg`
    
    说明不是 Qt 绑定引入冲突。
    
3. **分步导入定位**  
    分别在 `import torch`、`import numpy`、`import matplotlib.pyplot` 之后打印日志，确定是 PyTorch 自带的 OpenMP runtime 在第一次导入时就已初始化。

---

## 三、解决方案

### 方案 1：环境变量“打补丁”（推荐）

在脚本最前面（任何库 import 之前）加入：

python

复制

`import os os.environ["KMP_DUPLICATE_LIB_OK"] = "TRUE"`

- **原理**：告诉 Intel OpenMP，即使检测到重复初始化，也不要报错，继续执行。
    
- **优点**：无需修改环境、DLL 或重新编译，最简单直接。
    
- **缺点**：仍有多重 runtime，可能略微影响性能或稳定性。

### 方案 2：移除存根 DLL（有风险）

1. 找到 PyTorch 的 DLL 目录（如 `…\envs\my_torch\Lib\site-packages\torch\lib\`）。
    
2. 将 `libiompstubs5md.dll` 重命名或移出（例如改名为 `.bak`）。
    
3. 重启 Python 并测试脚本。

- **风险**：如果存根库提供了必要符号，可能导致链接错误或功能异常。

### 方案 3：彻底重建环境（极端方案）

- 在 Linux 下自行编译 PyTorch，禁用 Intel MKL/OpenMP，改用 GNU OpenMP。
    
- 或寻找不带 Intel OpenMP 的 PyTorch 构建版本。

此方案复杂且耗时，通常不推荐。

---

## 四、最终推荐

> **在脚本最前面设置**
> 
> python
> 
> 复制
> 
> `import os os.environ["KMP_DUPLICATE_LIB_OK"] = "TRUE"`
> 
> 既能快速消除报错，又不会对现有环境做侵入式修改，是最实用的应急办法。
