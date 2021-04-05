[TOC]

[原来的 readme](README-OLD.md)

# 学习 PHP 源码加中文注释 #

原始分支：[PHP-7.0.12](https://github.com/feistiny/php-src/tree/PHP-7.0.12)

当前分支：[COMMENT-PHP-7.0.12](https://github.com/feistiny/php-src/tree/COMMENT-PHP-7.0.12)

如果您需要联系到我，可以给我<a href="mailto:liuzhanfei166@126.com?subject=你好，关于你的  COMMENT-PHP-7.0.12 我有一些问题想跟你探讨一下&body=" >发邮件</a>。

## 学习工具 ##

### IDE 用 Clion ###

Clion，jetbrains 系列用熟了，学习其他语言很方便，很多实用的功能，后续会把常用的功能单独详细的列出来，方便其他小伙伴能直接上手。

因为 Clion 是基于 Cmake 来管理项目的，用 Clion 可以方便的生成 `CMakeLists.txt`，虽然不能直接通过 `cmake` 来编译项目，因为编译 php 源码有很多的依赖关系，只是通过 `CMakeLists.txt` 的 `add_executable`来让 IDE 知道哪些文件是当前项目的，从而建立文件索引，以使用 IDE 的查找引用和跳转定义等功能。

### 断点调试工具 gdb ###

由于编译过程比较复杂，如果用 Clion 的 remote gdb target 或者 gdb remote debug 等功能需要参与到编译过程，而且要保证本地的源码文件和编译出来的符号表对应，比较折腾，不如直接用命令行的 gdb，而且如果本地机是 mac 或 windows，调试起来也不方便，直接上 linux 上搞就完了。

如果是比较简单的单个或几个文件的断点调试可以使用 Clion 自带的 lldb，本地直接断点就行了。

# 开始 #

## 准备看源码 ##

由于以下文件都是根据本机环境生成的，就不添加到仓库了，需要自己生成。

### 本地生成 CmakeLists.txt ###

Clion 执行 Action: `Create CMakeLists.txt` ，默认选项就行。

### 本地生成 ./configure ###

```
./buildconf --force
```

### 本地生成 main/php_config.h ###

因为`php_config.h` 里有很多根据本机环境生成的宏，还有很多 include 了系统的头文件，如果不生成，找不到头文件就无法跳转。

```
# 什么扩展都不用带
./configure --without-iconv

# 最后输出
config.status: creating php7.spec
config.status: creating main/build-defs.h
config.status: creating scripts/phpize
config.status: creating scripts/man1/phpize.1
config.status: creating scripts/php-config
config.status: creating scripts/man1/php-config.1
config.status: creating sapi/cli/php.1
config.status: creating sapi/cgi/php-cgi.1
config.status: creating ext/phar/phar.1
config.status: creating ext/phar/phar.phar.1
config.status: creating main/php_config.h
config.status: executing default commands
```

### 可以看源码了 ###