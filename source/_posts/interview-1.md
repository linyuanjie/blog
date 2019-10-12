---
title: 前端面试问题记录
date: 2019-10-09 16:42:23
tags:
    - 面试
    - 前端
---
## 1、用jquery让页面中有值的文本框背景色变红
```bash
    var inputLength = $("input[type='text']").length; //获取type为text文本框个数
    $("input[type='text']").each(function(){
        var textData = $(this).val();//通过循环获取文本框的数据
        if(textData !=null && textData !=undefined && textData !=''){
          textData.css("background-color","red");
        }
    });
```
<!--more-->
## 2、在js中获取text的input所有值并用对话框弹出窗口
```bash
        window.onload=function(){
            //获取页面中所有input
            var list=document.getElementByTagName("input");
            var strData="";
            对表单中所有的input进行遍历
            for(var i=0;i<list.length && list[i];i++){
            //判断是否为文本框，如果是用"--"分开
            if(list[i].type=="text"){
            strData+=list[i].value+"--";
            }
            }
            alert(strData);
        }
```
## 3、null 和undefined 的区别
1、undefined
　表示"缺少值"，当声明了一个变量未初始化时返回的值
　典型用法是：
　　（1）变量被声明了，但没有赋值时，就等于undefined。
　　（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。
　　（3）对象没有赋值的属性，该属性的值为undefined。
　　（4）函数没有返回值时，默认返回undefined。

2、null
　表示"没有对象"，代表空值，代表一个空对象指针，使用typeof运算得到object,可以认为它是一个特殊对象值。
　典型用法是：
　　（1） 作为函数的参数，表示该函数的参数不是对象。
　　（2） 作为对象原型链的终点

## 4、angular组件生命周期
1、ngOnChanges：在ngOnInit之前， 当数据绑定输入属性的值发生变化时调用。 并且有一个SimpleChanges类型的参数，
它其实是一个类型为SimpleChange，并且键值为属性名的数组:
2、ngOnInit：在第一次ngOnChanges之后。
3、ngDoCheck：每次Angular变化检测时。
4、ngAfterContentInit：在组件使用 ng-content 指令的情况下，Angular 会在将外部内容放到视图后用。它主要用于获取通过 @ContentChild 或 @ContentChildren 属性装饰器查询的内容视图元素。
5、ngAfterContentChecked：在组件使用 ng-content 指令的情况下，Angular 会在检测到外部内容的绑定或者每次变化的时候调用。
6、ngAfterViewInit：在组件相应的视图初始化之后调用，它主要用于获取通过 @ViewChild 或 @ViewChildren 属性装饰器查询的视图元素。
7、ngAfterViewChecked：在子组件视图和子视图检查之后。
8、ngOnDestroy：在Angular销毁组件/指令之前。
## 5、前端常见跨域解决方案
####  跨域解决方案
1、 通过jsonp跨域
2、 document.domain + iframe跨域
3、 location.hash + iframe
4、 window.name + iframe跨域
5、 postMessage跨域
6、 跨域资源共享（CORS）
7、 nginx代理跨域
8、 nodejs中间件代理跨域
9、 WebSocket协议跨域
详细访问如下链接；
https://segmentfault.com/a/1190000011145364?utm_source=tag-newest
