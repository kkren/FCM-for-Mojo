# FCM for Mojo
Push QQ Messages to Android devices with [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq).

Design for Android 7.0+ specially, full use Android notification feature (Reply in notification and bundled notifications, etc.)

[简体中文](/README_zh.md)

# Getting Started
[Noob](#Noob)

[Geek](#Geek)

# Noob
Just input one command, and anwser some question.

*Waiting @kotomei build Dockerfile*

Return to FFM cilent to finish the last step.

# Geek
## Mojo-Webqq
FFM is depending on Mojo-Webqq, you need install it at first.

[Installtion guide](https://github.com/sjdy521/Mojo-Webqq)

## You are...
[Node.js user](#Node.js)

[Nginx user](#Nginx)

## Node.js
We recommend to use Node.js.

You need [install Node.js](https://nodejs.org/en/download/package-manager) at first.
And get server cilent files by git. Then, runing node:

```Shell
git clone https://github.com/RikkaW/FCM-for-Mojo.git
mv FCM-for-Mojo/server ffm-server
cd ffm-server
```

Congratulation, HTTP FFM server can be run now!
But that's not finished yet, we need something to protect your messages.

### HTTP Basic Authorization
Generate a password with openssl:

```Shell
$ openssl passwd
Password:
Verifying - Password:
<MD5>
```

Copy MD5 and create a file with:

```
<username>:<MD5>
```

Edit ```config.json```, add it in first brace "```{}```":

```json
	"basic_auth": {
		"file": "/path/to/passwd"
	},
```

### HTTPS
Attention, you need **SSL certificates** to set up HTTPS.
Edit ```ffm-server/config.json```, and add it in first brace "```{}```" also:
```json
	"https": {
			"key": "/path/to/privkey.pem",
			"cert": "/path/to/fullchain.pem"
		}
```

Run ```node node/index.js```. FFM server running now!
Next step: [configure your FFM cilent](#Cilent).

## Nginx

*Waiting for Perl Nginx module finish*


~~# Cilent
After FFM server started, you need configure your cilent.
Open FFM, click "Server settings. Then, click "Server URL".
Input server URL and click "show advanced option", input username and password. Click "OK" when you finish.
Back to last interface, click "Manage devices". Then, click "+" button at upper right corner.
Click "upload", done!~~
