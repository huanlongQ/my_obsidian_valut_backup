-  [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae) 似乎这里cmd `set http_proxy`无效, 应当使用`set HTTP_PROXY`etc. 
-  [Windows系统下设置cmd命令行(终端)走代理的方法 - zhuibo6 - 博客园](https://www.cnblogs.com/yerenwz/p/15925848.html) 
*  [Gemini - Git Line Endings and Filename Errors](https://g.co/gemini/share/3ac13b269887) 

# Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) [Set Proxy in Terminal (Bash, CMD, PowerShell, etc.) · GitHub](https://gist.github.com/m3y54m/b3d97b9067b2b4eb447a5d1182a326ae)  

Assume that you want to set 127.0.0.1:10809 as HTTP proxy and 127.0.0.1:10808 as SOCKS proxy.

[How to set a proxy for CMD/Powershell/Terminal/Git](https://theodorecooper.github.io/other/2022-cmd-proxy/)

## CMD / PowerShell Using `netsh`

[Configure the proxy server manually using netsh command](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-proxy-internet?view=o365-worldwide#configure-the-proxy-server-manually-using-netsh-command)

### Tunnel all your internet traffic through a HTTP proxy 

```
netsh winhttp set proxy 127.0.0.1:10809 bypass-list="localhost"
```

### Tunnel all your internet traffic through a SOCKS proxy

```
netsh winhttp set proxy proxy-server="socks=127.0.0.1:10808" bypass-list="localhost"
```

### View the current proxy settings:

```
netsh winhttp show proxy
```

### Clear all proxy settings:

```
netsh winhttp reset proxy
```

## CMD / PowerShell Using Env. Variables

### Set

```
set http_proxy=http://127.0.0.1:10809
set https_proxy=http://127.0.0.1:10809
```

### Unset

```
set http_proxy=
set https_proxy=
```

To delete variables for future cmd instances, do this:

```
setx http_proxy ""
setx https_proxy ""
```

## PowerShell Using Env. Variables

```
$env:HTTPS_PROXY="http://127.0.0.1:10809"
$env:HTTP_PROXY="http://127.0.0.1:10809"
$env:all_proxy="socks5://127.0.0.1:10808"
```

## Bash

```
export https_proxy=http://127.0.0.1:10809
export http_proxy=http://127.0.0.1:10809
export all_proxy=socks5://127.0.0.1:10808
```

## Git

### Set

```
git config --global http.proxy http://127.0.0.1:10809
git config --global https.proxy http://127.0.0.1:10809
git config --global http.proxy socks5://127.0.0.1:10808
git config --global https.proxy socks5://127.0.0.1:10808
```

### Show

```
git config --get --global http.proxy  
git config --get --global https.proxy
git config --get --global http.proxy socks5  
git config --get --global https.proxy socks5
```

### Unset

```
git config --global --unset http.proxy  
git config --global --unset https.proxy
git config --global --unset http.proxy socks5 
git config --global --unset https.proxy socks5
```
