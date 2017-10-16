[//]: #@corifeus-header

  [![Build Status](https://travis-ci.org/patrikx3/lede-redis.svg?branch=master)](https://travis-ci.org/patrikx3/lede-redis)  [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master)  [![Code Coverage](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master) 

# The LEDE Stable Redis 4 package 

---

 
                        
[//]: #@corifeus-header:end

## The feed

http://cdn.corifeus.com/lede/17.01.3/packages/arm_cortex-a9_vfpv3/redis

```text
src/gz reboot_redis http://cdn.corifeus.com/lede/17.01.3/packages/arm_cortex-a9_vfpv3/redis
```

http://cdn.corifeus.com/lede/17.01.3/packages/mipsel_24kc/redis

```text
src/gz reboot_redis http://cdn.corifeus.com/lede/17.01.3/packages/mipsel_24kc/redis
```

## Your own build

```bash
cp feeds.conf.default feeds.conf
echo 'src-git redis https://github.com/patrikx3/lede-redis.git' >> feeds.conf
./scripts/feeds update -a
./scripts/feeds install -a
./scripts/feeds update redis
./scripts/feeds install -a -p  redis
```

## The Info

Your built package:
  
* Like Linksys WRT ARM ```atomic instructions```
  * https://cdn.corifeus.com/lede/17.01.3/packages/arm_cortex-a9_vfpv3/redis/  

* Like D-Link RAMIPS ```pthreads```
  * https://cdn.corifeus.com/lede/17.01.3/packages/mipsel_24kc/redis/


## The router service

Please, where you can find it in  [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia), of course it includes ```init.d``` service as well.

```bash
/etc/init.d/redis stop|start
```

## Bulding

### It is very important so that Makefile is a TAB instead 8 spaces!   

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis and https://github.com/pdf/openwrt-14.07-x86_64-packages/tree/master/net/redis .

It will be in all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia).

### CPU type
Right now, I only tested on ARM (Linksys WRT1200ACS, Linksys 3200ACM) and D-Link RAMIPS since it is 4.0.2

### Patch 4.0.2 or building as a package

The location:  
  
```text
packages/feeds/redis/redis
```


#### Help for creating patching with packages
https://lede-project.org/docs/guide-developer/use-patches-with-buildsystem   
  
### Build a package and add patches  

#### Prepare

```bash
# first run yes, but we don't need it, it is in lede-insomnia
rm build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis* -rf
rm build_dir/target-mipsel_24kc_musl-1.1.16/redis-4.0.2
rm build_dir/target-mips_24kc_musl-1.1.16/redis-4.0.2/
rm feeds/redis* -rf
./scripts/feeds update -a
./scripts/feeds install -a

# once you already updated the all
./scripts/feeds install redis
./scripts/feeds update -a -p redis

# build the package
cd /build/source
```

### Build a package

```bash
make package/feeds/redis/redis/{clean,prepare,compile} package/index V=s
```

### To create the patch

```bash
make package/feeds/redis/redis/{clean,prepare} V=s QUILT=1

# either
cd /build/source/build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0.2/

# or
cd /build/source/build_dir/target-mipsel_24kc_musl-1.1.16/redis-4.0.2

# or
cd /build/source/build_dir/target-mips_24kc_musl-1.1.16/redis-4.0.2/

quilt push -a
quilt new 010-redis.patch
quilt edit ./deps/jemalloc/src/pages.c 
quilt edit src/Makefile 
# if work with CONFIG_EDAC_ATOMIC_SCRUB if it is atomic instructions or threads 
quilt edit src/atomicvar.h
quilt series
quilt diff
quilt refresh
```

### To edit a patch

```bash
make package/feeds/redis/redis/{clean,prepare} V=s QUILT=1

# either
cd /build/source/build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0.2/

# or
cd /build/source/build_dir/target-mipsel_24kc_musl-1.1.16/redis-4.0.2

# or
cd /build/source/build_dir/target-mips_24kc_musl-1.1.16/redis-4.0.2/

quilt series
quilt refresh
quilt push 010-redis.patch
quilt edit ./deps/jemalloc/src/pages.c 
quilt edit src/Makefile 
quilt edit src/atomicvar.h
quilt diff
quilt refresh
```


[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v4.0.35-121 

[![Like Corifeus @ Facebook](https://img.shields.io/badge/LIKE-Corifeus-3b5998.svg)](https://www.facebook.com/corifeus.software) 
 

[//]: #@corifeus-footer:end