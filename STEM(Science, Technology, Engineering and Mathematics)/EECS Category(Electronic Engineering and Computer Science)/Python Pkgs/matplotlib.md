
- [‎Gemini - Matplotlib 绘图心得与模板](https://g.co/gemini/share/5a4362c3a1f8)
-  [Quick start guide — Matplotlib 3.10.5 documentation](https://matplotlib.org/stable/users/explain/quick_start.html#quick-start)
- [Customizing Matplotlib with style sheets and rcParams — Matplotlib 3.10.5 documentation](https://matplotlib.org/stable/users/explain/customizing.html#customizing) 
- [Animations using Matplotlib — Matplotlib 3.10.5 documentation](https://matplotlib.org/stable/users/explain/animations/animations.html#animations) 
matplot has 2 kinds of coding style: `object oriented`, based on `figure and axes etc` and `pyplot` style. 

# matplot tutorial

![[Pasted image 20250815152647.png]] 

# 紧凑的子图写法 tight `ax` coding

**`GridSpec`大法好!!!**
```python
import matplotlib.gridspec as gridspec
```

## `Obj Oriented` style

### 1. Matplotlib 的基本概念

要掌握 Matplotlib，首先要理解两个最核心的对象：`Figure` 和 `Axes`。

- **`Figure` (画布)**：可以把它想象成是你要画画的那张**白纸或者画布**。它是所有绘图元素的顶级容器。一个 `Figure` 对象可以包含一个或多个 `Axes` 对象。你可以设置整张画布的大小、背景色等。
    
- **`Axes` (坐标系/子图)**：`Axes` 并不是指数学上的“坐标轴”（那是 `Axis`），而是指画布上的一个**独立的绘图区域**。我们所有的数据可视化操作，比如 `plot`（画线）、`scatter`（画散点）、`bar`（画柱状图），实际上都是在 `Axes` 对象上进行的。一个 `Figure` 上可以有多个 `Axes`，这就是子图的由来。

**一个常见的误区**： 很多初学者直接使用 `plt.plot()`、`plt.title()` 这样的函数。这被称为“状态机”写法。Matplotlib 在背后会默默地帮你找到“当前”的 `Axes` 来执行操作。这种方法在画单张简单图时很方便，但一旦涉及到多个子图，就很容易变得混乱，难以控制到底在哪张图上操作。

**我们的目标**： 采用“面向对象”的写法。明确地创建 `Figure` 和 `Axes` 对象，然后调用这些对象的方法来进行绘图和设置。这种方法逻辑更清晰，控制更精确，是编写复杂、可维护图形代码的**最佳实践**。

---

### 2. 最紧凑的 Matplotlib 写法心得：面向对象风格

这种写法的核心起点是 `plt.subplots()`。这个函数非常强大，它能同时创建一个 `Figure` 对象和一个（或多个）`Axes` 对象的 `numpy` 数组。

这是我推荐的“万能模板”，它覆盖了创建子图、在每个子图上绘图、以及精细调节参数的全过程。

#### 代码模板

```python
import matplotlib.pyplot as plt
import numpy as np

# ------------------- 1. 数据准备 (Data Preparation) -------------------
x = np.linspace(0, 2 * np.pi, 100)
y1 = np.sin(x)
y2 = np.cos(x)
y3 = x**2
y4 = np.random.rand(10) * 10

# ------------------- 2. 创建 Figure 和 Axes (The Core) -------------------
# 创建一个 2x2 的子图网格。
# fig 是整个画布对象。
# axs 是一个包含 4 个 Axes 子图对象的 2x2 NumPy 数组。
# figsize 控制整个画布的大小 (宽, 高)，单位是英寸。
# constrained_layout=True 会自动调整子图布局，防止标题、标签重叠，非常推荐！
fig, axs = plt.subplots(nrows=2, ncols=2, figsize=(10, 8), constrained_layout=True)

# ------------------- 3. 在指定的 Axes 上绘图和设置 -------------------
# ---- 子图 1: 左上角 (axs[0, 0]) ----
ax1 = axs[0, 0]
ax1.plot(x, y1, color='blue', linestyle='-', label='sin(x)')
ax1.set_title('正弦曲线 (Sine Wave)')
ax1.set_xlabel('X-轴 (rad)')
ax1.set_ylabel('Y-轴 (value)')
ax1.grid(True, linestyle='--', alpha=0.6) # 添加网格
ax1.legend() # 显示图例

# ---- 子图 2: 右上角 (axs[0, 1]) ----
ax2 = axs[0, 1]
ax2.scatter(x, y2, color='red', marker='x', label='cos(x)')
ax2.set_title('余弦散点图 (Cosine Scatter)')
ax2.set_xlabel('X-轴 (rad)')
# 右上角的 Y 轴标签可以省略，以保持简洁
# ax2.set_ylabel('Y-轴 (value)')
ax2.axhline(0, color='gray', linewidth=0.8) # 添加一条 y=0 的水平线
ax2.legend()

# ---- 子图 3: 左下角 (axs[1, 0]) ----
ax3 = axs[1, 0]
ax3.bar(['A', 'B', 'C', 'D'], [3, 5, 2, 7], color=['#FF5733', '#33FF57', '#3357FF', '#FF33A1'])
ax3.set_title('柱状图 (Bar Chart)')
ax3.set_ylabel('数量 (Quantity)')
ax3.tick_params(axis='x', rotation=45) # X轴刻度标签旋转45度

# ---- 子图 4: 右下角 (axs[1, 1]) ----
ax4 = axs[1, 1]
ax4.plot(y4, color='purple', marker='o', label='随机数据')
ax4.set_title('折线图与范围设定 (Line with Limits)')
ax4.set_ylim(0, 12) # 设定 Y 轴的显示范围
ax4.set_xlim(-1, 10) # 设定 X 轴的显示范围
ax4.legend()

# ------------------- 4. 全局设置和显示 -------------------
# 为整个 Figure 添加一个总标题
fig.suptitle('Matplotlib 核心写法演示', fontsize=16)

# 保存图像 (可选，可以保存为多种格式)
# plt.savefig('my_awesome_plot.png', dpi=300)

# 显示图像
plt.show()
```

#### 心得总结：

1. **统一入口**：永远从 `fig, axs = plt.subplots(...)` 开始。即使只画一张图（`fig, ax = plt.subplots()`），也保持这个习惯。
    
2. **明确对象**：通过索引（如 `axs[0, 0]`）获取你想要操作的那个 `Axes` 对象，然后所有针对该子图的操作都由这个对象的方法来完成（`ax.plot()`, `ax.set_title()` 等）。绝不混用 `plt.title()`。
    
3. **布局管理**：使用 `constrained_layout=True` 或在最后调用 `plt.tight_layout()` 来解决元素重叠问题，前者是更新、更推荐的方式。
    
4. **先局部后整体**：先在各个 `axs` 上完成各自的绘图和设置，最后再用 `fig` 对象进行全局设置（如 `fig.suptitle()`）。

---

### 3. 常用参数调节汇总（速查表）

以下是在 `Axes` 对象上最常用的一些设置方法。

|目标|方法|示例|
|---|---|---|
|**标题和标签**|||
|设置子图标题|`.set_title()`|`ax.set_title('My Plot', fontsize=12)`|
|设置 X 轴标签|`.set_xlabel()`|`ax.set_xlabel('Time (s)')`|
|设置 Y 轴标签|`.set_ylabel()`|`ax.set_ylabel('Temperature (°C)')`|
|**坐标轴范围**|||
|设置 X 轴范围|`.set_xlim()`|`ax.set_xlim(0, 10)`|
|设置 Y 轴范围|`.set_ylim()`|`ax.set_ylim(-1.5, 1.5)`|
|**刻度和刻度标签**|||
|设置 X 轴刻度|`.set_xticks()`|`ax.set_xticks([0, 5, 10])`|
|设置 Y 轴刻度|`.set_yticks()`|`ax.set_yticks([-1, 0, 1])`|
|设置 X 轴刻度标签|`.set_xticklabels()`|`ax.set_xticklabels(['Start', 'Mid', 'End'])`|
|设置 Y 轴刻度标签|`.set_yticklabels()`|`ax.set_yticklabels(['Low', 'Zero', 'High'])`|
|旋转刻度标签|`.tick_params()`|`ax.tick_params(axis='x', rotation=45)`|
|**图例 (Legend)**|||
|显示图例|`.legend()`|`ax.legend(loc='upper right')`|
|**网格 (Grid)**|||
|显示网格|`.grid()`|`ax.grid(True, linestyle=':', alpha=0.5)`|
|**辅助线**|||
|添加水平线|`.axhline()`|`ax.axhline(y=0, color='r', linestyle='--')`|
|添加垂直线|`.axvline()`|`ax.axvline(x=5, color='g', linestyle='--')`|
|**绘图函数内部参数**|(在 `plot`, `scatter` 等函数内)||
|颜色|`color`|`ax.plot(x, y, color='cyan')`|
|线条样式|`linestyle`|`ax.plot(x, y, linestyle='-.')`|
|线条宽度|`linewidth`|`ax.plot(x, y, linewidth=3)`|
|标记样式|`marker`|`ax.plot(x, y, marker='o')`|
|透明度|`alpha`|`ax.scatter(x, y, alpha=0.7)`|
|图例标签|`label`|`ax.plot(x, y, label='Data Series 1')`|

## `pyplot` style

### Pyplot 风格的核心思想

`pyplot` 风格的工作方式就像一个有记忆的画家。你告诉他“画条线”，他就在他**当前正在看的**那块画布（`Axes`）上画。你告诉他“写个标题”，他就在这块画布上写。

- **`plt.figure()`**: 相当于拿出一张新的大画布（`Figure`）。
    
- **`plt.subplot(nrows, ncols, index)`**: 这是 `pyplot` 风格处理子图的**关键**。它会做两件事：
    
    1. 在 `nrows` x `ncols` 的网格中，创建或**激活**第 `index` 个位置的子图（`Axes`）。`index` 从 1 开始，按从左到右、从上到下的顺序计数。
        
    2. 一旦激活，后续所有的 `plt.plot()`、`plt.title()` 等命令都会作用于这个刚刚被激活的子图上。

你需要通过反复调用 `plt.subplot()` 来切换当前要操作的子图。

---

### Pyplot 风格的代码示例 (2x2 子图)

让我们用 `pyplot` 风格重现之前的四宫格图。请注意代码结构的变化。

```python
import matplotlib.pyplot as plt
import numpy as np

# ------------------- 1. 数据准备 (和之前一样) -------------------
x = np.linspace(0, 2 * np.pi, 100)
y1 = np.sin(x)
y2 = np.cos(x)
y3 = x**2
y4 = np.random.rand(10) * 10

# ------------------- 2. 创建 Figure 和 子图 -------------------
# 首先，创建一个 Figure 画布
plt.figure(figsize=(10, 8))

# ---- 子图 1: 左上角 ----
# 激活 2x2 网格中的第 1 个位置。后续命令都作用于此。
plt.subplot(221) 
plt.plot(x, y1, color='blue', linestyle='-', label='sin(x)')
plt.title('正弦曲线 (Sine Wave)')
plt.xlabel('X-轴 (rad)')
plt.ylabel('Y-轴 (value)')
plt.grid(True, linestyle='--', alpha=0.6)
plt.legend()

# ---- 子图 2: 右上角 ----
# 激活 2x2 网格中的第 2 个位置。
plt.subplot(222)
plt.scatter(x, y2, color='red', marker='x', label='cos(x)')
plt.title('余弦散点图 (Cosine Scatter)')
plt.xlabel('X-轴 (rad)')
plt.axhline(0, color='gray', linewidth=0.8) # 添加水平线
plt.legend()

# ---- 子图 3: 左下角 ----
# 激活 2x2 网格中的第 3 个位置。
plt.subplot(223)
plt.bar(['A', 'B', 'C', 'D'], [3, 5, 2, 7], color=['#FF5733', '#33FF57', '#3357FF', '#FF33A1'])
plt.title('柱状图 (Bar Chart)')
plt.ylabel('数量 (Quantity)')
plt.xticks(rotation=45) # 旋转 X 轴刻度标签

# ---- 子图 4: 右下角 ----
# 激活 2x2 网格中的第 4 个位置。
plt.subplot(224)
plt.plot(y4, color='purple', marker='o', label='随机数据')
plt.title('折线图与范围设定 (Line with Limits)')
plt.ylim(0, 12)
plt.xlim(-1, 10)
plt.legend()


# ------------------- 3. 全局设置和显示 -------------------
# 添加总标题
plt.suptitle('Pyplot 风格演示', fontsize=16)

# 自动调整布局，防止重叠。在 pyplot 风格中尤其重要。
plt.tight_layout()

# 显示图像
plt.show()

```

## `ax`size adjustment under `OO` or `pyplot` style

### 1. Pyplot 风格 — 状态机方法 $\star \star \star$ 

**核心思想**：`matplotlib.pyplot` (通常简写为 `plt`) 维护一个内部“状态”，记录着当前活跃的 `Figure` 和 `Axes`。你不需要持有 `fig` 或 `ax` 对象，而是通过调用 `plt.subplot()` 来**切换**当前要操作的 `Axes`。后续的 `plt.plot()`、`plt.title()` 等函数都会自动作用于这个“当前”的 `Axes`。

**代码结构是线性的**：你必须先激活一个子图，然后完成它所有的绘图和设置，接着再激活下一个子图，继续操作。顺序非常重要。

```python
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec # 需要单独导入
import numpy as np

# --- 1. 准备数据 ---
x = np.linspace(0, 10, 100)

# --- 2. 创建 Figure 和 GridSpec ---
# 创建一个 Figure，它会自动成为“当前 Figure”
plt.figure(figsize=(10, 6))
plt.suptitle('Pyplot Style - State-Machine Approach', fontsize=16)

# 定义一个 2x2 的网格系统
# 注意：这里的 gs 没有和任何 Figure 对象关联，它将在 plt.subplot 中被使用
gs = gridspec.GridSpec(2, 2, width_ratios=[2, 1])


# --- 3. 激活子图 -> 绘图 -> 切换到下一个 ---
# 激活第一个子图 (占据所有行的第0列)，它成为“当前 Axes”
plt.subplot(gs[:, 0])

# 以下所有 plt 命令都作用于上面这个子图
plt.plot(x, np.sin(x), 'b')
plt.title('Large Subplot')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.grid(True)


# 激活第二个子图 (占据第0行的第1列)，它成为新的“当前 Axes”
plt.subplot(gs[0, 1])

# 以下所有 plt 命令都作用于这个新的子图
plt.plot(x, np.cos(x), 'r')
plt.title('Top-Right Subplot')
plt.grid(True)


# 激活第三个子图 (占据第1行的第1列)，再次切换“当前 Axes”
plt.subplot(gs[1, 1])

# 以下所有 plt 命令都作用于这个最新的子图
plt.scatter(np.random.rand(20)*10, np.random.rand(20), c='g', marker='^')
plt.title('Bottom-Right Subplot')
plt.grid(True)


# --- 4. 调整布局并显示 ---
plt.tight_layout()
plt.show()
```

### 2. 面向对象 (OO) 风格 — 推荐的最佳实践

**核心思想**：先创建“画布” `Figure` 对象，它是一切的容器。然后，使用这个 `fig` 对象的方法（如 `fig.add_gridspec` 和 `fig.add_subplot`）来精确地在画布上添加和管理各个“坐标系” `Axes` 对象。所有的绘图和设置都通过调用具体的 `ax` 对象的方法来完成。

**代码结构清晰**：先定义好所有 `Axes` 对象 (`ax1`, `ax2`, `ax3`)，然后再分别对它们进行内容填充。你可以随时回到任何一个 `ax` 对象上进行修改，顺序无关紧要。

```python
import matplotlib.pyplot as plt
import numpy as np

# --- 1. 准备数据 ---
x = np.linspace(0, 10, 100)

# --- 2. 创建 Figure 和 GridSpec (网格系统) ---
# 创建一个 Figure 对象，把它想象成我们的“画布”
fig = plt.figure(figsize=(10, 6))
fig.suptitle('OO Style - Object-Oriented Approach', fontsize=16)

# 在 Figure 对象上定义一个 2x2 的网格系统 (GridSpec)
# width_ratios=[2, 1] 表示第一列的宽度是第二列的 2 倍
gs = fig.add_gridspec(2, 2, width_ratios=[2, 1])

# --- 3. 在网格上创建 Axes 对象 ---
# ax1 占据所有行 (:) 的第 0 列
ax1 = fig.add_subplot(gs[:, 0])

# ax2 占据第 0 行的第 1 列
ax2 = fig.add_subplot(gs[0, 1])

# ax3 占据第 1 行的第 1 列
ax3 = fig.add_subplot(gs[1, 1])


# --- 4. 在各自的 Axes 对象上进行绘图和设置 ---
# 对 ax1 操作
ax1.plot(x, np.sin(x), 'b')
ax1.set_title('Large Subplot (ax1)')
ax1.set_xlabel('X-axis')
ax1.set_ylabel('Y-axis')
ax1.grid(True)

# 对 ax2 操作
ax2.plot(x, np.cos(x), 'r')
ax2.set_title('Top-Right Subplot (ax2)')
ax2.grid(True)

# 对 ax3 操作
ax3.scatter(np.random.rand(20)*10, np.random.rand(20), c='g', marker='^')
ax3.set_title('Bottom-Right Subplot (ax3)')
ax3.grid(True)


# --- 5. 调整布局并显示 ---
fig.tight_layout()
plt.show()
```

---

# `animation`
