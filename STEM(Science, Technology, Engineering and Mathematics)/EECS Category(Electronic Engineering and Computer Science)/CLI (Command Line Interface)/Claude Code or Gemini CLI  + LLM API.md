
- [DeepSeek V3.1接入Claude Code教程](https://zhuanlan.zhihu.com/p/1941910745546744995)
- [claudecode接入deepseek-v3.1试用评价](https://zhuanlan.zhihu.com/p/1942268647717438161)
- [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae)
- [Claude Code - Gemini CLI Linker](https://zhuanlan.zhihu.com/p/1941776168769519921) 利用Gemini CLI的长文本能力. 
- [zhihu Gemini CLI介绍](https://www.zhihu.com/question/1922038210793546944)
- [Claude Code Router](https://zhuanlan.zhihu.com/p/1943248560784122119) ⭐

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

-  [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae) 似乎这里cmd `set http_proxy`无效, 应当使用`set HTTP_PROXY`etc. 
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
