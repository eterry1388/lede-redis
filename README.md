[//]: #@corifeus-header

  [![Build Status](https://travis-ci.org/patrikx3/lede-redis.svg?branch=master)](https://travis-ci.org/patrikx3/lede-redis)  [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master)  [![Code Coverage](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master) 

# The LEDE Stable Redis 4 package 

 
                        
[//]: #@corifeus-header:end

## The feed

http://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/redis

```text
src/gz reboot_redis http://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/redis
```

http://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/redis

```text
src/gz reboot_redis http://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/redis
```

## Built package:
  
* Like Linksys WRT ARM ```atomic instructions```
  * https://cdn.corifeus.com/lede/17.01.4/packages/arm_cortex-a9_vfpv3/redis/  

* Like D-Link RAMIPS ```pthreads```
  * https://cdn.corifeus.com/lede/17.01.4/packages/mipsel_24kc/redis/


## The router service

Please, where you can find it in  [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia), of course it includes ```init.d``` service as well.

```bash
/etc/init.d/redis stop|start
```

## Your own build

```bash
cp feeds.conf.default feeds.conf
echo 'src-git redis https://github.com/patrikx3/lede-redis.git' >> feeds.conf
./scripts/feeds update -a
./scripts/feeds install -a
./scripts/feeds update redis
./scripts/feeds install -a -p  redis

# create a .config
make menuconfig
# might need as well
make kernel_menuconfig

# either
make package/feeds/redis/redis/{clean,prepare,compile} package/index V=s

# or
make V=s
```


# PS

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis and https://github.com/pdf/openwrt-14.07-x86_64-packages/tree/master/net/redis .

It will be in all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia).

### CPU type
Right now, I only tested on ARM (Linksys WRT1200ACS, Linksys 3200ACM) and D-Link RAMIPS since it is 4.0.2


[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v4.0.40-128 

[![Like Corifeus @ Facebook](https://img.shields.io/badge/LIKE-Corifeus-3b5998.svg)](https://www.facebook.com/corifeus.software) 
 

[//]: #@corifeus-footer:end