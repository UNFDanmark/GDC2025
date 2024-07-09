# Opgave 3 (If&apos;s og input)

## C# `if` sætninger

Det er tid til at introducere `if` sætninger. 
`if` sætninger er en måde at lave en beslutning i koden. 
Hvis en betingelse er sand, så udføres en blok kode. 
Hvis betingelsen er falsk, så udføres en anden blok kode.

Tag som eksempel denne kode:

```C#
void Update()
{
    if (speed > 18)
    {
        print("Du er speed");
    }
    else
    {
        print("Du er aight");
    }
}
```

Her tjekker vi om `speed` er større end 18. Hvis det er, så skriver vi "Du er speed" i konsollen.
Ellers skriver vi "Du er aight".

## Input

Hvis vi vil lave en beslutning baseret på input, så kan vi bruge `Input` klassen.
`Input` klassen har en metode `GetKey` som tager en `KeyCode` som argument.
`KeyCode` er en type der repræsenterer en tast på tastaturet.
Tag som eksempel koden `Input.GetKey(KeyCode.W)` den ville returnere `true` hvert frame hvor W-tasten er trykket ned. Man kunne bl.a. blande det med viden om `if`-sætninger til at flytte en spiller fremad.
```C#
if (Input.GetKey(KeyCode.W))
{
    forwardDirection = 1;
}
```
Det er også muligt at bruge `Input.GetKeyDown` som kun returnerer `true` den første frame hvor tasten er trykket ned. 
```C#
if (Input.GetKey(KeyCode.W))
{
    forwardDirection = 1;
}
```


## Opgave 3
- Lav en if-then-else der skriver “pew” i konsollen baseret på input
- Slå “GameObject.Destroy()” op i Unitys dokumentation
- Prøv at bruge “GameObject.Destroy()” til at fjerne et objekt
