---
title: 在使用lombok的时候，如何override Setter方法
date: 2016-02-18 15:15:20
tags: lombok
---

使用lombok插件会自动帮助我们生成Getter和Setter方法，帮我们省去了很多代码。
但是有时候，我们会需要重写Getter 或者 Setter方法。
我的例子是我有一个BO类叫ReportDailyClientSession，其中有一个字段是reportDate，存在数据库中的是Long型，另外一个字段是reportDateStr，为reportDate的字符型日期，如2015/11/06

## 解决方案1：

``` java
@Getter @Setter
public class ReportDailyClientSession extends BaseBo{
private static final long serialVersionUID = 8100184254725887852L;

private @Setter(AccessLevel.NONE) Long reportDate;
private String reportDateStr;
private Integer sumCount;
private Integer portalAuthClickCount;
private Integer portalAuthSmsCount;
private Integer portalAuthUserCount;
private Integer portalAuthWechatCount;
private Integer portalAuthThirdCount;
private Integer portalAuthNoSuccess;

public void setReportDate(Long reportDate) {
	this.reportDate = reportDate;
	this.reportDateStr = DateTimeUtil.getDateStrFromLong(reportDate);
	}
}
```

## 解决方案2：

``` java
public class ReportDailyClientSession extends BaseBo{
private static final long serialVersionUID = 8100184254725887852L;

private @Getter Long reportDate;
private @Getter @Setter String reportDateStr;
private @Getter @Setter Integer sumCount;
private @Getter @Setter Integer portalAuthClickCount;
private @Getter @Setter Integer portalAuthSmsCount;
private @Getter @Setter Integer portalAuthUserCount;
private @Getter @Setter Integer portalAuthWechatCount;
private @Getter @Setter Integer portalAuthThirdCount;
private @Getter @Setter Integer portalAuthNoSuccess;

public void setReportDate(Long reportDate) {
	this.reportDate = reportDate;
	this.reportDateStr = DateTimeUtil.getDateStrFromLong(reportDate);
	}
}
```

## 结论：
解决方案2不适用于字段很多的情况，建议采用解决方案1来Override
