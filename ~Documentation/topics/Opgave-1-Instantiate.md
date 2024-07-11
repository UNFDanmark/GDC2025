# Del 1 (Instantiate)

## Prefabs
For at kunne skyde skal vi først lave en patron vi kan skyde med. Start med at lave en sphere og skaler den ned så den er en rimelig størrelse.
For at patronen senere kan skydes afsted får den også en `Rigidbody` component. Dernæst vil vi gerne sørge for at vi
kan genbruge det patron objekt som vi lige har lavet, det gør vi nemt ved at vælge patronen og drag-and-droppe den ned i vores project-vindue.
Ved at drag-and-droppe på denne måde laver man det man kalder et *prefab*, det er en kopi med alle de samme egenskaber
som det originale objekt som kan genbruges forskellige steder.
Hvis man ændrer på egenskaberne i prefabben så ændrer det også på alle steder hvor man bruger den.

Nu hvor vi har et prefab kan vi slette den originale patron uden at at få problemer senere.

![prefab.gif](prefab.gif)

## Instantiering
Vi åbner vores script hvor vi skrev rotationskoden siden det er rotationen der styrer retningen vi skal skyde i.
For at kunne skyde skal vi kunne lave nye objekter mens spillet kører, det gør man med funtionen [`Instantiate`](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html).
`Instantiate` skal bruge en reference til det objekt man gerne vil lave, så vi laver en `public` variabel `bulletPrefab` af typen `GameObject` som 
kan indeholde referencen. Vi kan nu drag-and-droppe vores prefab af patronen over i feltet for `Bullet Prefab`. 

![drag-prefab-to-inspector-field.gif](drag-prefab-to-inspector-field.gif)

<note>
Vær obs på at hvis I glemmer dette step så får i understående fejl. Dette er en meget almindelig fejl man ofte kommer til at møde. Den kendes blandt andet også under navnet "Null Reference".
<img src="nullref.gif" alt="Dette er et eksempel på en null reference fejl"/>
</note>

Tilbage i vores script kan vi nu i `Update`-funktionen kalde `Instantiate` med `bulletPrefab` som parameter.
```C#
void Update()
{
    Instantiate(bulletPrefab);
}
```
Hvis vi nu starter spillet kan vi se at der kommer massere af patroner, men de starter alle der hvor den originale patron var sat.
Heldigvis kan man også fortælle `Instantiate` hvor den skal lave det nye objekt henne, når man gør dette skal man dog osgå give en rotation med således at det nye objekt er roteret som man vil have det. 
Til at give positionen hvor vi vil lave de nye patroner bruger vi bare `transform.position`, og som rotation bruger vi `quaternion.identity`, som vist nedenunder.
```C#
void Update()
{
    Instantiate(bulletPrefab, transform.position, Quaternion.identity);
}
```
## Input GetKey
`Input` klassen har også en metode [`GetKey`](https://docs.unity3d.com/ScriptReference/Input.GetKey.html) som tager en `KeyCode` som argument.
`KeyCode` er en type der repræsenterer en tast på tastaturet.
Denne metode returnerer `true` hvis tasten er trykket ned og `false` ellers.
Tag som eksempel koden `Input.GetKey(KeyCode.W)` den ville returnere `true` hvert frame hvor W-tasten er trykket ned.
Man kunne bl.a. blande det med viden om `if`-sætninger til at flytte en spiller fremad.
```C#
if (Input.GetKey(KeyCode.W))
{
    print("W er holdt nede");
}
```
Det er også muligt at bruge [`Input.GetKeyDown`](https://docs.unity3d.com/ScriptReference/Input.GetKeyDown.html) som kun returnerer `true` den første frame hvor tasten er trykket ned.
```C#
if (Input.GetKeyDown(KeyCode.W))
{
    print("W er trykket en gang");
}
```
Vi kan sætte en `if`-statement rundt om kaldet til `Instantiate` således at man kun skydder når man trykker på mellemrumstasten.
```C#
if (Input.GetKeyDown(KeyCode.Space))
{
    Instantiate(bulletPrefab, transform.position, Quaternion.identity);
}
```

## Physics Layer
Som man kan se når man starter spillet, så støder de patroner som man skyder ind i spilleren selv. Til at løse det problem
gør vi brug af det som Unity kalder Physics layers. Disse layers dikterer hvad der kan kollidere med hvad, så vi skal bruge
nogle layers til at repræsentere vores spiller og patroner. Man kan tilføje nye physics layers ved at vælge et objekt og
klikke på "Add layer..." knappen i Layer dropdown menuen under objektets navn.

![create-layers.png](create-layers.png)

<tip>
Husk at, efter du har tilføjet layer's, skal du også gå tilbage til <b>spilleren</b> og <b>bullet</b> og vælge de ny skabte layers.
</tip>

Når man har lavet lagene skal man huske at tildele dem til ens `gameObjects`, det gør man samme sted som hvis man skulle lave nye lag.

Som vist herunder kan vi i project managerens Physics sektion deaktivere kollisioner mellem Player og Bullet lagende.

![collisionLayerMatch.gif](collisionLayerMatch.gif)

## Cooldown
Vi tilføjer en cooldown periode mellem vores skud, således at der skal være gået mindst en rum tid fra at man har skudt 
til at man kan skyde igen. Til vores cooldown skal vi bruge to variable til at at holde styr på værdier:
1. Definere en konstant værdi for hvor lang tid den cooldown skal varer
2. Definere en ændrende værdi for hvor mange sekunder der er tilbage før man må skyde igen.

```C#
public float cooldown = 0.2f;
float cooldownLeft;
```
Inde i den `if`-statement vi satte rundt om `Instantiate` kan vi nu sætte `cooldownLeft` til at være lig med `cooldown`
Desuden skal vi ændre på betinglesen for `if`-statementet således at vi kun kan skyde når `cooldownLeft` er mindre eller lig 0 som vist herunder.

```C#
if (Input.GetKeyDown(KeyCode.Space) && cooldownLeft <= 0) 
{
    Instantiate(bulletPrefab, transform.position, Quaternion.identity);
    cooldownLeft = cooldown;
}
```

Nu kan man, hvis man starter spillet, kun skyde en enkelt gang, fordi vi aldrig gør `cooldownLeft` mindre. Heldigvis 
kræver det kun en enkelt linje kode før `if`-statementet hvor vi gør variablen mindre.
```C#
cooldownLeft = cooldownLeft - Time.deltaTime;
```
`Time.deltaTime` er den mængde af tid der er gået siden sidste frame.

Noter at du kommer til at møde det her mønster ret meget I spil programmering:

```C#
// Værdi for cooldown tid i sekunder
public float someCooldown = 0.2f;

// Værdi for cooldown tid tilbage i sekunder
float someCooldownLeft;

void Update()
{
    // Tæl tiden ned
    someCooldownLeft = someCooldownLeft - Time.deltaTime;
    if (someCooldownLeft <= 0) 
    {
        // Gør noget her 
        // ...
        
        // Reset hvor meget tid er tilbage
        someCooldownLeft = someCooldown;
    }
}
```

<tip>
Det kunne måske være at i skal bruge det meget snart ;)
</tip>

## Opgave 1
- Slå `GameObject.Destroy()` op i Unity's dokumentation
- Prøv at bruge `GameObject.Destroy()` til at fjerne bullets efter et stykke tid

<deflist collapsible="true">
<def title="Hint A" default-state="collapsed">
    For at løse denne opgave skal I selv lave jeres egen MonoBehaviour script og tilføje det på et GameObject
</def>
<def title="Hint B" default-state="collapsed">
    Det MonoBehaviour script skal tilføjes på Bullet prefab'et
<img src="EnemyScript.gif" alt="Viser hvordan enemy script kan tilføjes"/>
<def title="Hint C" default-state="collapsed">
    Det er vigtigt at reset dine cooldown/lifetime til at starte ved det rigtige antal sekunder, og ikke 0.
<code-block lang="C#">
void Start()
{
    lifetimeLeft = lifetime;
}
</code-block>
</def>
</def>
</deflist>

Når opgaven er løst bør det gerne se sådan ud:

![InstantiateTimed.gif](InstantiateTimed.gif)



## Bonus Opgave
Tænk over hvordan man ville kunne blive ved med at skyde uden at give slip på skyde knappen
