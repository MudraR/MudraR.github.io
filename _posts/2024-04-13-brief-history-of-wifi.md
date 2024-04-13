---
layout: post
title: A Brief History of 802.11 (Wi-Fi)
date: 2024-04-13 03:41 -0500
---

As I look to purchase a new router, I wanted to be reminded of what the latest standards (Wi-Fi 7) actually introduce compared to the other 802.11 standards.

I'm also hoping this will save me time in 5 years when Wi-Fi 8 routers hit the market. 

# What is 802.11?

- The first wireless technology standard
- Defined wireless connectivity at 1Mbps and 2Mpbs within a LAN
- Applied to layers 1 and 2 of the OSI Model

```mermaid
flowchart TD
    Application-->Presentation
    Presentation-->Session
    Session-->Transport
    Transport-->Network
    Network-->Data
    Data-->Physical
  subgraph Application[Application]
    A[Top most layer that serves the application to the end user. \n Exmaple protocols are HTTP and HTTPS.]
  end
  subgraph Presentation[Presentation]
    P[The presentation layer is where the final format of the data is processed. \n For example, it would format the data in a way the application layer can read. \n It would be where json, csv, or xml data is processed.]
  end
  subgraph Session[Session]
    S[The session layer is where sessions between two communicating processes is established. ]
  end
  subgraph Transport[Transport]
    T[Transport Layer]
  end
  subgraph Network[Network]
    N[Network Layer]
  end
  subgraph Data[Data Link]
    D[Data Link Layer]
  end
  subgraph Physical[Physical]
    Ph[Physical Layer]
  end
```

