# Del 2 (Kollision)

## Påvirk andre objekter
Nu hvor vi kan lave patroner vil vi gerne have at patronerne også flyver frem så man rigtig skyder. Istedet for at lave et 
script til patronen så kan vi istedet gøre det fra spilleren af. Når man kalder `Instantiate` får man faktisk også 


## OnCollisionEnter
Når nu vi faktisk kan skyde, så vil vi gerne have noget at skyde efter. Lidt ligesom da vi lavede spilleren laver vi en simpel kapsel
som vi kan kalde "Enemy". Fjenderne skal naturligvis dø når de
rammes af en patron. Unity har defineret funktionen `OnCollisionEnter` som kaldes automatisk når to objekter koliderer.
Det er nemmest hvis fjenderne selv holder styr på hvornår de bliver ramt, så vi laver et script til dem, og tilføjer den nedenstående kode.

```C#
void OnCollisionEnter (Collider other)
{
    //Code here
}
```

I denne funktion får man information om det andet objekt i kollisionen gennem variable `other`. Vi er kun interesserede i 
kollisioner der involverer patroner, så vi benytter en `if`-statement. I den statements betingelse kan vi benytte det der 
hedder tags til at kende forskel på patroner og andre typer af objekter. Som vist nedenunder laver vi et tag "Bullet" og 
tildeler det til vores prefab af patronen.

![PrefabBulletTag.gif](PrefabBulletTag.gif)

For at sikre at `other` er koblet til et `gameObject` med tagget "Bullet" bruger vi funtionen `CompareTag` som vist nedenunder.

```C#
if (other.gameObject.CompareTag("Bulllet")){
    
}
```

## GameObject.Destroy
Når man gerne vil fjerne `gameObjects` kan man med fordel bruge funktionen `Destroy`, som tager det `gameObject` som skal
fjernes som parameter.
Eksempelvis kan vi, når vi har sikret at fjenden er ramt af en patron, fjerne fjenden med `Destroy` som vist nedenunder.

```C#
if (other.gameObject.CompareTag("Bulllet")){
    Destroy(gameObject);
}
```

## Opgave 
1. Slå “OnTriggerEnter” op i unitys dokumentation 
2. Anvend funktionen til at lave en mønt der forsvinder når spilleren rammer den

![CoinsCollect.gif](CoinsCollect.gif)