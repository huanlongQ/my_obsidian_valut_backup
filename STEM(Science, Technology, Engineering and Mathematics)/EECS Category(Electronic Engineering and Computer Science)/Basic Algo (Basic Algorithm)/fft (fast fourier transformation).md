
-  [Gemini - fft, fftfreq与单位制转换的系统化思路](https://g.co/gemini/share/50b998ee0af4)

# DFT(Discrete Fourier Theory) Theory and Gauge

`fft` 
$$
\begin{align}
 X_{k}  = &  \sum_{n=0}^{N-1} x_{n} \times \exp\left( -i 2\pi \frac{k}{N} n\right) \ \ \\
 &  k \in \left[ -\frac{N}{2}, \frac{N}{2} \right], \\
 &  n \in [0,N-1].
\end{align}
$$

`fftfreq`
$$
\begin{align}
f_{k} = &  k\times \frac{1}{Nd} \\
 & d \text{ is time domain distance between amples, } \\
 & f_{k}\text{'s unit is } 1/(\text{time domain unit})
\end{align}
$$

# Algo 

- goto [Gemini - fft, fftfreq与单位制转换的系统化思路](https://g.co/gemini/share/50b998ee0af4)
- take care of the 2-power length issue, do not use non 2-power length as possible as can. 

- `fftshift` do `freq` axis shift for convenience. 
