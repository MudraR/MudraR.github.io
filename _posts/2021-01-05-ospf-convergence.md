---
layout: post
title: OSPF Convergence with Messages, Data Structures and the Dijkstra Algorithm
date: 2021-01-05 02:29 -0500
categories: [CCNA]
tags: [Routing and Switching]
---
# What is OSPF?

Open Shortest Path First (OSPF) is a link-state routing protocol that uses the Dijkstra's Shortest Path First (SPF) Algorithm to calculate the best paths through the network. 

OSPF is a classless, vendor-neutral routing protocol that supports VLSM and CIDR. It sends the entire routing table to its neighbors, which is called the Link State Database (LSDB). OSPF routers use the LSDB to calculate the best routes through the network.

Convergence in OSPF is the process of routers learning about the network topology and creating the best routes through the network. Convergence is the process of establishing OSPF neighbor adjacencies, creating the Link State Database (LSDB), and calculating the best routes through the network.

## Messages Used in OSPF Convergence

- Hello
- Database Description
- Link State Request
- Link State Update
- Link State Acknowledge

The Hello Messages are used for knowing the routers' neighbors and maintain adjacency.

Once the Neighbor Adjacency is established, a Database Description message is used to describe the LSDB so that the routers can make sure the LSDBs are in sync throughout the network.

Once the adjacency is established, the routers exchange Link State Advertisements (LSAs). These advertisements are flooded throughout the network until each router has each other's LSAs. LSAs contain the state and cost of each directly connected link.

Even if the LSDB is synchronized, there could still be LSAs that are missing in the database. The Link State Request (LSR) message is used to inform OSPF neighbors to send the most current version of the missing LSAs.

The Link State Update messages are sent to directly connected neighbors who have requested LSRs.

Link State Acknowledgement (LSAck) messages make the flooding of LSAs reliable. Each LSA must be explicitly acknowledged. Multiple LSAs can be acknowledged in a single LSAck packet.

Once the Adjacency Database and LSDB is created, the router uses Dijkstra's SPF Algorithm to calculate the Forwarding Database. The SPF Algorithm creates an SPF Tree with all of the routes calculated with the speed and cost throughout the network and updates the routing table with the best possible routes.

- The Hello Messages → Neighbor Adjacency Table
- The Database Description and LSAs → LinkState Database
- The SPF Algorithm → SPF Tree → Forwarding Database
