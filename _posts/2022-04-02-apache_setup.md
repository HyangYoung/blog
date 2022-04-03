---
toc: true
layout: post
description: How to run Apache and PHP for on a macOS Monterey version 12.3
comments: true
categories: [PHP]
title: PHP & Apache Initial Setup on macOS
---

## Start PHP on macOS
> macOS has PHP and apache (apachectl) installed by default.<br>
However, if you look at the httpd.conf file, it says PHP has been removed from macOS 12 version.
<br>"PHP was deprecated in macOS 11 and removed from macOS 12" (/etc/apache2/httpd.conf)<br>
Therefore, we need some prep work to run PHP and apache servers on Mac.

1. PHP installation
'''bash
brew install php@8.0
'''

2. httpd(apache) installation 
'''bash
brew install httpd
'''

3. Modifying the httpd.conf file
    - file find command $find 'Find Path' 'Format' "'File Name'.extension"
      '''bash
      find / -name "httpd.conf"
      '''
    - Go to the folder where httpd is installed
      '''bash
      cd /opt/homebrew/etc/httpd
      '''
    - Open the httpd.conf file as admin (enter the password)
      '''bash
      sudo vi httpd.conf
      '''
    - Modify httpd.conf
          - Line 53 -> Change to Listen 80
          - Line 182 -> Uncomment LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so
          - Add LoadModule php_module /opt/homebrew/opt/php@8.0/lib/httpd/modules/libphp.so to the bottom line.(path installed in brew install php)
          - Line 195 -> Change User Username
          - Line 196 -> Change to Group staff
          - Line 217 -> Change to ServerAdmin localhost
          - Line 250 -> Change to DocumentRoot "Project Path"
          - Line 251 -> Change to <Directory "Project Path">
          - Line 271 -> Change to Allow Override All
          - add to the bottom line
              - AddType application/x-httpd-php .html .php
              - AddType application/x-httpd-php-source .phps
              - PHPIniDir /etc
          - Save (:wq)
