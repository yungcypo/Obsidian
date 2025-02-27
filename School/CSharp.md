# C# a .NET

```cs
Console.WriteLine("Hello World");
```

`C#` je programovaci jazyk, `.NET` je framework ktory umoznuje beh `C#` kodu

Samotny programovaci jazyk je fess podobny Jave

`.NET` sa sklada z

- `.NET Runtime` - iba spusta uz predkompilovany kod (`.dll`)
- `.NET SDK` - Software Development Kit - obsahuje vsetko potrebne na vyvoj - kompilator aj nastroj na spustenie
- `.NET Libraries`

## Basics

### Installation

Na buildovanie a spustenie programu treba nainstalovat _.NET SDK_

```shell
yay -S dotnet-sdk
```

_SDK_ uz obsahuje _Runtime_, ktory je zodpovedny za spustanie predkompilovanych `.dll` suborov  
_Runtime_ sa da nainstalovat aj samostatne, ale nie je to potrebne kedze je sucastou _SDK_

```shell
yay -S dotnet-runtime
```

Pri nejakych webovych srandickach sa pouziva _ASP.NET Runtime_

```shell
yay -S aspnet-runtime
```

### Useful commands

General

```shell
dotnet --help
dotnet --version
dotnet --list-sdks
dotnet --list-runtimes
```

Creating new app

```shell
dotnet new console  # vytvori novu konzolovu aplikaciu
dotnet new console --output HelloWorldApp  # vytvori novu konzolovu aplikaciu do noveho priecinku
dotnet new console --use-program-main  # vytvori okrem hello world aj triedu
dotnet new list # pre zobrazenie vsetkych moznosti/typov projektu

dotnet new --help
```

Running and/or Building

```shell
dotnet run
dotnet build
```

## Data Types

- Hodnotove
  - int, float, double, struct, DateTime, Enum, tuples, record struct
  - nullable - int?, DateTime? - moze 'nadobudat null' (aj ked actually nie) lebo by default napr int nemoze byt null
  - Vytvaraju sa na zasobniku
- Referencne
  - class, record, delegate, interface
  - Maju referenciu v pamati

`int` je alias na `System.Int32`, `long` na `System.Int64` atd atd (slajd v prezentacii)

Ak mam vacsie cislo ako `ulong` ($2^{64}$) mozem pouzit big integer?

### Premenne

```cs
int a = 5;
var b = 6;  // typ sa automaticky odvodi

Student abc = new('meno', 'priezvisko');  // automaticky zavola konstruktor?

string s1 = "Hello world";
var s2 = new string("Hello world");
string s3 = new("Hello world");
```

Pouzitie vyhradeneho slova ako nazov premennej

```cs
int new = 123;  // nemozeme spravit lebo new je vyhradene slovo
int @new = 123;
```

#### Rozsah platnosti premennej (scope)

```cs

```

Kompilator premiestnuje deklaracie premennej niekam na zaciatok!!! Nemozeme 2x deklarovat premennu

#### `const`

```cs
const doulbe pi = 3.141592654
```

#### Literaly

Predpony

```cs
var deci = 42;
var hexa = 0x2A;
var bina = 0b11001010;

var prehladnejsie = 123_456_789;
var abc = 0x234_34A_FFF;
```

Pripony (radsej pouziat velke pismeno)

- F/f float
- D/d double
- L/l long?
- ...
- M/m ako money

Explicitne konverzie

```cs
int x = 123.456;
int y = (int)x;  // explicitna konverzia, ale stracame presnost

var signedbyte = (sbyte)43;
```

## Class

```cs
public class MyClass
{
    // telo triedy
}
```

### Pristupove modifikatory

- public
- private - fields by default (konvencia hovori `private string _name;`)
- protected
- internal - triedy by default
  - podobne ako private, ale v ramci projektu
  - da sa pouzit iba v ramci jedneho projektu
  - ak mame nejaku kniznicu, tak vsetko co je internal sa nemoze pouzit mimo kniznice
- ak je vnorena trieda moze mat aj dalsie
  - private protected
  - protected internal

Staticke a instancne cleny

- static - zdielane pre vsetky instancie (konvencia hovori `private static int s_count;`)
- instancne - kazda instancia ma svoje vlastne

```cs
var myInstance = new MyClass();
MyClass myInstance2 = new();
var list = new List<MyClass>();
var list2 = new List<MyClass>() = { new MyClass(), new MyClass() };
```

Konstanta - nikdy sa nemoze zmenit  
`readonly` - v podstate ako konstanta, moze sa pouzit pri stringu - moze sa menit iba pri inicializacii, deklaracii a v konstruktore

### Co vsetko moze trieda obsahovat

- Datove cleny (fields) - na INF1 oznacovane ako atribut, ale v C# je atribut uplne nieco ine
- Finalizery (finalizers) - na INF3 oznacovane ako destruktor (takmer vobec sa nepouziva lebo garbage collector)
- Dekonstruktor - z jedneho objektu vytvorime viac objektov - rozbalime objekt do tuplu
- Indexery - v C++ je to `operator[]`
- Udalosti (events) - su na nich zalozene GUIs
- Operatory - podobne ako v C++
- Vnorene typy (nested types) - trieda v triede, enum v enum, ...
- Vlastnosti (properties)
- ... take bezne veci

### Properties

```cs
public class Person
// stara syntax
{
    private int _age;

    public int Age
    {
        get {return _age;}
        set {_age = value;}  // value je akoze implicitny parameter
    }
}

// nova syntax
public class Person2
{
    private int _age;

    public int Age
    {
        get => _age;
        set => _age = value;
    }
}
```

