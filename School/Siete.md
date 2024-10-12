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

