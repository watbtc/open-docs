## 用户信息接口

GET

`
https://rfinex.vip/oauth/user_info
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
	node: 所属节点的拥有者
        parent_node: 上一层节点的拥有者
	sn: 用户编码
	display_name: 用户名
	nick_name: 用户昵称
	ancestry: 用户的完整推荐关系，例如： 3/24/123 即：3邀请了24，24邀请了123
        invite_url: 邀请链接
}
```
