---
title: 判断对象是否为空
date: 2019-09-12 09:39:47
tags:
    - IT技术
    - 前端
---
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
<!--more-->
    /**
     * 判断对象的属性是否为空
     * @param obj 
     */
    isNotEmptyObject(obj: any): boolean {
        if (typeof obj === "object") {
            if (Object.keys(obj).length > 0) {
                return true;
            }
        }
        return false;
    }
    /**
     * 判断对象是否为空对象
     * @param value 
     */
    isNotBlankAndEmptyObject(value): boolean {
        if (value === null || value == undefined || value === "") {
            return false;
        }
        if (this.isNotEmptyObject(value)) {
            return true;
        } else {
            return false;
        }
    }
