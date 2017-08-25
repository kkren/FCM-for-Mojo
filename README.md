# FCM for Mojo
Push QQ Messages to Android devices with [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq).
Design for Android 7.0+ specially, full use Android notification feature
(Reply in notification and bundled notifications, etc.)

[简体中文](/README_zh.md)

# Getting Started
[Noob](#Noob)

[Geek](#Geek)

# Noob
As [official installtion guilde](https://www.docker.com/community-edition), 
install [Docker](https://www.docker.com) by one command.

```Shell
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Then, install as [kotomei's guilde](https://github.com/kotomei/fcm-for-mojo/blob/master/README.md).

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
git clone https://github.com/RikkaW/FCM-for-Mojo.git && mv FCM-for-Mojo/server ffm-server
cd ffm-server && node node/index.js
```

Congratulation, HTTP FFM server running now at basic mode now!
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

Edit ```config.json```, finding the line with ```basic_auth```
and del annotation (```/*``` and ```*/```) near that's line:

```js
	"basic_auth": {
		"file": "/path/to/passwd"
	},
```

### HTTPS
Attention, you need **SSL certificates** to set up HTTPS.
Edit ```ffm-server/config.js```, finding the line with "```https```"
and del annotation (```/*``` and ```*/```) near that's line:

```js
	"https": {
			"key": "/path/to/privkey.pem",
			/* Add ca-cert here if you have
			"ca": "./keys/ca-cert.pem" */
			"cert": "/path/to/fullchain-or-server-cert.pem"
		}
```

Run ```node node/index.js```. FFM server running now!

You can find out more usage about the ```config.conf``` in [wiki](/wiki/usage-of-config).

## Nginx

*TODO, please install by Node.js method now```
