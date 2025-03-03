# PS2 - Commands

Prikazy PS2

## EIGRP

Show prikazy

```
show ip eigrp neighbors
show ip eigrp topology
show ip eigrp topology all-links  # aj susedia co nesplnaju FC

show ip eigrp interfaces
show ip protocols
show ip eigrp traffic
show ip eigrp events
```

Konfiguracia

```
router eigrp AUTONOMOUS-SYSTEM-NUMBER
    no auto-summary
    network NUMBER [WILDCAD-MASK]
    network NUMBER [NETWORK-MASK]

    eigrp router-id IPV4-ADDRESS

    passive-interface g0/0
    passive-interface default  # nastavi vsetky

int g0/0
    bandwidth KILOBITS
    delay TENS_OF_MICROSECONDS
```

Ak treba ovplyvnit vyber cesty tak nepouzivat `bandwidth`, pouzivat `delay`

Overenie

```
do show ip eigrp neighbors
do show ip eigrp neighbors detail

do show ip eigrp interfaces
do show ip eigrp interfaces detail

do show ip protocols
do show ip eigrp topology
do show ip eigrp topology all-links

do show ip route eigrp
do show ip eigrp traffic
do show ip eigrp events
```

IPv6

```
ipv6 unicast-routing
int g0/0
    ipv6 eigrp 1

ipv6 router eigrp AUTONOMOUS-SYSTEM-NUMBER
    eigrp router-id 1.1.1.1
    no shut

int g0/1
    ipv6 eigrp 1
```

Manualna Sumarizacia

```
int g0/0
    ...
```

## OSPF

```
do show ip osfp neighbor
do show ip osfp interface g0/0
```
