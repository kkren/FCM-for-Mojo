# FCM for Mojo
借助 [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq) 实现将 QQ 消息通过 Firebase Cloud Messaging (FCM) 推送至 Android 设备。
专为 Android 7.0 以上设计，充分利用 Android 通知特性（直接回复，捆绑通知等）。

[English](/README.md)

# Docker
Docker 更加易于安装，配置的步骤较少

你需要先安装 [Docker](https://www.docker.com/)，如果还没有，
按照[官方教程](https://www.docker.com/community-edition)，使用脚本安装 [Docker](https://www.docker.com)

```Shell
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

然后参照 [kotomei 的说明](https://github.com/kotomei/fcm-for-mojo/blob/master/README.md)安装即可

# 自行配置
## Mojo-Webqq
FFM 依赖于 Mojo Webqq，所以你必须先[安装好 Mojo WebQQ](https://github.com/sjdy521/Mojo-Webqq)

## 获取服务端
我们推荐使用 Node.js。

你需要先[安装 Node.js](https://nodejs.org/en/download/package-manager)。
然后 Git 获取客户端文件，运行 node：

```Shell
git clone https://github.com/RikkaW/FCM-for-Mojo.git && mv FCM-for-Mojo/server ffm-server
cd ffm-server && node node/index.js
```

恭喜，你已经跑起了一个 HTTP FFM 服务！
但这还没结束，我们需要用一些东西保护你的信息。

### HTTP 基本认证
通过 OpenSSL，用密码来生成一个 MD5

```Shell
$ openssl passwd
Password:
Verifying - Password:
<MD5>
```

复制好 MD5，然后创建一个包含以下内容的文件：

```
<用户名>:<密码>
```

编辑 ```config.js```，找到有 ```basic_auth``` 那几行并去掉附近的注释（即 ```/*``` 和 ```*/```）：
```js
	"basic_auth": {
		"file": "<密码文件路径>"
	},
```

### HTTPS
注意，你需要有 **SSL 证书**才能设置 HTTPS。

编辑 ```config.js```，找到有 ```https``` 的那几行并去掉附近的注释（即 ```/*``` 和 ```*/```）：
```js
	"https": {
			"key": fs.readFileSync("<证书私钥路径>"),
			/* 如果你有 CA 证书，就加上这行
			"ca": fs.readFileSync("<CA 证书路径>"), */
			"cert": fs.readFileSync("<含完整证书链证书（fullchain）或服务端证书（server cert）的路径>")
		}
```

运行 ```node node/index.js```，并[下载客户端](https://github.com/RikkaW/FCM-for-Mojo/releases)，完成最后的配置即可！

注：你可以在 [wiki](https://github.com/RikkaW/FCM-for-Mojo/wiki/配置文件的用法) 中找到更多用法。
