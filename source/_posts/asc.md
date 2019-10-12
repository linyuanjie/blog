---
title: 升序、降序方法
date: 2019-09-12 09:35:55
tags:
    - IT技术
    - 前端
---
	public compareDesc: any //降序方法
    public compareAsc: any //升序方法
<!--more-->
    this.compareDesc = (value1: any, value2: any) => {
            value1 = Number(value1.key);
            value2 = Number(value2.key);
            if (value1 < value2) {
                return 1;
            } else if (value1 > value2) {
                return -1;
            } else {
                return 0;
            }
        }
        this.compareAsc = (value1: any, value2: any) => {
            value1 = Number(value1.key);
            value2 = Number(value2.key);
            if (value1 < value2) {
                return -1;
            } else if (value1 > value2) {
                return 1;
            } else {
                return 0;
            }
        }