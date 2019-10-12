---
title: 数学中的加减乘除运算
date: 2019-09-12 08:42:57
tags:
    - IT技术
    - 前端
---
  
    private digit: number;
    private precision: number;

    constructor() {
        this.setDigit(2);
    }
    /**
     * 设置小数位数
     * @param d 
     * pow() 方法可返回 x 的 y 次幂的值
     */
    setDigit(d: number) {
        this.digit = d;
        this.precision = Math.pow(10, this.digit);
    }
<!--more--> 
    /**
     * 加法
     * @param v1 
     * @param v2 
     * round() 方法可把一个数字舍入为最接近的整数。
     */
    add(v1: number, v2: number): number {        
        return Math.round((v1 * this.precision + v2 * this.precision)) / this.precision;
    }
    /**
     * 减法
     * @param v1 
     * @param v2 
     */
    sub(v1: number, v2: number): number {
        return Math.round((v1 * this.precision - v2 * this.precision)) / this.precision;
    }
    /**
     * 乘法
     * @param v1 
     * @param v2 
     */
    mul(v1: number, v2: number): number {
        return Math.round((v1 * v2) * this.precision) / this.precision;
    }
    /**
     * 除法
     * @param v1 
     * @param v2 
     */
    div(v1: number, v2: number): number {
        return Math.round((v1 / v2) * this.precision) / this.precision;
    }

