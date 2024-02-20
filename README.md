# Windows-Server-Configuration
在Windows Server上搭建Gost代理服务

##使用Certbot生成证书

##使用powershell命令行搭建Gost

在powershell中进入gost.exe所在的文件夹，输入以下命令：
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

Start-Process -FilePath ".\gost.exe" -ArgumentList $gostArgs -WindowStyle Hidden
```

