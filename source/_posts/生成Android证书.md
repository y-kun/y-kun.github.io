---
title: 生成Android证书
abbrlink: 2867075872
date: 2021-05-31 16:25:11
categories:
tags:
---

<meta name="referrer" content="no-referrer" />

# <font color="#ff0000">前提：安装JRE环境</font>

## 生成签名证书：

<font color="#ff0000">使用keytool -genkey命令生成证书：</font>

```shell
keytool -genkey -alias testalias -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore
```



- testalias是证书别名，可修改为自己想设置的字符，建议使用英文字母和数字
- test.keystore是证书文件名称，可修改为自己想设置的文件名称，也可以指定完整文件路径
- 36500是证书的有效期，表示100年有效期，单位天，建议时间设置长一点，避免证书过期

## 查看证书信息：

```shell
keytool -list -v -keystore test.keystore  
```

### 输出结果：

```shell
Keystore type: PKCS12    
Keystore provider: SUN    

Your keystore contains 1 entry    

Alias name: test    
Creation date: 2019-10-28    
Entry type: PrivateKeyEntry    
Certificate chain length: 1    
Certificate[1]:    
Owner: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
Issuer: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
Serial number: 7dd12840    
Valid from: Fri Jul 26 20:52:56 CST 2019 until: Sun Jul 02 20:52:56 CST 2119    
Certificate fingerprints:    
         MD5:  F9:F6:C8:1F:DB:AB:50:14:7D:6F:2C:4F:CE:E6:0A:A5    
         SHA1: BB:AC:E2:2F:97:3B:18:02:E7:D6:69:A3:7A:28:EF:D2:3F:A3:68:E7    
         SHA256: 24:11:7D:E7:36:12:BC:FE:AF:2A:6A:24:BD:04:4F:2E:33:E5:2D:41:96:5F:50:4D:74:17:7F:4F:E2:55:EB:26    
Signature algorithm name: SHA256withRSA    
Subject Public Key Algorithm: 2048-bit RSA key    
Version: 3
```

- MD5
  证书的MD5指纹信息（安全码MD5）
- SHA1
  证书的SHA1指纹信息（安全码SHA1）
- SHA256
  证书的SHA256指纹信息（安全码SHA245）

## 安卓签名获取工具

直接通过一个apk，获取安装到手机的第三方应用签名的apk包。 详情：[https://developers.weixin.qq.com/doc/oplatform/Downloads/Android_Resource.html](https://developers.weixin.qq.com/doc/oplatform/Downloads/Android_Resource.html)

