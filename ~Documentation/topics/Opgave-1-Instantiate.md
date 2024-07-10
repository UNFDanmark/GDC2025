# Del 1 (Instantiate)

## Prefabs
For at kunne skyde skal vi først lave en patron vi kan skyde med. Start med at lave en sphere og skaler den ned så den er en rimelig størrelse.
For at patronen senere kan skydes afsted får den også en ````Rigidbody```` component. Dernæst vil vi gerne sørge for at vi
kan genbruge det patron objekt som vi lige har lavet, det gør vi nemt ved at vælge patronen og drag-and-droppe den ned i vores project-vindue.
Ved at drag-and-droppe på denne måde laver man det man kalder et *prefab*, det er en kopi med alle de samme egenskaber
som det originale objekt som kan genbruges forskellige steder.
Hvis man ændrer på egenskaberne i prefabben så ændrer det også på alle steder hvor man bruger den.

\\*insert gif of making prefab here*
## Instantiering


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

## Physics Layer

## Timer

## Opgave 1
- Slå “GameObject.Destroy()” op i Unity's dokumentation
- Prøv at bruge “GameObject.Destroy()” til at fjerne bullets efter et stykke tid

/-- Indsæt gif her --/

## Bonus Opgave
Tænk over hvordan man ville kunne blive ved med at skyde uden at give slip på skyde knappen
