---
title: java把base64转图片保存
categories: java
tags: base64
abbrlink: 1256897339
date: 2021-05-11 10:05:49
---

```java
Long shopId = productVo.getShopId();
String imageName = shopId + "/" + IdUtil.simpleUUID() + ".png";
File file = new File(LOCAL_URL);
OutputStream outputStream = null;
BASE64Decoder decoder = new BASE64Decoder();
try {
	if (!file.exists()) {
		file.mkdirs();
	}
	file = new File(LOCAL_URL + imageName);
	String baseStr = productVo.getPicUrl();
	// 前台在用Ajax传base64值的时候会把base64中的+换成空格，所以需要替换回来。
	String baseValue = baseStr.replaceAll(" ", "+");
	// 解密
	byte[] b = decoder.decodeBuffer(baseValue.replace("data:image/jpeg;base64,", ""));
	// 处理数据
	for (int i = 0; i < b.length; ++i) {
		if (b[i] < 0) {
			b[i] += 256;
		}
	}
	outputStream = new FileOutputStream(file);
	outputStream.write(b);
	outputStream.flush();
} catch (IOException e) {
	e.printStackTrace();
} finally {
	try {
		outputStream.close();
	} catch (IOException e) {
		e.printStackTrace();
	}
}
product.setPicUrl(REMOTE_URL + imageName);
```