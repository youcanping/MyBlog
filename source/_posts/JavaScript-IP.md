---
title: JavaScript 获取IP地址
toc: true
comments: true
date: 2018-06-26 15:04:44
tags:
- JavaScript 获取IP地址
categories:
- JavaScript
- IP
---

> [前端WEB获取IP地址问题](https://segmentfault.com/q/1010000010330099)

## 淘宝IP地址库
本人比较喜欢用淘宝的IP地址接口，支持查询本机IP和指定IP，精确度也挺高的。
* [淘宝IP地址库首页](http://ip.taobao.com/)

### 使用说明
1. 请求接口（GET）：
```
/service/getIpInfo.php?ip=[ip地址字串]
```
2. 响应信息：
```
（json格式的）国家 、省（自治区或直辖市）、市（县）、运营商
```
3. 返回数据格式：
```json
{
    "code": 0,
    "data": {
        "ip": "210.75.225.254",
        "country": "中国",
        "area": "华北",
        "region": "北京市",
        "city": "北京市",
        "county": "",
        "isp": "电信",
        "country_id": "86",
        "area_id": "100000",
        "region_id": "110000",
        "city_id": "110000",
        "county_id": "-1",
        "isp_id": "100017"
    }
}
```
> * 其中code的值的含义为，0：成功，1：失败。
> * 获取本机IP[http://ip.taobao.com/service/getIpInfo.php?ip=myip](http://ip.taobao.com/service/getIpInfo.php?ip=myip)

##  httpbin
> [http://httpbin.org/](http://httpbin.org/)

### 获取IP地址
[http://httpbin.org/ip](http://httpbin.org/ip)
### 返回数据
```json
{
    "origin": "67.209.191.219"
}
```
