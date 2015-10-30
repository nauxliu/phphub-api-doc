## Access Token

在使用 API 需要先申请应用。

接口： `POST` : `https://api.phphub.org/oauth/access_token`

### client_credentials 认证

无需用户身份即可获取，拥有部分接口的访问权限

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | client\_credentials | 指明认证类型 |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 


### login_token 认证

扫描用户的登陆二维码，解析后会获得用户名和用于登陆的 `login_token`, `{username},{login_token}`,然后使用 `username` 和 `login_token` 获取 `access_token`

例：

```
summerblude,nWKEYFZ2wmSikRMjJ2Vl
```

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | login\_token | 指明认证类型 |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 
| username | 传入 username | 扫描获取的 username |
| login_token | 传入 user_token | 扫描获取的 user_token |

### 刷新 access_token

在 `access_token` 过期后可使用 `refresh_token` 重新申请新的 ``access_token``

__POST 参数__

| key | 值 |描述 |
|---|---|---|
|  grant\_type | refresh\_token | 指明此次请求为刷新 token |
|  client\_id  | 传入 client\_id  | 申请 client\_id |
| client\_secret | 传入 client\_secret | 申请的 client\_secret | 
| refresh\_token | 传入 refresh\_token | 获得的 refresh\_token | 
