---
title: 日期时间处理
date: 2019-09-12 13:59:38
tags:
    - IT技术
    - 前端
---
![](rainbow.jpg)

    timeZone: number = 8;

    /**
     * 日期转换处理
     * @param date 
     * @param format 
     */
    formatDate(date: string, format: string): string {
        let tmpDate = moment(date, 'YYYY/MM/DD');
        return tmpDate.format(format)
    }

 <!--more-->
 
    /**
     * 调用保存接口前，日期需要在service层进行减8小时处理
     * @param date
     */
    transform(date: string | Date): string {
        let formatDate: Date;
        // 若日期非法则直接返回空
        if (date === null || date === '' || date == undefined) {
            return '';
        }
        console.log("transform日期处理开始 " + date);
        // 若日期为yyyy-MM-ddTHH:mm:ss.fff的字符串则需要转换
        if (typeof date === "string") {
            date = this.datePipe.transform(date, 'yyyy/MM/dd HH:mm:ss');
            formatDate = new Date(date);
        } else {
            formatDate = date;
        }
        formatDate = new Date(formatDate.setTime(formatDate.getTime() - 1000 * 60 * 60 * 8));
        let value = this.datePipe.transform(formatDate, 'yyyy-MM-ddTHH:mm:ss.0');
        console.log("transform日期处理结束 " + value);
        return value;
    }
    /**
     * 对于接口返回的日期且展示页面可编辑(nzDatePicker控件),使用此方法在service层进行日期加8小时处理
     * @param date (yyyy-MM-ddTHH:mm:ss.fff)
     */
    showEditTransform(date: string): any {
        let formatDate: Date;
        if (date == null || date == undefined || date === "") {
            return "";
        }
        console.log("showEditTransform日期处理开始 " + date);
        date = this.datePipe.transform(date, 'yyyy/MM/dd HH:mm:ss');
        formatDate = new Date(date);
        formatDate = new Date(formatDate.setTime(formatDate.getTime() + 1000 * 60 * 60 * 8));
        console.log("showEditTransform日期处理结束 " + formatDate);
        return formatDate;
    }
    /**
     * 将字符串日期加8小时且格式化成Date对象类型(页面显示数据前进行日期处理)
     * @param formatData 
     * @param formatObj 
     */
    increaseAndformatDate(formatData: any, formatObj = []) {
        if (formatObj.length == 0) {
            return formatData;
        }
        if (formatData instanceof Array) {
            formatData.forEach(item => {
                for (let index = 0; index < formatObj.length; index++) {
                    let objKey = formatObj[index];
                    if (item.hasOwnProperty(objKey)) {
                        item[objKey] = this.showEditTransform(item[objKey]);
                    }
                }
            });
            return formatData;
        }
        if (this.isNotBlankAndEmptyObject(formatData)) {
            for (let index = 0; index < formatObj.length; index++) {
                let objKey = formatObj[index];
                if (formatData.hasOwnProperty(objKey)) {
                    formatData[objKey] = this.showEditTransform(formatData[objKey]);
                }
            }
        }
        return formatData;
    }
    /**
     * 将Date类型数据减8小时且格式化成字符串类型(调用保存更新接口前进行日期处理)
     * @param formatData 
     * @param formatObj 
     */
    reduceAndToStringDate(formatData: any, formatObj = []) {
        if (this.isBlank(formatObj) || formatObj.length == 0) {
            return formatData;
        }
        if (formatData instanceof Array) {
            formatData.forEach(item => {
                for (let index = 0; index < formatObj.length; index++) {
                    let objKey = formatObj[index];
                    if (item.hasOwnProperty(objKey)) {
                        item[objKey] = this.transform(item[objKey]);
                    }
                }
            });
            return formatData;
        }
        if (this.isNotBlankAndEmptyObject(formatData)) {
            for (let index = 0; index < formatObj.length; index++) {
                let objKey = formatObj[index];
                if (formatData.hasOwnProperty(objKey)) {
                    formatData[objKey] = this.transform(formatData[objKey]);
                }
            }
        }
        return formatData;
    }

    /**
     * 保存更新前进行日期格式化,减8小时处理
     * @param newData 
     * @param oldData 
     */
    formatDataForDate(newData: any, oldData: any, formatObj = []): { "newData": any, "oldData": any } {
        let tempVar = { "newData": null, "oldData": null };

        if (formatObj.length == 0) {
            tempVar.newData = newData;
            tempVar.oldData = oldData;
            return tempVar;
        }
        tempVar.newData = this.reduceAndToStringDate(newData, formatObj);
        tempVar.oldData = this.reduceAndToStringDate(oldData, formatObj);
        return tempVar;
    }

    /**
     * 格式化时间为GMT标准时区时间，返回字符串
     * 使用场景：
     * 1. 调用查询接口前，格式化时间参数，
     * @param date 
     */
    formatDateToStringUseGMT(date: string | Date): string {
        let formatDate: Date;
        // 若日期非法则直接返回空
        if (date === null || date === '' || date == undefined) {
            return '';
        }
        // 若日期为yyyy-MM-ddTHH:mm:ss.fff的字符串则需要转换
        if (typeof date === "string") {
            formatDate = new Date(this.datePipe.transform(date, 'yyyy/MM/dd HH:mm:ss'));
        } else {
            formatDate = new Date(date.getTime());
        }
        formatDate = new Date(formatDate.setTime(formatDate.getTime() - 1000 * 60 * 60 * this.timeZone));
        let value = this.datePipe.transform(formatDate, 'yyyy-MM-ddTHH:mm:ss.0');
        return value;
    }
    /**
     * 
     * @param v 
     */
    transferCordysDateStringToUTC(v: string): any {
        let fields = /(\d{4})-(\d{2})-(\d{2})T(\d{2}):(\d{2}):(\d{2})/.exec(v);
        fields[2] = String(Number(fields[2]) - 1); // month is zero base`d
        return new Date(Date.UTC(Number(fields[1]), Number(fields[2]), Number(fields[3]), Number(fields[4]), Number(fields[5]), Number(fields[6])));
    }

    /**
     * 
     */
    getUTCDate(): string {
        let oDate = new Date();

        // handle date part
        let dateSep = '-';
        let day = oDate.getUTCDate();
        let month = oDate.getUTCMonth() + 1;
        let sDay = (day < 10) ? '0' + day : day;
        let sMonth = (month < 10) ? '0' + month : month;
        let sValue = oDate.getUTCFullYear() + dateSep + sMonth + dateSep + sDay + 'T';

        // handle time part
        let timeSep = ':';
        let hours = oDate.getUTCHours();
        let minutes = oDate.getUTCMinutes();
        let seconds = oDate.getUTCSeconds();

        let sHours = (hours < 10) ? '0' + hours : hours;
        let sMinutes = (minutes < 10) ? '0' + minutes : minutes;
        let sSeconds = (seconds < 10) ? '0' + seconds : seconds;
        sValue += sHours + timeSep + sMinutes + timeSep + sSeconds;

        return sValue;
    }

    /**
     * 日期减8小时处理
     */
    dateFormat = function (date, format) {
        date = new Date(date);
        let o = {
            'M+': date.getMonth() + 1, //month  
            'd+': date.getDate(), //day  
            'H+': date.getHours() - 8, //hour+8小时</span>  
            'm+': date.getMinutes(), //minute  
            's+': date.getSeconds(), //second  
            'q+': Math.floor((date.getMonth() + 3) / 3), //quarter  
            'S': date.getMilliseconds() //millisecond  
        };
        if (/(y+)/.test(format))
            format = format.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length));

        for (let k in o)
            if (new RegExp('(' + k + ')').test(format))
                format = format.replace(RegExp.$1, RegExp.$1.length == 1 ? o[k] : ('00' + o[k]).substr(('' + o[k]).length));

        return format;
    }
