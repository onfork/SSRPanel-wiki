用mailgun发送邮件较为简单，仅需要改3个配置项

编辑 `.env` 文件：

- 1.将 `MAIL_DRIVER` 值改为 `mailgun`
- 2.将 `MAILGUN_DOMAIN` 值改为 `mailgun给你分配的 domain 值`
- 3.将 `MAILGUN_SECRET` 值改为 `mailgun给你分配的 secret 值`

忽略这些MAIL配置，（这些是用smtp、sendmail发邮件才需要的）
```
MAIL_HOST=smtp.exmail.qq.com
MAIL_PORT=465
MAIL_USERNAME=admin@ssrpanel.com
MAIL_PASSWORD=password
MAIL_ENCRYPTION=ssl
MAIL_FROM_ADDRESS=admin@ssrpanel.com
MAIL_FROM_NAME=SSRPanel
```