
-  [DeepSeek V3.1接入Claude Code教程](https://zhuanlan.zhihu.com/p/1941910745546744995)
- [claudecode接入deepseek-v3.1试用评价](https://zhuanlan.zhihu.com/p/1942268647717438161)

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

# CLI proxy setting 

[[Git, version control|@Git, version control]] similar
```bash
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
