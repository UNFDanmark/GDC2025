# Opgave 3 (Random og NavMesh)

## NavMesh

.. navmesh surface .. navmesh agent ..

## Random

```C#
Vector3 spawnPosition = transform.position;
spawnPosition.x = spawnPosition.x + Random.Range(-5, 5);
spawnPosition.z = spawnPosition.z + Random.Range(-5, 5);
Instantiate(prefab, spawnPosition, Quaternion.Identity);
```

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
