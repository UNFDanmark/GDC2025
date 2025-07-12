# Del 4 (Advanced AI)

I denne sektion vil vi prøve at lave et simpel AI, hvor når fjenden kan se spilleren, så skyder den.
## Raycasting
For at finde ud af om fjenden kan se spilleren, så tager vi brug af `RayCast`. Vi kan forstille os en raycast, som en linje vi skyder ud i rummet og, hvis vi rammer noget, så kan vi få noget information om hvad.

Vi laver et nyt script på Fjenden som hedder `AIEyes`. 

For at tjekke om vi rammer noget foran os, så kan vi gøre det følgende:
```c#
bool hitSomething;
void Update() 
{
    hitSomething = Physics.Raycast(transform.position, transform.forward);
    
    print(hitSomething);
    
}
```
Det første argument til `hitSomething` er start positionen af linjen, det andet er retningen som vi vil skyde mod.



Det er dog ofte ikke så spændende bare at vide om man har ramt noget, så hvis vi gerne vil have noget information om objektet vi har ramt, så kan vi gøre det følgende:

```c#
RaycastHit hit;
bool hitSomething;

void Update() {
    hitSomething = Physics.Raycast(transform.position, transform.forward, out hit);
    
    if(hitSomething) 
    {
        if(hit.transform.CompareTag("Player")) 
        {
            print("Fjenden kan se spilleren");
        }
    }
}
```



## OnDrawGizmos
Når vi arbejder med `Raycast` så er den en god ide for programmøren, at kunne visualisere, hvad vi rammer og hvordan vi skyder i Unity Editoren. Det kan vi opnå med Gizmos.


```c#
void OnDrawGizmos()
{
    if (hitSomething && hit.transform.CompareTag("Player"))
    {
        Gizmos.color = Color.green;
        
    }
    else
    {
        Gizmos.color = Color.red;
    }
    Gizmos.DrawRay(transform.position, transform.forward * 100f);
}
```
`OnDrawGizmos` er en funktion som bliver kaldt af Unity Editoren, hver gang den gerne vil tegne nye Gizmos. 
`Gizmos.DrawRay` tager to argumenter, en start position og en retningsvektor.

I Unity kan det nu ses, at vi skyder ud fra centrum af fjenden, dette er ikke hvad vi ønsker. 
Det kan også ses, at vi kan se uendeligt langt, hvilket er urealistisk.

## Fix af småfejl
For at fixe de to fejl, så skal vi tilføje to variabler til vores script.

```c#
public float sightDistance = 8f;
public Transform eyes;
```

Vi opdaterer nu `Raycast` til at tage højde for de nye variabler.

```c#
hitSomething = Physics.Raycast(eyes.position, eyes.forward, out hit, sightDistance);
```
Vi skal selvfølgelig også opdaterer Gizmos til at bruge den rigtige position:
```c#
Gizmos.DrawRay(eyes.position, eyes.forward * sightDistance);
```

Inde i Unity så skal vi tilføje et nyt tomt `GameObject` som barn af fjenden, som hedder "Eyes".

![fjende-eyes.png](fjende-eyes.png)

Vi skal huske at sørge for at vores `AIEyes` script på fjenden har en reference til "Eyes"


## Opgave 4
In progress


