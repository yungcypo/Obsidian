# ZBS

Poznamocky z predmetu Zaklady Bezdrotovych Sieti

## Historia

Prva teoria elektromagnetizmu - 1831 - Faraday  
Teoria pouzita v praxi - 1864 - Maxwell  
Prvy vyslany radiovy signal - 1870 - Mahlon Loomis  
Prvy dialkovy bezdrotovy hovor - 1915

## Zaklady

### Ziarenie

- Ionizujuce
  - Ionizacia = proces pri ktorom atom/castica straca/ziskava elektrony = meni sa na ion
  - Patri sem ultrafialove ziarenie, rontgenove ziarenie, gama ziarenie
  - Moze pochadzat z
    - Kozmicke - zo slnka - zvysuje sa s nadmorkou vyskou
    - Z hornin a pody - uran, torium, draslik, radon
    - Podzemna voda - je v nej rozpusteny radon
    - Umele - rontgen, urychlovace, ziarice
  - Moze sposobit popalenie, chorobu z oziarenia, geneticke poskodenie
  - Chranit sa voci nemu da vzdialenostou, casom, tienenim
- Neionizujuce
  - Patri sem viditelne svetlo, infracervene, mikrovlnne, radiove vlny, nizkofrekvencne polia vytvarane elektrickymi pristrojmi a vedeniami
  - Bezne nas obklopuje, nesposobuje zmenu v atomoch (nedostatocna energia) -> znacne nizsie riziko ohrozenia
  - Rizika
    - Viditelne svetlo - priamy pohlad moze poskodit sietnicu
    - Tepelny efekt (popaleniny) vysokofrekvencneho ziarenia (infracervene, mikrovlnne)
    - Pri beznom vystaveni je bezpecne

Elektromagneticke vlnenie (EM) je jav, pri ktorom sa elektromagneticka vlna prenasa od zdroja k spotrebicu  
Je dane frekvenciou `f [Hz]`

Magneticke pole - magneticka indukcia `B [T]` _(Tesla)_

Elektricke pole - intenzita `E [V/m]` _(voltmeter)_

### Pojmy suvisiace so sirenim riadovych vln

- Ohyb (Difrakcia)
- Lom (Refrakcia)
- Rozptyl (Scattering)
- Odraz (Reflection)
- Prienik (Transmission)

### Fresnelova zona

Pre kazdu vysielanu frekvenciu sa da definovat rozhranie, ktore tvori hranicu Fresnelovej zony v tvare '3D elipsy'  
Moze ich byt lubovolen vela  
Najdolezitejsia je 1. Fresnelova zona - najblizsie k sponici medzi vysielacom a prijimacom - siri sa v nej najvacsia cast (60%) EM vlnenia

Polomer Fresnelovej zony (v metroch) vypocitame ako $r = \sqrt{\dfrac{d \cdot \lambda}{4}}$, alebo $r = 8.657 \cdot \sqrt{\dfrac{d}{f}}$

> $d$ = vzdialenost vysielaca a prijimaca \[m]  
> $\lambda$ = vlnova dlzka \[m]  
> $f$ = frekvencia \[GHz]

Vzdialenost dotyku 1. Fresnelovej zony od povrchu zeme $d \cong \dfrac{4 \cdot h_{zs} \cdot h_{ms}}{n \cdot \lambda}$

> $zs$ = zakladova stanica
> $ms$ = mobilna stanica
> $h$ = vyska \[m]
> $d_1$ = priama vzdialenost \[m]
> $d_2$ = odrazena vzdialenost \[m]
> $\lambda$ = vlnova dlzka \[m]
> $n$ = cinitel
> Zmena koeficientu tlmenia nastava az pri tieneni viac ako 55% 1. Fresnelovej zony

### Definovanie zakladnych velicin

#### Vykon

Mnozstvo prace `W` vykonanej za jednotku casu `t`

Znacka `P`, jednotak `W` (Watt)

$P = \dfrac{W}{T}$

#### Elektricky vykon

Praca elektrickeho prudu vykonana za jednotu casu

$P = U \cdot I$

#### Vyzarovaci vykon - EIRP

Effective Isotropic Radiated Power  
Vykon, ktory by musela vyziarit hypoteticka izotropna antena, aby bolo dosiahnute rovnakej urovne signalu v smere maximalneho vyzarovania danej anteny _(???)_

Maximalny vyzarovaci vykon je dany normami

- 2.4GHz Wi-Fi - $100mW$ = $20 dBm$
- 5GHz Wi-Fi - $200mW$ = $23 dBm$

Vypocet: `Vykon vysielaca [dBm]` + `zisk anteny [dBi]` - `utlm kabla [dB]` - `utlm konektorov [dB]`

#### Decibel (`dB`)

**Relativny** udaj o dvoch roznych urovniach vykonu  
Udava pomer
Pouziva sa na vyjadrenie zisku/straty jedneho zariadenia ($P_2$) vo vztahu k druhemu ($P_1$)

$A/G = 10 \log \left( \dfrac{P_2}{P_1} \right)$

##### Decibel miliwatt (`dBm`)

Logaritmicka jednotka vykonu  
Vztahuje sa k vykonu `1mW`

##### Decibel Watt `dBW`

Logaritmicka jednotka vykonu  
Vztahuje sa k vykonu `1W`

##### Energeticky zisk izotropnej anteny (`dBi`)

## WLAN

1. PAN - Personal (Bluetooth)
2. LAN - Local
3. MAN - Metropolitan
4. WAN - Wide

IEEE 802.11 WLAN

Prvy 802.11 standard v roku 1997

Dve hlavne frekvencie

- 2.4 GHz
- 5 GHz

> 6 GHz - WiFi6E a WiFi7

Organizacie

- ITU - International Telecommunication Union (1865)
- IEEE - Institute of Electrical and Electronics Engineers
  - Rodina standardov `802`, napr. `802.11`, `802.3` atd. atd.

WLAN network topologies

- Infrastructure mode
  - Umoznuje pouzit controller - jednoduchsie manazovanie viacerych AP
- Ad-hoc mode
  - V podstate hotspot na mobile?

IEEE terminology

- AP - Access Point
- STA - Station - konocove zariadenie
- BSS - Basic Service Set - zariadenia pripojene na jedno AP
- ESS - Extended Service Set - zariadenia pripojene na 2+ APs
- IBSS - Independent Basic Service Set - Ad-hoc
- SSID - Service Set ID - textove ID
- BSSID - Basic Service Set ID - MAC adresa ako ID
- DCF - Distributed Coordination Function - riesenie kolizii pomocou nejakeho time slotu (dnes namiesto toho CSMA/CA)

### L1 podla IEEE 802.11

2.4 GHz channels

- Sirka kanalu 22 MHz
- Odstup jednotlivych kanalov 5 MHz -> prekryvaju sa
- Neprekryvajuce sa kanaly - `1`, `6`, `11`
- 13 kanalov v EU, 14 v Japonsku, 11 v US

5 GHz channels

- Odstup jednotlivych kanalov je tiez 5 MHz
- Pouzivaju sa kazde 4 kanaly (`36`, `40`, `44`) co poskytuje 20MHz kanaly ktore sa neprekryvaju

#### Modulacia

- Amplitudova
- Frekvencna
- Fazova

- BPSK - Binary Phase Shift Keying - otocime fazu o 180 stupnov
- QPSK - Quadrature Phase Shift Keying - otocime fazu o nasobok 45 stupnov
- QAM - Faza + amplituda? - QAM-16, QAM-64, QAM-256

#### Znizenie interferencie

- FHSS - Frequency Hopping Spread Spectrum - rychle prepinanie kanalov - starsie
- DSSS - Direct Squece Spread Spectrum
- CCK - Complementary Code Keying
- OFDM - Orthogonal Frequency Division Multiplexing
