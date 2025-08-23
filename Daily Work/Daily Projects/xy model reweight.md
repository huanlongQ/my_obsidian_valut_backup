- XYCNN 
theta $\to$ sin, cos $\to$ fft_r, fft_i input
分辨能力差
- XYCNNWithNChannel
theta $\to$ $\sin n\theta$, $\cos n \theta$ $\to$ fft_r, fft_i input
分辨能力差
- XYCNNv2
fft_r, fft_i $\to$ fft_amp, fft_phase input
分辨能力变好
- XYCNNv3
log(fft_amp), fft_phase input
分辨能力变好
- XYCNNv302
log(1 + fft_amp)
- XYCNNv5
加入residual block
出现严重过拟合







