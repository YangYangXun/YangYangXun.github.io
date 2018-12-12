---
title: Laravel Session 機制
date: 2018-12-2 11:25:00
author: Yang
img: https://img.itw01.com/images/20171105/013720rYafdS_V5UOEGV.jpg!r1024x0.jpg
category: Backed-End
tag: 
 - Laravel
 - Session 
---


## 前言

HTTP 是無狀態的，所以需要有一種能夠在請求之間紀錄狀態的法，透過這種紀錄的方法網站系統才能夠判別使用者目前狀態 ( 登入 登出 權限等...)，
因此 Session 就誕生拉。Session 提供了一個在多個請求之間儲存有關用戶訊息的方法，本次主要介紹 Laravel 的 Session 機制。
之後會再使用原生 PHP 來比較一下。

## 配置

Session 的配置檔在 config / session.php 內
初始配置以 File 的方式來記錄 Session
* file- 將會話存儲在storage/framework/sessions中。

![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Laravel_Framework%2F2018-12-2-Laravel-HTTP-Session%2Fcongif_session_driver.jpg?alt=media&token=55150f2e-8381-4840-94b9-0dc27c173010)


除了使用 File 方式來儲存 Session， Laravel 還提供以下幾種方式 :


* **cookie** - Session 存儲在安全加密的cookie中。
* **database** - 將會話存儲在數據庫中。
* **memcached** / redis- Session 存儲在基於高速緩存的存儲系統中。
* **array** - Sessions 存儲在 PHP 數組中，但不會被持久化。

這篇先介紹以 Database 方式來存 Session。之後有時間再來一一嘗試其他方法。

## 以 Database 方式來存 Session

### 設定資料表

* 我們利用 Migrate 的方式來建立 sessions 資料表，Schema 如下 :

```php

Schema::create('sessions', function ($table) {
    $table->string('id')->unique();
    $table->unsignedInteger('user_id')->nullable();
    $table->string('ip_address', 45)->nullable();
    $table->text('user_agent')->nullable();
    $table->text('payload');
    $table->integer('last_activity');
});

```

* 使用 artisan 命令來 migrate


`$ php artisan session:table`

`$ php artisan migrate`



* 完成後如下

![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Laravel_Framework%2F2018-12-2-Laravel-HTTP-Session%2Fsessions_table.jpg?alt=media&token=8f2e5018-7ea0-47f4-90f8-1d342f2af86a)

接著下一章我們就來觀察 Session 如何記錄使用者狀態吧!


## 使用 Session

### Session 存入 sessions table 的時機

* 當瀏覽器第一次訪問網站時 (分別用 IE 和 Chrome 請求)
>   可以看到下圖產生了兩個 Session

![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Laravel_Framework%2F2018-12-2-Laravel-HTTP-Session%2Fbrowser_visit_web.PNG?alt=media&token=fda207a1-0081-46d5-82e9-fcec39bacf90)


* 透過 Laravel Auth 機制登入時

**>ToDo<**


### 獲取 Session 

* 如果你想要获取所有的 Session 数据，可以使用 all 方法：

```php
 $data = $request->session()->all();
```
Result : 
![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Laravel_Framework%2F2018-12-2-Laravel-HTTP-Session%2Fsession_all.jpg?alt=media&token=e71b7234-b7c7-406d-b394-e494313ab12e)



* 獲取 Sessio 中部份資料

```php

// 得到 Token
$token = $request->session()->get('_token');
// 得到上一次請求的 URL
$request->session()->get('_previous')['url']

```

* 判断 Session 中是否存在某个值

```php

// 存在且不為 null 可以用 has 判斷
if ($request->session()->has('users')) {
    
}

// 存在且其值為 null 可以用 exists 判斷
if ($request->session()->exists('users')) {
    
}
```

### 存儲數據

* 存入鍵值對到 Session 中有 2 種方法

1. 通過請求實例
2. 通過全局函數

```php

// 通過請求實例
$request->session()->put('key', 'value');

// 通過全局函數
session(['key' => 'value']);

```


## 結語

今天先簡單介紹，之後遇到相關問題會回來補充。