# Siete
Nieco ku predmetom PIKS, PS1, PS2, PS3   

# Basic config
Defaultna konfiguracia ktora by mala byt vykonana vzdy pri novom zariadeni   

```
hostname
banner motd
line console 0
	logging sync
no ip domain lookup
```

```
username student secret student
username admin privilege 15 secret admin
line console 0
	login local
line vty 0 15
	login local
service password-encryption
enable secret class
```

```
ip domain-name B303.sk
crypto key gen rsa modulus 1024
ip ssh version 2
line vty 0 15
	transport input ssh
```

# Troubleshooting commands
Prikazy ktore len nieco vypisuju  

```
do show run
do show ip int b
do show protocols
do show ip route
```

# Staticke smerovanie
```
ip route {siet} {maska} {vystupna siet | vystupne rozhranie} [metrika]
```
Toto basically hovori, ze *"ak pride paket smerujuci do {siet} s maskou {maska}, posli ho na {vystupnu siet/rozhranie}"*  

Napriklad `ip route 192.168.1.2 255.255.255.0 s0/0/0` hovori *"ak pride paket, ktory ma ist na adresu 192.168.1.2, posli ho na s0/0/0"*  
Napriklad `ip route 192.168.1.2 255.255.255.0 192.168.99.1` hovori *"ak pride paket, ktory ma ist na adresu 192.168.1.2, posli ho na zariadenie s IP 192.168.99.1"*  

Ak je v statickej adrese zadane **vystupne rozhranie**, musime sa uistit ze "za tym rozhranim nieco je" a ze to je prave jeden smerovac ktory bude vediet narabat s paketom  
Ak je v statickej adrese zadana **vystupna IP adresa**, vystupne rozhranie (priamo pripojene) sa zisti rekurzivnym vyhladavanim v smerovacej tabulke

Da sa uviest aj vystupne rozhranie aj adresa - **fully specified**   
```
ip route 172.16.1.0 255.255.255.0 g0/0 172.16.2.2 [metrika]
```

## Default route
Normalna staticka cesta, ktora bude vybrata iba ked sa nenajde ziadne ine zhodne rozhranie (longest prefix match)  
```
ip route 0.0.0.0 0.0.0.0 192.168.1.1
```

## Floating static routes
*"Pojmom \"floating static route\" sa oznacuje staticky zaznam o nejakej sieti, ktory sa do smerovacej tabulky dostane az vtedy, ked iny zaznam o tej istej sieti zo smerovacej tabulku vypadne"*  
Basically zalozna cesta - ak jeden smerovac/cesta vypadne, bude nahradeny/a inym  

Na vytvorenie zaloznej cesty sa zvysi metrika pri jej vytvarani   
```
ip route 0.0.0.0 0.0.0.0 172.16.2.2  
ip route 0.0.0.0 0.0.0.0 10.10.10.2 5  
```

Prvy zaznam je primarny (metrika = default = 0)  
Druhy zaznam je sekundarny (metrika = 5)  

Smerovac vybera zaznam s mensou metrikou  

## Sumarne smerovacie zaznamy
*"Sumarizacia je proces, pri ktorom sa isty pocet cielovych sieti popise jednou vacsou sietou"*  
Znizuje sa pocet zaznamov v tabulke  

Napr. namiesto sieti...  
```
10.1.0.0 /16
10.2.0.0 /16
10.3.0.0 /16
10.4.0.0 /16
```

...mozeme zapisat jeden sumarny zapis ako  
```
10.0.0.0 /14
```

## Troubleshooting 
Prikazy na overovanie  
```
do show ip route
do show ip route static
do show ip route 192.168.1.0

do show ip int b

do show cdp neighbors
do show cdp neighbors detail
```

## IPv6
Basically to iste ako IPv4
```
ipv6 unicast-routing
ipv6 route {siet/prefix} {dalsi smerovac} [metrika]
ipv6 route {siet/prefix} {vystupne rozhranie} [metrika]
ipv6 route {siet/prefix} {dalsi smerovac} {vystupne rozhranie} [metrika]

ipv6 route ::/0 {siet | interface}
```

Sumarny zapis 
```
ipv route 2001:db8:acad::/61
```

# RIP
Routing Information Protocol  
RIP je distance-vector dynamicky smerovaci protokol  
Ako metriku pouziva hop  
Adminstrativna vzdialenost je 120  

|                   | RIPv1     | RIPv2     |
| ----------------- | --------- | --------- |
| Updaty cez        | Broadcast | Multicast |
| VLSM?             | Nie       | Ano       |
| CIDR? (classless) | Nie       | Ano       |
| Sumarizacia       | Nie       | Ano       |
| Autentifikacia    | Nie       | Ano       |

Updaty sa posielaju kazdych 30 sekund cez UDP port 520  

## Basic config
```
router rip
	version 2
	network 192.168.1.0
	network 192.168.2.0
	...
	no auto-summary

do show ip route
do show ip route rip
do show ip protocols
```

## Manualna sumarizacia
```
int s0/0/0
	ip summary-address rip 192.168.1.0 255.255.255.0
```

## Pasivne rozhrania
Pasivne rozhrania budu prijimat updates, ale nebudu posielat  
Vhodne pri stub sietach  
```
router rip
	passive-int g0/0 
```

Alebo mozeme zvolit vsetky ako pasivne a iba niektore "odpasivnit"

```
router rip
	passive-int default
	no passive-int s0/0/0
```

## Redistribucia statickej cesty + default route
Ked potrebujeme cez RIP oznamovat staticku cestu   
```
router rip
	redistribute static
```

Taktiez je mozne redistribuovat priamo pripojene cesty  
```
router rip
	redistribute connected
```

Oznamovanie ostatnym ze "ja som default route"   
```
router rip
	default-information originate
```

Overenie pomocout `do show ip route | begin Gateway`

## Discard route
Discard route je fiktivne virtualne rozhranie ktore zahodi vsetky pakety ktore mu pridu  
Vyuzitie pri vzniku smerovacej slucky  
Basically sa spravi staticka route na rozhranie `Null0`  
```
ip route 192.168.1.0 255.255.255.0 Null0
```

## Autentifikacia v RIP
```
key chain KLUCENKA
	key 1
		key-string h@slisko

int g0/0
	ip rip auth mode {md5 | text}
	ip rip auth key-chain KLUCENKA

do show key chain
do show ip proto
```

## RIPng
RIP pre IPv6
```
ipv6 unicast routing

int g0/0
	ipv6 rip NAZOV enable
int s0/0/0
	ipv6 rip NAZOV enable

do show ipv6 proto
```

> Note: NAZOV je akysi nazov procesu alebo co? Actually sa to *asi* moze volat aj inak, napr. RIP1 

### RIPng Default route
```
int s0/0/0
	ipv6 rip NAZOV default-information originate
```

> Note: Same as before, NAZOV je len nazov, napr. RIPt




# VLAN
Virtual LAN

Access (pristupove) porty - medzi switchom a koncovym zariadenim - neznacuje sa  
Trunk porty - medzi switchom a switchom *(resp. routerom (?))*  

## Trunk Protokoly

| 802.1Q                                       | ISL (Inter-Switch Link)                                            |
| -------------------------------------------- | ------------------------------------------------------------------ |
| Open source od IEEE                          | Cisco Proprietary                                                  |
| Pridana polozka TAG do Ethernet II. hlavicky | Znackovanie formou tunelovania = Enkapsulovany cely Ethernet ramec |
| Velkost +4B pre TAG (0x8100, CoS, DEI, VID)  | Velkost +Hlavicka (26B) +CRC (4B) = +30B                           |

### 802.1Q
Pridava sa TAG do Ethernet hlavicky:  
- TPID (Tag Protocol Identifier) 
	- Velkost **16b**
	- Hodnota `0x8100`
- Priority
	- Velkost **3b**
	- Dovoluje robit prioritne ramce v rozsahu 0 az 7
	- Niekedy sa toto prioritne znackovanie nazyva **CoS** (Class of Service)
- CFI
	- Canonical Format Indicator
	- Velkost **1b**
	- V minulosti pre Token Ring siete
	- V sucastnosti vyuzivany pre **Discard Eligible Indicator** = v pripade nutosti zahod ramec
- VID
	- Vlan ID
	- Velkost **12b** 
	- Dovoluje vytvarat $2^{12} = 4096$ VLAN   

Treba prepocitat FCS na konci Ethernetoveho ramca - zmena hlavicky  
Potencionalny problem - *Baby Jumbo frames* - velkost sa zvacsi na 1522B

#### Vyhradene VLAN
- VLAN 0
	- Vyjadruje, ze TAG sluzi len na prenos informacie o priorite (CoS a DEI)
- VLAN 4095
	- Nemalo by sa nikdy objavit
	- Urcene pre vyrobcov na interne testovanie

- VLAN 1 (nie je vyhradena)
	- Default VLAN 
	- Vzdy defaultne pritomna, neda sa zmazat
	- Su tu defaultne zaradene vsetky porty
	- Defaultne je zaroven aj Native VLAN, je dobre to zmenit

#### Proces komunikacie
Na jednom prepinaci
1. Prepinac prijme ramec
2. Pozre sa do smerovacej tabulky **iba na zaznamy pre danu vlan**
3. Ramec ostane nezmeneny a posle sa na vystupne rozhranie

Cez viac prepinacov
1. Prvy prepinac
	1. Prepinac prijme ramec
	2. Pozre sa do smerovacej tabulky **iba na zaznamy pre danu vlan**
	3. Prepinac vidi, ze vystupne rozhranie je oznacene ako **trunk port** *(napr. Fa0/1)*
	4. Prepinac vlozi identifikator (TAG)
	5. Prepne na prislusny interface
2. Druhy prepinac
	1. Prepinac prijme ramec
	2. Pozre sa do smerovacej tabulky **iba na zaznamy pre danu vlan**
	3. Odstrani TAG
	4. Prepne ramec

> Note: V pripade, ze by takato komunikacia nastala pre viac prepinacov (nie len 2), tak *Druhy prepinac* **neodstranuje TAG**, iba ramec prepne dalej na dalsi prepinac  

#### Nativna VLAN
Napr. v pripade ze cez trunk port pride ramec bez znacky  
Cisco pouziva pojem *Native VLAN*, iny vyrobcovia aj *Untagged VLAN* alebo *Primary VLAN*  
Definuje sa pre kazdy port zvlast *(?)*  

- Ak ma byt frame odoslany do nativnej vlan, tak znacku nedostane, resp. ak ju ma tak odstrani
- Ak pride frame bez znacky, bude zaradeny do nativnej vlan

Best practice:  
- Nativna VLAN bude iba jedna *(pre dvojicu portov MUSI byt, medzi troma smerovacmi sa da zmenit na inu, ale preco by to niekto robil)*  
- Zmenime, aby VLAN 1 (default VLAN) nebola nativna

## VLAN vo vacsich sietach
Ak mame `xy` prepinacov s `xyz` VLAN, tak konfiguracia moze byt narocna/zdlhava  

Riesenim mozu byt viacere protokoly:  
- VTP *(VLAN Trunking Protocol)* - Cisco
- MVRP *(Multiple VLAN Registration Protocol)* - IEEE - predchodca GVRP
- SNMP *(Simple Network Management Protocol)*

**Iba sirenie VLAN databazy!**  

Protokoly spravia jeden smerovac ako server, ktory to bude posielat viac klientom   
Zarucuju identicky zoznam VLAN na prepinacoch v sieti  
Existuju este aj transparentne smerovace - rozosielaju VLAN databazu, ale neovplyvnuju ju svojou databazou - mozu mat inu konfiguraciu  

## Typy VLAN
Pre Cisco smerovace  

Range:
- 0 - 1005
	- *Normal range*  
	- Podporovane vsade  
	- Prenasane pomocou VTP, ak je pouzity
	- Su vzdy ulozene vo `flash:vlan.dat` - uchovane aj pri reboot aj pri zmazani `running-config`
	- Mozu byt ulozene aj v `running-config`
- 1006 - 4096
	- *Extended range*
	- Podporovane na novsich prepinacoch
	- Prenasane pomocou VTPv3 - len velmi nove prepinace
	- Su ulozene v `running-config`
	- Iba pri VTPv3 mozu byt aj vo `flash:vlan.dat`

Typy
- Default VLAN *(1)*
- Native VLAN *(napr. 100)*
- Access VLAN, resp. Data VLAN *(napr. 10, 20, ...)*
	- Konkretna jedna VLAN, do ktorej je zaradeny jeden access port 
- Voice VLAN
	- Data z/do IP telefonu
- Management VLAN *(napr. 99)*

### Management VLAN
Pouziva za na management prepinaca  
Defaultna VLAN 1 by sa mala zmenit na inu
```
interface vlan 99
	ip add 192.168.1.2
```


## DTP - Dynamic Trunk Protocol
Interface moze byt na jednom z nasledovnych rezimov  

```
# DTP, preferujem trunk, ale prisposobim sa druhej strane
switchport mode dynamic desirable 

# DTP, preferujem access, ale prisposobim sa druhej strane (defaultne je toto)
switchport mode dynamic auto   

# nie DTP, napevno trunk
switchport mode trunk   

# nie DTP, napevno access
switchport mode access    


# v netacade bolo aj tento prikaz, ale nie som si sure ze co robi
switchport nonegotiate
```


Ak su na obidvoch stranach rovnake mody tak nie je problem  
Situacia `trunk` a `access` = chyba - limited connectivity  
Situacia `dynamic desirable` a `dynamic auto` = trunk port (vyssia priorita)   

Nejaka ta konfiguracia  
```
interface range fa 0/7 - 8  # kofigurujem interfaces 7 a 8
	switchport trunk encapsulation dot1q   # pouzivam enkapsulaciu 802.1Q
	switchport mode trunk

do show interface trunk 
do show interface f0/7 switchport 
```

## Best practice
- Presunut nepouzivane porty do osobitnej nepouzivanej VLAN *(napr. 1000)*  
	- Idealne tuto VLAN aj suspendovat a vypnut nepouzivane porty
	- Tzv. *Black Hole VLAN*
- Osobitna VLAN pre management  
- Zmenit nativnu VLAN 
- Pouzivat iba SSH
- Po konfiguracii a rozbehu portov vypnut DTP + neponechavat ziadne porty v dynamickom rezime
- Vyhnut sa akemukolvek pouzivaniu VLAN 1

## Prikazy
```
do show vlan brief
do show vlan [brief | id {vlan-id} | name {vlan-name} | summary]

do show int vlan 20
do show int f0/1 switchport

do show dtp int f0/1
```

```
int f0/1
	switchport mode access
	switchport access vlan 20

int f0/2
	switchport mode trunk
	switchport trunk native vlan 99
	switchport trunk allowed vlan 10,20,30,99

int f0/3
	switchport mode access
	switchport voice vlan 150


mls qos trust cos  # enable QoS
```

Zmena z Trunk na Access   
```
int f0/1
	no switchport trunk allowed vlan
	no switchport trunk native vlan
	switchport mode access
```

Vytvorenie VLAN  
Tento priklad vytvori VLAN s cislom `10` a nazvom `studenti`
```
vlan 10
	name studenti
```

Zmazanie VLAN  
Ak zmazem VLAN, v ktorej bol nejaky port, tak port **nebude priradeny nikde**  
```
no vlan 20
```

## VTP


# STP
Spanning Tree Protocol - `IEEE 802.1d`  
 
```
I think that I shall never see
A graph more lovely than a tree.
A tree whose crucial preperty
Is loop-free connectivity.
A tree that must be sure to span
So packet can reach every LAN.
First, the root must be selecter.
By ID, it is elected.
Least-cost path from root are traced.
In the tree, these paths are placed.
A mesh is made by folks like me,
Then bridges find a spanning tree.

*Radia Perlman*
``` 

L2 protokol ktory zabranuje vzniku sluciek na L2  
 > Slucky, Broadcastove burky, nestabilita MAC/CAM tabulky, zacyklenie a zahltenie az kolaps siete  

Komunikacia prebieha pomocou specialnych **BPDU** ramcov *(Bridge Protocol Data Unit)*  
1. Volba Root Bridge (RB) - referencny bod stromu, je len jeden  
2. Volba Root Ports - porty najblizsie k RB  
3. Urcenie Designated (aktivne) a Non-Designated (blokovane) portov  

BPDU okrem ineho obsahuju  
- Root ID
- Cost of Path - vzialenost od RB
- Bridge ID - ID prepinaca ktory posledny manipuloval BPDU
- Port ID - Port, cez ktory bolo odoslane BPDU

**BID** - Bridge ID - jednoznacny identifikator Bridge-a  
Pozostava z Priority *(2B)* a MAC Address *(6B)*  

Podla priority sa urcuje Root - Bridge s najnizsim BID sa stane Root-om  
Pomalsi port = vyssie cislo Priority = mensia sanca byt Root  

## Stavy portov   
Ked sa pripoji/odblokuje port switch-a, nemoze hned forwardovat (nevie co je dalej - dalsi switch = slucka)  

`Disabled port -> Inicialization -> Listening`  

`Listening -> Blocking` alebo `Listening -> Learning -> Forwarding`  

- **`Listening`**
	- Port pocuva a snazi sa zistit, aka je topologia a kde je RB 
	- Prijima, spracovava a preposiela BPDU
	- Neprijima datove ramce, neuci sa MAC adresy
	- Zdrzi sa tu 15 sekund  
	- Podla toho, ci by vznikla slucka alebo nie sa prepne do stavu `Blocking` alebo `Learning`
	- **`Blocking`**
		- Dostane sa sem, ak by forwardovanie sposobilo slucky
		- Iba prijima iba BPDU
		- Zdrzi sa tu 20 sekund 
		- Po 20 sekundach ide zase `Init -> Listening`
	- **`Learning`**
		- Spracovava BPDU
		- Iba prijima datove ramce, z ktorych sa uci MAC adresy
		- Zostane tu 15 sekund, potom ide do `Forwarding`
		- **`Forwarding`**
			- Bezny beh portu

Problem - rychlost konvergenicie - 30 az 50 sekund - riesenie - *Rapid STP (RSTP)* - radovo do 1 sekundy  


| Port state | BPDU             | MAC address table | Forwarding data frames |
| ---------- | ---------------- | ----------------- | ---------------------- |
| Blocking   | Receive          | No update         | No                     |
| Listening  | Receive and Send | No update         | No                     |
| Learning   | Receive and Send | Updating table    | No                     |
| Forwarding | Receive and Send | Updating table    | Yes                    |
| *Disabled* | -                | -                 | -                      |

## Role portov
Aku ulohu hra dany port v strome  

Na RB su vsetky porty `Designated`  
Na Non-Root Bridge su porty `Root`, `Designated` alebo `Non-designated`  

*`Designated port` je port, ktory ma prijima horsie BPDU ako to, ktore odosiela*  
*`Root port` je ten, ktory spomedzi vsetkych portov dostava najlepsie BPDU*  


## Casovace

| Nazov         | Popis                                | Default hodnota | Mozne hodnoty  |
| ------------- | ------------------------------------ | --------------- | -------------- |
| Hello Time    | Cas medzi dvoma BPDU                 | 2 sekundy       | 1 az 10 sekund |
| Forward Delay | Cas v stave `Listening` a `Learning` | 15 sekund       | 4 az 30 sekund |
| Maximum Age   | Cas v stave `Blocking`               | 20 sekund       | 6 az 40 sekund |

## Rozhodovaci proces pouzivany pri porovnavani BPDU
Prepinace pri STP funguju na principe porovnavania ramcov - lepsi ramec = superior, horsi ramec = inferior  

Porovnavaju sa v nasledovnom poradi (nizsie = lepsie)  

---
1. Root Bridge ID
	1. 1. Priority
	2. MAC Address
2. Root Path Cost
3. Sender Bridge ID
4. Sender Port ID
5. Receiver Port ID (len vynimocne)
---

Path cost - podla rychlosti linky (kabla)

| Speed    | STP Path Cost |
| -------- | ------------- |
| 10 Gbps  | 2             |
| 1 Gbps   | 4             |
| 100 Mbps | 19            |
| 10 Mbps  | 100           |

### Port Fast
Access port nemusi cakat na konvergenciu  

## Prikazy
Overovacie prikazy
```
do show spanning-tree
do show spanning-tree summary
do show spanning-tree vlan VLAN_ID
```

Nastavenie/zrusenie STP pre danu VLAN
```
spanning-tree vlan VLAN_ID
no spanning-tree vlan VLAN_ID
```

Nastavenie priority pre switch
```
spanning-tree vlan VLAN_ID priority PRIORITY
```

Nastavenie switcha ako Root (zisti si prioritu u Root-a a znizi ju)
```
spanning-tree vlan VLAN_ID root primary
```

Nastavenie switcha ako zalozny Root
```
spanning-tree vlan VLAN_ID root secondary
```

Konfiguracia Port-fast (jeden port/vsetky porty)
```
int f0/1
	spanning-tree portfast

spanning-tree portfast default
```


## RSTP
Rapid STP  

Ma len 3 stavy  
Zavadza `Edge port` - nieco ako Port Fast vlastnost  
Pouziva take iste BPDU, ale vyuziva mechanizmus *Proposal/Agreement*  
BPDU posiela kazdy switch (nie len Root ako v STP)  
Je spatne kompatibilny  

### Zmena stavov portov   

| STP Port State | RSTP Port State | Aktivny? | Uci sa MAC adresy? |
| -------------- | --------------- | -------- | ------------------ |
| Disabled       | Discarding      | Nie      | Nie                |
| Blocking       | Discarding      | Nie      | Nie                |
| Listening      | Discarding      | Ano      | Nie                |
| Learning       | Learning        | Ano      | Ano                |
| Forwarding     | Forwarding      | Ano      | Ano                |
### Zmena definicie portov

- Root 
	- Iba na Non-Root Bridge
	- Najblizsi port k Root
- Designated
	- Odosiela lepsie BPDU ako prijima 
- Alternate
	- Zaloha Root portu
	- Ked padne Root, snazi sa aktivovat Alternate
- Backup
	- Zaloha Designated portu
	- Ked padne Designated, snazi sa aktivovat Backup
- Edge 
	- Po starom Port Fast
	- Access port, iba koncove stanice (nie dalsi switch)
	- Nepredpoklada sa zmena topo
	- Neflushuju sa CAM tabulky


### Nove typy liniek
#### Edge linky
Spaja koncove zariadenie so switchom  
Access port  

#### Non-Edge linky
Medzi switchami  
Trunk port  

Dalej sa deli na 2 kategorie  
- Point-to-point
	- Full-duplex
- Shared Port
	- Half-duplex
	- V pripade ak je spojenie switch - hub
	- Konvergencia do 15 sekund
	- V modernych sietach takmer nepouzivane  

### Proposal/Agreement mechanizmus  
Mechanizmus na zrychlenie konvergencie  
Napr. situacia ked sa novy switch priamo napoji na RB (novy switch ma aj inu cestu k RB)  
RB posle novemu switchu **Proposal** - ponukne mu cestu  
Novy switch to moze prijat (v tejto situacii prijme) - **Agreement**  
Pri tomto procese sa docasne zablokuju ostatne porty (ak prijmem Proposal tak ostane block, inak sa naspat aktivuje)  

#### Konfiguracia
Zapnutie Rapid PVST+ *(Rapid Per-Vlan Spanning Tree +)*
```
spanning-tree mode rapid-pvst
```

Ostatne prikazy su rovnake
```
spanning-tree vlan VLAN_ID priority PRIORITY
spanning-tree vlan VLAN_ID root primary
spanning-tree vlan VLAN_ID root secondary

int f0/1
	spanning-tree portfast
	spanning-tree link-type point-to-point
```

Show prikazy
```
do show spanning-tree
do show spanning-tree vlan VLAN_ID
do show spanning-tree detail
do show spanning-tree active
```

# ACL
Access control list
*"ACLs are among the most commonly used features of Cisco IOS software"*  
Najcastejsie nasadenie ako pravidla riadenia IP prevadzky. Pouzite aj vsade kde potrebna nejaka klasifikacia alebo identifikacia toku  

Sklada sa z podmienok - ACL Statements = Access Control Entries - ACEs  
Kazdy zaznam obsahuje testovaciu podmienku a akciu (`permit` alebo `deny`)  
Existuje este jedna akcia okrem `permit` a `deny` - `remark` - sluzi len ako poznamka/comment a nevykonava ziadnu akciu

## Co sa riesi v ACL  
Akoze co sa da specifikovat  
- Smer toku dat
	- Odkial - source/sender
	- Kam - destination/receiver
- Kto
	- Jednotlivec/Skupina/Vsetci
	- Rozlisuje sa pomocou parametrov
		- IP adresa 
		- Typ protokolu (IP, ICMT, TCP, UDP )
		- Sluzba (cislo portu)

## Nasadenie ACL
- Jeden ACL per **interface**  
- Jeden ACL per **protokol**  
- Jeden ACL per **smer**  

Cize napr. ak jedno rozhranie podporuje aj IPv4 aj IPv6, tak budeme mat  
- Jeden ACL pre IPv4 pre smer Inbound
- Jeden ACL pre IPv4 pre smer Outbound
- Jeden ACL pre IPv6 pre smer Inbound
- Jeden ACL pre IPv6 pre smer Outbound

Samozrejme ACL nemusi byt nasadeny vsade, napr. moze byt len IPv4 Inbound  

## Ako pracuje ACL
- Zoznam sa prehladava postupne jeden zaznam po druhom - preto specificke zaznamy treba na zaciatok, vseobecne na koniec  
- Ak sa najde zhoda v podmienke
	- Pozrie ci je `permit` alebo `deny`
		- Ak je `permit` tak sa pokracuje v normalnom smerovani
		- Ak je `deny` tak sa paket zahodi
	- **Po prvej zhode sa uz dalej nepokracuje v hladani v ACL!**  
- Ak sa v celom zozname nenajde zhoda v podmienke
	- Na konci je implicitna default akcia (nie je viditelna) `deny any`, ktora zahodi vsekty pakety

Pri Inbound sa kontroluje ACL pred smerovanim  
Pri Outbound sa kontroluje ACL po smerovani  
Cize v podstate: Pride paket - ACL na vstupnom rozhrani - Smerovanie - ACL na vystupnom rozhrani 

## Typy ACL
### Standard ACL
Cislo `1-99` alebo `1300-1999`  

- Povoluje/Zakazuje cely protokolovy stack
	- Napr. zakaze celu IPv4
- Kontroluje iba source IP add
- Nevie specifikovat sluzby (port)

### Extended ACL
Cislo `100-199` alebo `2000-2699`

- Specifikuje aj source aj destination IP add
- Specifikuje aj source aj destination port

## Cislovane a Pomenovane ACL
ACL sa da bud pomenovat alebo ocislovat  

### Cislovane 
- Standard ACL
	- `1-99`
	- `1300-1999`
- Extended ACL
	- `100-199`
	- `2000-2699`

Nevyhoda (len na starsich IOS) - nedaju sa mazat podmienky, pridavat sa daju len na koniec  

### Pomenovane
- Vacsinou uppercase nazov  
- Prehladnejsie - meno moze napovedat o co ide    
- Daju sa mazat aj pridavat hociktore zaznamy  


## Prikazy
### Standardne cislovane ACL
```
access-list CISLO [deny|permit|remark] TESTOVACIA_PODMIENKA [WILDCARD_MASK] [log] 

do show access-lists 1
```

Ak specifikujeme *log* na konci, tak vzdy ked sa paket zachyti na tomto pravidle, tak sa vypise nejaky vypis na konzolu (raz za 5 minut)

## Wildcard mask
*"Opacna subnet mask"*   
*"Ma sa dany bit ignorovat?"*  

Moze vyzerat napr. takto: `0.0.0.255`  

- 0 = kontroluj zhodu
- 1 = ignoruj zhodu

### Priklady
Mame siet **172.16.10.0/24** a chceme specifikovat to co je v tabulke  
Aka bude testovacia podmienka a wildcard maska  

> Nie som si sure ze to tak ma byt

| Co chceme specifikovat | Poznamka                                | Testovacia podmienka | Wildcard mask (posledny oktet)             |
| ---------------------- | --------------------------------------- | -------------------- | ------------------------------------------ |
| Prvu polovicu hostov   | `172.16.10.0` az  <br>`172.16.10.127`   | `172.16.10.0`        | bin `1000 0000`  <br>dec `128`             |
| Druhu polovicu hostov  | `172.16.10.128` az  <br>`172.16.10.255` | `172.16.10.255`      | bin `1000 0000`  <br>dec `128`             |
| Parne IP adresy        |                                         | `172.16.10.0`        | bin `1111 1110`  <br>dec `254`             |
| Neparne IP adresy      |                                         | `172.16.10.1`        | bin `1111 1110`  <br>dec `254`             |
| Presne jeden host      |                                         | Napr. `172.16.10.1`  | bin `0000 0000`  <br>dec `0`               |
| Cokolvek               | Pustit hocikoho                         | Napr. `172.16.10.1`  | bin `1111 1111`  <br>dec `255.255.255.255` |

| Co chceme specifikovat                                   | Testovacia podmienka | Wildcard mask                                       |
| -------------------------------------------------------- | -------------------- | --------------------------------------------------- |
| Vsetci hostia  <br>`172.16.0.0/24` az  <br>`172.16.15.0` | `172.16.0.0`         | bin `0.0.0000 1111.1111 1111`  <br>dec `0.0.15.255` |
| Vsetci hostia  <br>`172.16.32.0` az  <br>`172.16.47.0`   | `172.16.32.0`        | bin `0.0.0001 1111.1111 1111`                       |

### Klucove slova `host` a `any`
Ked specifikujeme `any` tak pustame vsetkych dnu - wildcard mask = `255.255.255.255`  
`host` je presne naopak - specifikujeme len jedneho hosta - wildcard mask = `0.0.0.0`  

```
access-list 2 permit 192.168.10.123 0.0.0.0
access-list 2 permit host 192.168.10.123

access-list 2 permit 192.168.20.123 255.255.255.255  # ip moze byt hocico
access-list 2 permit any 
```

## Priradenie ACL na rozhranie
```
int g0/0
	ip access-group {ACL_number | ACL_name} {in | out}
	ip access-group 2 out

line vty 0 4
	ip access-class {ACL_number | ACL_name} {in | out}
	ip access-class 3 in
```

## Editovanie ACL
Iba v novsich IOS  
```
do show access-list 1  # vsimneme si cislo zaznamu  

ip access-list standard 1
	no 10  # vymaze zaznam 10
	10 deny host 192.168.1.10  # novy zaznam na index 10
```

## Pozor na mazanie ACL
Ked sa zmaze ACL, ktory je aktualne aplikovany na nejakom rozhrani  
Vymaze sa len obsah ACL a na konci zostane `deny any`  
Tym padom sa znefunkcni kazdy interface na ktorom je aplikovane dane ACL  

Treba najprv zrusit ACL z daneho rohrania, az potom vymazat ACL  

```
int f0/0/0
	no ip access-group 2 

no access-list 2
```

## Konfiguracia pomenovaneho ACL  

```
access-list 2 permit host 192.168.1.10  # kofiguracia cislovaneho

# vytvorenie
ip access-list [standard | extended] NAZOV
	[permit | deny | remark] TESTOVACIA_PODMIENKA WILDCARD_MASK [log]

# aplikacia na interface
int f0/0/0
	ip access-group NAZOV [in | out]
```

---

```
do show access-list
do show access-list 1

do show ip access-list

do show run | include access-list
do show run | include access-list 1
```

Reset pocitadiel (pri specifikovani `log` na konci)
```
do show access-list
do clear access-list counters 1
```

## Konfiguracia extended ACL
```
access-list CISLO {deny | permit | remark} PROTOKOL {SOURCE SOURCE_WILDCARD} [OPERATOR PORT [PORT_NUMBER | WILDCARD]] {DESTINATION DESTINATION_WILDCARD} [OPERATOR PORT [PORT_NUMBER | WILDCARD]]

access-list 101 remark Povol HTTP
access-list 101 permit tcp 192.168.1.0 0.0.0.255 any eq 80 
access-list 101 remark Povol HTTPS
access-list 101 permit tcp 192.168.1.0 0.0.0.255 any eq 443 

access-list 101 remark Nejaky pokus
access-list 101 permit ip 192.168.1.0 0.0.0.255 lt 100 any ip 
```

