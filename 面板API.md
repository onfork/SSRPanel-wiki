API为了方便大家自定定制客户端


## 登录API
```
请求地址：/api/login    例如：http://demo.ssrpanel.com/api/login
请求方式：支持GET、POST
请求限制：10分钟内请求失败15次，则封IP一小时（账号不存在、账号被封禁、账号密码错误等导致账号信息无法正常获取的）
请求参数：username 用户名 password 密码
```

##### 成功返回示例
```
{"status":"success","data":{"user":{"id":1,"username":"admin","port":1026,"passwd":"7S7VDhwY","transfer_enable":0,"u":0,"d":0,"t":1507733348,"enable":0,"method":"rc4-md5","protocol":"auth_chain_a","protocol_param":null,"obfs":"http_simple","obfs_param":null,"speed_limit_per_con":204800,"speed_limit_per_user":204800,"gender":1,"wechat":"qq","qq":"22","usage":1,"pay_way":3,"balance":2844,"score":0,"enable_time":"2017-08-06","expire_time":"2018-05-08","ban_time":0,"remark":"<p>\u7ba1\u7406\u5458<\/p>","level":2,"is_admin":1,"reg_ip":"127.0.0.1","last_login":1523362740,"referral_uid":0,"traffic_reset_day":8,"status":0,"created_at":null,"updated_at":"2018-04-10 20:30:01"},"link":"https:\/\/ssrpanel.xyz\/s\/QtbEt"},"message":"\u767b\u5f55\u6210\u529f"}
```

###### 失败返回示例
```
{"status":"fail","data":[],"message":"\u8d26\u53f7\u4e0d\u5b58\u5728\u6216\u5df2\u88ab\u7981\u7528"}
```
