---
layout: post
title: What are High Availability, Fault Tolerance, Diaster Tolerance, and Disaster Reconvery
categories: en
category: en
tag: HighAvailability FaultTolerance DiasterTolerance DisasterReconvery

---

# Preface
While talking about availability, There are some concepts must be involved, which are High Availability,  Fault Tolerance,  Diaster Tolerance, and  Disaster Reconvery.

For talking about these concepts with others, I did some research to find out what are they.

# High Availability
[High Availability](https://en.wikipedia.org/wiki/High_availability) is
>a characteristic of a system, which aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period.

Most time, HA is measured by [SLA](https://en.wikipedia.org/wiki/Service-level_agreement)

HA is a macroscopic concept.

You system can be called High Availability System, if your system have high uptime.

Disaster Recovery and Fault Tolerance are solutions of High Availability.

While research, I found two wrong way to use HA.
1. Article says it will compare HA and DR, but the real content is comparing DR and FT
2. Article consider that HA is a solution of DR

# Fault Tolerance
[Fault Tolerance](https://en.wikipedia.org/wiki/Fault_tolerance) is:
>the property that enables a system to continue operating properly in the event of the failure of (or one or more faults within) some of its components.

Note that faults appear inside the system. If you want do Fault Tolerance, you should recognize the boundry of system.

# Disaster Tolerance and Disaster Recovery
Why do I talk about DT and DR together？Because, I found DT and DR are same concepts.

Let's see the definition first.
[Disaster Recovery](https://en.wikipedia.org/wiki/Disaster_recovery)
>involves a set of policies, procedures and tools to enable the recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster.

DR has [Seven Tiers](https://en.wikipedia.org/wiki/Seven_tiers_of_disaster_recovery)。

I did not find the definition on Internet. But I found some articles like [this](1) and [this](2).

The definition of DT in these articles seems concrete solution of [highest tier of DR](https://en.wikipedia.org/wiki/Seven_tiers_of_disaster_recovery#Tier_7:_Highly_automated.2C_business_integrated_solution).

So I conclude that DR and DT are same concepts.

I'm prefer to Disater Recovery than Disater Tolerance, because of data below.
## Interesting Data
Google "容灾", Disater Tolerance in chinese, showing 1 million results.

Google "灾难恢复", Disater Recovery in chinses, showing 6 million results.

Google "Disaster Tolerance", showing 660 thousand results.

Google "Disaster Recovery", showing 38 million results。

## Difference between Fault Tolerance and Disaster Recovery
Fault Tolerance is a solution to eliminate the faults **inside** system.

Disaster Recovery is a solution to recovery from disater **outside** system.

[1]:http://docs.oracle.com/cd/E19528-01/819-0420/introduction-7/index.html

[2]:https://docstore.mik.ua/manuals/hp-ux/en/T1906-90022/ch01s02.html

