# 1. Introduction for Basic Conceptions
An **Agent** takes **Action** in a **Environment** to learn a **Policy** via **Reward** and **Value**. 
- **Agent**: 一个可行动的对象. 
- **Action**: $a \in \mathcal{A}$ 可执行操作. 
- **Environment**: $s \in \mathcal{S}$ 当前env的state(状态).
- **Policy**: $\pi(a|s)$ agent的决策规则. 本质上最后需要的是这个inference阶段的policy $\pi$: 
$$
s \to \pi \to a \to s \to a \to s
$$
- **Reward**: $r$, 环境给出的即使反馈信号.
- **Value**: 对一个状态或动作的好坏程度的估计.
	**State-Value Func**: $V$ 
	**Action-Value Func**: $Q$ 
- **Model**: 环境的动态模型
	RL可以分为Model-Based RL与Model-Free RL两种类型, 现今更常用的是Model-Free RL. 

Deep Reinforcement Learning指的是通过Deep Neural Networks近似表示policy, value function或env model. 
# 2. Algo for RL
# 2.1 Value Based 
参与学习的obj是价值函数$V(s)$$Q(s,a)$
## 2.2 Policy Based
参与学习的obj是policy $\pi(a|s)$ 
## 2.3 Actor-Critic: Actor for policy while Critic for Value
参与学习的obj是value func和policy $V_{\theta_{\text{critic}}}(s)$ or $Q_{\theta_{\text{critic}}}(s,a)$, $\pi_{\theta_{\text{actor}}}(a|s)$ 

# 2.4 PPO Proximal Policy Optimization
**Notation:** 
- $r_{t}(\theta) = \frac{\pi_{\theta}(a_{t}|s_{t})}{\pi_{\theta_{\mathrm{old}}(a_{t}|s_{t})}}$ : 概率比例, 用于判断是否需要进行clip. 
- $\hat{A}_{t} =\sum_{l = 0}^{T-t-1}(\gamma \lambda)^{l}\delta_{t+l}$ 其中$\delta_{t+l} = r_{t+l} + \gamma V(s_{t+l+1}) - V(s_{t+l})$. 
	广义优势估计GAE Generalized Advantage Estimation. 
	其中$\delta_{t}$表示单步"惊喜"和"失望", 而$\hat{A}_{t}$表示全局考虑的动作优劣

那么整个PPO的策略就可以表示为对一个$\theta$代表的policy model和一个$\phi$代表的value model的ML. 
其损失函数可以表示为: 
$$L(\theta,\phi)=\underbrace{-\mathbb{E}_t\left[L^{\mathrm{CLIP}}(\theta)\right]}_\text{策略损失}+\underbrace{c_1\mathbb{E}_t\left[\left(V_\phi(s_t)-R_t\right)^2\right]}_\text{价值回归}-\underbrace{c_2\mathbb{E}_t\left[\mathcal{H}[\pi_\theta]\right]}_\text{熵正则}$$ 其中有: 
$$L^{\mathrm{CLIP}}(\theta)=\mathbb{E}_t\left[\min\left(r_t(\theta)\hat{A}_t,\mathrm{clip}(r_t(\theta),1-\epsilon,1+\epsilon)\hat{A}_t\right)\right]$$

**策略损失**指的是PPO希望最大化$L^{\mathrm{CLIP}}$, 即为以GAE$\hat{A}_{t}$的比例, 最大化一个$a$的$r_{t}(\theta)$. 
**价值回归损失**指的是期望$V_{\phi}$最佳拟合Reward的Loss. 
**熵正则化**表示低熵高损失, 即给策略带来更大的随机性, 抑制选择确定性策略. 
