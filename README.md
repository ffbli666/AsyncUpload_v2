AsyncUpload
===========
一個用 ajax 的實現非同步上傳的檔案，並可以客製 progress bar
並簡化原 asyncUpload 使用方法

兩個主要實作 `AsyncSend` 和 `AsyncUpload`

#Demo site
[Demo](http://ffbli.no-ip.org/works/AsyncUpload_v2/)

## AsyncSend(url, file, fileUpload)
ajax 上傳檔案，使用 XMLHttpRequest實作


#### Arguments
`name`：input name 即 server 接收的 name

`url`：上傳的 url

`file`：file

`FileUpload`：一個可以客製檔案上傳事件的類別，預設可以不給，即可使用
#### Methods
`send`：啟動上傳

`abort`：中斷上傳

#### Example
```
var input = document.querySelector('#input');
var as = AsyncSend("name", "url", input.files[0]);
as.send();
```

## AsyncUpload(CSS_Selector, options)

將 Css selector 後的 html 元表轉變成 input(type=file) 按鈕並利用 asyncSend 實現 ajax uplaod

#### Arguments
`CSS_Selector`: [Css Selector](http://www.w3schools.com/cssref/css_selectors.asp)

### options
`name`：input name 即 server 接收的 name，default name is "file"

`url`：上傳 url

`multiple`：true or false. 是否多選 file

`accept`: filter 副檔名，可參考 [HTML input accept Attribute](http://www.w3schools.com/tags/att_input_accept.asp)

`manualSend`：手動決定上傳時間

`FileUpload`：一個可以客製檔案上傳事件的類別，預設可以不給，即可使用

#### Example
```
var upload = new AsyncUpload('#upload', {
    url: '../upload_submit.php',
    multiple: true
});
```


## FileUpolad
想像成一個 Abstract 類別

需要實作四個 method

如果不帶，預設是如下的實作類號
#### Example

```
var DefaultFileUpload = function(customize) {
    return {
        check: function (file) {return true},
        progress: function (e) {},
        success: function (response) {},
        error: function (e) {}
    };
};
```
#### Methods
##### check(file)
`file`：file 實體
##### progress(e)
`e`：xhr event, percentComplete = e.loaded / e.total
##### success(response)
`response`：server response
##### error(e)
`e`：error message


## Issue
ayncUpload 建立一次只能 send or cancel 一次

## 關鍵技術
XMLHttpRequest()

## Reference

[Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest#Using_FormData_objects)
