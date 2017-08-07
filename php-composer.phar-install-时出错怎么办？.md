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