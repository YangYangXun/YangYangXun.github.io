---
title: JavaScript 學習歷程 - 1.變數與型別
date: 2019-01-13
author: Yang
img: https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/JavaScript%20%E5%AD%B8%E7%BF%92%E6%AD%B7%E7%A8%8B%2Fjavascript-740x374.png?alt=media&token=10c2ca86-2d87-4e47-8ea2-95f6e86a9168
category: Front End
tag: 
 - JavaScript 
---



## 變數 (Variable)

從大學時期到現在學過不少語言，變數是入門各種語言會在一開始碰到的。什麼是變數呢？
變數幫助我們在 coding 解問題的過程中儲存重要資訊，主要分兩種：


* 全域變數 (Global Variable) ： 所有範圍皆能存取
* 區域變數 (Local Variable) ： 只有在特定範圍內有效

### 以 var 宣告變數

注意如果使用 var 宣告變數則只有在 function 中的宣告才會視為區域變數，
其餘如 if-else statement 及 for loop 等宣告皆會是為全域變數


```javascript

var isProgrammer = true; // 全域

if (isProgrammer) {
    var var_in_if = 'say hello in if' // 全域
    console.log('Print in if statement -> ' + var_in_for) // say hello in if
}

for (var i = 0; i < 1; i++) {
    var var_in_for = 'say hello in for loop' // 全域
    console.log('Print in for loop -> ' + var_in_for) // say hello in for loop
}

function test() {
    var var_in_function = 'var which delcare in function '
    console.log('Print in function  -> ' + var_in_function)
}

console.log('Print in global area => ' + var_in_if) // say hello in if
console.log('Print in global area => ' + var_in_for) // say hello in for 
console.log('Print in global area => ' + var_in_function) // ReferenceError: var_in_function is not defined

```


### ES6 新增 let 以及 const 

* let 區域分明，只要在 `{}` 中宣告的變數都是區域變數，可以免污染全域變數。
* const 是常數必須在宣告時給定初值，不能重新定值以及重新宣告。


```javascript

// let 很適合用來當 for 迴圈變數使用
for (let i = 0; i < array.length; i++) {
    const element = array[i];
}

// const 必須在宣告時給予初值
const a = 'a'
a = 3 // TypeError: Assignment to constant variable.
const a = 'a2' // SyntaxError: Identifier 'a' has already been declared
const b // SyntaxError: Missing initializer in const declaration

```


## 型別 (Type)

JavaScript 弱型別語言，他對型別要求沒有這麼嚴謹，可以在過程中一再的做型別轉換。

> *小觀念*：變數其實沒有型別，因為可能在過程中不斷轉換。**值**才有型別。

1. Number
2. String
3. Boolean
~~4. Array~~
5. **Object**
6. **Null**
7. **Undefined**
8. Symbol (ES6)

### 使用 typeof 檢視型別

```javascript

// 一些 typeof 範例

console.log(typeof 1234); // number
console.log(typeof 12.34); // number
console.log(typeof 0.1234); // number
console.log(typeof "1234"); // string
console.log(typeof '1234'); // string
console.log(typeof true); // boolean
console.log(typeof false); // boolean
console.log(typeof []); // object
console.log(typeof {}); // object
console.log(typeof null); // object ( JavaScript Bug )
console.log(typeof undefined); // undefined

```

### null 與 undefined

* null : 空值，變數其實有被指定一個值，只不過是空值
* undefined : 未定義，變數沒有被指定一個值

**變數應避免設定為 undefined 而是 null，因為 undefine 常造成程式出錯**

*Q&A：如何判斷是否為 null ?*

方法1 : 利用 falsy value

```javascript
if (value) {

} else {

}
```

**JavaScript falsy value 有**

* NaN
* 0, -0
* " " 空字串
* undefined
* null
* false


方法2 : 精確判斷可搭配 typeof 

```javascript
if (！value && typeof value === 'object') {
  // 我是 null
} 
```


## 結語

我覺得 JavaScript 的執行結果有許多出乎意料之處，唯有仔細了解背後原理才不會
落入深坑，進入痛苦的隕石開發。


