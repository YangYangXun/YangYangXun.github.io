---
title: Laravel 表單驗證
date: 2018-12-1 09:25:00
author: Yang
img: https://github.com/YangYangXun/ProjectImage/blob/master/EcommerceFashe/cart.png?raw=true
category: Backed-End
tag: Laravel
---

# Laravel 表單驗證

* 在laravel中，其實可以說是有兩種方式來進行表單驗證：使用 Request 和使用 Validation 。
* 5.5 新增 make rule 方式

## Request 表單驗證

* 使用artisan這個工具

`php artisan make:request TestRequest`

* File

```php

class TestRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     * 
     * @return bool
     */
    public function authorize()
    {
     /**  
        authorize()可以這樣簡單地理解：我們在處理這個表單請求(通常是一個post請求)的時候是否是需要進行身份驗證，這種驗證是指：  
        比如A發表的評論，B能不能進行編輯。如果不能，則保留返回false，如果可以，則修改返回true。  
        那麼我們這裡的邏輯是：既然是發表文章，在我們這個站點註冊的用戶(如果開放註冊的話)都是可以發表文章的，  
        所以我們首先修改authorize()方法，將其返回值改為：return true;。  
      */
        
        return false;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            //
        ];
    }
}


```

## Validation 表單驗證

* 使用 ValidatesRequestsTrait 的 validate 方法

```php

 v5.6

 $validatedData = $request->validate([
    'title' => 'required|unique:posts|max:255',
    'body' => 'required',
 ]);
 
 v5.4
 
 $this->validate($request, [
    'title' => 'required|unique:posts|max:255',
    'body' => 'required',
    'publish_at' => 'nullable|date',
 ]);
    
```

* 如果你不想要使用請求上使用 validate 方法，你可以通過 validator Validator facade 手動創建一個驗證器實例。用 Facade 上的 make 方法生成一個新的驗證器實例：

```php

<?php

namespace App\Http\Controllers;

use Validator;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;

class PostController extends Controller
{
    /**
     * 保存一篇新的博客文章。
     *
     * @param  Request  $request
     * @return Response
     */
    public function store(Request $request)
    {
    
        // 傳給 make 方法的第一個參數是要驗證的數據。第二個參數則是該數據的驗證規則。
        $validator = Validator::make($request->all(), [
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
        ]);

        if ($validator->fails()) {
            return redirect('post/create')
                        ->withErrors($validator)
                        ->withInput();
        }

        // 保存文章...
    }
}

```



## 可用驗證規則

* `Unique` : 驗證的字段在給定的數據庫表中必須是唯一的。如果沒有指定 column ，將會使用字段本身的名稱。
```
'email' => 'unique:users,email_address'
```

## 顯示驗證錯誤信息


如果傳入的請求參數未通過給定的驗證規則呢？正如前面所提到的，Laravel會自動把用戶重定向到之前的位置。另外，**所有的驗證錯誤信息會被自動閃存到session** .

重申一次，我們不必在GET路由中將錯誤消息顯式綁定到視圖。**因為Lavarel會檢查在Session數據中的錯誤信息，並自動將其綁定到視圖**（如果這個視圖文件存在）。而其中的變量 $errors 是Illuminate\Support\MessageBag 的一個實例。


## 處理錯誤消息



## Google ReCAPTCHA 我不是機器人

* reCAPTCHA 本來專做 CAPTCHA 的公司, 在 2009 年被 Google 收購
主要的目的大部是為了防止機器人濫用服務、大量留言等問題
我們會為了防止這些問題, 請使用者輸入一些被混淆過的文字、圖形字進判斷使用者是不是真人.... , 其中最明顯的受害者就是線上訂票系統.
* Google最早之前是使用reCAPTCHA v1，必須要輸入圖形驗證碼後才能夠通過驗證，而就在今年(2018/03/31)，Google正式取消reCAPTCHA v1的使用
* reCAPTCHA v2


##  請先向Google大神申請一組reCAPTCHA驗證碼

填寫Google reCAPTCHA申請表單 - https://www.google.com/recaptcha/admin
Label： 填入標籤文字以便日後辨識哪一組reCAPTCHA是屬於那一類用途

Domains：可填入多組網域名，每換一行為一組，以dev.neticrm.tw為例


點擊Register

申請成功！至Adding reCAPTCHA to your site區塊中，取得兩個金鑰：Site key及Secret Key(如下圖中被黃色矩形覆蓋的內容)



* ref

https://cola.workxplay.net/what-is-google-recaptcha/



* Packagelist 
* google/recaptcha
* anhskohbo/no-captcha https://packagist.org/packages/anhskohbo/no-captcha
```
composer require google/recaptcha "~1.1"
差異?
composer require google/recaptcha "^1.2"

"require": {
    "google/recaptcha": "^1.2"
}

```


* laravel make:rule 
* 研究 laravel app\Rules

```
php artisan make:rule Captcha
```

