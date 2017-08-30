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
# LEDE-REDIS

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

[//]: #@corifeus-footer

---

[**P3X-LEDE-REDIS**](https://pages.corifeus.com/lede-redis) Build v1.0.2-13

[Corifeus](http://www.corifeus.com) by [Patrik Laszlo](http://patrikx3.com)

[//]: #@corifeus-footer:end