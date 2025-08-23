
- The power of **extremely high dimensionality**:  
  [bilibili video: Neural Network, an optimizer 'without' local minimum](https://www.bilibili.com/video/BV1DP5czzESC/?spm_id_from=333.337.search-card.all.click)  
- [chat with gemini](https://g.co/gemini/share/55a66445139f) 
  ![[Pasted image 20250518140323.png]] 
# Basic Conceptions

## Kohn thm: 
guarantee that if you have a $H$, its$n_{\mathrm{GS}}$ is unique and they act as a bijection. $H[n]$. 
guarantee that if you find a $n_{\mathrm{}}$ that enable $E[n]$ to be a minimum, this $n$ is $n_{\mathrm{GS}}$. 

**in this paper,** they utilize $E[H_{\mathrm{DFT}}]$, which is also right cuz $n = n(H_{\mathrm{DFT}})$. meanwhile, $H_{\mathrm{DFT}}$ has many advantage. 

![[Pasted image 20250518160655.png]] 

they use a external $\tilde{H}_{\mathrm{DFT}}$ to fasten the whole nn generated $H_{\mathrm{DFT}}$ to the real one. 
$$
\mathrm{Loss} = E[H_{\mathrm{DFT}}] + \frac{1}{2}\lambda(H_{\mathrm{DFT}}-\tilde{H_{\mathrm{}}}_{\mathrm{DFT}}(\rho))^{2}
$$
![[Pasted image 20250518160935.png]] 


![[Pasted image 20250518161735.png]] 







