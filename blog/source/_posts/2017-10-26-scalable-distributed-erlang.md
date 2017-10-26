---
title: Scalable Distributed Erlang
date: 2017-10-26 15:22:18
tags: Erlang
categories: Programming Language
---

Erlang从语言层面就提供了构建分布式系统的能力，多个node可以互相通信连接。但是套用在现代常用的分布式架构上会有些奇怪。少量的node还可以，node多起来的话，node之间的连接维护会很恐怖的。原生erlang比较适合于构建基于比较少节点的分布式运算。今天读到了一篇[*论文*](http://release-project.softlab.ntua.gr/documents/ifl12.pdf)就是讲述怎样构建适用于现代云平台的Scalable Distributed Erlang。里面也提到了节点通信问题，另外还提到了一个大规模节点下显性进程调用问题并且给出了一套解决方案，能够扩展erlang节点并且保留supervisor等很好的特性。但其实我想构建小规模的erlang集群其实也挺适用于现在流行的微服务框架吧，毕竟现在的业务都是比较复杂的。