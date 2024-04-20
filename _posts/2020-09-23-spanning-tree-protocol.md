---
layout: post
title: How is Spanning Tree Protocol Established?
date: 2020-09-23 013:43 -0500
categories: [CCNA]
tags: [Routing and Switching]
---
# Spanning Tree Protocol

## 1. Determine the Root Bridge
The Root Bridge is selected from the lowest Bridge ID, which consists of the default BID (32768) + VLAN ID + MAC Address.

## 2. Determine the Root Ports
Root Ports are calculated from the Root Path Cost, which is the following:

| Link Speed | STP Cost-- 802.1D |
|------------|------------------|
| 10 Gbps    | 2                |
| 1 Gbps     | 4                |
| 100 Mbps   | 19               |
| 10 Mbps    | 100              |


If there is an equal cost path, the root port is elected from:
1. Lowest SENDER BID
2. Lowest SENDER port priority
3. Lowest SENDER port ID

## 3. Determine the Designated Ports
The Designated Ports are the best path to receive traffic leading to the root bridge. If one end is a root port, the other end is a designated port.

## 4. Determine the Blocked Ports
Any port that is not a root or designated port is a blocked port.