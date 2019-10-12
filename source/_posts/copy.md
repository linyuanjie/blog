---
title: 克隆或合并数据
date: 2019-09-12 09:43:50
tags:
    - IT技术
    - 前端
---
	/**
     * 克隆或合并数据，数组合并会根据索引进行覆盖(注意：数据必须是json对像格式)
     * @param orignObj 源对象
     * @param targetObj 目标对象
     */
<!--more-->
    copyObjectValue(orignObj: any, targetObj = null) {
        if (this.isBlank(orignObj)) {
            return null;
        }
        if (this.isBlank(targetObj)) {
            if (orignObj instanceof Array) {
                targetObj = [];
            } else {
                targetObj = {};
            }
        }
        let tmpobj = Object.assign(targetObj, orignObj);
        if (orignObj instanceof Array) {
            let tmpArray = [];
            tmpobj.forEach(item => {
                let obj = Object.assign({}, item);
                let keyArray = Object.keys(item);
                let key: any;
                for (let i = 0; i < keyArray.length; i++) {
                    key = keyArray[i];
                    if (typeof item[key] === "object" && item[key] instanceof Date) {
                        obj[key] = new Date(item[key].getTime());
                        continue;
                    }
                }
                tmpArray.push(obj);
            });
            return tmpArray;
        } else {
            let obj = Object.assign({}, tmpobj);
            let keyArray = Object.keys(tmpobj);
            let key: any;
            for (let i = 0; i < keyArray.length; i++) {
                key = keyArray[i];
                if (typeof tmpobj[key] === "object" && tmpobj[key] instanceof Date) {
                    obj[key] = new Date(tmpobj[key].getTime());
                    continue;
                }
            }
            return obj;
        }
    }
    /**
     * 判断对象是否为空
     * @param value 
     */
    isBlank(value: any): boolean {
        if (value === null || value == undefined || value === "") {
            return true;
        }
        return false;
    }
