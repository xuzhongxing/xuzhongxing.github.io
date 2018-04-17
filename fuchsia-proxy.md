# 下载fuchsia源码代理的设置

## 启动shadowsocks代理
```
sslocal -c proxy.json
```

## 启动polipo代理
/etc/polipo/config
```
socksParentProxy = localhost:1080
socksProxyType = socks5
```

## 配置代理环境变量，jiri需要用到
```
export HTTP_PROXY=http://127.0.0.1:8123
export HTTPS_PROXY=http://127.0.0.1:8123
```

## 配置curl代理
~/.curlrc
```
-x http://127.0.0.1:8123
```
注意这里不能直接用socks代理，否则会出现
curl: (35) OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to chrome-infra-packages.appspot.com:443

## 执行官方说明中的命令
```
curl -s "https://fuchsia.googlesource.com/scripts/+/master/bootstrap?format=TEXT" | base64 --decode | bash -s topaz
```