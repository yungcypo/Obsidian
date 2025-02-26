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

Na buildovanie a spustenie programu treba nainstalovat *.NET SDK*  

```shell
yay -S dotnet-sdk
```

*SDK* uz obsahuje *Runtime*, ktory je zodpovedny za spustanie predkompilovanych `.dll` suborov  
*Runtime* sa da nainstalovat aj samostatne, ale nie je to potrebne kedze je sucastou *SDK*  

```shell
yay -S dotnet-runtime
```

Pri nejakych webovych srandickach sa pouziva *ASP.NET Runtime*

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