---
title: 使用Hutool生成验证码
categories: java
abbrlink: 693567828
date: 2021-05-11 09:07:55
tags:
---

## jar包引入

```java
<dependency>
    　<groupId>cn.hutool</groupId>
    　<artifactId>hutool-captcha</artifactId>
    　<version>5.2.1</version>
</dependency>
```


## controller

```java
@RestController
@Api(value = "测试controller")
public class CaptchaController {
    @Autowired
    private StringRedisTemplate redisTemplate;
    /**
　   * 验证码图片存储路径前缀
 　  **/
    private static final String PREFIX = "E:/";
    /**
　   * 验证码图片存储路径后缀
 　  **/
    private static final String SUFFIX = ".png";
    @GetMapping(value = "captcha")
    public String captcha() {
        String path;
        CircleCaptcha captcha;
        // 先生成一个验证码，判断是否存在，如果存在，则重新生成
        do {
            //定义图形验证码的长、宽、验证码字符数、干扰元素个数
            captcha = CaptchaUtil.createCircleCaptcha(200, 100, 4, 50);
            //CircleCaptcha captcha = new CircleCaptcha(200, 100, 4, 20);
            //验证码的值
            String code = captcha.getCode();
            //该图片可以在登录完成后删除掉，避免占用资源（取消登陆时也应删除）
            path = PREFIX + code + SUFFIX;
        }
        while (new File(path).exists());
        //图形验证码写出
        captcha.write(path);
        //把验证码存入到redis中
        redisTemplate.opsForValue().set("1", captcha.getCode());
        //当后端代码和验证码图片在同一台服务器上时，可直接返回
        //否则，上传图片到服务器，返回服务器地址
        return path;
    }
    @GetMapping(value = "login")
    @ApiOperation(value = "登录判断")
    public Boolean login(String username, String password, String code) {
        if (!check(code)) {
            return false;
        }
        if (username.equals("admin") && password.equals("admin")) {
            //业务逻辑代码...
            delFile(PREFIX + code + SUFFIX);
            return true;
        }
        return false;
    }
    /**
　   * 检查验证码是否正确
　   *
　   * @param code
　   * @return boolean
　   * @author shmily
　   * @since 2020/7/6 16:52
 　  **/
    public Boolean check(String code) {
        if (redisTemplate.opsForValue().get("1").equalsIgnoreCase(code)) {
            return true;
        }
        return false;
    }
    /**
 　  * 删除验证码文件
 　  *
 　  * @param path
 　  * @return boolean
 　  * @author shmily
 　  * @since 2020/7/6 16:52
 　  **/
    private Boolean delFile(String path) {
        File file = new File(path);
        return file.delete();
    }
}
```