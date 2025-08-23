# 1. Tensor Networks for Interpretable and Efficient Quantum-Inspired Machine Learning
Introduce TN, feature mapping, Modeling, and ML by Quantum computation. 
## 1.1 Feature Mapping

$$
∣ ψ ⟩ = \frac{1}{Z}    ∑ _ m x_m ∣ φ_m ⟩
$$
or
$$
|x_{m}> = \cos(\pi x_{m} / 2)|0> + \sin(\pi x_{m}/2)|1>
$$

## 1.2 Parameterized modeling and Quantum Probabilistic *Interpretation*. TN for ML
entanglement entropy, quantum mutual information, quantum correlations, decoherence and controllability of quantum systems can be used for ML interpretation. 
## 1.3 Quantum inspired TN ML with quantum computation. For *efficiency*. 
VQA perchasing high fidelity quantum state shows a similar scheme to backforwad propagation. 

# 2. Visualizing Quantum Phases And Identifying Quantum Phase Transitions By Nonlinear Dimensionality Reduction
Steps: 
1. DMRG $\to$ Ground States of a Quantum System. $\mathcal{H}$
2. unsupervised machine learning: $\mathcal{H}\to \mathcal{R}^{2}$ from the quantum states to a 2D feature space
	Our proposal is to probe the ground states (GS) distribution in Hilbert space (denoted as H) by the unsupervised nonlinear dimensionality reduction (DR) scheme19–24 known as **t-distributed stochastic neighbor embedding (t-SNE)** 
	and then, we use naked eyes or classical classification algos like **k means** to classify the phases. 

Key point: 
1. Unsupervised training. 
2. Ground States Learning. 

**Related:** 
- ## Certification of quantum states with hidden structure of their bitstrings
    
    |   |   |
    |---|---|
    |条目类型|期刊文章|
    |作者|O. M. Sotnikov|
    |作者|I. A. Iakovlev|
    |作者|A. A. Iliasov|
    |作者|M. I. Katsnelson|
    |作者|A. A. Bagrov|
    |作者|V. V. Mazurenko|
    |摘要|Abstract The rapid development of quantum computing technologies already made it possible to manipulate a collective state of several dozens of qubits, which poses a strong demand on efficient methods for characterization and verification of large-scale quantum states. Here, we propose a numerically cheap procedure to distinguish quantum states which is based on a limited number of projective measurements in at least two different bases and computing inter-scale dissimilarities of the resulting bit-string patterns via coarse-graining. The information one obtains through this procedure can be viewed as a ‘hash function’ of quantum state—a simple set of numbers which is specific for a concrete wave function and can be used for certification. We show that it is enough to characterize quantum states with different structure of entanglement, including the chaotic quantum states. Our approach can also be employed to detect phase transitions in quantum magnetic systems.|
    |日期|2022-04-22|
    |语言|en|
    |文库编目|DOI.org (Crossref)|
    |网址|[https://www.nature.com/articles/s41534-022-00559-7](https://www.nature.com/articles/s41534-022-00559-7)|
    |访问时间|2025/4/6 12:38:48|
    |其他|JCR分区: Q1 中科院分区升级版: 物理与天体物理1区 影响因子: 6.6 5年影响因子: 8.0 EI: 是|
    |卷次|8|
    |页码|41|
    |刊名|npj Quantum Information|
    |DOI|[10.1038/s41534-022-00559-7](http://doi.org/10.1038/s41534-022-00559-7)|
    |期号|1|
    |刊名简称|npj Quantum Inf|
    |ISSN|2056-6387|
    |添加日期|2025/4/6 12:38:48|
    |修改日期|2025/4/6 12:38:49|
    
    ### 附件
    
    - Sotnikov 等 - 2022 - Certification of quantum states with hidden structure of their bitstrings.pdf
- ## Exploring phases of the su-schrieffer-heeger model with tSNE
	* Key Points: 
	1. non Hermitian Hamiltonian system. 
	2. wavefunc input instead of Bloch vectors. 
	- History: 
	1. 
    |   |   |
    |---|---|
    |条目类型|预印本|
    |作者|R. M. Woloshyn|
    |摘要|T-distributed stochastic neighborhood embedding (tSNE) is used as a tool to reveal the phase diagram of the Su-Schrieffer-Heeger model and some of its extended and non-Hermitian variants. Bloch vectors calculated at different points in the parameter space are mapped to a two-dimensional reduced space. The clusters in the reduced space are used to visualize different phase regions included in the input. The tSNE mapping is shown to be effective even in the challenging case of the non-Hermitian extended model where five different phases are present. An example of using wavefunction input, instead of Bloch vectors, is presented also.|
    |日期|2021-03-17|
    |文库编目|arXiv.org|
    |网址|[http://arxiv.org/abs/2101.08704](http://arxiv.org/abs/2101.08704)|
    |访问时间|2025/4/6 12:39:17|
    |其他|arXiv:2101.08704 [cond-mat]|
    |DOI|[10.48550/arXiv.2101.08704](http://doi.org/10.48550/arXiv.2101.08704)|
    |仓库|arXiv|
    |存档ID|arXiv:2101.08704|
    |添加日期|2025/4/6 12:39:17|
    |修改日期|2025/4/6 12:39:18|
    
    ### 标签：
    
    - Condensed Matter - Mesoscale and Nanoscale Physics
    - High Energy Physics - Lattice
    - Quantum Physics
    
    ### 笔记：
    
    - Comment: References added
        
    
    ### 附件
    
    - Snapshot
    - Woloshyn - 2021 - Exploring phases of the su-schrieffer-heeger model with tSNE.pdf
- ## Identification of topological phases using classically-optimized variational quantum eigensolver
    
    |   |   |
    |---|---|
    |条目类型|期刊文章|
    |作者|Ken N. Okada|
    |作者|Keita Osaki|
    |作者|Kosuke Mitarai|
    |作者|Keisuke Fujii|
    |摘要|Variational quantum eigensolver (VQE) is regarded as a promising candidate of hybrid quantum-classical algorithm for the near-term quantum computers. Meanwhile, VQE is confronted with a challenge that statistical error associated with the measurement as well as systematic error could significantly hamper the optimization. To circumvent this issue, we propose classically-optimized VQE (co-VQE), where the whole process of the optimization is efficiently conducted on a classical computer. The efficacy of the method is guaranteed by the observation that quantum circuits with a constant (or logarithmic) depth are classically tractable via simulations of local subsystems. In co-VQE, we only use quantum computers to measure nonlocal quantities after the parameters are optimized. As proof-of-concepts, we present numerical experiments on quantum spin models with topological phases. After the optimization, we identify the topological phases by nonlocal order parameters as well as unsupervised machine learning on inner products between quantum states. The proposed method maximizes the advantage of using quantum computers while avoiding strenuous optimization on noisy quantum devices. Furthermore, in terms of quantum machine learning, our study shows an intriguing approach that employs quantum computers to generate data of quantum systems while using classical computers for the learning process.|
    |日期|2023-12-8|
    |文库编目|arXiv.org|
    |网址|[http://arxiv.org/abs/2202.02909](http://arxiv.org/abs/2202.02909)|
    |访问时间|2025/4/6 12:38:13|
    |其他|arXiv:2202.02909 [quant-ph] 中科院分区升级版: 物理与天体物理2区 影响因子: 3.5 5年影响因子: 3.8 EI: 是|
    |卷次|5|
    |页码|043217|
    |刊名|Physical Review Research|
    |DOI|[10.1103/PhysRevResearch.5.043217](http://doi.org/10.1103/PhysRevResearch.5.043217)|
    |期号|4|
    |刊名简称|Phys. Rev. Research|
    |ISSN|2643-1564|
    |添加日期|2025/4/6 12:38:13|
    |修改日期|2025/4/6 12:38:14|
    
    ### 标签：
    
    - Quantum Physics
    
    ### 笔记：
    
    - Comment: 8 pages, 6 figures
        
    
    ### 附件
    
    - Okada 等 - 2023 - Identification of topological phases using classically-optimized variational quantum eigensolver.pdf
    - Snapshot
- ## Machine learning approach to study quantum phase transitions of a frustrated one dimensional spin-1/2 system
    
    |   |   |
    |---|---|
    |条目类型|期刊文章|
    |作者|Sk Rahaman|
    |作者|Sumit Haldar|
    |作者|Manoranjan Kumar|
    |摘要|Frustration driven quantum fluctuation leads to many exotic phases in the ground state and study of these quantum phase transitions is one of the most challenging areas of research in condensed matter physics. We study a frustrated Heisenberg $J_1-J_2$ model of spin-1/2 chain with nearest exchange interaction $J_1$ and next nearest exchange interaction $J_2$ using the principal component analysis (PCA) which is an unsupervised machine learning technique. In this method most probable spin configurations (MPSC) of ground-state (GS) and first excited state (FES) for different $J_2/J_1$ are used as the input in PCA to construct the co-variance matrix. The `quantified principal component' $p_1(J_2/J_1)$ of the largest eigenvalue of co-variance matrix is calculated and it is shown that the nature and variation of $p_1(J_2/J_1)$ can accurately predict the phase transitions and degeneracies in the GS. The $p_1(J_2/J_1)$ calculated from the MPSC of GS only exhibits the signature of degeneracies in the GS, whereas, $p_1(J_2/J_1)$ calculated from MPSC of FES captures the gapless spin liquid (GSL)-dimer phase transition as well as all the degeneracies of the model system. We show that jump in $p_1(J_2/J_1)$ of FES at $J_2/J_1 \approx 0.241$, indicates the GSL-dimer phase transition, whereas its kinks give the signature of the GS degeneracies. The scatter plot of first two principal components of FES shows distinct band formation for different phases. The MPSC are obtained by using an iterative variational method which gives the approximate eigenvalues and eigenvectors.|
    |日期|2023-01-13|
    |文库编目|ResearchGate|
    |其他|JCR分区: Q3 中科院分区升级版: 物理与天体物理4区 影响因子: 2.3 5年影响因子: 2.2 EI: 是|
    |卷次|35|
    |刊名|Journal of Physics: Condensed Matter|
    |DOI|[10.1088/1361-648X/acb030](http://doi.org/10.1088/1361-648X/acb030)|
    |刊名简称|Journal of Physics: Condensed Matter|
    |添加日期|2025/4/6 12:37:44|
    |修改日期|2025/4/6 12:37:45|
    
    ### 附件
    
    - Rahaman 等 - 2023 - Machine learning approach to study quantum phase transitions of a frustrated one dimensional spin-1.pdf
    - ResearchGate Link
- ## Self-attention assistant classification of non-hermitian topological phases
    
    |   |   |
    |---|---|
    |条目类型|预印本|
    |作者|Hengxuan Jiang|
    |作者|Xiumei Wang|
    |作者|Xingping Zhou|
    |摘要|Classification of non-Hermitian topological phases becomes challenging due to interplay of the band topology and non-Hermiticity. The significant increase in data dimensions and the number of categories has rendered traditional supervised learning and unsupervised manifold learning failed. Here, we propose the self-attention assistant machine learning for clustering topological phases. By incorporating the self-attention mechanism, the model can effectively capture long-range dependencies and important patterns, resulting in a more compact and information-rich latent space. It can directly classify the eigenvectors and obtains the information of all topological phases. Our results provide a general method for studying non-Hermitian topological phase via machine learning.|
    |日期|2024-10-06|
    |语言|en-US|
    |文库编目|arXiv.org|
    |网址|[http://arxiv.org/abs/2409.14453](http://arxiv.org/abs/2409.14453)|
    |访问时间|2025/4/6 12:36:38|
    |其他|arXiv:2409.14453 [cond-mat]|
    |DOI|[10.48550/arXiv.2409.14453](http://doi.org/10.48550/arXiv.2409.14453)|
    |仓库|arXiv|
    |存档ID|arXiv:2409.14453|
    |添加日期|2025/4/6 12:36:38|
    |修改日期|2025/4/6 12:36:39|
    
    ### 标签：
    
    - Condensed Matter - Other Condensed Matter
    
    ### 附件
    
    - Jiang 等 - 2024 - Self-attention assistant classification of non-hermitian topological phases.pdf
    - Snapshot
- ## Snake net with a neural network for detecting multiple phases in the phase diagram
    
    |   |   |
    |---|---|
    |条目类型|期刊文章|
    |作者|Xiaodong Sun|
    |作者|Huijiong Yang|
    |作者|Nan Wu|
    |作者|T. C. Scott|
    |作者|Jie Zhang|
    |作者|Wanzhou Zhang|
    |日期|2023-6-22|
    |语言|en|
    |文库编目|DOI.org (Crossref)|
    |网址|[https://link.aps.org/doi/10.1103/PhysRevE.107.065303](https://link.aps.org/doi/10.1103/PhysRevE.107.065303)|
    |访问时间|2025/4/6 12:36:28|
    |其他|JCR分区: Q1 中科院分区升级版: 物理与天体物理3区 影响因子: 2.2 5年影响因子: 2.2 EI: 是|
    |卷次|107|
    |页码|065303|
    |刊名|Physical Review E|
    |DOI|[10.1103/PhysRevE.107.065303](http://doi.org/10.1103/PhysRevE.107.065303)|
    |期号|6|
    |刊名简称|Phys. Rev. E|
    |ISSN|2470-0045, 2470-0053|
    |添加日期|2025/4/6 12:36:28|
    |修改日期|2025/4/6 12:36:30|
    
    ### 附件
    
    - Sun 等 - 2023 - Snake net with a neural network for detecting multiple phases in the phase diagram.pdf
- ## Unsupervised machine learning for identifying phase transition using two-times clustering
	History and Gap: 
	1. Common clustering method based on ML: 
		- PCA 
		- tSNE
		- diffusion map
		- the confusion method
		- the active contour model (snake model)
		- Calinski-Harabaz index
	2. Most NN need real data and labels. But [Annals of Physics 391, 312 (2018)](https://doi.org/https://doi.org/10.1016/j.aop.2018.02.018) this paper is an exception. 
	3. This is a 2 time clustering
	
	
	Steps of 2 time clustering: 
	4. K mean for each hyperparamed point and choose center sample of MC. 
	5. K mean and Calinski-Harabaz index into 6 categroy. 
	6. Grouped similar categroy. (Overlap Degree )
	 ![[Pasted image 20250407214203.png]]
	Steps of the overall process:
	7. MC generate configs. 2 time clustering to different phases as labels
	8. Training a CNN through these labeled data. 
	9. Use **gradients of similarity** to visual phase boundary. 
	
	|   |   |
    |---|---|
    |条目类型|预印本|
    |作者|Nan Wu|
    |作者|Zhuohan Li|
    |作者|Wanzhou Zhang|
    |摘要|In recent years, developing unsupervised machine learning for identifying phase transition is a research direction. In this paper, we introduce a two-times clustering method that can help select perfect configurations from a set of degenerate samples and assign the configuration with labels in a manner of unsupervised machine learning. These perfect configurations can then be used to train a neural network to classify phases. The derivatives of the predicted classification in the phase diagram, show peaks at the phase transition points. The effectiveness of our method is tested for the Ising, Potts, and Blume-Capel models. By using the ordered configuration from two-times clustering, our method can provide a useful way to obtain phase diagrams.|
    |日期|2023-05-28|
    |文库编目|arXiv.org|
    |网址|[http://arxiv.org/abs/2305.17687](http://arxiv.org/abs/2305.17687)|
    |访问时间|2025/4/6 12:40:11|
    |其他|arXiv:2305.17687 [cond-mat]|
    |DOI|[10.48550/arXiv.2305.17687](http://doi.org/10.48550/arXiv.2305.17687)|
    |仓库|arXiv|
    |存档ID|arXiv:2305.17687|
    |添加日期|2025/4/6 12:40:11|
    |修改日期|2025/4/6 12:40:11|
    
    ### 标签：
    
    - Condensed Matter - Disordered Systems and Neural Networks
    
    ### 笔记：
    
    - Comment: 8 pages, 7 figures
        
    
    ### 附件
    
    - Snapshot
    - Wu 等 - 2023 - Unsupervised machine learning for identifying phase transition using two-times clustering.pdf







# 3. Towards Heisenberg limit without critical slowing down via quantum reinforcement learning
- [Towards Heisenberg limit without critical slowing down via quantum reinforcement learning](https://doi.org/10.48550/arXiv.2503.02210) 
**Quantum Reinforcement Learning** + **Quantum Sensing**. 

## 3.1 Reinforcement Learning
An **Agent** takes **Action** in a **Environment** to learn a **Policy** via **Reward** and **Value**. 
- **Agent**: 一个可行动的对象
- **Action**: $a \in \mathcal{A}$ 可执行操作. 
- **Environment**: $s \in \mathcal{S}$ 当前env的state(状态).
- **Policy**: $\pi(a|s)$ agent的决策规则. 本质上最后需要的是这个inference阶段的policy $\pi$: 
$$
s \to \pi \to a 
$$
- **Value**: 对未来回报的估计.
- **Reward**: $r$, 环境给出的即使反馈信号.

具体学习策略如PPO, GRPO都过于复杂喽. 

## 3.2 Quantum Sensing
Establish a **quantum state** sensitive to **a certain param**, then put this quantum state into a environment including this physical param. this is **fully quantum sensing**. 
Very pretty thought. 


# 4. 


























