---
title: "Es数据延迟"
slug: "Es数据延迟"
description: "" 
date: 2022-05-29T01:32:05+08:00
image: 
math: 
license: 
hidden: false
comments: false
draft: false    
categories: ["学习&笔记"]
tags: ["ES"]
---



### ES数据延迟

ES本身被定义为近实时搜索, ES中每个shard默认会每隔1s自动refresh一次,  也就是说数据可能有1s的延迟, 一般情况下可能对数据要求的可能没有那么高, 延迟数据1s可以接受, 但是有些情况可能就没办法接受了, 那就需要我们来优化了.

+ 修改索引刷新时间`refresh_interval`, 生产环境注意数值过小会影响系统性能

  ~~~
  PUT /my_logs
  {
    "settings": {
      "refresh_interval": "30s"  # 100ms
    }
  }
  
  # 关闭自动刷新
  PUT /my_logs/_settings
  { "refresh_interval": -1 } 
  ~~~

+ 手动刷新

  ~~~
  POST /_refresh   # 刷新所有索引
  POST /blogs/_refresh   # 刷新blogs索引
  ~~~

  

