
## AccessToken换取
GET
`
https://rfinex.com/oauth/access_token
`

参数

```
	code: 授权接口分发的code码
	grant_type: "authorization_code" // 此处为固定值
```

返回

```
{
	uid: 用户唯一识别号
	access_token: 用户的身份令牌
	expire_at: 令牌失效时间
}
```

## app换取 Access Token
注：此方法仅供内部产品调用

GET
`
https://rfinex.com/oauth/access_token
`

参数

```
	token: Rfinex的登录token
	grant_type: "login" // 此处为固定值
```
返回

```
{
	uid: 用户唯一识别号
	access_token: 用户的身份令牌
	expire_at: 令牌失效时间
}
```