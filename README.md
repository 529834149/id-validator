# IdValidator.php

`中华人民共和国居民身份证`、`中华人民共和国港澳居民居住证`以及`中华人民共和国台湾居民居住证`号码验证工具（PHP Composer 版）支持 15 位与 18 位身份证号。基于 [JavaScript 版本](https://github.com/mc-zone/IDValidator)。

Chinese Mainland Personal ID Card Validation.


[![Build Status](https://travis-ci.org/jxlwqq/id-validator.svg?branch=master)](https://travis-ci.org/jxlwqq/id-validator)
[![StyleCI](https://github.styleci.io/repos/147758862/shield?branch=master)](https://github.styleci.io/repos/147758862)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/jxlwqq/id-validator/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/jxlwqq/id-validator/?branch=master)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjxlwqq%2Fid-validator.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjxlwqq%2Fid-validator?ref=badge_shield)

## 安装

```bash
composer require "jxlwqq/id-validator"
```

## 使用

> `440308199901101512` 和 `610104620927690` 示例大陆居民身份证均为随机生成的假数据，如撞车，请联系删除。
> `810000199408230021` 和 `830000199201300022` 示例港澳台居民居住证为北京市公安局公布的居住证样式号码。

### 验证身份证号合法性

验证身份证号是否合法，合法返回 true，不合法返回 false：

```php
use Jxlwqq\IdValidator\IdValidator;

$idValidator = new IdValidator();
$idValidator->isValid('440308199901101512'); // 大陆居民身份证 18 位
$idValidator->isValid('610104620927690');    // 大陆居民身份证 15 位
$idValidator->isValid('810000199408230021'); // 港澳居民居住证 18 位
$idValidator->isValid('830000199201300022'); // 台湾居民居住证 18 位
```

### 获取身份证号信息

当身份证号合法时，返回分析信息（地区、出生日期、星座、生肖、性别、校验位），不合法返回 false：
```php
use Jxlwqq\IdValidator\IdValidator;

$idValidator = new IdValidator();
$idValidator->getInfo('440308199901101512'); // 18 位
$idValidator->getInfo('610104620927690'); // 15 位
```
返回信息格式：

```php
[
'addressCode'   => '440308',
'address'       => '广东省深圳市盐田区',
'birthdayCode'  => '1999-01-10',
'constellation' => '水瓶座',
'chineseZodiac' => '卯兔',
'sex'           => 1,
'length'        => 18,
'checkBit'      => '2', 
]
```

### 生成可通过校验的假数据
伪造符合校验的身份证：

```php
use Jxlwqq\IdValidator\IdValidator;

$idValidator = new IdValidator();
$idValidator->fakeId(); // 18 位
$idValidator->fakeId(false); // 15 位
```

## 参考资料
* ~~GB 11643-1999 公民身份证号码~~

* ~~GB 2260-1995 中华人民共和国行政区划代码~~

* [中华人民共和国公民身份号码](https://zh.wikipedia.org/wiki/中华人民共和国公民身份号码)

* [中华人民共和国民政部：行政区划代码](http://www.mca.gov.cn/article/sj/xzqh/)

* [港澳台居民居住证](https://zh.wikipedia.org/wiki/港澳台居民居住证)

## Change Log
* 1.1.0 身份证号返回信息新增生肖和星座内容；

* 1.2.0 支持港澳台居民居住证；

* 1.3.0 行政区划代码（地址码）数据改由从中华人民共和国民政部官方网站获取。

## License
MIT


