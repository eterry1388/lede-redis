[//]: #@corifeus-header

## The LEDE Stable Redis package

---
                        
[//]: #@corifeus-header:end

# LEDE-REDIS 4.0.1

# It is very important so that Makefile is a TAB instead 8 spaces!   

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis and https://github.com/pdf/openwrt-14.07-x86_64-packages/tree/master/net/redis .

It will be all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia) (renamed from LEDE-NODE) named firmware and packages.

# CPU type
Right now, I only tested on ARM (Linksys WRT1200ACS, Linksys 3200ACM),since it is 4.0.1

https://redis.io/topics/ARM

I think though it works anywhere even MIPS.

# Patch 4.0.1 or building as a package

This is not installed on one of the repo's, might add it in later: https://stackoverflow.com/questions/38631251/issue-with-redis-install-geohash-int-geohash-o  .

The location:
```packages/feeds/redis/redis```

#### Help for creating patching with packages
https://lede-project.org/docs/guide-developer/use-patches-with-buildsystem   
  
  
## Create a package and add patches  

```bash
# first run yes, but we don't need it, it is in lede-insomnia
./scripts/feeds update -a
./scripts/feeds install -a

# once you already updated the all
./scripts/feeds install redis
./scripts/feeds update -a -p redis

# to create the patch
make package/feeds/redis/redis/{clean,prepare} V=s QUILT=1
cd build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0.1/
quilt push -a
quilt new 010-redis.patch
quilt edit ./deps/jemalloc/src/pages.c 
quilt edit src/Makefile 

# if you edit
# (add in the plus from https://github.com/pdf/openwrt-14.07-x86_64-packages/tree/master/net/redis )
quilt series
quilt refresh
cd /build/source
make package/feeds/redis/redis/update V=s
make package/feeds/redis/redis/{clean,compile} package/index V=s

#quilt push redis.patch
# artifacts/patch-files/deps/jemalloc/src
#quilt edit ./deps/jemalloc/src/pages.c 
## artifacts/patch-files/src/Makefile
#quilt edit src/Makefile 
#quilt diff
#quilt refresh
```

## Shoud be in it as well

```
define Package/redis/conffiles
/etc/redis.conf
endef


$(INSTALL_DIR) $(1)/etc/init.d
$(INSTALL_BIN) ./files/redis.init $(1)/etc/init.d/redis
$(INSTALL_DIR) $(1)/etc
$(INSTALL_DATA) $(PKG_BUILD_DIR)/redis.conf $(1)/etc
```


[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v1.0.1-2

[Corifeus](http://www.corifeus.com) by [Patrik Laszlo](http://patrikx3.com)

[//]: #@corifeus-footer:end