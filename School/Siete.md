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
