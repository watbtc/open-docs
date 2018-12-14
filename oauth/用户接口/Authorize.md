## 授权接口

GET
`
https://rfinex.com/oauth/authorize
`

参数

```
	app_id:	系统分配的app_id
	call_back_url:	用户授权后的回调地址,此地址的host必须与预设的回调host一致
```

返回参数

```
 code：授权码，10分钟有效期
```
