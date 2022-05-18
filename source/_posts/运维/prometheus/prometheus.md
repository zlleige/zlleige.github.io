---
title: prometheus学习笔记
date: 2022-05-18  
categories:
- [运维监控,可观测性]
tags:
- prometheus
- 可观测性
- 运维监控
description: prometheus学习笔记
---



> ​	[Prometheus马哥亲讲_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1PT4y1P7bX?p=1)





# 一、监控系统的前世今生



## 1.1 监控系统发展史



SNMP 监控时代



当今的监控系统



未来的监控系统

- DataOps 
- AiOps

## 1.2 监控系统组件

监控系统基本组件

- 指标数据采集
- 指标数据存储
- 指标数据趋势分析及可视化
- 告警



## 1.3  监控体系



![image-20220518202002188](Untitled/image-20220518202002188.png)

## 1.4 云原生时代的可观测性



![image-20220518202147401](Untitled/image-20220518202147401.png)

## 1.5 监控方法论

![image-20220518202745411](prometheus/image-20220518202745411.png)

### 1.5.1 Google的四大黄金指标

![image-20220518202939768](prometheus/image-20220518202939768.png)



### 1.5.2Use 方法



![image-20220518203122001](prometheus/image-20220518203122001.png)

### 1.5.3RED 方法



![image-20220518203246735](prometheus/image-20220518203246735.png)



# 二 Prometheus 入门



## 2.1 prometheus 是什么

​	时序数据库TSDB

![image-20220518203459841](prometheus/image-20220518203459841.png)



## 时序数据简介





![image-20220518203621518](prometheus/image-20220518203621518.png)



## prometheus do



![image-20220518203709738](prometheus/image-20220518203709738.png)



- 基于http协议
- pull 模式 作为客户端从endpoint抓取数据



白盒监控：作为一种自行方式，被监控系统内部能够自己生成指标，由监控系统采集

黑盒监控：对于目标系统没有侵入性，基于探针的方式

采用以下三种方式进行白盒监控

![image-20220518203907700](prometheus/image-20220518203907700.png)



![image-20220518204608811](prometheus/image-20220518204608811.png)



- Exporters
  - 指标获取器，作为服务的客户端，采集原始指标，转换为prometheus格式的指标数据
- instructiontation
  - 系统上报的指标符合prometheus的格式
- pushgateway
  - 瞬时应用，上报指标



## pull or push 



![image-20220518204632508](prometheus/image-20220518204632508.png)





## prometheus 生态组件



![image-20220518204649614](prometheus/image-20220518204649614.png)



storage: TSDB 时序数据库

![image-20220518205047870](prometheus/image-20220518205047870.png)



## prometheus  数据模型

![image-20220518205157706](prometheus/image-20220518205157706.png)



- 每个指标都会生成时序点
- 同一个指标比如cpu_usage，可能匹配三个甚至多台主机，用标签区分

## 	指标类型

![image-20220518205736031](prometheus/image-20220518205736031.png)

指标的数据格式：

​	

## 作业（job）和实力（instance）



![image-20220518205936127](prometheus/image-20220518205936127.png)





## PromQL

![image-20220518210447931](prometheus/image-20220518210447931.png)





## Instrumentation (程序仪表)



![image-20220518210714619](prometheus/image-20220518210714619.png)





## Alerts



![image-20220518210826906](prometheus/image-20220518210826906.png)



# 三 Prometheus 架构及组件



![image-20220518211408854](prometheus/image-20220518211408854.png)



















