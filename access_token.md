## Access Token 简介

我们使用 `OAuth2` 协议做权限验证，所以在您使用使用接口之前需要先申请 `client_id` 与 `client_secret`。 

目前尚未开放申请，如需开发客户端，请联系 `nauxliu@gmail.com`

在访问其他接口之前，你需要先获取 `access_token`，可通过三种授权方式获取。

* client_credentials
* login_token
* refresh_token

### client_credentials 介绍
仅需要 `client_id` 与 `client_secret` 即可，无需用户身份。此认证方式获得的 `access_token` 拥有大部分接口的读取权限。

### login_token 介绍
需要 `client_id`， `client_secret` 与用户身份来获取，获取到的 `access_token` 拥有几乎所有接口的访问于写入权限。

由于 PHPHub 的用户没有密码（通过 Github 注册），所以需要通过扫描用户的登录二维码来获取用户的授权。


### refresh_token 介绍
通过 `login_token` 方式获取 `access_token`的时候同时接口会同时返回 `refresh_token`。当 `access_token` 过期后，无需再次扫码即可通过 `refresh_token` 获得一个全新的 `access_token`。


## client_credentials 认证

接口地址 `https://api.phphub.org/oauth/access_token`

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | client\_credentials | 指明认证类型 |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 


## login_token 认证

扫描用户的登陆二维码，解析后会获得用户名和用于登陆的 `login_token`。

数据的格式为 `{username},{login_token}`

`login_koken`长度为20-32 个字符，然后使用 `username` 和 `login_token` 获取 `access_token`

例：

```
summerblude,nWKEYFZ2wmSikRMjJ2Vl
```

接口地址 `https://api.phphub.org/oauth/access_token`

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | login\_token | 指明认证类型 |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 
| username | 传入 username | 扫描获取的 username |
| login_token | 传入 user_token | 扫描获取的 user_token |

## refresh_token

接口地址 `https://api.phphub.org/oauth/access_token`

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | refresh\_token | 指明此次请求为刷新 token |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 
| refresh\_token | 传入 refresh\_token | 获得的 refresh\_token | 
