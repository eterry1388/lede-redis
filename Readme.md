[//]: #@corifeus-header

## The LEDE Stable Redis package

---
                        
[//]: #@corifeus-header:end
# LEDE-REDIS

This is based on:
https://github.com/chrisber/openwrt-ipkg-redis

It will be all of my LEDE-INSOMNIA (renamed from LEDE-NODE) named firmware and packages.

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

[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v1.0.1-2

[Corifeus](http://www.corifeus.com) by [Patrik Laszlo](http://patrikx3.com)

[//]: #@corifeus-footer:end