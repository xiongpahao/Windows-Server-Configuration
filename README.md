# Windows-Server-Configuration
在Windows Server上搭建Gost代理服务

## 使用Certbot生成证书

1.首先按照[certbot](https://certbot.eff.org/instructions?ws=webproduct&os=windows)官方步骤下载安装certbot
2.安装好后，在powershell中使用以下命令将certbot添加到系统环境变量中：
```shell
setx PATH "$env:PATH;C:\Program Files\Certbot\bin" -m
```
3.然后输入一下命令：
```shell
certbot certonly --standalone
```

## 使用powershell命令行搭建Gost

首先将gost.zip解压到C:\Program Files文件夹中（任意文件夹都可以，下面的命令中的文件夹地址要跟这里一致）。
然后将gost添加到环境变量中，在powershell中输入以下命令：
```shell
setx PATH "$env:PATH;C:\Program Files\Gost" -m
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

