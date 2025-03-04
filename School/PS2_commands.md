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

Redistribucia IPv6 default route

```
ipv route ::/0 OUT_INTERFACE NEXT_HOP_IP  # odporuca sa next hop IP
ipv router eigrp 1
    redistribute static
    redistribute static metric BW DEL REL LOAD MTU
```

Manualna Sumarizacia

```
router eigrp AS
    no auto-summary

int g0/0
    ip summary-address eigrp AS SIET MASKA
    ipv summary-address eigrp AS IPV6_ADDRESS [ADMIN_DISTANCE]
```

Autentifikacia (iba MD5)

```
key chain MENO
    key CISLO
        key-string HESLO
    key INE_CISLO
        key-string INE_HESLO

int g0/0
    ip authentication mode eigrp AS md5
    ip authentication key-chain eigrp AS MENO

do show key chain
```

Zmena casovacov

```
ip hello-interval eigrp AS_NUMBER HELLO_INTERVAL
ip hold-time eigrp AS_NUMBER HOLD_TIME

ipv hello-interval eigrp AS_NUMBER HELLO_INTERVAL
ipv hold-time eigrp AS_NUMBER HOLD_TIME
```

Load balancing

```
router eigrp 100
    variance 2
    maximum-paths 3  # LB nad max 3 cestami
ip hello-interval eigrp AS_NUMBER HELLO_INTERVAL
ip hold-time eigrp AS_NUMBER HOLD_TIME
```

## OSPF

```
do show ip osfp neighbor
do show ip osfp interface g0/0
```
