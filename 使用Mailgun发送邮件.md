用mailgun发送邮件较为简单，仅需要改3个配置项；通用必填项是无论用什么发件方式，都要填写的；注意，用什么方式就填什么其他留空即可

## 编辑 `.env` 文件，修改如下配置：

#### 通用必填项：
- 将 `MAIL_FROM_ADDRESS` 值改为 `你的发信地址，例如：admin@ssrpanel.com`
- 将 `MAIL_FROM_NAME` 值改为 `你的发信人名称，例如：SSRPanel`

#### mailgun配置如下项：
- 将 `MAIL_DRIVER` 值改为 `mailgun`
- 将 `MAILGUN_DOMAIN` 值改为 `mailgun给你分配的 domain 值`
- 将 `MAILGUN_SECRET` 值改为 `mailgun给你分配的 secret 值`

#### SMTP、sendmail发信配置如下项：
- MAIL_HOST=smtp.exmail.qq.com
- MAIL_PORT=465
- MAIL_USERNAME=admin@ssrpanel.com
- MAIL_PASSWORD=password
- MAIL_ENCRYPTION=ssl
