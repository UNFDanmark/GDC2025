# Del 3 (If&apos;s og input)

## Forberedelse af scenen
Vi tilføjer en Plane til scenen, så de to cubes, ikke flyver ud af skærmen. 
Det gøres ved, at højreklikke i hierarkiet og derefter trykke på `3D Object -> Plane`. 

![CreatePlane.png](CreatePlane.png)

Det kan være at planet ikke ligger ved `(0,0,0)`. For at sørge for det, så kan man højreklikke på Transform-komponenten derefter trykke på `reset` 

![ResetTransform.png](ResetTransform.png)



## C# `if`-statements

Det er tid til at introducere `if`-statements. 
`if`-statements er en måde at lave en beslutning i koden. 
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

## Brug Components

Snart har vi brug for at flytte vores spiller. Derfor skal vi bruge Rigidbody komponenten.
For at gøre det kan vi gemme en reference til vores Rigidbody komponent i en variabel ved at skrive:
```C#
Rigidbody rb;

void Start()
{
    rb = GetComponent<Rigidbody>();
}
```

Syntaksen `GetComponent<Rigidbody>()` er måske jeres allerførste gang i ser en funktion. 
Selve `GetComponent` er navnet på funktionen. Denne specifikke funktion findes på alle MonoBehaviours i Unity.
Det næste er `<RigidBody>` og det er fordi `GetComponent` tager en type som <tooltip term="argument">argument</tooltip> og returnerer en reference til den første komponent af den type på objektet.

Altså `GetComponent<RigidBody>()` returnere en reference til den første Rigidbody komponent på objektet som scriptet er koblet til.

## Input

Hvis vi vil lave en beslutning baseret på input, så kan vi bruge `Input` klassen.
Input klassen har en funktion [`GetAxisRaw`](https://docs.unity3d.com/ScriptReference/Input.GetAxisRaw.html) som tager en string som argument. 
Denne string repræsenterer navnet på en akse. Unity har nogle indbyggede akser som f.eks. `"Horizontal"` og `"Vertical"`.
Når man kalder funktionen [`GetAxisRaw`](https://docs.unity3d.com/ScriptReference/Input.GetAxisRaw.html) returnerer den en `float` værdi fra -1 til 1 baseret på input fra computeren.
<tip>
Når I bruger Rider skulle den gerne fortælle jer hvilke akser der er tilgængelige.
</tip>

Som eksempel kan vi skrive:
    
```C#
void Update()
{
    float horizontalInput = Input.GetAxisRaw("Horizontal");
    float verticalInput = Input.GetAxisRaw("Vertical");
}
```
for at gemme to variable `horizontalInput` og `verticalInput` som indeholder input fra computeren.

Vi kan gange disse input værdier med vores `speed` variabel  for at flytte vores spiller.
```C#
void Update()
{
    Vector3 movement = rb.linearVelocity;
    movement.x = Input.GetAxisRaw("Horizontal") * speed;
    movement.z = Input.GetAxisRaw("Vertical") * speed;
    rb.linearVelocity = movement;
}
```
Her gemmer vi vores nuværende hastighed i `movement` og så sætter vi `x` og `z` komponenterne lig resultaterne fra før.
Derefter sætter vi vores hastighed til at være lig `movement` som indeholder vores ændringer.

## Forberedelse til Opgave 3

### Input Manager

Her til sidst vil vi give lidt ekstra info til at løse den sidste opgave. Det er nemlig sådan at man kan lave sine egne input og akser i "Input Manager".
Der har vi tænkt os at lave en ny input akse vi kan bruge til at dreje spilleren med.

![inputmanager.png](inputmanager.png)

Ret `30` til `31` i toppen af input manageren, så vi har et input mere. Scroll derefter ned i bunden og:
1. Kald den nye akse `TurnAround`. 
2. Sæt `Positive Button` til `right`.
3. Sæt `Negative Button` til `left`.
4. Sæt `Type` til `Key or Mouse Button`.

### Split Spiller fra Model

For at dreje spilleren er det lettest at opdele modellen og spillerobjektet.
Tilføj en 'capsule' som child af spiller. Dernæst, for at indikere hvad der er frem
kan vi også tilføje en cube. Det ser sådan ud:

![ParentLogicVisualChild.png](ParentLogicVisualChild.png)

### Transform Rotate
Ligesom tidligere kan vi få vores `Transform` component I koden ved at skrive `GetComponent`.
```C#
void Update()
{
    var transform = GetComponent<Transform>();
}
```

Men når vi gør det spotter vi at vi får en fejl som nævner at den findes allerede. Det skyldes at Unity allerede har lavet den variabel med den specifikke værdi for os.
En af funktionerne vi kan kalde på vores `Transform` er `Rotate`, et eksempel på hvordan funktionen bruges kan ses herunder:

```C#
void Update()
{
    transform.Rotate(0, 5, 0);
}
```
Denne kode roterer 5 grader om Y-aksen hvert frame. 

## Opgave 3

- Slå "Rotate unity manual" op på din favorit search engine
- Ud fra `“TurnAround”` axis få karakteren til at dreje rundt når du trykker på `left` og `right` knapperne.

Når opgaven er færdig *Skriv noget her*

![MoveAndTurn.gif](MoveAndTurn.gif)
