# Windows-Server-Configuration
在Windows Server上搭建Gost代理服务

##使用Certbot生成证书

##使用powershell命令行搭建Gost

首先将gost.zip解压到C:\Program Files文件夹中。
然后将gost添加到环境变量中，在powershell中输入以下命令：
```shell
setx gost "C:\Program Files\Gost\gost.exe" -m
```
可以在powershell中直接输入`gost`来确认是否成功添加环境变量。

然后输入以下命令：
```shell
#更改以下四个参数
$DOMAIN="DOMAIN"
$USER="username"
$PASS="password"
$PORT=2333

$BIND_IP="0.0.0.0"
$CERT_DIR="C:\\Certbot\\"
$CERT="${CERT_DIR}live\\${DOMAIN}\\fullchain.pem"
$KEY="${CERT_DIR}live\\${DOMAIN}\\privkey.pem"
$gostArgs = "-L", "http2://${USER}:${PASS}@${BIND_IP}:${PORT}?certFile=${CERT}&keyFile=${KEY}&probeResistance=code:404&knock=www.google.com"

Start-Process -FilePath "gost" -ArgumentList $gostArgs -WindowStyle Hidden
```

