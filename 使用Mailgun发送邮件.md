用mailgun发送邮件较为简单，仅需要改3个配置项

编辑 `.env` 文件：

- 1.将 `MAIL_DRIVER` 值改为 `mailgun`
- 2.将 `MAILGUN_DOMAIN` 值改为 `mailgun给你分配的 domain 值`
- 3.将 `MAILGUN_SECRET` 值改为 `mailgun给你分配的 secret 值`