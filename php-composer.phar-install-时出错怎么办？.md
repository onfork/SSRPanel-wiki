```
[root@centos-2gb-sgp1-01 ssrpanel]# php composer.phar install
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
Warning: The lock file is not up to date with the latest changes in composer.json. You may be getting outdated dependencies. Run update to update them.
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Installation request for doctrine/inflector v1.2.0 -> satisfiable by doctrine/inflector[v1.2.0].
    - doctrine/inflector v1.2.0 requires php ^7.0 -> your PHP version (5.6.31) does not satisfy that requirement.
  Problem 2
    - Installation request for doctrine/instantiator 1.1.0 -> satisfiable by doctrine/instantiator[1.1.0].
    - doctrine/instantiator 1.1.0 requires php ^7.1 -> your PHP version (5.6.31) does not satisfy that requirement.
  Problem 3
    - doctrine/inflector v1.2.0 requires php ^7.0 -> your PHP version (5.6.31) does not satisfy that requirement.
    - laravel/framework v5.4.30 requires doctrine/inflector ~1.0 -> satisfiable by doctrine/inflector[v1.2.0].
    - Installation request for laravel/framework v5.4.30 -> satisfiable by laravel/framework[v5.4.30].
```

因为扩展组件需要用到7.1以上的PHP，所以先给环境里装个PHP7.1吧，不懂得话看WIKI


## 漏了php扩展fileinfo
```
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
Warning: The lock file is not up to date with the latest changes in composer.json. You may be getting outdated dependencies. Run update to update them.
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Installation request for intervention/image 2.4.1 -> satisfiable by intervention/image[2.4.1].
    - intervention/image 2.4.1 requires ext-fileinfo * -> the requested PHP extension fileinfo is missing from your system.
  Problem 2
    - intervention/image 2.4.1 requires ext-fileinfo * -> the requested PHP extension fileinfo is missing from your system.
    - mews/captcha 2.1.7 requires intervention/image ~2.2 -> satisfiable by intervention/image[2.4.1].
    - Installation request for mews/captcha 2.1.7 -> satisfiable by mews/captcha[2.1.7].

  To enable extensions, verify that they are enabled in your .ini files:
    - /www/server/php/71/etc/php.ini
  You can also run `php --ini` inside terminal to see which files are used by PHP in CLI mode.
```

看WIKI，WIKI里有一个手动编译fileinfo的，如果是宝塔，请看宝塔安装ssrpanel的wiki