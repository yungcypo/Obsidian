# PSA

Poznamky ku predmetu Python v Sietovych Aplikaciach

# Sockety

Socket je nastroj na komunikaciu medzi procesmi cez siet/v ramci jedneho PC

Pri vytvarani socketu sa specifikuje domena socketu a typ socketu

```python
import socket

sock = socket.socket((DOMENA, TYP))
```

## Domena socketu

- `AF_INET`
  - pracuje na sietovej vrstve (**L3**)
  - IPv4
- `AF_INET6`
  - pracuje na sietovej vrstve (**L3**)
  - IPv6
- `AF_PACKET`
  - pracuje na linkovej vrstve (**L2**)
  - Ethernet

## Typ socketu

- `SOCK_STREAM`
  - TCP
  - vytvori Ethernet, IP a TCP hlavicku
- `SOCK_DGRAM`
  - UDP
  - vytvori Ethernet, IP a UDP hlavicku
- `SOCK_RAW`
  - pracuje na nizsej urovni
  - hlavicky musim vytvorit sam
    - pri pouziti s `AF_PACKET` vytvaram Ethernet hlavicku
    - pri pouziti s `AF_INET` alebo `AF_INET6` vytvarame IP hlavicku

---

Cize finalne vytvorenie socketu moze vyzerat nejak takto...

```python
sock = socket.socket((AF_INET, SOCK_STREAM))
```

## Priklad

### Server

```python
import socket

IP = "0.0.0.0"  # ip adresa, na ktorej bude pocuvat - v tomto pripade vsetky adresy
PORT = 9999  # port na ktorom bude pocuvat

sock = socket.socket((AF_INET, SOCK_STREAM))  # vytvorenie socketu
sock.bind((IP, PORT))  # 'aktivacia' socketu?
sock.listen(10)  # 10 = pocet cakajucich vo fronte

while True:
    (client_sock, (client_addr, client_port)) = sock.accept()  # prijimanie sprav
    ...
    client_sock.close()

sock.close()
```

### Klient

```python
import socket

SERVER_IP = 127.0.0.1
SERVER_PORT = 9999

sock = socket.socket((AF_INET, SOCK_STREAM))  # vytvorenie socketu
sock.connect((SERVER_IP, SERVER_PORT))

sock.send("Toto je moja uzasna sprava ktoru poslem na server".encode())
sock.recv(1000)  # prijimanie zo servera; 1000 = buffer na prijmanie = 1000 B
```

# Poradie bajtov

Poradie bajtov pri prenose udajov cez siet zavisi od architektury procesora

## Big-endian

"Najvyznamnejsi" bajt (prvy) sa ulozi na miesto s najnizsou adresou (normalne)  
Napr. sprava `01234567` by bola rozdelena na `01` - `23` - `45` - `67`  
Pouzivaju architektury ako PowerPC, SPARK, ARM a sietove zariadenia

## Little-endian

"Najmenej vyznamny" bajt (posledny) sa ulozi na miesto s najnizsou adresou  
Napr. sprava `01234567` by bola rozdelena na `67` - `45` - `23` - `01`  
Pouzivaju architektury x86 a ARM

# REST API

## Stavove Kody

**100 - Informacne odpovede**

| Kod       | Vyznam              |
| --------- | ------------------- |
| 100 - 199 | Informacne odpovede |

**200 - Uspesne**

| Kod | Vyznam     |
| --- | ---------- |
| 200 | OK         |
| 201 | Created    |
| 202 | Accepted   |
| 204 | No content |

**300 - Presmerovane**

| Kod | Vyznam            |
| --- | ----------------- |
| 301 | Moved Premanently |
| 302 | Found             |

**400 - Chyba klienta**

| Kod | Vyznam             |
| --- | ------------------ |
| 400 | Bad Request        |
| 401 | Unauthorized       |
| 403 | Forbidden          |
| 404 | Not Found          |
| 405 | Method Not Allowed |
| 406 | Not Acceptable     |

**500 - Chyba servera**

| Kod | Vyznam                |
| --- | --------------------- |
| 500 | Internal Server Error |
| 501 | Not Implemented       |

## CRUD operations

- GET
  - Ziskavanie informacii
  - Pouzivana napr. pri navsteve stranky
  - Priklady
    - `GET /api/users` - vsetci pouzivatelia
    - `GET /api/users/:id` - pouzivatel so specifickym `id`
    - `GET /api/books?lang=sk` - vsetky slovenske knihy
  - Najcastejsie su odpovede `200`, `404`, `400`
  - **DATA SU NESIFROVANE!!!** - neposielat citlive udaje
- POST
  - Odosielanie dat na server (vytvaranie zaznamov)
  - Data sa posielaju v tele HTTP(S) poziadavky
  - Priklady
    - `POST /api/users` - vytvori pouzivatela
    - `POST /api/users/:id/accounts` - vytvori ucet pouzivatelovi
- DELETE, PUT, PATCH
  - Sluzi na vykonanie operacie nad datami
  - `DELETE /api/users/:id` - vymaze pouzivatela s danym id, odpoved by mala byt dany zaznam
  - PUT sa pouziva ako POST, aktualizuje cely zaznam
  - PATCH sa pouziva podobne ako POST, aktualizuje cast zaznamu

---

Kazde API by malo byt zdokumentovane  
[Swagger Editor](https://editor.swagger.io/)
