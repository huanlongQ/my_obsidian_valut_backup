  

# 1. XY Model and BKT phase transition

- [凝聚态中的拓扑（一）：Kosterlitz-Thouless相变：拓扑元激发导致的特殊相变]([https://zhuanlan.zhihu.com/p/23670323](https://zhuanlan.zhihu.com/p/23670323))
    
- [https://zhuanlan.zhihu.com/p/472326906](https://zhuanlan.zhihu.com/p/472326906) Berezinskii-Kosterlitz-Thouless相变(1)
    
- [**_https://www.zhihu.com/column/c_1369948732012740609_**](https://www.zhihu.com/column/c_1369948732012740609) [**_热力学与统计物理随想_**](https://www.zhihu.com/column/c_1369948732012740609)
    
- [https://www.zhihu.com/question/644939614/answer/3440497313](https://www.zhihu.com/question/644939614/answer/3440497313) 拉格朗日的忧郁 谈Mermin-Wagner theorem与BKTphase transition.
    
- [**_https://zhuanlan.zhihu.com/p/539424683_**](https://zhuanlan.zhihu.com/p/539424683) [**_凝聚态场论｜KT相变与拓扑激发_**](https://zhuanlan.zhihu.com/p/539424683)
    

![[Pasted image 20250328111020.png]]


XY Model 的Topological phase transition与它的这个2D标量场的场函数的"紧致性"密切相关.

对于2DIsingModel, 也是2D标量场, 而常函数spin的值

# 2. XY Model的Monte Carlo

**normal mc and checkboard algo mc have a same disadvant, frozen in low temp. wolff algo can overcome this disadvant but can not be parallelized. thus here is a hard trade off.** 


- [**_https://zhuanlan.zhihu.com/p/697577868?utm_psn=1869087184071565312_**](https://zhuanlan.zhihu.com/p/697577868?utm_psn=1869087184071565312) **_蒙卡带你从Ising走到XY-1.烧GPU的Ising_**
    

## 2.1 GPU+checkboard algorithm
![[Pasted image 20250328111049.png]] 
![[Pasted image 20250328111117.png]] 


## 2.2 MonteCarlo的dtheta为什么产生小的随机扰动.