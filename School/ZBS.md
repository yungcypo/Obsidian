# ZBS

Poznamocky z predmetu Zaklady Bezdrotovych Sieti

## Historia

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
