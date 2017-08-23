# FCM for Mojo
Push QQ Messages to Android devices with [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq).
Design for Android 7.0+ specially, full use Android notification feature (Reply in notification and bundled notifications, etc.)

[简体中文](/README_zh.md)

# Getting Startted
[Noob](#noob)

[Geek](#geek)

# Noob
Just input one command, and anwser some question. Enjoy!

*Waiting @kotomei build Dockerfile*

# Geek
## Mojo-Webqq
FFM is depending on Mojo-Webqq, you need install it at first.
[Read installtion guide of Mojo-Webqq.](https://github.com/sjdy521/Mojo-Webqq)

## Which is you
[Node.js user](#node.js)

[Nginx user](#nginx)

### Node.js
We recommend use Node.js, you need [install Node.js](https://nodejs.org/en/download/package-manager) at first.

Get server cilent files by git. And then, runing node.

```Shell
git clone https://github.com/RikkaW/FCM-for-Mojo.git && mv FCM-for-Mojo/server ffm-server
cd ffm-server && node node/index.js
```

Congratulation, you run a basic server just now!
But that's not finished yet, we need something to protect your messages.

#### HTTP Basic Authorization
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

```
{
	#...#
	"basic_auth": {
		"file": "/path/to/passwd"
	},
}
```

Open server settings in FFM cilent, edit server URL and click "show advanced options".
Then, input the username and password and click "OK".

#### HTTPS
Attention, you need **SSL certificates** to set up HTTPS.
Edit ```ffm-server/config.json```, and add it in first brace "```{}```" also:
```
{
	#...#
	"https": {
			"key": "/path/to/privkey.pem",
			"cert": "/path/to/fullchain.pem"
		}
}
```

Run ```node node/index.js```, enjoy it!

### Nginx

*Waiting for Perl Nginx module finish*
