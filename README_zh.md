# FCM for Mojo
借助 [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq) 实现将 QQ 消息通过 Firebase Cloud Messaging (FCM) 推送至 Android 设备。
专为 Android 7.0 以上设计，充分利用 Android 通知特性（直接回复，捆绑通知等）。

[English](/README.md)

# 入门
[小白](#小白)

[极客](#极客)

# 小白
按照[官方教程](https://www.docker.com/community-edition)，一键安装 [Docker](https://www.docker.com)

```Shell
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

然后参照[kotomei 的说明](https://github.com/kotomei/fcm-for-mojo/blob/master/README.md)安装即可

# 极客
## Mojo-Webqq
FFM 依赖于 Mojo Webqq，所以你必须先安装好它。

[查看安装教程](https://github.com/sjdy521/Mojo-Webqq)

## 你是……
[Node.js 用户](#Node.js)

[Nginx 用户](#Nginx)

## Node.js
我们推荐使用 Node.js。
你需要先[安装 Node.js](https://nodejs.org/en/download/package-manager) 才能继续。

用 Git 获取客户端文件，然后运行 node：

```Shell
git clone https://github.com/RikkaW/FCM-for-Mojo.git && mv FCM-for-Mojo/server ffm-server
cd ffm-server && node node/index.js
```

恭喜，你已经跑起了一个最基础的服务！
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

编辑 ```config.json```，添加如下内容至第一个括号“```{}```”内：
```json
	"basic_auth": {
		"file": "<密码文件路径>"
	},
```

打开 FFM 客户端中的服务器设置，点击服务器地址并勾选“显示高级选项”。
然后输入用户名和密码并确认

### HTTPS
注意，你需要有 **SSL 证书**才能设置 HTTPS。

编辑 ```config.json```，然后添加如下内容至第一个括号“```{}```”内：
```json
	"https": {
			"key": "<证书私钥路径>",
			"cert": "<含完整证书链证书（fullchain）>"
		}
```

运行 ```node node/index.js```，享受 FFM！

## Nginx
*此坑待填，还是按照 Node.js 弄吧*

