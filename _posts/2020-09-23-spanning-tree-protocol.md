---
layout: post
title: How is Spanning Tree Protocol Established?
date: 2020-09-23 013:43 -0500
categories: [CCNA]
tags: [Routing and Switching]
---
# Spanning Tree Protocol
Imagine you are a switch. You are connected to another switch, and both of you are connected to a third switch. If you send a broadcast message to the internet, it will go through all of the switches connected to you, and then back. This causes a loop, and the broadcast message will continue to loop through the switches until the network is congested.

Spanning Tree Protocol (STP) is a layer 2 protocol that prevents loops in a network by disabling redundant paths between switches.

# How is Spanning Tree Protocol Established?
Spanning Tree Protocol is established by the following steps:

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