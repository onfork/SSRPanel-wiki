## 时间
2018-10-25
## 原因
由于早期开发时并没有使用Laravel框架自带的Auth组件，故一直使用手动记session这种最原始的方式，在某次实践过程中由于需要加入RBAC权限管理，故使用起框架自带的Auth组件，让用户登录、认证全部交给Auth组件处理，使得代码精简了不少。

## 症状
更新完代码后发现所有用户无法登录，提示账号或者密码错误。
因为Auth组件用的是HASH密码，而不是MD5，早期我只使用最简单的MD5对密码加密，升级后密码当然全错了。

## 更新
进入到SSRPanel项目目录下，执行：`php artisan upgradeUserPassword`
等待执行结束（中间没有任何提示），要执行过程可以看 storage/logs/laravel-xxx.log 日志
注意：更新密码后，所有用户的密码跟登录账号一样，比如 admin 账号如果没有改过用户名，则密码也是admin

## 相关
https://cmmdwl.com/index.php/ssrpanel-hash-update/

## 不想升级
如果你不想使用新版本，还要继续使用md5那种加密方式，这个版本包是最后一个稳定版本
##### V4.4.2 
https://github.com/ssrpanel/SSRPanel/archive/V4.4.2.tar.gz