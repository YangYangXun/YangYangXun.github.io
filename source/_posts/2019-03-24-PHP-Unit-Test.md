---
title: 使用 PHP Unit 進行測試
date: 2019-03-24
author: Yang
img: https://i.imgur.com/KlY9wSP.png
category: PHP
tag: 
 - PHP
 - UnitTest
---


## 安裝 PHP Unit

```
$ composer require phpunit/phpunit
```

## 建立 app 目錄夾與測試目錄夾


```
application                // 主要目錄  
├── app                  // 你存放 PHP 專案的資料夾
│    ├── demo.php       // 你的 PHP 程式
│    ├── demo2.php
│    └── demo3.php
├── tests                // 存放測試單元的資料夾
└── phpunit.xml         // 用來設置 PHPUnit 的檔案

```


## 配置 psr-4

composer.json 檔設定，加入 autoload

```json
{
    "require": {
        "phpunit/phpunit": "^7.5"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app"
        }
    }
}
```

執行

```
$ composer dump-autoload -o
```

## 配置 phpunit.xml

新增 phpunit.xml

```xml

<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="vendor/autoload.php"
         colors="true"
         verbose="true"
         stopOnFailure="false">
    <testsuites>
        <testsuite name="Test suite">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
</phpunit>

```

配置完後執行

```
$ ./vendor/bin/phpunit
```
可看見下方結果

![](https://i.imgur.com/oJ6q7o4.png)

## 建立第一個測試類別


```php
// SampleTest.php

use PHPUnit\Framework\TestCase;

class SampleTest extends TestCase
{
    public function testHello()
    {
        $this->assertEquals('hello', 'hello');
    }

}

```

執行
```
$ ./vendor/bin/phpunit
```

![](https://i.imgur.com/Zrg2TAQ.png)

太棒了我們完成了第一個測試。

