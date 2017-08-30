[//]: #@corifeus-header

## The LEDE Stable Redis package

---
                        
[//]: #@corifeus-header:end

# LEDE-REDIS 4.0.1

# It is very important so that Makefile is a TAB instead 8 spaces!   


Working on it,

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis

It will be all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia) (renamed from LEDE-NODE) named firmware and packages.

## Usage
Add follow line to feeds.conf or feeds.conf.default
```
src-git redis https://github.com/patrikx3/lede-redis.git
```

Run
```
./scripts/feeds update redis
./scripts/feeds install -a -p redis
```

# CPU type
Right now, I only tested on ARM (Linksys WRT1200ACS, Linksys 3200ACM),since it is 4.0.1

https://redis.io/topics/ARM

I think though it works anywhere even MIPS.

# Patch 4.0.1 or building as a package

https://github.com/pdf/openwrt-14.07-x86_64-packages/blob/master/net/redis/Makefile

https://stackoverflow.com/questions/38631251/issue-with-redis-install-geohash-int-geohash-o

must to clone into the deps https://github.com/yinqiwen/geohash-int

packages/feeds/redis/redis

https://lede-project.org/docs/guide-developer/use-patches-with-buildsystem
  

```/build/source/build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0`.1/deps/geohash-int```



```bash
# first run yes, but we don't need it, it is in lede-insomnia
./scripts/feeds update -a
./scripts/feeds install -a

echo "set linenumbers" > "/home/docker/.nanorc"

# once you already updated the all
./scripts/feeds install redis
./scripts/feeds update -a -p redis

# to create the patch
make package/feeds/redis/redis/clean V=s
make package/feeds/redis/redis/compile V=s

# but you want to path

sudo apt install -y quilt
cat > ~/.quiltrc <<EOF
QUILT_DIFF_ARGS="--no-timestamps --no-index -p ab --color=auto"
QUILT_REFRESH_ARGS="--no-timestamps --no-index -p ab"
QUILT_SERIES_ARGS="--color=auto"
QUILT_PATCH_OPTS="--unified"
QUILT_DIFF_OPTS="-p"
EDITOR="nano"
EOF

# if you add a new
cd build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0.1/
quilt push -a
quilt new redis.patch

# if you edit
quilt series
quilt push redis.patch

# artifacts/patch-files/deps/jemalloc/src
quilt edit ./deps/jemalloc/src/pages.c 
# artifacts/patch-files/src/Makefile
quilt edit src/Makefile 
quilt diff
quilt refresh
cd /build/source


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