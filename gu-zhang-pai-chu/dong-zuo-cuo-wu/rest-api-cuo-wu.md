# REST API 错误

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 1、缺少URL

```
DEFAULT_REST_DATASOURCE is not correctly configured. Please fix the following and then re-run: \n[Missing URL.]
```

此消息表示API 编辑器表单中的 REST API 的 URL 字段已留空。

可以通过编辑REST API 表单并提供 URL来修复此错误。



### 2、缺少客户端密码/客户端 ID/访问令牌

```
DEFAULT_REST_DATASOURCE is not correctly configured. Please fix the following and then re-run: \n[Missing Client Secret, Missing Client ID, Missing Access Token URL]
```

此消息表示提到的参数字段 - //`Client Secret`已留空。这些字段嵌套在子部分中，如果该字段已被选为OAuth 2.0 ，则子部分将变得可见`Client IDAccess Token URLAuthenticationAuthentication Type`



### 3、需要密钥

```
Secret key is required when sending session details is switched on, and should be at least 32 characters in length.
```

此消息表示该`Send Appsmith signature header`字段已被标记为`Yes`但该`Session Details Signature Key`字段留空。

可以通过填写该字段或通过选择`Session Details Signature Key`禁用该字段来解决此错误。`Send Appsmith signature headerNo`













