---
title: input框的千分位功能
date: 2019-09-12 09:54:28
tags:
    - IT技术
    - 前端
---
	/**
     * 判断是否为数字
     * @param num 
     */
    isNumber(value: any) {
        if (value != '') {
            value = value.replace(/[^0-9-]+/, '');
            return value;
        }
    }

    isNotCompleteNumber(num: string | number): boolean {
        return (isNaN(num as number) ||
            num === '' ||
            num === null ||
            (num && num.toString().indexOf('.') === num.toString().length - 1)
        );
    }
<!--more-->
    //input框的千分位功能
    fmoney(s, n) {
        if (this.isBlank(s) || this.isNotCompleteNumber(s)) {
            return "";
        }
        let flag = false;
        if (s < 0) {
            s = s.toString().replace('-', '');
            flag = true;
        }
        n = n > 0 && n <= 20 ? n : 2;
        s = parseFloat((s + '').replace(/[^\d\.-]/g, '')).toFixed(n) + '';
        let l = s.split('.')[0].split('').reverse(),
            r = s.split('.')[1];
        let t = '';
        for (let i = 0; i < l.length; i++) {
            t += l[i] + ((i + 1) % 3 == 0 && (i + 1) != l.length ? ',' : '');
        }
        if (flag) {
            return '-' + t.split('').reverse().join('') + '.' + r;
        }
        return t.split('').reverse().join('') + '.' + r;
    }

    //去除千分位
    delcommafy(num:any) {
        num = num.replace(/,/g, '');
        return num;
    }

    //去除%
    dislodge(num: any) {
        if (num == '' || num == null || num == undefined) {
            return '';
        }
        num = num.replace(/%/g, '');
        num = num / 100;
        return num
    }

    //添加%
    addDislodge(num: any) {
        if (num == '' || num == null || num == undefined) {
            return '';
        }
        num = num * 100 + "%";
        return num
    }
