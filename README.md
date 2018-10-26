## Rfinex 开放授权平台

### 声明
本系统仅开放给rfinex各产品组以及相关合作产品，凭分发的 app\_id 与 app\_secret 访问接口  
关键接口做了签名验证，请阅读接口文档

### 平台接口规则
1.本平台接口规则依据Oauth2.0  
[简易文档](https://oauth.net/2/)  
[墙内文档](https://baike.baidu.com/item/OAuth2.0/6788617?fr=aladdin)
	

### 签名说明
#### 签名字符串的构成
1.http请求类型，GET POST DELETE PUT PATCH.  
2.请求的path.  
3.请求的参数，其中signature参数不参与签名.  
#### 签名字符串示例
	注： 构建签名字符串时，各参数按字母升序排列

```
"GET|/oauth/transfers/enterprise_cashier|access_token=liixi0uuzhqcyar952w6v4okr6aqmoli&app_id=0493320dff91aa9bd0c85c75b91b36d2bcb7df9f78aa79af9fefb3ba0e68baea&amount=1&call_back_url=https%3a%2f%2ftest.rfinex.com%2fa%2fb%2fc%3fd%3d1%26e%3d2&currency=eth&notify_url=https%3a%2f%2ftest.rfinex.com%2fa%2fb%2fc%3fd%3d1%26e%3d2&sn=123456789&timestamp=1540539254"
```

算法

```
	HMAC-SHA256(payload, secret).to_hex
	payload为签名字符串
	secret为分配的app_secret
	将签名获得的字符串赋值给signature参数
```
