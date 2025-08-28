# 1. Powertoy

- remap shortcut can send just text, not key. 
![[Pasted image 20250808134652.png|319]] 

# 2. GPU

Nvidia 730 + 2K显示屏解决方案: [zhihu Nvidia 730+2K](https://www.zhihu.com/question/343682582) 

# 3. Disk Storage Clean 磁盘存储清理

- ![[Pasted image 20250808131312.png|689]]
	- [zhihu - 春风过客的回答](https://www.zhihu.com/question/326534542/answer/2415359028) 
		- `win + R` $\to$ `%tmp%` $\to$ 发现所有tmp文件
	- `cmd pip cache info pip cache purge(净化)` make pip 0 size. [‎Gemini - Pip Cache: Safe to Delete](https://g.co/gemini/share/3e6a2e079f6c) 
	- Tencent works for QQ etc. 
	- [‎Gemini - mklink transfer `%appdata%` to non-`C:\\` disk](https://g.co/gemini/share/4f03f2d15a9e) `mklink eg: mklink /D "C:\Users\可爱的辣鸡\AppData\Roaming\Kingsoft" "E:\Softwares\kingsoft" `  
	- [Gemini - c盘扩容方案](https://g.co/gemini/share/23aaf2d18aa8) 

# 4. ActivityWatch 

- [ActivityWatch - Open-source time tracker](https://activitywatch.net/?hl=zh-CN) 
- [‎Gemini - 自动化时间日志实现指南](https://gemini.google.com/share/c38c03149b67)

# 5. startup

- `win + R -> shell:startup -> start.bat`
- `.bat` syntax [Batch File Commenting: REM vs. ::](https://g.co/gemini/share/cc6bad211041)  
	- `::` as comment
	- `start " " "D:\SOFTWARES\ActivityWatch\aw-qt.exe"` 

顺便给startup文件夹 `C:\Users\可爱的辣鸡\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`加入了一个`cmdd`

```DOS
:: ============================================================================
:: Self-elevating admin rights check
:: ============================================================================
::net session >nul 2>&1
::if %errorlevel% neq 0 (
::    echo Requesting administrative privileges...
::    powershell.exe -Command "Start-Process '%~f0' -Verb RunAs"
::    exit
::)

start " " "D:\SOFTWARES\Wechat2\WeChat.exe"
::start " " "D:\SOFTWARES\clash-verge\clash-verge.exe"
start " " "D:\SOFTWARES\Jamjams\Jamjams.exe"
start " " "D:\SOFTWARES\ActivityWatch\aw-qt.exe"
::start " " "D:\SOFTWARES\Everything\Everything.exe"
start cmdd
```
