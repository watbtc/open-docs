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

以上3部分以'|'连接
注： 构建签名字符串时，各参数按字母升序排列
#### 签名字符串示例

```
"GET|/oauth/transfers/cashier|access_token=2tld4x191p51d5ciqfht7nihsutsed3x&amount=0.00001&app_id=cbbf0b84a2a4888d401d2ed12e54b2393dcd31e23f52de8edfb7264ff65fade4&call_back_url=http://www.unicoin365.com/n/transferCallBackUrl/RFINEX.html&currency=eth&notify_url=http://www.unicoin365.com/n/transferCallback/RFINEX.html&sn=1161&timestamp=1551430060"

bec5e6df9eec26ca4e7d4f198fa6df51dafdfa5b9f7530c8796f2e5bf3575d08
```

调试签名算法的网址[http://encode.chahuo.com/](http://encode.chahuo.com/)

算法

```
	HMAC-SHA256(payload, secret).to_hex
	payload为签名字符串
	secret为分配的app_secret
	将签名获得的字符串赋值给signature参数
```

## 非对称签名（安全升级）
### 应用签名，平台验签
#### 生成私钥
```
openssl genrsa -out my.pem
```

例子

```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAwRcSIkIiZaHlG5Qv7sGT6pi17+2OYkPnvxlx9QgB8XaGgFJ7
Cqub1qn/q1yvDcXIfDCbS1CkVFkVFNKl5MzOBP08yq5fk21yZVCHb88q6zjhZ2Y6
ec8iskSYsM080fe0UHuuPabtzNpEZBTpwcwkJNsWooNQGPSIsB/mxFRWvAKSyDac
ddgvbnC+fo/jUN9BmjQF7YLr4NivygJWPCl4BI5F4hb7LwMs6wSFeEyzdjBEe6L4
YFYknm3DEGCUmUuShLviTgKfNQZ7SxQSG5VoGqcu4WqKtmeHKFeGF+1/4Agx/k/G
qnNgYk1aihrBQC38xfy8xZTksUNCysdowIMiywIDAQABAoIBAQCq7mF/MkyA6/CF
mYlVMshexRFKdGG3W6Wr5jqbT5toxiQLNPj3WTN7tMJAUKwm5Q+14NGYuqq+gJ3I
8TEqeqNmh0dppTO2rwy147QBpsO3t4LSpgzeCCAO7+q7mPRea4mUNejpavzYe+BP
OLQ2eyED/27qLpSZgt/+Cj+fTYn6pEEpzNCGajfDxZt//lieN7BENPtNVB/qf4wn
6ZETHlQYHRKVFaCvq9HDtGtxw5X+gnbVV5eymVuY03A+aXt5KN0h0o4khr+9d0MP
r24+zVYfU1J9cSFh+xpvhaxASQ56OqOWgRft5gbsBBFtl4Ls6amJ2qyHC0Kp7/KG
QkU9zjYBAoGBAPRHfkzfD6YPVax5Nn8qQOEuleh2QzH4XFl6Bvgwe/12D8FcagVf
BKEejIji/+n6OTYJZN0p3XPvQl1ki3HRlZIV+Qo0j843BELsDWE4dWtvt8vDL6/O
+jHdFbOh2yVN25BHUETi7AW2aaI26dXXYvYXEB8+ZiExra2kff/+g3L5AoGBAMpa
0Oe4aagXhxftOxC3I1NOgbxO8Cu5L2xOnX+qmoaZ2xlpHdN6FotOfSTwl3Lq+8Nc
231NsdCECVPNCvYB3gE7k5yxSkW/fuZNS1MQ5N894pmwf+iELWJhAHbLZ7dTlNlF
39Bc7g7EILsSMtLSExTbzt0z6NNcV8BmlVNLcbDjAoGABM0C5m/b1t+mR2V6dLVX
4RURTShF2c2PwxJq4KXTSf/v/1TZoJFlfeUjzezoKqkIRs+Yc+BGweiJ3VwEgZAk
6GIWKuUtjlf2dXo+KRL6+8mOSyri3QmsUR6PNqCPtgP5tLQyF6h+Cv6yxMVfgxxg
jYWWg4auayiWyTraXxWZb8ECgYA9cnhvdRt4dLSMOniuKb6rZHKW+S2LSW+yJulC
xE6qQvw6aiYperBv2wS7e+exeNO8zmzETxyI4h9m+CO08no0y5+WfGu+ZFknnB8c
eUvW0pcF7ofY1pJlhmk6qae0DshrdgFx51ZO25XI2MzgIfSzZ9AYcdPooujuvvfn
VEiQ2wKBgDNvqjEDOxqe4ViTb1zYC5NYajTUgvIVN5ULJPCkePfVs2IjNVbiDkfz
ZIFaDvCAX2RfywcuK/coENyjqLE3vtaGEb8OSVQhuje2WR81WHyPsss4/4LKGIAE
2j3STo5/jEDCJU1GuRm1KEU3fH49snyKvWZL+bmttp8O71t8VAjo
-----END RSA PRIVATE KEY-----
```

#### 生成公钥,并将公钥上传至交易所平台
```
openssl rsa -in my.pem -pubout -out pub.pem
```
例子

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwRcSIkIiZaHlG5Qv7sGT
6pi17+2OYkPnvxlx9QgB8XaGgFJ7Cqub1qn/q1yvDcXIfDCbS1CkVFkVFNKl5MzO
BP08yq5fk21yZVCHb88q6zjhZ2Y6ec8iskSYsM080fe0UHuuPabtzNpEZBTpwcwk
JNsWooNQGPSIsB/mxFRWvAKSyDacddgvbnC+fo/jUN9BmjQF7YLr4NivygJWPCl4
BI5F4hb7LwMs6wSFeEyzdjBEe6L4YFYknm3DEGCUmUuShLviTgKfNQZ7SxQSG5Vo
Gqcu4WqKtmeHKFeGF+1/4Agx/k/GqnNgYk1aihrBQC38xfy8xZTksUNCysdowIMi
ywIDAQAB
-----END PUBLIC KEY-----
```

#### 签名字符串的构成
1.http请求类型，GET POST DELETE PUT PATCH.  
2.请求的path.  
3.请求的参数(其中signature参数不参与签名),追加参数sign_type，其值为private_key  

以上3部分以'|'连接
注： 构建签名字符串时，各参数按字母升序排列
#### 签名字符串示例

```
payload = "GET|/oauth/transfers/enterprise_cashier|access_token=liixi0uuzhqcyar952w6v4okr6aqmoli&amount=1&app_id=0493320dff91aa9bd0c85c75b91b36d2bcb7df9f78aa79af9fefb3ba0e68baea&call_back_url=https%3a%2f%2ftest.rfinex.vip%2fa%2fb%2fc%3fd%3d1%26e%3d2&currency=eth&notify_url=https%3a%2f%2ftest.rfinex.vip%2fa%2fb%2fc%3fd%3d1%26e%3d2&sign_type=private_key&sn=123456789&timestamp=1540539254"
```

签名算法  
1.构建待签名的字符串。  
2.使用私钥签名。  
3.将签名所得的字符串做Base64编码。 


ruby算法示例

```
pkey = OpenSSL::PKey::RSA.new "-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAwRcSIkIiZaHlG5Qv7sGT6pi17+2OYkPnvxlx9QgB8XaGgFJ7
Cqub1qn/q1yvDcXIfDCbS1CkVFkVFNKl5MzOBP08yq5fk21yZVCHb88q6zjhZ2Y6
ec8iskSYsM080fe0UHuuPabtzNpEZBTpwcwkJNsWooNQGPSIsB/mxFRWvAKSyDac
ddgvbnC+fo/jUN9BmjQF7YLr4NivygJWPCl4BI5F4hb7LwMs6wSFeEyzdjBEe6L4
YFYknm3DEGCUmUuShLviTgKfNQZ7SxQSG5VoGqcu4WqKtmeHKFeGF+1/4Agx/k/G
qnNgYk1aihrBQC38xfy8xZTksUNCysdowIMiywIDAQABAoIBAQCq7mF/MkyA6/CF
mYlVMshexRFKdGG3W6Wr5jqbT5toxiQLNPj3WTN7tMJAUKwm5Q+14NGYuqq+gJ3I
8TEqeqNmh0dppTO2rwy147QBpsO3t4LSpgzeCCAO7+q7mPRea4mUNejpavzYe+BP
OLQ2eyED/27qLpSZgt/+Cj+fTYn6pEEpzNCGajfDxZt//lieN7BENPtNVB/qf4wn
6ZETHlQYHRKVFaCvq9HDtGtxw5X+gnbVV5eymVuY03A+aXt5KN0h0o4khr+9d0MP
r24+zVYfU1J9cSFh+xpvhaxASQ56OqOWgRft5gbsBBFtl4Ls6amJ2qyHC0Kp7/KG
QkU9zjYBAoGBAPRHfkzfD6YPVax5Nn8qQOEuleh2QzH4XFl6Bvgwe/12D8FcagVf
BKEejIji/+n6OTYJZN0p3XPvQl1ki3HRlZIV+Qo0j843BELsDWE4dWtvt8vDL6/O
+jHdFbOh2yVN25BHUETi7AW2aaI26dXXYvYXEB8+ZiExra2kff/+g3L5AoGBAMpa
0Oe4aagXhxftOxC3I1NOgbxO8Cu5L2xOnX+qmoaZ2xlpHdN6FotOfSTwl3Lq+8Nc
231NsdCECVPNCvYB3gE7k5yxSkW/fuZNS1MQ5N894pmwf+iELWJhAHbLZ7dTlNlF
39Bc7g7EILsSMtLSExTbzt0z6NNcV8BmlVNLcbDjAoGABM0C5m/b1t+mR2V6dLVX
4RURTShF2c2PwxJq4KXTSf/v/1TZoJFlfeUjzezoKqkIRs+Yc+BGweiJ3VwEgZAk
6GIWKuUtjlf2dXo+KRL6+8mOSyri3QmsUR6PNqCPtgP5tLQyF6h+Cv6yxMVfgxxg
jYWWg4auayiWyTraXxWZb8ECgYA9cnhvdRt4dLSMOniuKb6rZHKW+S2LSW+yJulC
xE6qQvw6aiYperBv2wS7e+exeNO8zmzETxyI4h9m+CO08no0y5+WfGu+ZFknnB8c
eUvW0pcF7ofY1pJlhmk6qae0DshrdgFx51ZO25XI2MzgIfSzZ9AYcdPooujuvvfn
VEiQ2wKBgDNvqjEDOxqe4ViTb1zYC5NYajTUgvIVN5ULJPCkePfVs2IjNVbiDkfz
ZIFaDvCAX2RfywcuK/coENyjqLE3vtaGEb8OSVQhuje2WR81WHyPsss4/4LKGIAE
2j3STo5/jEDCJU1GuRm1KEU3fH49snyKvWZL+bmttp8O71t8VAjo
-----END RSA PRIVATE KEY-----"

signature = Base64.encode64(pkey.sign_pss("SHA256", payload, salt_length: :max, mgf1_hash: "SHA256"))

payload为签名字符串
将签名获得的字符串赋值给signature参数
签名结果示例：
JXqYhBNhvut2K/WjH0pYehydpzk+R+W13qHpDr8oyNY+G6MzZfZ7R2p/Vnstw2hNNv+4li26wstdmzd14HHzylBkPoH2qxoWKxYjQMwOFl51s+zUw9BzN/PK3hQ4vPWkfHLL6wcn8YLj87qO4NIRPdeb1rUmBW8dFWvGzSQirciVpG8NibcePpDjsz04VANGhPcMn/3wftf53mg8HHzFUwVgdXy5WFMiX5meZQhwfMJ2hRgvgZED7ilkdrZQbVKQhOPs8BsmROyrfecLeB+byp6eosrMjE1ndq15tINT8KvUIcgPjq9P1fLgdm3QK5vVsR0yBi4YRNYzNjV0pYowsg==
```

### 平台签名，应用验签
用户转账后，会触发同步回调和异步通知到应用服务器，原先使用签名方式即改为公私钥签名方式，算法同上
#### 平台发放公钥给应用，人工操作

