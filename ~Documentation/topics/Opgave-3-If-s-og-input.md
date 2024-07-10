# Opgave 3 (If&apos;s og input)

## Bonus Info: C# `if` sætninger

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

## Brug Components

Snart har vi brug for at flytte vores spiller. Derfor skal vi bruge Rigidbody komponenten.
For at gøre det kan vi gemme en reference til vores Rigidbody komponent ved at skrive:
```C#
Rigidbody rb;

void Start()
{
    rb = GetComponent<Rigidbody>();
}
```

Syntaksen `GetComponent<Rigidbody>()` er måske jeres allerførste gang i ser en funktion. 
Selve `GetComponent` er en navnet på den funktion. Denne specifikke funktion findes på alle MonoBehaviours i Unity.
Det næste er `<RigidBody>` og det er fordi `GetComponent` tager en type som <tooltip term="argument">argument</tooltip> og returnere en reference til den første komponent af den type på objektet.

Altså `GetComponent<RigidBody>()` returnere en reference til den første Rigidbody komponent på objektet.

## Input

Hvis vi vil lave en beslutning baseret på input, så kan vi bruge `Input` klassen.
Input klassen har en funktion [`GetAxisRaw`](https://docs.unity3d.com/ScriptReference/Input.GetAxisRaw.html) som tager en string som argument. 
Denne string repræsenterer navnet på en akse. Unity har nogle indbyggede akser som f.eks. `"Horizontal"` og `"Vertical"`.
Når man kalder den funktion retunere den en `float` værdi fra -1 til 1 baseret på input fra computeren.
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

Vi kan så tage at blande de to variable med vores `speed` variabel for at flytte vores spiller.
```C#
void Update()
{
    Vector3 movement = rb.velocity;
    movement.x = Input.GetAxisRaw("Horizontal") * speed;
    movement.z = Input.GetAxisRaw("Vertical") * speed;
    rb.velocity = movement;
}
```
Her gemmer vi vores nuværende hastighed i `movement` og så ændrer vi `x` og `z` komponenterne baseret på input fra computeren.
Derefter sætter vi vores hastighed tilbage til `movement`.

## Forberedelse til Opgave 3

### Input Manager

Her til sidst ville vi give lidt ekstra info til at løse den sidste opgave. Det er nemlig sådan at man kan selv lave sine egne input og akser i "Input Manager".
Der har vi tænkt os at lave en ny input akse vi kan bruge til at dreje spilleren med.

![inputmanager.png](inputmanager.png)

Ændre `30` til `31`, så vi har et mere input. Derefter:
1. Kald den `TurnAround`. 
2. Sæt `Positive Button` til `right`.
3. Sæt `Negative Button` til `left`.
4. Sæt `Type` til `Key or Mouse Button`.

### Split Spiller fra Model

Men for at dreje spilleren er det lettest at fjerne modellen fra spilleren
og, tilføje en 'capsule' som child. Dernæst, for at let indikere hvad er frem
kan vi også tilføje en cube. Det er sådan ud:

![ParentLogicVisualChild.png](ParentLogicVisualChild.png)

### Transform Rotate
Ligesom tidligere kan vi få vores `Transform` component I koden ved at skrive GetComponent
```C#
void Update()
{
    var transform = GetComponent<Transform>();
}
```

Men når vi gør det spotter vi at vi får en fejl, der nævner at den findes allerede. Det skyldes at Unity allerede har lavet den variable med den specifikke værdi for os.
En af funktionerne vi kan kalde på den er `Rotate` et eksempel på at bruge den kan ses under:

```C#
void Update()
{
    transform.Rotate(0, 5, 0);
}
```
Den kode rotere 5 grader om Y-aksen hvert frame. 

## Opgave 3

- Slå "Rotate unity manual" op på din favorit search engine
- Ud fra `“TurnAround”` axis få karakteren til at dreje rundt når du trykker på `left` og `right` knapperne.

Når opgaven er 

![MoveAndTurn.gif](MoveAndTurn.gif)