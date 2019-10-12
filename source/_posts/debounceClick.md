---
title: js点击事件节流与防抖，防止重复提交、防止频繁重复点击
date: 2019-09-19 08:52:21
tags:
    - IT技术
    - 前端
---
## 限制按钮连续点击触发事件时间间隔
 代码如下:
``` bash
        var time = null;
        var flag = true;//按钮是否可用true 可用，false 不可用
        //捕获普通按钮事件
        $("body").on("click", ".layui-btn", function () {
            if (flag) {
                flag = false;//将按钮设置不可用
                time = setInterval(function () {
                    clearInterval(time);//清除定时器
                    flag = true;//按钮可用
                }, 1000);//一秒后可用
                return true;
            } else {
                return false;
            }
        });
```
<!-- more -->
## 事件节流与防抖
### 函数节流(throttle)
这里以判断页面是否滚动到底部为例，普通的做法就是监听 window 对象的 scroll 事件，然后再函数体中写入判断是否滚动到底部的逻辑,这样做的一个缺点就是比较消耗性能，因为当在滚动的时候，浏览器会无时不刻地在计算判断是否滚动到底部的逻辑，而在实际的场景中是不需要这么做的，在实际场景中可能是这样的：在滚动过程中，每隔一段时间在去计算这个判断逻辑。而函数节流所做的工作就是每隔一段时间去执行一次原本需要无时不刻地在执行的函数，所以在滚动事件中引入函数的节流是一个非常好的实践：
代码如下:
``` bash
$(window).on('scroll', throttle(function() {
    // 判断是否滚动到底部的逻辑
    var pageHeight = $('body').height(),
        scrollTop = $(window).scrollTop(),
        winHeight = $(window).height(),
        thresold = pageHeight - scrollTop - winHeight;
    // 到页面底部
    if (thresold > -100 && thresold <= 20) {
        $("script:first").before("<p>hello world</p>");
    }
}, 500));

```
加上函数节流之后，当页面再滚动的时候，每隔 300ms 才会去执行一次判断逻辑。

简单来说，函数的节流就是通过闭包保存一个标记（canRun = true），在函数的开头判断这个标记是否为 true，如果为 true 的话就继续执行函数，否则则 return 掉，判断完标记后立即把这个标记设为 false，然后把外部传入的函数的执行包在一个 setTimeout 中，最后在 setTimeout 执行完毕后再把标记设置为 true（这里很关键），表示可以执行下一次的循环了。当 setTimeout 还未执行的时候，canRun 这个标记始终为 false，在开头的判断中被 return 掉。
```bash
function throttle(fn, interval = 300) {
    var canRun = true;
    return function() {
        if (!canRun) return;
        canRun = false;
        setTimeout(() => {
            fn.apply(this, arguments);
            canRun = true;
        }, interval);
    };
};
```
### 函数防抖(debounce)
这里以用户注册时验证用户名是否被占用为例，如今很多网站为了提高用户体验，不会再输入框失去焦点的时候再去判断用户名是否被占用，而是在输入的时候就在判断这个用户名是否已被注册，这样的做法不好的是当用户输入第一个字符的时候，就开始请求判断了，不仅对服务器的压力增大了，对用户体验也未必比原来的好。而理想的做法应该是这样的，当用户输入第一个字符后的一段时间内如果还有字符输入的话，那就暂时不去请求判断用户名是否被占用。在这里引入函数防抖就能很好地解决这个问题：
```bash
$('input.user-name').on('input', debounce(function () {
    $.ajax({
        url: `https://just.com/check`,
        method: 'post',
        data: {
            username: $(this).val(),
        },
        success(data) {
            cb();
        },
        error(error) {
            console.log(error);
        },
    });
}));
```
其实函数防抖的原理也非常地简单，通过闭包保存一个标记来保存 setTimeout 返回的值，每当用户输入的时候把前一个 setTimeout clear 掉，然后又创建一个新的 setTimeout，这样就能保证输入字符后的 interval 间隔内如果还有字符输入的话，就不会执行 fn 函数了。
```bash
function debounce(fn, interval = 300) {
    let timeout = null;
    return function () {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            fn.apply(this, arguments);
        }, interval);
    };
}
```
## ionic4 click防抖指令
原文链接：https://blog.csdn.net/baidu_21349635/article/details/91042848
