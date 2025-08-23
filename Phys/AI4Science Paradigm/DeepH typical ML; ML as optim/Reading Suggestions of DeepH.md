下面先给出一段整体概览，再按照**前置知识**与**阅读顺序**两大部分，提供你所需的背景补充、文章排序及重点阅读建议。

DeepH 系列工作始于 2021 年，利用消息传递神经网络（MPNN）直接学习 DFT 哈密顿量，绕过自洽迭代，大幅提升计算效率；随后，研究者陆续在**对称性保持**（E(3)-等变）、**局部坐标变换**、**混合泛函**、**实空间**、**材料数据库**以及**通用化大模型**等方向对原始架构进行拓展。要高效入门，你需先掌握 DFT 基础、图神经网络（GNN）、等变网络、混合泛函与实空间 DFT 的基本概念；之后按照文章发展脉络，由浅入深地阅读每篇论文，并重点关注各自的**网络架构创新**与**实验验证**。

---

## 前置知识

### 量子力学与 DFT 基础

- DFT 基于 Hohenberg–Kohn 定理，指出电子基态能量是电子密度的唯一定义泛函[物理评论链接管理器](https://link.aps.org/doi/10.1103/PhysRev.136.B864?utm_source=chatgpt.com)。
    
- Kohn–Sham 方法借助虚拟非交互电子体系，将多电子相互作用问题化为一组单电子方程，实用性极高[物理评论链接管理器](https://link.aps.org/doi/10.1103/PhysRev.140.A1133?utm_source=chatgpt.com)。
    

### 机器学习与图神经网络

- 图神经网络通过在原子图上**消息传递**（MPNN）机制学习原子与键的表示，已在化学与材料性质预测中取得突破性成果[arXiv](https://arxiv.org/abs/1704.01212?utm_source=chatgpt.com)。
    

### 等变神经网络

- 等变网络（如张量场网络）保持对三维空间**旋转**、**平移**与**置换**的等变性，省去复杂的数据增强与坐标标准化过程[arXiv](https://arxiv.org/abs/1802.08219?utm_source=chatgpt.com)。
    

### 混合泛函

- HSE（Heyd–Scuseria–Ernzerhof）混合泛函通过引入**屏蔽精确交换**，在准确性与计算成本间找到平衡，常用于半导体与过渡金属体系[物理评论链接管理器](https://link.aps.org/doi/10.1103/PhysRevB.80.115205?utm_source=chatgpt.com)。
    

### 实空间 DFT 方法

- 实空间 DFT 直接在物理空间网格上描述电子密度与势场，无需原子轨道基底，适合大规模并行与深度网络学习局部势能分布[arXiv](https://arxiv.org/abs/2407.14379?utm_source=chatgpt.com)。
    

---

## 阅读顺序与建议

1. ### DeepH（原始框架）
    
    - **论文**：arXiv:2104.03786 “Deep-Learning Density Functional Theory Hamiltonian”[arXiv](https://arxiv.org/abs/2104.03786?utm_source=chatgpt.com)
        
    - **建议**：先读引言与方法部分，弄清 MPNN 如何将原子结构映射到 DFT 哈密顿量；实验部分重点比较不同体系上与传统自洽 DFT 的效率与精度对比。
        
2. ### DeepH-E3（E(3)-等变网络）
    
    - **论文**：arXiv:2210.13955 “General framework for E(3)-equivariant neural network representation …”[arXiv](https://arxiv.org/abs/2210.13955?utm_source=chatgpt.com)
        
    - **建议**：深入网络构造章节，重点理解等变张量表示如何编码旋转、平移及自旋-轨道耦合对称性，及其在超大超胞（＞10⁴ 原子）上的性能优势。
        
3. ### DeepH-2（局部坐标变换器）
    
    - **论文**：arXiv:2401.17015 “DeepH-2: Enhancing … via an equivariant local-coordinate transformer”[arXiv](https://arxiv.org/abs/2401.17015?utm_source=chatgpt.com)
        
    - **建议**：关注局部坐标变换器的设计思想与实现细节，对比 DeepH-E3，思考二者在计算成本与模型复杂度上的取舍。
        
4. ### DeepH-hybrid（混合泛函扩展）
    
    - **论文**：Nature Commun. 15, 3245 (2024) / arXiv 相应预印本
        
    - **建议**：重点在训练数据准备与网络如何对 HSE06 泛函的哈密顿量进行参数化学习；对比原始 DeepH 在不同泛函下的适用性差异。
        
5. ### DeepH-r（实空间方法）
    
    - **论文**：arXiv:2407.14379 “Deep learning density functional theory Hamiltonian in real space”[arXiv](https://arxiv.org/abs/2407.14379?utm_source=chatgpt.com)
        
    - **建议**：研究势场网络架构及其如何在实空间捕捉“近视性”（nearsightedness）先验；比较实空间与基底展开方法的精度与效率。
        
6. ### DDHT（扭曲材料数据库）
    
    - **论文**：arXiv:2404.06449 “Deep-Learning Database of DFT Hamiltonians for Twisted Materials”[arXiv](https://arxiv.org/abs/2404.06449?utm_source=chatgpt.com)
        
    - **建议**：了解高通量计算流程、数据库构建策略及接口设计；结合自己的研究需求思考如何利用该数据库进行异质结构预测。
        
7. ### 通用材料模型 & 通用 Kohn–Sham 哈密顿量
    
    - **论文**：arXiv:2406.10536 “Universal materials model …”[arXiv](https://arxiv.org/abs/2406.10536?utm_source=chatgpt.com)
        
    - **论文**：arXiv:2402.09251 “Universal Machine Learning Kohn–Sham Hamiltonian for Materials”[arXiv](https://arxiv.org/html/2404.06449v1?utm_source=chatgpt.com)
        
    - **建议**：重点在**大规模训练策略**、**fine-tuning**方法及模型在多元素、多结构体系上的泛化能力评估。
        

> **阅读顺序由浅入深、由基础至前沿，既能快速掌握核心思想，又能系统了解各项改进与应用场景。祝你阅读顺利，学习有成！**