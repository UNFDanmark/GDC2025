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
`Instantiate` skal bruge en reference til det objekt man gerne vil lave, så vi laver en `public` variabel `bullet` af typen `GameObject` som 
kan indeholde referencen. Vi kan nu drag-and-droppe vores prefab af patronen over i feltet for `bullet. 

*gif af at drag-and-droppe prefab ind i variabel*

Tilbage i vores script kan vi nu i `Update`-funktionen kalde `Instantiate` med `bullet` som parameter.
```C#
void Update()
{
    Instantiate(bullet);
    
}
```
Hvis vi nu starter spillet kan vi se at der kommer massere af patroner, men de starter alle der hvor den originale patron var sat.
Heldigvis kan man også fortælle `Instantiate` hvor den skal lave det nye objekt henne, når man gør dette skal man dog osgå give en rotation med således at det nye objekt er roteret som man vil have det. 
Til at give positionen hvor vi vil lave de nye patroner bruger vi bare `transform.position`, og som rotation bruger vi `quaternion.identity`, som vist nedenunder.
```C#
void Update()
{
    Instantiate(bullet,transform.position,quaternion.identity);
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
    Instantiate(bullet,transform.position,quaternion.identity);
}
```

## Physics Layer
Som man kan se når man starter spillet, så støder de patroner som man skyder ind i spilleren selv. Til at løse det problem
gør vi brug af det som Unity kalder Physics layers. Disse layers dikterer hvad der kan kollidere med hvad

## Timer

## Opgave 1
- Slå “GameObject.Destroy()” op i Unity's dokumentation
- Prøv at bruge “GameObject.Destroy()” til at fjerne bullets efter et stykke tid

/-- Indsæt gif her --/

## Bonus Opgave
Tænk over hvordan man ville kunne blive ved med at skyde uden at give slip på skyde knappen
