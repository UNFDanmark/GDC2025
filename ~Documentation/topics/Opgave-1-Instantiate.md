# Opgave 1 (Instantiate)

## Lav Prefab



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
