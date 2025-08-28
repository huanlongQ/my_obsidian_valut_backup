
- [DeepSeek V3.1接入Claude Code教程](https://zhuanlan.zhihu.com/p/1941910745546744995)
- [claudecode接入deepseek-v3.1试用评价](https://zhuanlan.zhihu.com/p/1942268647717438161)
- [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae)
- [Claude Code - Gemini CLI Linker](https://zhuanlan.zhihu.com/p/1941776168769519921) 利用Gemini CLI的长文本能力. 
- [zhihu Gemini CLI介绍](https://www.zhihu.com/question/1922038210793546944)
- [Claude Code Router](https://zhuanlan.zhihu.com/p/1943248560784122119) ⭐
- [‎Gemini - ccli&gecli conflicts solving, proxy and bat setting](https://g.co/gemini/share/9c6dafd88c18) 

# Node.js download 

```bash
# Download and install Chocolatey+:
powershell -c "irm https://community.chocolatey.org/install.ps1|iex"
# Download and install Node.js:
choco install nodejs--version="22.18.0"
# Verify the Node.js version:
node -v # Should print "v22.18.0".
# Verify npm version:
npm -v # Should print "10.9.3".
```

# CLI Proxy setting 

⭐**Gemini CLI似乎强要求使用http/https代理, socks代理会报错.** 
⭐为保证Gemini CLI平稳运行, 我们采用 [Windows系统下设置cmd命令行(终端)走代理的方法 - zhuibo6 - 博客园](https://www.cnblogs.com/yerenwz/p/15925848.html)中的环境变量方法强制设置`https_proxy`和`http_proxy`

-  [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae) 似乎这里cmd `set http_proxy`无效, 应当使用`set HTTP_PROXY`etc, 当然, 我这里的jamjams只有http代理, 没有https代理, 所以全用http代理就好. 
-  [[Git, version control|@Git, version control]] similar

```powershell
# git config --global https.proxy socks5://127.0.0.1:1080
netsh winhttp set proxy proxy-server="socks=127.0.0.1:10808" bypass-list="localhost"

>当前的 WinHTTP 代理服务器设置:
>
>    代理服务器:  socks=127.0.0.1:1080
>    绕过列表     :  localhost
```

```cmd
set HTTP_PROXY=http://127.0.0.1:1080
set HTTPS_PROXY=http://127.0.0.1:1080
```

# Proxy Conflicts Solving

[‎Gemini - ccli&gecli conflicts solving, proxy and bat setting](https://g.co/gemini/share/9c6dafd88c18)

 - `Gemini CLI`要求: 
	1) `Path Variables: http_proxy, https_proxy` 经过`proxy http or https`实现. 
- `Claude Code Router`要求: 
	1) `.claude-code-router/config.json`文件`HOST`对齐到本地`"HOST": "127.0.0.1"` 
	2) `Path Variables: http_proxy, https_proxy`为空值. 
```json
{
  "LOG": false,
  "HOST": "127.0.0.1", ⭐,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "deepseek",
      "api_base_url": "https://api.deepseek.com/anthropic", ⭐,
      "api_key": "sk-513f3c58c5c1407981c52a216ff0ddf1", 
      "models": ["deepseek-chat", "deepseek-reasoner"],
      "transformer": {
        "use": ["deepseek"],
        "deepseek-chat": {
          "use": ["tooluse"]
        }
      }
    },
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "xx",
      "models": ["gemini-2.5-flash", "gemini-2.5-pro"],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "deepseek,deepseek-chat",
    "background": "deepseek,deepseek-chat",
    "think": "deepseek,deepseek-reasoner",
    "longContext": "gemini,gemini-2.5-pro",
    "longContextThreshold": 60000,
    "webSearch": "gemini,gemini-2.5-flash"
  }
}
```
最终实现方案: 
`ccli.bat, gecli.bat`
```DOS
@echo off

set "http_proxy=http://127.0.0.1:1080"
set "https_proxy=http://127.0.0.1:1080"

if "%1"=="" (
    start "Gemini CLI" cmd.exe /K gemini
) else (
    start "Gemini CLI" cmd.exe /K "cd /d %1 && gemini"
)
```

```DOS
@echo off

set "http_proxy="
set "https_proxy="

if "%1"=="" (
    start "CCR Code" cmd.exe /K "color 02 && ccr code"
) else (
    start "CCR Code" cmd.exe /K "cd /d %1 && color 02 && ccr code"
)
```

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

# API setting 

deepseek的api要用`https://api.deepseek.com/anthropic`. 
