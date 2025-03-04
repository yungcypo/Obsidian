# Databazove Systemy

## Basics

DML - Select, Update, Delete, Insert  
DDL (Data Definition Language) - Create, Alter, Drop - automaticky robi commit  
DCL  
TCL (Transaction Control Language, niekedy aj DAS) - Commit, Rollback

### Datove typy

- `VARCHAR(5)` - ako keby string s variabilnou dlzkou (max 5 znakov)
- `VARCHAR2(5)` - novsia verzia `VARCHAR`
- `CHAR(5)` - ako keby string s pevne danou dlzkou 5

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

| Skratka | Meaning                   | Popis                                                                                                                                 |
| ------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `NN`    | Not Null                  | Hodnota musi byt zadana, nemoze byt Null                                                                                              |
| `PK`    | Primary Key               | Primarny, unikatny kluc v tabulke, je `NN`, **je najviac jeden** (moze byt kompozitny - skladat sa z viacerych atributov?), minimalny |
| `FK`    | Foreign Key               | Odkazuje na primarny kluc z inej tabulky, moze byt aj Null                                                                            |
| `PFK`   | Primary Foreign Key       | Primary + Foreign                                                                                                                     |
| `KPK`   | Kandidat primarneho kluca | Nieco, co teoreticky moze byt tiez primarny kluc                                                                                      |

## SELECT

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

Nejake selectiky

```sql
select meno,priezvisko
    from os_udaje join student(using rod_cislo)
    where rocnik=2;

select meno,priezvisko
    from os_udaje
    where rod_cislo IN (select rod_cislo from student where rocnik=2);
```

```sql
select meno,priezvisko
    from os_udaje
    where rod_cislo not in (select rod_cislo from student);

select meno,priezvisko
    from os_udaje
    where rod_cislo in (select rod_cislo from student where rocnik is null);
    -- cez IN sa neda spravit, vnoreny select nikdy nic nevrati lebo rocnik je NN

select meno,priezvisko
    from os_udaje o
    where NOT EXISTS
    (select 'x' from student s where s.rod_cislo=o.rod_cislo);
    -- univerzalnejsie riesenie - mozeme dat viac podmienok
```

Toto bude dolezite pri INSERT, DELETE a UPDATE

## INSERT

Vztahuje sa iba na jednu tabulku

```sql
INSERT INTO os_udaje
    values('560123/1234', 'Michal', 'Kvet', 'Univerzitna', '01026', 'Zilina')

INSERT INTO os_udaje
    values('560123/1235', 'Michal', 'Kvet', null, null, null)

INSERT INTO os_udaje(meno, priezvisko, rod_cislo)
    values('Michal', 'Kvet', '560123/1236')
```

Ulozim vysledok selectu do tabulky

```sql
select *
    from priklad_db2.os_udaje  -- z inej db, tabulka pouzivatela "priklad_db2"

insert into os_udaje(rod_cislo, meno, priezvisko)
    select rod_cislo, meno, priezvisko
        from priklad_db2.os_udaje;
        where priklad_db2.rod_cislo not in
            (select rod_cislo from os_udaje)

insert into os_udaje(rod_cislo, meno, priezvisko)
    select rod_cislo, meno, priezvisko
        from priklad_db2.os_udaje p;
        where p.rod_cislo not in
            (select rod_cislo from os_udaje)
```

VALUES vlozi jeden riadkok, presne definujem co idem vlozit  
Pomocou SELECT mozem vlozit lubovolny pocet udajov

```sql
desc student
insert into student
    values(500123412, 100, 0, '311234/1234', 1, '5ZI011', 'S', null, sysdate)
    -- error - narusene referencen obmedzenie - v druhej tabulke neexistuje uvedene rodne cislo
```

## UPDATE

Vzdy modifikuje jednu tabulku

```sql
update student
    set rocnik=3
    where os_cislo = 123456;

update student
    set rocnik=3,st_skupina=5'5ZI031'
    where os_cislo = 123456
```

Vylucim vsetkych petrov zo studia

```sql
update student
    set ukoncenie=sysdate
    where rod_cislo in
        (select rod_cislo from os_udaje
            where meno='Peter')

-- nepouzivat JOIN

update student
    set ukoncenie=sysdate
    where EXISTS
        (select 'x' from os_udaje
            where meno='Peter' AND os_udaje.rod_cislo=student.rod_cislo)
```

```sql
update student
    set stav='x'
    where exists
        (select 'x' from zap_predmety join predmet using (cis_premdetu)
        where nazov='Zaklady databazovych Systemy')
```

## DELETE

Vzdy pracujem s jednou tabulkou  
Ziadny JOIN  
Ak su nejake FK na polozku ktoru chcem vymazat tak to neprejde - ak student existuje v zapisanych predmetoch, studenta nemozem vymazat

```sql
delete -- nepisu sa ziadne atributy - vymazavam cely riadok
    from zap_predmety
    where os_cislo=501313

delete from student
    where os_cislo=501313
```

Chcem vymazat predmet DBS

```sql
delete from predmety where nazov='DBS'
-- toto nemozem spravit lebo predmet je este v inych tabulkach

delete from zap_predmety
    where cislo_predmetu in
        (select cis_premdetu from predmet
            where nazov='DBS')
delete from st_program
    where cislo_predmetu in
        (select cis_premdetu from predmet
            where nazov='DBS')
delete from predmet_bod
    where cislo_predmetu in
        (select cis_premdetu from predmet
            where nazov='DBS')
delete from predmet where nazov='DBS'
```

Chcem vymazat studijny odbor

```sql
delete from st_program p
    where EXISTS
        (select 'x' from st_odbory o
        where popis_odboru='Manazment' -- iba takto sa vymaze vsetko!!!
        and p.st_odbor = o.st_odbor
        and p.st_zameranie = o.st_zameranie) -- treba toto doplnit!
delete from zap_predmety zp
    where EXISTS
        (select 'x' from st_odbory o join student using(st_odbor, st_zameranie)
        where popis_odboru='Manazment'
        and student.os_cislo = zp.os_cislo
delete from student s
    where EXISTS
        (select 'x' from st_odbory o
        where popis_odboru='Manazment' -- iba takto sa vymaze vsetko!!!
        and s.st_odbor = o.st_odbor
        and s.st_zameranie = o.st_zameranie) -- treba toto doplnit!

delete from st_odbory where popis_odboru='Manazment'
```

---

Chcem zmenit rodne cislo studentovi (`801234/1234` -> `8801234/1234`)

```sql
insert into os_udaje(rod_cislo, meno, priezvisko, ulica, psc, obec)
    select '880123/1234', meno, priezvisko, ulica, psc, obec
        from os_udaje
            where rod_cislo = '801234/1234'

update student
    set rod_cislo='881234/1234'
    where rod_cislo='801234/1234'

delete -- vymazem povodneho studenta
```

## TCL

Chcem aby presla operacia bud cela, alebo vobec  
Napr. bankove transakcie

- `COMMIT` - potvrdit zmeny
- `ROLLBACK` - zahodit vsetky zmeny

Ak raz spravim commit, uz mi ziadny rollback nepomoze  
Rollback sa vracia ku poslednemu commitu (resp. na zaciatok?)

Vlastnost **atomicita** - bud transakcia prebehne cela alebo vobec - **A**  
Vlastnost **konzistencia** - vsetky obmedzenia (PK, NN, ) su zachovane - **C**  
Vlastnost **izolovanost** - ked mame 2 sessions - ak spravim zmeny v jednej session, v druhej to budem vidiet iba ak dam commit - **I**  
Vlastnost **durabilita** - **D**

= **ACID**

## Datove Modelovanie

- Struktura dat - ake tabulky chcem vytvorit,
- Manipulacia dat (DML (insert, update, delete, select)) - mozno nebudem chciet DELETE, alebo UPDATE alebo co ja viem co z nejakeho dovodu
- Integritne obmedzenia - musim obmedzit datovy typ na nejaku hodnotu - PSC nemoze byt `ABCDE`, rodne cislo nemoze byt `000000_0000`

### ERA Model

ER = Entity Relation - konceptualny model

Entita - je objekt realneho sveta, schopny nezavislej existencie, jednoznacne odlisitelny od ostatnych objektov  
Vztah - vazba medzi 2+ entitami  
Popisny typ - dvojica mnoziny hodnot a mnoziny operacii (napr. rocnik = cislo, mozem ho zmenit)  
Atribut - funkcia priradujuca entitam alebo vztahom hodnotu  
Typ entity - mnozina vlastnoti entity (osoba, ma 6 atributov (rodne cislo, meno, priezvisko, ...) )  
Typ vztahu - mnozina vlastnoti vztahu  
Instancia entity - samotna realizacia entity - samotny zaznam ktory ma svoje hodnoty  
Instancia vztahu - podobne ako instancia entity  
Identifikacny kluc - KPK, jeho hodnota sluzi na indentifikaciu

Typy atributov

- Atomnicke - neda sa delit na mensie zlozky (Rodne cislo - sklada sa sice z casti ale jednotlive casti maju rovnocenny vyznam)
- Neatomnicke - skupinove (strukturovane), viachodnotove

Superkluc - unikatny, ale nemusi byt minimalny

Definovanie kompozitneho PK

```sql
create table Tab(
    a integer primary key,
    b integer primary key  -- toto nemozem spravit - definujem 2 PK
)

create table Tab2(
    a integer,
    b integer,
    primary_key(a, b)  -- takto sa to robi
)
```

Definovanie FK

```sql
alter table Tab2 add foreign key (id) references Tab (id)
```

### Typ, Kardinalita, Clenstvo

**Typ vztahu**

Identifikacny vztah - prislusny FK sa stane castou PK
Neidentifikacny vztah -prislusny FK sa **ne**stane castou PK

**Kardinalita** - integritne obmedzenie, ktore vyjadruje (jedna osoba moze byt n-krat studentom)

- 1:1 - napr. jeden ujo moze byt starosta jedneho mesta
- 1:n - napr. v jednom dome moze byt viac ludi, ale jeden clovek moze byt iba v jednom dome
- m:n - napr. student a predmet - jeden student moze mat viac predmetov, jeden predmet moze mat viac studentov - v tomto pripade musi vzniknut nova tabulka - zap_predmety

**Clenstvo** - povinne vs. nepovinne - ci FK moze nabudat null alebo nie

V grafe

- Plna ciara = identifikacny vztah
- Prerusovana ciara = neidentifikacny vztah
- Ak je kardinalita 1:n, tak tam kde je `n` su "metlicky"
- Nepovinne clenstvo = kruzok

### Slabe entitne typy

Aby som definoval \_ tak potrebujem \_ z inej tabulky

### Rekurzivny vztah

Vzdy neindetifikacny

### ISA hierarchia

#### Generalizacia

#### Specializacia
