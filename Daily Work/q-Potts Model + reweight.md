
# 20250413
今天想到了更多办法处理XY Model的feature extraction. 


# 1. Theoretical aspect of project
$$
T_{c } = \frac{2}{\ln(1+\sqrt{ q })}
\ \ \ 

\beta_{c} = \frac{\ln(1+\sqrt{ 2 })}{2}
$$

![[Pasted image 20250330211349.png]]

there is not a 2 factor. the above pic is wrong.
The reason is that for 2 potts model and Ising model: 
$$
H_{\text{q-potts}} = \sum_{<i,j>} - J_{\text{potts}} \delta_{\sigma_{i}\sigma_{j}}
$$
$$
H_{\text{Ising}} = \sum_{<i,j>}-J_{\text{Ising}} \sigma_{i }\sigma_{j}
$$
Thus here we have a counterpart relation:
$$
J_{\text{potts}} = 2\times J_{\text{Ising}}
$$
Thus 
$$
T_{c\text{potts}} = \frac{J_{\text{Potts}}}{k_{B}\ln(1+\sqrt{ q })}
$$
$$
T_{c\text{Ising}} = \frac{2J_{\text{Ising}}}{k_{B}\ln(1+\sqrt{ 2 })}
$$
$$
T_{c\text{Ising}} = T_{c\text{potts}}
$$

# 2. Technical Realization
## 2.1 the strangel frozen effect(Solved): 
I have to skip this and go on. 
**Still, I dont know the reason why cuz this before 600 after 600 difference.But I adjust the wrong lable discriminate criterion from 0.9 temp to 1.0 temp. This adjustment solved this problem.** 
![[Pasted image 20250401164557.png]]
![[Pasted image 20250401164641.png]]
## 2.2 All rg_ed configs give output 1, no 0. why? 
This circumstance of no phase transition below near critical temperature dues to low **`thermalization_step`**. And there is a random initate, it also contribute to this failed Monte Carlo. I should use **`cold_boot`**  instead.  
![[Pasted image 20250402212322.png]]
![[Pasted image 20250402212816.png]]
this is the reason, **hard to learn the local cluster feature.**  
I can try 128x128~256x256 version code, this may shield the big cluster feature in low size models. Failed in cnn arch. 
tomorrow, try **ViT**. 
maybe larger sample interval. 




beta for E and g for Sx. thus IVM + ML can work! 
DMRG can do this too.