## 用户信息接口

GET

`
https://rfinex.com/oauth/user_info
`

参数

```
	access_token: 用户的身份令牌
  app_id: ''
```

返回

```
{
	uid: 用户唯一编码
	sn: 用户编码
	display_name: 用户名
	nick_name: 用户昵称
	ancestry: 用户的推荐关系
}
```