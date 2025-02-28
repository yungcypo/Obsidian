# AUS

Radsej pouzivat referenciu (`&`) ako pointer (`*`) ak sa da

- Jednoduchsia syntax (netreba dereferencovat)
- Zabera menej pamate
- Je to v podstate nieco ako alias?

```c++
int x = 20;
int* ptr = &x;  // pointer
int& ref = x;  // referencia
```

Pri ASCII stringu: pocet pismenok = pocet bitov  
Pri Unicode stringu: pocet pismenok sa nemusi = pocet bitov (UTF-16 pismenko = dvojbajt, UTF-32 pimenko = stvorbajt)

Najlepsie pouzivat UTF-8

Primitivne typy (int, short, long,...) vs. Odvodene typy (class, struct)

```c++
enum WeekDay: short {
    Monday,
    Tuesday,
    // ...
    Sunday
};
```

---

## Pamat

### Zasobnik - Call stack

Malicky  
Stack pointer - vrchol zachobnika - tam kde zasobnik konci  
Deli sa na ramce (frames)

- Novy ramec sa vytvori vzdy ked sa zavola nejaka funkcia?
- Znici sa ked sa skonci funkcia (`}`)

My default na windowse `1MB`, stack overflow - "minul" sa zasobnik

Odovzdavanie parametrov funkcii

- Hodnotou - pass by value
  - `void print(int val) {...}`
  - Implicitne alokuje novu pamat pre dany typ (int `4B`, class `vela`), pozor na velke typy (class, pole)
- Adresou - pass by address
  - `void print(int* val) {...}`
  - Implicitne alokuje novu pamat pre pointer (`8B`)
  - Trebe dereferencovat `{ (*val) += 5; }`
- Odkazom - pass by refrence
  - `void print(int& val) {...}`
  - Netreba dereferencovat `{ val += 5; }`
  - Implicitne alokuje novy pamat pre pointer (`8B`)
  - Da sa zabranit modifikaciam `void print (const int& val) {...}`
  - Kedze referencia je synonimum, tak

Prudko nepouzivat `mutable` a `const cast`

### Halda - Heap

Velka kapacita, (skoro) vsetka ostatna pamat

```c++
Osoba o = new Osoba();
delete o;
```

Dangling pointer

- Visiaci ukazovatel
- 2 pointre ukazuju na ten isty objekt, jeden spravi delete objektu, druhy ukazuje na neexistujuci objekt = je dangling pointer
- Riesi sa pomocou `nullptr`

Memory leak

- Aby sa dalo pristupit k pamati v halde, musi v zasobniku existovat premenna, pomocou ktorej sa da dohladat
- Ked prideme o alokovanu adresu v pamati (nahradime ju novou), nemozeme k povodnej pamati pristupovat a iba zabera miesto = memory leak

Smart pointers - unique pointers,

### Spravca pamate

- Zodpovedny za pridelovanie a vratenie pamate
- Udrziava informaciu o
- First-fit (rychlejsie) vs. Best-fit (menej fragmentacie) vs. Worst-fit (mam zoznam volneho miesta, pouzijem prve = najvacsie -> najrychlejsie)
- Objektove typy
  - Alokuje pamat + vola konstruktor
  - Pri destrukcii najprv zavola destruktor a potom uvolni pamat
