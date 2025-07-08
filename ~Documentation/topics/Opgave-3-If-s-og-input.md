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
Hvis vi gerne vil have vores spiller til at bevæge sig, så skal vi først læse inputtet, i den ønsket retning. For at opnå det, så skal man bruge en `InputAction`. Som er en samling af forskellige input muligheder, som kan bruges til at udføre det samme. Vi har så mulighed for at læse statussen af handlingen.

```c#
using UnityEngine.InputSystem;

//... inde i klassen
public InputAction moveAction;
```

Før vi anvender InputAction, så skal den klargøres i Unity. Det gøres ved at skabe en ny `Up/Down/Left/Right Composite` og derefter navngive den `WASD`. Vi tilføjer de individuelle retninger ved at dobbeltklikke på dem, klik på dropdown, herefter `Listen` og til sidst angive den tiltænkte knap ved at trykke på den.

![InputActionSetup.gif](InputActionSetup.gif)

For at anvende en InputAction, så er det vigtigt, at den er aktiveret inden. Dette burde gøres i starten af spillet:
```C#
void Start() 
{
    //.. andre ting
    // Aktiver Inputtet
    moveAction.Enable();
}
```

For at anvende inputtet så skal det læses fra `moveAction`. Det gør vi med `moveAction.ReadValue<Vector2>()`. Da der mange forskellige brugsscenarier for et `InputAction`. Så skal vi specificerer, at vi forventer en værdi af typen `Vector2`.

Hvis vi får fat på resultatet, så er det strukturer på følgende måde. Vi får en vektor med 2 værdier. Den første repræsenterer x-aksen, hvis vi har trykket `a` så er værdien -1, `d` så er værdien 1 ellers er værdien 0. Den anden værdi repræsenterer y-aksen, og er det samme for `w` og `s`.

Flytningen af spilleren kan opnås på følgende måde:
```C#
void Update()
{
    // Læs inputtet
    Vector2 moveInput = moveAction.ReadValue<Vector2>();
    
    // Reference til spillerens nuværende hastighed
    Vector3 newVelocity = rb.linearVelocity;
    // Vi ændrer referencens hastighed i x-aksen
    newVelocity.x = moveInput.x * speed;
    // Vi ændrer referencens hastighed i z-aksen
    newVelocity.z = moveInput.y * speed;
    // Vi opdaterer hastigheden
    rb.linearVelocity = movement;
}
```
Her gemmer vi vores nuværende hastighed i `newVelocity` og så sætter vi `x` og `z` komponenterne lig med retningen vi gerne vil bevæge os, multipliceret med vores ønsket hastighed. Til sidst så opdaterer vi hastigheden på `rb` så den faktisk bevæger sig.

## Forberedelse til Opgave 3

### Split Spiller fra Model
For at roterer spilleren, så vælger vi at flytte modellen væk fra bevægelselogikken. Så vi splitter modellen og spilleren op i 3 dele. Først så laver vi en ny `Capsule` som skal være et barn af Spilleren. Herefter, så laver vi 

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
