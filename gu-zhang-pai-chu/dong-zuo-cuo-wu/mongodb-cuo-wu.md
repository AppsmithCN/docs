# MongoDB 错误

本节帮助您排查 Pageplug 平台上常见的 MongoDB 错误。

### 1、503 - service unavailable <a href="#503---service-unavailable" id="503---service-unavailable"></a>

您可能会在 Pageplgu 上看到 503 - 服务不可用错误。



### 2、503—将Pageplug升级到最新版本1.8.15以上

错误信息

> Pageplug server is unavailable. Please try again later.

如果您使用 Pageplug 平台并遇到 503 - Service Unavailable 错误，可能是因为升级到 Pageplug v1.8.15 并使用了旧版本的 MongoDB（v5.0 之前）



要解决此问题，请将您的 MongoDB 升级到版本 5.0。有关更多信息，请按照 MongoDB 官方文档中详述的步骤将副本集升级到 5.0。
