# Beskrivelse (Krop og kode)

Velkommen, dette er starten af dit eventyr for at lære Unity!
Vi ville nu starte med åbne projektet og se på nogle af de grundlæggende ting i Unity.
Dette segment begynder vi også at se på, hvordan vi kan bruge kode til at interagere med vores spil.

![unitybrugerflade](unitybrugerflade.png)


## Åbne projektet
For at starte skal i åbne Unity Hub og åbne projektet "Unity Basics" som vi har gjort klar til jer.

![unityhub.png](unityhub.png)

Når i har åbnet projektet, er i klar til at begynde at arbejde i Unity.

## Unity brugerflade

Når i har åbnet projektet, vil i se Unity brugerfladen. Her er nogle af de vigtigste elementer i brugerfladen:

1. **Scene view**: Her kan i se jeres spil og redigere det.
2. **Game view**: Her kan i se jeres spil som det vil se ud for spilleren.
3. **Hierarchy**: Her kan i se alle objekter i jeres scene.
4. **Inspector**: Her kan i se og redigere egenskaberne for det valgte objekt.
5. **Project**: Her kan i se alle filer i jeres projekt.
6. **Console**: Her kan i se fejl og beskeder fra Unity.

## Spiller Objektet

I jeres scene vil i kunne højre klikke og vælge "Create Cube" for at lave et nyt objekt. Dette objekt vil være jeres spiller objekt. 
I kan flytte spilleren ved at klikke på objektet og trække det rundt i scenen.

![create-cube.png](create-cube.png)

## Kode

Lav et script til spilleren ved at klikke på spilleren i hierarkiet og derefter klikke på "Add Component" i inspektoren.
Vælg "New Script" og kald det "PlayerScript". Dobbeltklik på scriptet for at åbne det i Rider.

![Unity_Kbm2Suo9W9.gif](Unity_Kbm2Suo9W9.gif)


I bør se en stump kode der ser sådan ud:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

Her er der to metoder, `Start` og `Update`. 
- `Start` bliver kaldt når spillet starter.
- `Update` bliver kaldt en gang hver gang der tegnes et billede på skærmen. (en gang per frame).


## Start
Hvis vi skriver `print("Jeg er kaldt en gang")` i `Start` metoden, vil vi se "Jeg er kaldt en gang" i konsollen når spillet starter.
```C#
void Start()
{
    print("Jeg er kaldt en gang");
}
```


## Update
Hvis vi skriver `print("Jeg er kaldt meget")` i `Update` metoden, vil vi se "Jeg er kaldt meget" i konsollen en masse gange. En gang per frame for at være nøjagtig.
```C#
void Update()
{
    print("Jeg er kaldt meget");
}
```

## Opgave 1
Her er jeres første opgave:
1. Lav endnu et objekt som kan bruges om fjende, med samme komponenter som spilleren
2. Få fjenden til at skrive “hej, jeg er ond” en gang i konsollen

Når i er færdige med at gentage hvad vi har lavet og lave opgaven, bør det se ud som under. 
I er velkommen til at læse foran men så kan det hurtig blive kedeligt.

![writerside64_nU9hKH4rE9.gif](writerside64_nU9hKH4rE9.gif)