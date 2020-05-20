### 签名说明
#### 签名字符串(payload)的构成
1.http请求类型，GET POST DELETE PUT PATCH.  
2.请求的path.  
3.请求的参数，其中signature参数不参与签名.  

以上3部分以'|'连接
注： 构建签名字符串时，各参数按字母升序排列
#### 签名字符串示例 

```
"GET|/api/v1/orders|access_key=liixi0uuzhqcyar952w6v4okr6aqmoli&tonce=1540539254"
```

算法

```
	HMAC-SHA256(payload, secret)
	payload为签名字符串
	secret为分配的secret_key
	将签名获得的字符串赋值给signature参数
```

示例

```
payload = "GET|/api/v1/orders|access_key=liixi0uuzhqcyar952w6v4okr6aqmoli&tonce=1540539254"
secret = "49f0032b37d39ad6f273333cf9427ff403ccb1816ebf5f757d3f6a81e4f4bb30"
signature = "a7c16c33ede92be0c5e35b2290b5ec9e62f3525de47a4534ba1b431d06830d3d"
```

是用这个网址的 HmacSHA256 校验

`
[在线加密解密](http://encode.chahuo.com/)
`