---
layout: post
title: Reasons Of The Failure Of Client Call In Distributed System
categories: zh
category: zh
tag: Availability

---

# Preface

As a provider of RPC and backend service, what I most interest in is the success ratio of client call. Because of high QPS,  any abnormal situation will arise large failures.

So I conclude seasons which arise failures in my work.

There is a precondition that logic of code is right.

Two reasons will arise failure:
1. Process time takes too long.
2. Process time is normal, but the connection of client and service in bad situation.

# Process time takes too long

Here is detail reason when process time takes too long.

## Application is no warm up
Normal application may depends on Cache, DB, RPC service. Components like Hystrix are needed. But Hystrix's thread pool and caches's connection of client and server are lazy init. When first batch requests come, application need init components, so the request will be longer than follows.

### Solutions

I have tried two solutions：

1. Add server weight incrementally. Less requests yield less failures.
2. Init components eagerly. But some components like Hystrix don't provide ability to init thread poll eagerly

There is another way which is more complex. After startup, copy some requests from online server, and use them to warm up this startup server.

## Dependency Failure
emmm. Dependencies may failure sometimes, especially RPC and Cache. Their availability is important to my application.

### Solutions

Common solution is isolating the failling dependencies.

When Cache is unavailable, my server's response time increament significantly. In my solution, I fetch data from more than one source concurrently beside of isolation.

## GC takes too long

My application use G1 GC. In some servers Reference Object Processing Takes Too Long

``-XX:+ParallelRefProcEnabled`` is useful

Document ：https://docs.oracle.com/javase/9/gctuning/garbage-first-garbage-collector-tuning.htm#GUID-40B64CD4-9844-4E3E-A0BB-81556AC04C74

Document above is about JDK 9, but argument is available in JDK 7/8.

## CPU problems

### CPU.steal too high

Today more and more server uses vm, we should share CPU with other vms. When CPU.steal is too high, My application will get less cpu to use.

Here is a good blog: http://blog.scoutapp.com/articles/2013/07/25/understanding-cpu-steal-time-when-should-you-be-worried

## Swap too high
Swap slow down my application. But why swap is too high, reason is different each case.

# Network

When failure ratio increase in client metrics, but response time is normal in server metrics. Problmes must be occurred in network. Commonly, connection between client and server use TCP, so there must be something wrong with TCP.


