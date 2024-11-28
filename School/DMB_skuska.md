# DMB skuska
Otazky ktore udajne maju byt na skuske  

---

# Uzavrete otazky

Aka je sucasna odmena za vytazenie bloku v Bitcoin sieti? (november 2024)
- ~~10 BTC~~
- ~~12.5 BTC~~
- ~~25 BTC~~
- ~~6.25 BTC~~
- 3.125 BTC

Ako nazyvame teoriu, ze siet moze podporovat iba dve z nasledujucich moznosti: bezpecnost, decentralizacia a skalovatelnost?  
- ~~Scalability problem~~
- Trilemma problem
- ~~Dilemma problem~~
- ~~Anonymity problem~~

Ako sa ziskava bitcoinova adresa 
- ~~Aplikovanim RIPEMD na privatny kluc~~
- ~~Aplikovanim hashovacej funkcie SHA256 a elyptickych kriviek na privatny kluc~~
- ~~Aplikovanim hashovacej funkcie SHA256 na nahodne cislo~~
- Aplikovanim hashovacej funkcie SHA256 a RIPEMD160 na verejny kluc

Ako sa ziskavaju nove bitcoiny 
- ~~Odmenou za drzanie (hold) bitcoinov~~
- Pri procese tzv. tazenia bitcoinov procesom matematickeho vypoctu
- ~~Pri obchodovanim na burzach~~
- ~~V Europskej centralnej banke~~

Aku ma ulohu tzv. "nonce" cislo v ramci bitcoinoveho bloku? 
- ~~Je to referencia na predchadzajuci blok~~
- ~~Indikuje aku verziu softveru pouziva taziar~~
- Dovoluje sieti jednoducho a rychlo overit vytazeny blok
- ~~Pridluje poradie jednotlivym transakciam~~

Aky typ konsenzualneho mechanizmu vyuziva Bitcoin?
- ~~Delegated proof of stake~~
- Proof-of-Work
- ~~Proof-of-Stake~~
- ~~Proof-of-Importance~~

Co je Bitcoin?
- Decentralizovana P2P (peer-to-peer) siet, ktora nema ziaden centralny bod
- ~~Digitalna alternativa eura~~ 
- ~~Software na zapisovanie vsetkych transakcii v bankovom systeme~~
- ~~Centralizovana databaza na zaznamenavanie transakcii~~

Co je Ethereum?
- ~~Jednoducha fintech databaza~~
- ~~Nevieme~~
- ~~Cloudova platforma~~
- Open-source platforma pre decentralicovane aplikacie - dapps

Co je to blockchain?
- ~~Decentralizovana P2P (peer-to-peer) siet, ktora nema ziaden centralny bod~~
- ~~Neviem~~
- Databaza na uschovu zakladnych udajov o transakciach, udalostiach alebo spravach vznikajucich v ramci ekosystemu vzajomne komunikujucich ucastnikov (stran)
- ~~Excelovska tabulka na evidenciu vsetkych financnych transakcii~~

Co je to smart contract
- ~~Set instrukcii na cetralnom serveri~~
- ~~Bankovnicky termin~~
- ~~Pravnicka zmluva, definuje vztah medzi zucastnenymi stranami~~
- Set instrukcii ktory dokaze vykonavat vypocty, ukladat informacie, urcovat podmienky ktore po vyplneni automaticky spustia akciu

Ake su 2 hlavne komponenty dapp - decentralizovanej aplikacie 
- ~~Aplikacia a cloud~~
- ~~Penazenka a bitcoin~~
- User interface a smart contract
- ~~User interface a back-end~~

Kolko Bitcoinov bude celkovo v obehu
- ~~22 milionov~~
- 21 milionov
- ~~20 milionov~~
- ~~23 milionov~~

Kto je tvorcom a zakladatelom Etherea?
- ~~Friedrich Niche~~
- ~~Satoshi Nakamoto~~
- Vitalik Buterin
- ~~Nick Szabo~~

Kto je tvorcom a zakladatelom Bitcoinu?
- Satoshi Nakamoto
- ~~Dorian Nakamoto~~
- ~~David Chaum~~
- ~~Nick Szabo~~

Privatny kluc je nahodne vygenerovany na zaklade
- ~~Pristpovych udajov ako prezyvka alebo meno~~
- ~~Hesla a emailu~~
- ~~Datum narodenia~~
- Nahodne vygenerovaneho kluca

> Bolo vravene je mozno bude doplnena otazka na styl "Kolko priblizne trva vytazenie jedneho bloku", odpoved je 10 minut  

---

# Otvorene otazky
> Otvorene otazky by nemali byt actually na teste ale who knows

## Ake 2 typy uctov pozname pri Ethereum blockchane? Pre bonusove body popiste rozdiely  
- Klasicky ucet, tzv. Externally Owned Account 
- Smart contract 

|Klasicky ucet|Smart contract|
|-|-|
|Ovladany fyzickou osobou|Naprogramovany kod|
|Ma privatny a verejny kluc|Nema privatny kluc|
|Transakcia sa podpisuje sukromnym klucom|Aktivuje sa vykonanim transakcie z klasickeho uctu|
|Poplatky (gas) sa uctuju za kazdu transakciu|Poplatky sa uctuju za vykonavanie kodu|
|Moze posielat a prijimat Ether|Moze prijimat a ukladat Ether, posielat ho moze iba na zaklade logiky v kode|

## Ake pozname 3 najhlavnejsie problemy skalovatelnosti verejnych (public) blockchanov
> Tzv. Blockchain Trilemma - snaha optimalizovat jednu z nasledovnych vlastnosti casto vedie k obmedzeniu ostatnych dvoch  

- Skalovatelnost
    - Verejne blockchainy maju obmedzenu kapacitu na spracovanie transakcii (cca 7 (btc) alebo 15-30 (eth) transakcii za sekundu, VISA cca 24000)
- Decentralizacia
    - Pre vyssiu skalovatelnost sa obetuje cast decentralizacie
    - Menej decentralizovane = rychlejsie ale nachylnejsie na utoky
- Bezpecnost
    - Zvysenie skalovatelnosti alebo zjednodusenie decentralizacie moze ohrozit bezpecnost siete
    - Bezpecne blockchainy vyzaduju vysoku vypoctovu silu alebo vysoky pocet uzlov (ochrana proti 51% utoku)

## Aky je rozdiel medzi hardware a software penazenkou na uschovu bitcoinu? 
- Hardware 
    - Fyzicke zariadenie
    - Vyssia bezpecnost, drahsie riesenie
- Software 
    - Program v PC, na mobile alebo web browser plugin
    - Jednoduche pouzitie, viac kryptomien, ale nachylne na hacky/malware/...

## Aky je rozdiel mezdi verejnymi a privatnymi blockchainami
- Verejne
    - Napr. Bitcoin, Ethereum
    - Ma pristup hocikto (samozrejme ten kto ma pripojenie na internet, PC, ...)
    - Decentralizacia
    - Transparentnost
    - Nizsia skalovatelnost
- Privatne
    - Ma pristup iba vybrana skupina autorizovanych ludi
    - Prevazne centralizovane
    - Nizka transparentnost
    - Zvycajne vyssia skalovatelnost
    - Firemne aplikacie, interne systemy

## Popiste aspon 3 priklady v akych oblastiach je mozne pouzit blockchain 
- Dodavatelske retazce
    - Zabezpecenie transparentnosti a sledovanosti tovarov a materialov v celom retazci, od vyroby az po konecneho spotrebitela
    - Zaznamy o povode tovaru 
    - Odhalenie podvodov a nelegalnych praktik 
- Hlasovanie 
    - Bezpecne a transparentne elektronicke hlasovanie 
    - Odolnost voci manipulacii 
    - Umoznuje vzdialene hlasovanie 
- Umenie a media 
    - NFT
    - Zabezpecenie autorskych prav 
    - Kazde dielo ma jedinecny zaznam ktory preukazuje jeho povod a vlastnictvo
    - Umelci dostavaju priame odmeny od kupujucich bez sprostredkovatela (galerie, platformy)
- Nehnutelnosti
    - Zlepsenie evidencie vlastnickych prav 
    - Bezpecne transakcie pri predaji nehnutelnosti
    - Eliminacia podvodov a duplikacie vlastnickych dokumentov
    - Zrychlenie procesu prevodu vlastnictva

## Napiste aspon 3 vlastnosti bitcoinu, ktory sa odlisuje od fiat mien (euro, uds, ...)
- Virtualna/elektronicka mena
- Pseudoanonymita
- Decentralizacia
- Obmedzene mnozstvo (21 milionov) 
- Transparentnost a nemennost 
- Overitelnost

## Popiste aspon jeden z typov utokov na blockchainove siete
- 51% utok
    - Ak niekto ovladne viac ako polovicu (51%) vypoctoveho vykonu na sieti 
    - Nachylne najma pre mensie siete
    - Utocnik moze 
        - Zvratit transakcie
        - Zablokovat potvrdenie transakcii
        - Vytvorit falosne bloky
        - Manipulovat s historiou transakcii
- Double spending
    - Utocnik sa pokusa utratit tu istu kryptomenu 2 krat (pre tym ako bola potvrdena)
    - Pokus o zmenu historie vyvolanim konfliktu medzi transakciami
    - V pripade uspechu moze utocnik ziskat vacsie mnozstvo kryptomien ako by mal 
- Pretazenie siete
    - V podstate DOS/DDOS utok 
    - Utocnik zahlti siet velkym mnozstvom transakcii za ucelom spomalenia az celkoveho zlyhania siete
- Smart contract exploit
    - Hlada a vyuziva zranitelnosti v kode smart contractov 
    - Utocnik sa snazi neopravnene vybery kryptomien alebo manipulaciu s podmienkami contractu

## Vypiste aspon dva sposoby ako si mozete zadovazit bitcoin
- Kupou - ci uz z nejakej verejnej burzy alebo od znameho
- Tazenim
- Prijatie platby v bitcoinoch 
- Bitcoin automaty

## Vypiste aspon 3 priklady, kde mozete utratit svoje bitcoiny (obchody/sluzby)
- www.alza.sk
- sluzby ako Spotify alebo Netflix 
- niektore online kurzy, napr. Udemy
- niektore luxusne znacky, napr. Porsche alebo Tesla

