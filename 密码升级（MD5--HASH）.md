## 原因
由于早期开发时并没有使用Laravel框架自带的Auth组件，故一直使用手动记session这种最原始的方式，在某次实践过程中由于需要加入RBAC权限管理，故使用起框架自带的Auth组件，让用户登录、认证全部交给Auth组件处理，使得代码精简了不少。因为Auth组件用的是HASH密码，而不是MD5，早期我只使用最简单的MD5对密码加密，升级后密码当然全错了。

## 担忧
其实N个月前就有人提issue说用md5加密很不安全，其实我很清楚，因为md5密码会被类似cmd5.com这样的网站查出来。
不过在我看来，如果是个骇客要来黑你的数据，99%的人的数据都是不值钱的。

## 症状
更新完代码后发现所有用户无法登录，提示账号或者密码错误。

## 更新
进入到SSRPanel项目目录下，执行：`php artisan upgradeUserPassword`
等待执行结束（中间没有任何提示），要执行过程可以看 storage/logs/laravel-xxx.log 日志

## 相关
https://cmmdwl.com/index.php/ssrpanel-hash-update/