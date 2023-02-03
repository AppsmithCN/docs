# MySQL错误

```
dev.miku.r2dbc.mysql.client.MySqlConnectionException
```

```
dev.miku.r2dbc.mysql.client.MySqlConnectionClosedException: Connection unexpectedly closed
```

```
Error was received while reading the incoming data. The connection will be closed.
```

此错误消息表示您尝试连接的MySQL服务器不支持 SSL。可以通过编辑数据源配置表单中的 SSL 字段并将其设置为来解决此错误`Disabled`。

