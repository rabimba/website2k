---
title: 'Installing PHPUnit+PEAR in Ubuntu 12.10 and Overcoming the "PHP_CodeCoverage_Filter::getInstance" Fatal Error'
date: 2013-01-04T11:24:00.000-06:00
draft: false
aliases: [ "/2013/01/installing-phpunitpear-in-ubuntu-1210.html" ]
---

PHP was one of the very first languages I learnt on my way to the world of web dev/design and it still is a very strong tool in my Swiss Army Knife for any web based projects.  

  

In recent times however with the advent of various frameworks I started to realize finally my days of painstaking coding is over and I now can finally work on my small-medium sized applications with minimal effort needed for testing.......how wrong I was.

  

When introduced to the world of testing I started to realize how inefficient and poor my coding standards were also how terrible they were in terms of maintenance. Also the flaws I started to find in my old projects urged me to unit-test my newer ventures. And I found the gem called [PHPUnit](https://github.com/sebastianbergmann/phpunit/)

  

There are three ways of installing it in your dev box (Assuming Ubuntu)

  

*   Install Through PEAR
*   Install Through Composer
*   Install using standalone PHAR file

And as a loyal user of PEAR I straight went to PEAR and just typed the following command which is supposed to install PHPUnit in one go

  

> $ sudo pear install phpunit/PHPUnit

Satisfied with the result I went to the terminal again and ran _\> phpunit_  
But to my surprise I got  
  
PHP Fatal error: Call to undefined method PHP\_CodeCoverage\_Filter::getInstance() in /usr/bin/phpunit on line 39  
  
Bewildered I ran to find what was causing it, but couldn't find any definite solution. So I again fired up my dev virtual box with ubuntu 12.04 and there it was running fine.  
  
Suspecting something was wrong with my PEAR package I went ahead and  typed  
  

> $ pear config-show

  
It showed me (unlike the config on my 12.10)  
  
Configuration (channel pear.php.net):  
\=====================================  
`Auto-discover new Channels auto_discover `  
`Default Channel default_channel pear.php.net`  
`HTTP Proxy Server Address http_proxy `  
`PEAR server [DEPRECATED] master_server pear.php.net`  
`Default Channel Mirror preferred_mirror pear.php.net`  
`Remote Configuration File remote_config `  
`PEAR executables directory bin_dir /usr/bin`  
`PEAR documentation directory doc_dir /usr/share/php/doc`  
`PHP extension directory ext_dir /usr/lib/php5/20090626+lfs`  
`PEAR directory php_dir /usr/share/php`  
`PEAR Installer cache directory cache_dir /tmp/pear/cache`  
`PEAR configuration file cfg_dir /usr/share/php/cfg`  
directory  
`PEAR data directory data_dir /usr/share/php/data`  
`PEAR Installer download download_dir /build/buildd/php5-5.3.10/pear-build-download`  
directory  
`PHP CLI/CGI binary php_bin /usr/bin/php`  
`php.ini location php_ini `  
`--program-prefix passed to php_prefix `  
PHP’s ./configure  
`--program-suffix passed to php_suffix `  
PHP’s ./configure  
`PEAR Installer temp directory temp_dir /tmp/pear/temp`  
`PEAR test directory test_dir /usr/share/php/test`  
`PEAR www files directory www_dir /usr/share/php/htdocs`  
`Cache TimeToLive cache_ttl 3600`  
`Preferred Package State preferred_state stable`  
`Unix file mask umask 2`  
`Debug Log Level verbose 1`  
`PEAR password (for password maintainers)`  
`Signature Handling Program sig_bin /usr/bin/gpg`  
`Signature Key Directory sig_keydir /etc/pear/pearkeys`  
`Signature Key Id sig_keyid `  
`Package Signature Type sig_type gpg`  
`PEAR username (for username `  
maintainers)  
`User Configuration File Filename /home/username/.pearrc`  
System Configuration File Filename /etc/pear/pear.conf  
  
Getting sniff of what was wrong I fixed my environments using the following commands  
  

> `sudo pear config-set bin_dir /usr/bin``sudo pear config-set doc_dir /usr/share/php/doc``sudo pear config-set php_dir /usr/share/php``sudo pear config-set cfg_dir /usr/share/php/cfg` (make (sudo mkdir cfg) directory here)`sudo pear config-set data_dir /usr/share/php/data`  
> 
> `sudi pear config-set test_dir /usr/share/php/test`

And then the following  
  

> `$ sudo pear uninstall phpunit/PHPUnit`  
> 
> `$ sudo pear install phpunit/PHPUnit`

And after that it ran like a charm.  
  
Note:  This happened quite a while ago. I finally got urge to post it because on of my friends faced the exact same problem last night and she couldn't find any solution. When she was telling me today I just figured out just by hearing the error what might be wrong. And the above fixed her issue.  
  
And it dawned to me maybe If I had posted this earlier it could have helped her :P