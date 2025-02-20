# Databazove Systemy

## Basics

DDL  
DML  
DAS/DCL  
DIS/TCL  

### Datove typy
- `VARCHAR(5)` - ako keby string s variabilnou dlzkou (max 5 znakov)
- `VARCHAR2(5)` - novsia verzia `VARCHAR`
-  `CHAR(5)` - ako keby string s pevne danou dlzkou 5

- `NUMBER(x, y)` - ciselna hodnota
	- `x` - maximalny pocet znakov ktore bude mat cislo
	- `y` - pocet znakov za desatinnou ciarkou
	- `NUMBER(10, 0) = NUMBER(10) = INTEGER(10)`
- `SMALLINT`, `FLOAT`, `DOUBLE`

- `DATE` - datum
- `TIME` - cas
- `DATETIME` - datum aj cas
- `TIMESTAMP(9)` - presnejsie ako sekundy (`9 = sekunda *`$10^{-9}$ )
- Oracle ma iba `DATE`, ktore je akokeby `DATETIME`

Formaty datumov
- `YYYY` / `YY` / `RRRR` / `RR`
- `MM`
- `DD`
- `HH` (12-hodinovy cas) / `HH24` (24-hodinovy cas)
- `MI`
- `SS`
- ...

### *neviem ako sa to vola*

|       |                     |                                                                                                                    |
| ----- | ------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `NN`  | Not Null            | Hodnota musi byt zadana, nemoze byt Null                                                                           |
| `PK`  | Primary Key         | Primarny, unikatny kluc v tabulke, je `NN`, je iba jeden (moze byt kompozitny - skladat sa z viacerych atributov?) |
| `FK`  | Foreign Key         | Odkazuje na primarny kluc z inej tabulky, moze byt aj Null                                                         |
| `PFK` | Primary Foreign Key | Primary + Foreign                                                                                                  |

## `SELECT`
```sql
SELECT * FROM studenti  -- vypise vsetko o vsetkych zaznamoch z tabulky studenti

SELECT meno, priezvisko, os_cislo FROM studenti  -- vypise iba meno, priezvisko a osobne cislo z tabulky studenti

SELECT meno, priezvisko
FROM studenti
WHERE meno='Peter'
-- vypise vsetkych Petrov z tabulky

SELECT meno AS m FROM studenti  -- alias, namiesto "meno" sa odteraz pouziva "m"

SELECT meno, rocnik+1 AS novy_rocnik FROM studenti
```

Praca s `Null`
```sql
-- NEMOZEME SPRAVIT TOTO
SELECT * FROM students WHERE ulica!=null

-- Treba spravit toto
SELECT * FROM students WHERE ulica IS NOT null
```


Zliepanie viac tabuliek dokopy - `JOIN`
```sql
SELECT * 
FROM osobne_udaje
JOIN student
USING (rodne_cislo)
-- spoji tabulky "osobne_udaje" a "student" podla kluca "rodne_cislo"
-- toto sa da pouzit iba ak obidve tabulky obsahuju "rodne_cislo", teda PK a FK su rovnake

SELECT *
FROM osobne_udaje
JOIN student
ON (osobne_udaje.cislo = student.cislo)
```

Popis tabulky - `description`
```sql
DESCRIBE osobne_udaje
DESC osobne_udaje
```

`Like` - pouzitie akoze wildcards spolu so znakmi `%` a `_`
```sql
-- Znak % specifikuje lubovolny pocet znakov
SELECT *
FROM osobne_udaje
WHERE meno LIKE "%a%"  -- vsetci co maju v mene "a"

-- Znak _ specifikuje jeden znak
SELECT *
FROM osobne_udaje
WHERE meno LIKE "_a%"  -- vsetci co maju na druhom mieste "a"
```

`Dual` - specialna tabulka s jednym zaznamom (dummy)
```sql
-- Ak by sme spustili nasledovny prikaz, vratilo by nam to tolko odpovedi kolko je zaznamov v tabulke
SELECT 1+1 FROM studenti

-- Ak chceme vratit iba jednu odpoved, mozeme pouzit tabulku dual, v ktorej je iba jeden zaznam
SELECT 1+1 FROM dual

```

Datumy
```sql
SELECT to_date('05-01-2025', 'DD-MM-YYYY') FROM dual -- formatovanie datumu

SELECT to_char(sysdate, 'DD.MM.YY') FROM dual  -- dnesny datum

SELECT sysdate+1 FROM dual  -- dnesny datum + 1 den
SELECT add_months(sysdate, 2)  -- za 2 mesiace
```