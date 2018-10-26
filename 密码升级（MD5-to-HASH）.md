## 原因
由于早期开发时并没有使用Laravel框架自带的Auth组件，故一直使用手动记session这种最原始的方式，在某次实践过程中由于需要加入RBAC权限管理，故使用起框架自带的Auth组件，让用户登录、认证全部交给Auth组件处理，使得代码精简了不少。

## 症状
更新完代码后发现所有用户无法登录，提示账号或者密码错误。
因为Auth组件用的是HASH密码，而不是MD5，早期我只使用最简单的MD5对密码加密，升级后密码当然全错了。

## 更新
进入到SSRPanel项目目录下，执行：`php artisan upgradeUserPassword`
等待执行结束（中间没有任何提示），要执行过程可以看 storage/logs/laravel-xxx.log 日志

## 相关
https://cmmdwl.com/index.php/ssrpanel-hash-update/