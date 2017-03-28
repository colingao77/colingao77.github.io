---
layout: post
category: "linux"
title:  "Linux Proxy Setting"
tags: [Linux, Proxy]
---

#### Proxy Setting Shell Script

``` shell
#!/bin/bash

function proxy_on() {
   PROXY_ENV="http_proxy https_proxy ftp_proxy rsync_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY RSYNC_PROXY ALL_PROXY"
   PROXY_VALUE="10.0.2.2:1080"

   if (( $# > 0 )); then
      PROXY_VALUE=$1
   fi

   for envar in $PROXY_ENV
   do
      export $envar=$PROXY_VALUE
   done

   NO_PROXY_ENV="no_proxy NO_PROXY"
   NO_PROXY_VALUE="localhost,127.0.0.1,localaddress,.localdomain.com"

   for envar in $NO_PROXY_ENV
   do
      export $envar=$NO_PROXY_VALUE
   done

   echo "Proxy environment variable set."

   env | grep "proxy"
}

function proxy_off(){
   PROXY_ENV="http_proxy https_proxy ftp_proxy rsync_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY RSYNC_PROXY ALL_PROXY"

   for envar in $PROXY_ENV
   do
      unset $envar
   done

   NO_PROXY_ENV="no_proxy NO_PROXY"
   for envar in $NO_PROXY_ENV
   do
      unset $envar
   done

   echo "Proxy environment variable removed."
}

```

Reference: [Proxy Setting](https://wiki.archlinux.org/index.php/proxy_settings#Using_a_SOCKS_proxy)
