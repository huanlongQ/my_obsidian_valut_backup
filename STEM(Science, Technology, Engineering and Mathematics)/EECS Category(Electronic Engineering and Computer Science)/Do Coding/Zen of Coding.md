# 面向对象

-  [为什么拥有C语言基础的人，依然学不会C++](https://www.zhihu.com/question/647517330/answer/1941522151241941686?share_code=2OKCoCdTfPg7&utm_psn=1941618348803733059)  
	**第一个坎：从“上帝视角”到“放权让对象自己管自己”, 一切操作通知对象来执行.**  

# 函数书写

- 保证一个函数只做一件事, 避免内部步骤. 
	e.g.
	下面这个函数实现了输入调制函数及其系数、实空间array、中心频率、高斯系数、batch_size并输出生成信号频谱. 
	它内部做了两件事: 
	1) 生成信号
	2) 生成信号的频域分布
	这是不好的. 
	
	另外, **它的接口依赖于具体而不是依赖于抽象**, 这也是不好的. 
    ```python    
	# --- 1. 信号生成函数 (基本无需改动) ---
	def generate_spectrum_torch_batched(mod_func, poly_coeffs, x, f0, alpha_envelope, batch_size):
	    """根据指定的调制函数和系数，并行生成一批信号的频谱"""
	    num_samples = len(x)
	    y_mod = mod_func(x, poly_coeffs) # Use the passed modulation function
	    env = envelopeFunc(alpha_envelpoe=alpha_envelope, x=x)
	    freq = f0 + y_mod
	    noise = torch.randn(batch_size, num_samples, device=device) * error_distance
	    sig = torch.cos(2 * torch.pi * freq * (x + noise)) * env
	
	    x_freq = torch.fft.fftfreq(num_samples, d=x[1]-x[0], device=device)
	    x_freq = torch.fft.fftshift(x_freq)
	    
	    freq_sig_batch = torch.fft.fft(sig, dim=1)
	    freq_sig_batch = torch.fft.fftshift(freq_sig_batch, dim=1)
	    freq_sig_batch = torch.abs(freq_sig_batch)
	    
	    max_vals = torch.max(freq_sig_batch, dim=1, keepdim=True).values
	    freq_sig_batch = freq_sig_batch / (max_vals.detach() + 1e-9)
	    
	    return x_freq, freq_sig_batch
    ```
- **接口传参依赖于抽象, 而不应该依赖于具体.** 
	依赖于抽象的点有:
	1) 数值计算中, 应当把整个数据结构(如Gaussian函数ndarray)传输出来, 而不是数据结构的参数(Gaussian $\sigma$)传输出来, 以便于更换函数.  
	2) 使用`dict[string->types.FunctionType]`传输函数时, 换函数不需要换一大堆具体参数`arg`. 
	e.g.
	**它的接口依赖于具体而不是依赖于抽象**, 这也是不好的. 
    ```python    
	# --- 1. 信号生成函数 (基本无需改动) ---
	def generate_spectrum_torch_batched(mod_func, poly_coeffs, x, f0, alpha_envelope, batch_size):
	    """根据指定的调制函数和系数，并行生成一批信号的频谱"""
	    num_samples = len(x)
	    y_mod = mod_func(x, poly_coeffs) # Use the passed modulation function
	    env = envelopeFunc(alpha_envelpoe=alpha_envelope, x=x)
	    freq = f0 + y_mod
	    noise = torch.randn(batch_size, num_samples, device=device) * error_distance
	    sig = torch.cos(2 * torch.pi * freq * (x + noise)) * env
	
	    x_freq = torch.fft.fftfreq(num_samples, d=x[1]-x[0], device=device)
	    x_freq = torch.fft.fftshift(x_freq)
	    
	    freq_sig_batch = torch.fft.fft(sig, dim=1)
	    freq_sig_batch = torch.fft.fftshift(freq_sig_batch, dim=1)
	    freq_sig_batch = torch.abs(freq_sig_batch)
	    
	    max_vals = torch.max(freq_sig_batch, dim=1, keepdim=True).values
	    freq_sig_batch = freq_sig_batch / (max_vals.detach() + 1e-9)
	    
	    return x_freq, freq_sig_batch
	```
- 参数`arg`应该控制输出端, 而不是控制输入端. 
	这里的参数`amp_noise:ndarray`的`amp`直接控制了输出端的`amp`, 因而我不需要多次调试`amp_noise`的`amp`来实现对`amplitude_norm_noise: ndarray`的精确控制. 
	```python
	def amplitude_norm_noise(amp_noise: np.ndarray, cutoff_freq: float, sample_rate: float) -> np.ndarray:
	    """
	    Filters noise, conserving its original maximum absolute amplitude.
	    """
	    filtered_signal = direct_filter_noise(amp_noise, cutoff_freq, sample_rate)
	    
	    original_max_amplitude = np.std(np.abs(amp_noise), axis=-1, keepdims=True)
	    filtered_max_amplitude = np.max(np.abs(filtered_signal), axis=-1, keepdims=True)
	    
	    normalization_factor = original_max_amplitude / (filtered_max_amplitude + 1e-9)
	    
	    return filtered_signal * normalization_factor
		```
