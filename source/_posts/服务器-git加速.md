设置 Git 全局代理的命令如下：

`git config --global http.proxy socks5://127.0.0.1:8080`

这里有两点要注意一下：

第一：代理参数永远是 http.proxy，不存在什么 https.proxy

第二：虽然参数名称是 http.proxy 但是支持使用不同类似的代理服务器。不同的代理服务器的写法如下：

HTTP 代理服务器：`http://127.0.0.1:8080`
HTTPS 代理服务器： `https://127.0.0.1:8080`
Socks 代理服务器：`socks://127.0.0.1:8080`
Socks5 代理服务器：`socks5://127.0.0.1:8080`

比如只针对 github.com 的 Git 代码库使用代理，语法是如下：

git config --global http.https://github.com.proxy socks5://127.0.0.1:8080
git config --global https.https://github.com.proxy socks5://127.0.0.1:8080

git config --global http.https://github.com.proxy socks://127.0.0.1:8080
git config --global https.https://github.com.proxy socks://127.0.0.1:8080

git config --global http.https://github.com.proxy http://127.0.0.1:8081
git config --global https.https://github.com.proxy http://127.0.0.1:8081

git config --global http.https://github.com.proxy https://127.0.0.1:8080
git config --global https.https://github.com.proxy https://127.0.0.1:8080

git config --global --unset
git config -l
