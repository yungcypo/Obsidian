# PS2 - Commands

Prikazy PS2

## EIGRP

```
show ip eigrp neighbors
show ip eigrp topology
show ip eigrp topology all-links

show ip eigrp interfaces
show ip protocols
show ip eigrp traffic
show ip eigrp events
```

```
router eigrp AUTONOMOUS-SYSTEM-NUMBER
    no auto-summary
    network NUMBER [WILDCAD-MASK]
```

IPv6

```
ipv6 unicast-routing
int g0/0
    ipv6 eigrp 1

ipv6 router eigrp 1
    eigrp router-id 1.1.1.1
    no shut
```

Manualna Sumarizacia

```
int g0/0
    ...
```
