## Access Token 简介

我们使用 `OAuth2` 协议做权限验证，所以在您使用使用接口之前需要先申请 `client_id` 与 `client_secret`。 

目前尚未开放申请，如需开发客户端，请联系 `nauxliu@gmail.com`

在访问其他接口之前，你需要先获取 `access_token`，可通过两种授权方式获取。

* client_credentials
* login_token

#### client_credentials 介绍
仅需要 `client_id` 与 `client_secret` 即可，无需用户身份。此认证方式获得的 `access_token` 拥有大部分接口的读取权限。

#### login_token 介绍
需要 `client_id`， `client_secret` 与用户身份来获取，获取到的 `access_token` 拥有几乎所有接口的访问于写入权限。

由于 PHPHub 的用户没有密码（通过 Github 注册），所以需要通过扫描用户的登录二维码来获取用户的授权。


## client_credentials 认证

接口地址 `https://api.phphub.org/v1/oauth/access_token`

__POST 参数__

| key | 传入 |
|---|---|---|
|  grant\_type | `client_credentials`
|  client\_id  | 申请 client\_id |
| client\_secret |申请的 client\_secret | 

__返回样例__

```json
{
  "access_token": "fnpi7B4wA4ZzTxkvjCnCESUyf6yPl7PXNgxZVne9",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

__返回字段说明__

| 字段 | 说明 |
|---|---|---|
| access_token | 成功获取到的 access_token
| token_type  | token 类型（始终为 Bearer）
| expires_in | token 有效期，单位为秒

## login_token 认证

扫描用户的登陆二维码，解析后会获得用户名和用于登陆的 `login_token`。

数据的格式为 `{username},{login_token}`

`login_koken`长度为 20 - 32 个字符，例：

```
nauxliu,nWKEYFZ2wmSikRMjJ2Vl
```

然后使用 `username` 和 `login_token` 获取 `access_token`

接口地址 `https://api.phphub.org/v1/oauth/access_token`

__POST 参数__

| key | 传入 |
|---|---|---|
|  grant\_type | `login_token` |
|  client\_id  | 申请 client\_id |
| client\_secret | 申请的 client\_secret | 
| username | 扫描获取的 username |
| login_token | 扫描获取的 login_token |

__返回__

```json
{
  "access_token": "A0nVbVy9waLf2v7Tr8npQZRd7SYw0Z4WPJkL8VFm",
  "token_type": "Bearer",
  "expires_in": 31536000,
  "refresh_token": "x1txmTcWP4l81BEbmlPdeOZWETvze13rBrDOzTmG"
}
```

__返回字段说明__

| 字段 | 说明 |
|---|---|---|
| access_token | 成功获取到的 access_token
| token_type  | token 类型（始终为 Bearer）
| expires_in | token 有效期，单位为秒
| refresh_token | 可用来获取新的 access_token

#### 刷新 access token

通过上面的返回数据可以看到，通过 `login_token` 认证方式获取 `access_token`的时候接口会同时返回 `refresh_token`。  
当 `access_token` 过期后，通过刷新机制，无需再次扫码即可再获得一个包含用户身份的 `access_token`。

接口地址 `https://api.phphub.org/v1/oauth/access_token`

__POST 参数__

| key | 传入 |
|---|---|---|
|  grant\_type | `refresh_token` |
|  client\_id  | 申请 client\_id |
| client\_secret | 申请的 client\_secret | 
| refresh\_token | 上次请求返回的 refresh\_token | 
