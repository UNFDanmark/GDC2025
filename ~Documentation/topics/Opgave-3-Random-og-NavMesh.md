# Del 3 (Random og NavMesh)

## NavMesh

### Navmesh Surface

For at kunne skabe nogle mere spændende fjender, vil vi gerne have de kan bevæge sig. 
Til det bruger vi NavMesh. Først skal vi fortælle unity hvorhenne vores enemy må og kan gå. 
Til det formål giver unity os komponentet `NavMeshSurface`. Lad os tilføje den til vores plane.

**INDSÆT BILLEDE AF NAVMESHSURFACE MENU**

Her er der en del indstillinger at lege rundt med, men for nu trykker vi på Bake knappen.

**INDSÆT BILLEDE AF BAKED OVERFLADE**

Det blå område der tegner sig er vores navmeshsurface. Det er det område vores enemy kan gå på.

### Navmesh Agent
Men før vores enemy kan finde rundt skal vi også lige fortælle vores enemy object at den kan gå.
Her giver vi den komponetet `Nav Mesh Agent`. Den fotæller unity at vores enemy object skal kunne navigere på en navmesh surface,
som den vi lige har lavet.

**INDSÆT BILLEDE AF NAV MESH AGENT MENU HER EVENTUELT**.

Vi skal dog stadig fortælle den hvor den skal gå hen. Det kan vi heldigvis nemt gøre med `SetDestination()` funktionen.
SetDestination tager imod en Vector3 position, som for eksempel vores spillers position. 
I vores enemy script skal vi hive fat i vores `Nav Mesh Agent`, brug enten `GetComponent<NavMeshAgent>()`,
eller lav en public NavMeshAgent og drag and drop den i Unity. 
Vi skal have en reference til vores player, her skal vi igen gøre brug af `Tags`, heldigvis har unity allerede et player tag.
Giv vores playerobject player tagget og brug `FindWithTag("Player")`.

**INDSÆT BILLEDE AF AT VÆLGE PLAYER TAG PÅ PLAYER OBJECT**

```c#
public NavMeshAgent agent;
private GameObject player;

void Start(){
    player = GameObject.FindWithTag("Player");
}

void Update(){
    agent.SetDestination(player.transform.position);
}
```
... Enemy spawner ...

**INDSÆT GIF AF ENEMY GÅR MOD PLAYER**

## Random
Det er jo ikke så spændende at der kun er en fjende.
Til det laver vi et enemySpawner object. Siden det ikke er noget vi skal kunne se, giver det mening at lave et empty object. 

**INDSÆT BILLEDE AF MENU MED MUS PÅ EMPTY OBJECT**

Så laver vi et enemySpawnerScript på vores enemySpawner.
I det skal vi have en reference til det object vi gerne vil spawne, altså vores enemyobject.
Som med vores bullet kan vi spawne flere med `Instantiate()`. 
```c#
public GameObject spawnObject

void Update(){
    Initiate(spawnObject, transform.position, Quaternion.identity);
}
```

**INDSÆT GIF AF SPAWNING FJENDER**

Det ville dog være kedeligt hvis de alle spawnede det sammes sted hver gang. 
Så hvad nu hvis vi generede nogle tilfælge positioner til vores fjender. 
Her kan vi bruge **Random.Range** der giver os et tilfældigt tal mellem 2 tal vi vælger. 
Vi starter småt med et tal mellem -5 og 5.
```c#
Vector3 spawnPosition = transform.position;
spawnPosition.x = spawnPosition.x + Random.Range(-5, 5);
spawnPosition.z = spawnPosition.z + Random.Range(-5, 5);
Instantiate(prefab, spawnPosition, Quaternion.Identity);
```
**GIF AF SPAWN AF FJENDER I TILFÆLDIG POSITION**.
Det er vigtig at huske at højre side af `=` tegnet bliver kørt først. Så selvom:

```C#
val = val + 1;
```

Ikke giver mening i Matematik, så er det helt ok i programming. 
Eksempelvis hvis `val` er `1` så når den linje er kørt ville `val` være `2` fordi:
1. Starter med: `val = val + 1` 
2. Men vi ved at val var `1`, altså `val = 1 + 1`
3. Det på højre bliver kørt så `val = 2`
4. Det betyder altså at `val` er nu `2`


## Opgave
1. Få mønter til at spawne på tilfældige steder
2. Få mønter til at rotere
