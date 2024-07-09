# Opgave 2 (Variabler)

## Variabler og typer
Når man skriver kode får man ofte brug for at gemme nogle værdier. Disse gemmepladser kalder vi variabler.
I C# ville en variabel kunne se sådan ud:
```C#
int alder = 10;
```
I koden ovenfor har vi lavet en variabel `alder` som er af typen `int` (integer) og sat den til at være 10.
Man skal altså læse det som "alder er lig med 10". Eller:
```
type variabelNavn = værdi;
```

Men der findes mange flere typer end `int`. Her er nogle af de mest brugte:
- `int` er heltal (f.eks. kan man skrive `int alder = 10;`)
- `float` er decimaltal (f.eks. kan man skrive `float vægt = 10.5f;`)
- `string` er tekst (f.eks. kan man skrive `string navn = "Mikkel";`)
- `bool` er sandt/falsk (f.eks. kan man skrive `bool erVoksen = true;`)

I Unity er der også nogle specielle typer som er specifikke for Unity:
- `Vector3` er en 3D vektor
- `GameObject` er et Unity objekt
- `Transform` er en position, rotation og skala

Disse typer kommer vi snart til at bruge. Men vi kommer ikke selv til at fokusere på at lave vores egne typer (endnu). Men vigtigt at huske at det også er en mulighed.
En anden vigtig detalje er at man ikke behøver at sætte en værdi. Man kalder dette for en variabel deklaration.
```C#
int alder;
```
Men det jo ikke så sjovt at have en variabel uden at vide hvad den indeholder. Så det er en god ide at sætte en værdi med det samme. 

## Men hvor skal variablerne være?

Variabler kan være i mange forskellig steder. Hvis vi husker første lektion, så har vi en `Start` og en `Update` metode.
- Hvis vi placerer en variabel i `Start` metoden, så vil den kun være tilgængelig i `Start` metoden. 
- Hvis vi placerer den i `Update` metoden, så vil den kun være tilgængelig i `Update` metoden.
- Hvis vi placerer den udenfor begge metoder, så vil den være tilgængelig i begge metoder.

```C#
public class PlayerScript : MonoBehaviour
{
    int alder = 10;
    
    // Start is called before the first frame update
    void Start()
    {
        int jegVirkerKunIStart = 20;
        print(alder + jegVirkerKunIStart); // Skriver 30 i konsollen
    }

    // Update is called once per frame
    void Update()
    {
        int jegVirkerKunIUpdate = 42;
        print(alder + jegVirkerKunIUpdate); // Skriver 52 i konsollen
    }
}
```

Hvis i bemærker, så kan i se at reglen er at variablerne er tilgængelige inde mellem hver `{}`. Så fordi `JegVirkerKunIStart` er inde i `Start` metoden's `{}`, så kan den ikke tilgås i `Update` metoden.

## Tilgængelighed i editoren
I C# kan man definere en variable der lever udenfor en metode som `public`. Det betyder at andre steder kan tilgå den. Så kigger vi på koden:
```C#
public class PlayerScript : MonoBehaviour
{
    public int alder = 10;
}
```
Så har vi altså lavet variablen `alder` til at være `public` så andre kan få værdien. I Unity betyder det også at den kan fås fat i fra Editoren. Så vi selv kan justere den.

![VariableIInspector.gif](VariableIInspector.gif)

## Kommentarer
I koden ovenfor har vi også brugt noget der hedder kommentarer. Kommentarer er tekst i koden som ikke bliver kørt. De er der for at forklare hvad koden gør.
I C# skriver `//` for at lave en kommentar. Hvor at alt efter `//` vil blive ignoreret af computeren.
```C#
// Dette er en kommentar
```

## Opgave 2
1. Lav en variabel til at styre spillerens hastighed og gør så man kan tilgå den i editoren
2. Lav en variabel til at håndtere cooldown af skud og gør så man kan tilgå den i editoren
