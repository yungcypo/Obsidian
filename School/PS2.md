# PS2

Poznamocky k predmetu Pocitacove Siete 2

## Opakovanie

Smerovaci proces

![](../others/images/ps2_smerovaci_proces.png)

Metody spracovania paketov

- Process switching
  - Kazdy paket prejde celym procesom smerovania
- Fast switching
  - Prvy paket do daneho ciela prejde celym procesom smerovania
  - Vysledok smerovania si router odlozi do tzv. "route cache", na zaklade coho budu smerovane dalsie pakety
- Cisco Express Forwarding (CEF)
  - Router si vysledky pre smerovanie pripravi dopredu

Smerovacie protokoly podla algoritmu

- Distance-vector
  - RIP, EIGRP
  - Celkovo jednoduchsie, vhodne pre mensie siete
  - Smerovace si vymienaju zoznam sieti a (z ich pohladu) najlepsie vzdialenosti do nich
  - Smerovace nepoznaju celu topologiu
  - Informacie ziskavaju od susedov
    - Periodicky (RIP + IGRP), aj ked sa nic nedeje (sluzi ako Keep-Alive)
    - Ked nastane zmena (Event-Driven) (EIGRP) - tabulka sa posle len na zaciatku a pri zmene, Keep-Alive pomocou Hello sprav
  - Spravy: vektory vzdialenosti
- Link-state
  - OSPF, IS-IS
  - Celkovo komplexnejsie, vhodne pre vacsie siete
  - Smerovace si vymienaju informacie pre tvorenie grafovej reprezentacie siete
  - Kazdy smerovac detailne pozna celu topologiu (lepsie, ale narocnejsie (CPU, RAM))
  - Link-state packets (LSP), Link-state databaza (LSDB)
  - Spravy: popisy prepojov
- Path-vector
  - BGP, MultiProtocol-BGP
  - Smerovace si vymienaju zoznam sieti a CESTU (namiesto vzdialenosti pri DV) od seba ku nim
  - Spravy: vektory atributov (t.j. polia)

Dalsie delenie smerovacich protokolov

- Interior Gateway Protocols (IGPs)
  - Smerovanie vo vnutri autonomneho systemu
  - RIP, EIGRP (Distance-vector) alebo OSPF, IS-IS (Link-state)
  - Pre IPv6 RIPng, EIGRP for IPv6, OSPFv3, IS-IS for IPv6
- Exterior Gateway Protocols (EGPs)
  - Smerovanie medzi jednotlivymi autonomnymi systemami
  - BGP (Path-vector)
  - Pre IPv6 BGP-MP

Metrika

- Ohodnotenie cesty do cielovej siete
- Ak do cielovej siete existuje viacej ciest, dany protokol vyberie tu najlepsiu na zaklade metriky
- Kazdy protokol si urcuje metriku inak
  - Protokoly pracujuce s jednym typom metriky
    - RIP - hops
    - OSPF - rychlost linky
  - Protokoly pracujuce s kompozitnou metrikou
    - EIGRP - rychlost + oneskorenie, volitelne aj zataz a spolahlivost

Administrativna vzdialenost

- "Doveryhodnost" smerovacieho protokolu
- Mozem mat nasadenych viacero protokolov ktore mi hlasia cestu do cielovej siete ale musim vybrat iba jeden - na zaklade metriky
- Cim nizsia metrika tym lepsie

| Protokol                      | Metrika |
| ----------------------------- | ------: |
| Priamo pripojena siet         |       0 |
| Staticka siet                 |       1 |
| EIGRP sumarna siet            |       5 |
| BGP z ineho AS                |      20 |
| EIGRP interna siet            |      90 |
| OSPF                          |     110 |
| IS-IS                         |     115 |
| RIP                           |     120 |
| On-Demand Routing (ODR)       |     160 |
| BGP z toho isteho AS          |     200 |
| DHCP                          |     254 |
| Absolutne nedoveryhodny zdroj |     255 |

## EIGRP

Enhanced Interior Gateway Routing Protocol

Cisco Proprietary, zacina sa rozsirovat IETF open standardizacia

Pokrocily classless distance-vector protokol (podla Cisco "hybridny", aj ked actually nie)

Jediny distance-vector ktory garatnuje bezsluckovost

Automaticka aj manualna sumarizacia, autentifikacia, rychla konvergencia

Multicast `224.0.0.10` a `FF02::A`

Admin distance

- Interne: 90 (jedno z najnizsich)
- Externe: 170
- Sumarne polozky (discar routes): 5

Podla cisco vhodny aj do velkych sieti

### Vlastnosti?

#### Protocol-dependent modules (PDM)

Cinnost EIGRP je rovnaka pre rozne L3 protokoly

Topology table namiesto Routing table

Susedia - ziadny neigh = ziadne routing info

#### Reliable Transport protocol (RTP)

Koncept, ktory zabezpecuje spolahlivost

Multicastom sa posielaju spravy - cislovanie multicast sprav a potvrdzovanie ich prijatia

- Ak sused potvrdi = Conditional Receive
- Ak sused nepotrvrdi = Laggard = pribrzdeny, vyzaduje viac komunikacie
  - Ak aj tak dlho nepotrvrdi - vyhlasim za mrtveho

#### Udrziavanie vztahov so susedmi

Info sa prenasa iba ked nastane zmena v topo

#### Hello mechanizmus a tabulka susedov

Hello sprava - info, ze sused este zije

Pravidelne sa posielaju v casovych intervaloch

- Na pomalsich linkach (< 1.5Mbps) kazdych 60 sekund
- Na rychlejsich linkach kazdych 5 sekund

Ak sa v priebehu `3 x Hello Time` (15, resp. 180 sekund) sused neozve, je mrtvy a zabudneme co nam poslal

Aby dvaja boli susedia, musia mat v pakete (co si vymenia) zhodne parametre:

- Cislo autonomneho systemu
- K-hodnoty - metriky ktore pouzivaju
- Spolocna IP siet (subnet?)

Ak susedia nie sme tak si nevymienaju routovacie tabulky

### Pojmy v EIGRP

#### Reported Distance (RD)

Vzdialenost do siete, ktoru mi nahlasil sused

Sused nareportoval ako je daleko do danej siete

#### Computed distance (CD)

Reported distance + moja vzdialenost k nemu

#### Feasible Distance (FD)

Doposial historicky najkratsia distance zo vsetkych CD

CD mozu byt viacere, FD iba jedna

Lokalna hodnota ktora nie je nikam ohlasovana

Nemoze stupat (lebo by sa ohrozila bezsluckovost), moze iba klesat

#### Feasibility Condition (FC)

Zarucuje bezsluckovost

RD < FD => nemoze obsahovat slucku

Ak RD >= FD, tak je mozne ze sused routuje cezomna = slucka

#### Successor a Feasile successor

Successor - najlepsia, najkratsia cesta do cielovej siete bez sluciek

Feasible successor - backup Successor (tiez bez sluciek)

Possible successor - mozno vedie do cielovej siete, ale moze mat slucky (ked nastane situacia kedy by sa mal pouzit tak sa ho opytam)

#### Diffusing computations

?

Hladanie cesty pri strate smerovacej info

#### Neighbod table

Tabulka susedov

#### Topology table

Tabulka informacii o cielovych sietach a ich stave, FD, RD

### Metrika v EIGRP

Zklada sa z 6 parametrov (najcastejsie sa vyuzivaju prve dva)

- Bandwidth (staticky parameter, implicitne zapnuty)
- Delay (staticky parameter, implicitne zapnuty)
- Reliability (dynamicky vyhodnocovany, implicitne vypnuty)
- Load (dynamicky vyhodnocovany, implicitne vypnuty)
- MTU (staticky parameter, nevstupuje do vypoctov)
- Hop count (funguje len ako tvrdy limit na max dlzku cesty v hopoch)

#### Vypocet metriky

`Metric = BW + D`

- BW - bandwidth = `(10^7 Kbps / najpomalsie rozhranie) * 256`
- D - delay (v desiatkach mikrosekund) = `SUM(vsetky oneskorenia / 10) * 256`

### Load balancing

`equal-cost load balancing` - vie kazdy protokol, rovnaka metrika = robim LB

`unequal-cost load balancing` - kedze je metrika v milionoch, je tazko trafit 2 rovnake metriky - nastavi sa variance = povolena odchylka?

### Druhy EIGRP paketov

- Hello (Type 5) - zistujem ci sused zije alebo nie
- Update (Type 1) -
- Query (Type 1) - pytam sa na specificku cestu ak som stratil cestu
- Reply (Type 4) -
- Ack (Type 2) -

### Default route

Neexistuje default route ako taka, treba workaround

```
ip route 0.0.0.0 0.0.0.0 serial0/1

redistribute static  # bud toto
network 0.0.0.0  # alebo toto

```
