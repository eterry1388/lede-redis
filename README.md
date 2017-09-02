[//]: #@corifeus-header

  [![Build Status](https://travis-ci.org/patrikx3/lede-redis.svg?branch=master)](https://travis-ci.org/patrikx3/lede-redis)  [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master)  [![Code Coverage](https://scrutinizer-ci.com/g/patrikx3/lede-redis/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/lede-redis/?branch=master) 

---

 
# The LEDE Stable Redis package

This is an open source project. Just code.

### Node Version Requirement 
``` 
>=7.8.0 
```  
   
### Built on Node 
``` 
v8.4.0
```   
   
The ```async``` and ```await``` keywords are required.

Install NodeJs:    
https://nodejs.org/en/download/package-manager/    

# Description  

                        
[//]: #@corifeus-header:end

# LEDE-REDIS 4.0.1

Your built package:  
https://cdn.corifeus.com/lede/17.01.2/packages/arm_cortex-a9_vfpv3/redis/  
  

Please, where you can find it in  [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia), of course it includes ```init.d``` service as well.

```bash
/etc/init.d/redis stop|start
```

## Bulding

### It is very important so that Makefile is a TAB instead 8 spaces!   

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis and https://github.com/pdf/openwrt-14.07-x86_64-packages/tree/master/net/redis .

It will be all of my [LEDE-INSOMNIA](https://pages.corifeus.com/lede-insomnia) (renamed from LEDE-NODE) named firmware and packages.

### CPU type
Right now, I only tested on ARM (Linksys WRT1200ACS, Linksys 3200ACM),since it is 4.0.1

https://redis.io/topics/ARM

I think though it works anywhere even MIPS.

### Patch 4.0.1 or building as a package

This is not installed on one of the repo's, might add it in later, but I think it is not needed, like in ```3.2```.

The location:  
  
```text
packages/feeds/redis/redis
```


#### Help for creating patching with packages
https://lede-project.org/docs/guide-developer/use-patches-with-buildsystem   
  
### Build a package and add patches  

```bash
# first run yes, but we don't need it, it is in lede-insomnia
rm build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis* -rf
rm build_dir/target-mipsel_24kc_musl-1.1.16/redis-4.0.1
rm feeds/redis* -rf
./scripts/feeds update -a
./scripts/feeds install -a

# once you already updated the all
./scripts/feeds install redis
./scripts/feeds update -a -p redis

# build the package
cd /build/source
make package/feeds/redis/redis/{clean,compile} package/index V=s
```
### To create the patch

```bash
make package/feeds/redis/redis/{clean,prepare} V=s QUILT=1
cd /build_dir/target-arm_cortex-a9+vfpv3_musl-1.1.16_eabi/redis-4.0.1/
cd /build/source/build_dir/target-mipsel_24kc_musl-1.1.16/redis-4.0.1
quilt push -a
quilt new 010-redis.patch
quilt edit ./deps/jemalloc/src/pages.c 
quilt edit src/Makefile 
```

### To edit a patch

```bash
quilt series
quilt refresh
quilt push 010-redis.patch
quilt edit ./deps/jemalloc/src/pages.c 
quilt edit src/Makefile 
quilt diff
quilt refresh
```

[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v4.0.5-27

[Corifeus](http://www.corifeus.com) by [Patrik Laszlo](http://patrikx3.com)

[//]: #@corifeus-footer:end