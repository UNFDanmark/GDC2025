# Del 1 (3D og Lyd)

## Download Assets
Alle resourcer som vi skal bruge i denne undervisning kan findes her:
- <resource src="ContentGDC2024.zip"/>

## Opsætning af Model på Spiller

Når vi sætter en model på en spiller, så skal vi først importere modellen. Dette gøres ved at trække modellen ind i `Assets` mappen i Unity.
Her tager vi og importer alle assets fra `ContentGDC2024.zip` til en mappe `/Content`.

![Unity_2SdPWbnbKh.gif](Unity_2SdPWbnbKh.gif)

Når modellen er importeret, så kan vi trække modellen ind i scenen. For at gøre dette skal vi først finde vores spiller GameObject, og derefter trække modellen ind i dette GameObject.

![Unity_jFKcQ1ewee.gif](Unity_jFKcQ1ewee.gif)

Du kan passende også her vælge at slette den del af modellen som du ej behøver.
<tabs>
<tab title="Før">
<img src="ModelBefore.png" alt=""/>
</tab>
<tab title="Efter">
<img src="ModelAfter.png" alt=""/>
</tab>
</tabs>

## Idle Animation

For at sæt idle animation ind på spilleren skal vi blot trække animationen ind i vores `Rogue` GameObject.

![InsertAnimation.gif](InsertAnimation.gif)

Når det er gjort skulle i gerne kunne double klikke på `Controller` (som ligger under det `Animator` component der ligger på `Rogue` GameObject).

![AnimatorWindow.png](AnimatorWindow.png)

Men bemærk at den ej gentager animationen. Det skyldes at vi ikke har sat den til at loope. Dette kan gøres ved at finde animationen på modellen og vælge `Loop Time`.
Dette skal gøres for alle animationer I vil have til at loope.



![LoopAnAnimation.gif](LoopAnAnimation.gif)

Så skulle idle gerne virke 🕺💃

![IdleAnimation.gif](IdleAnimation.gif)

## Opgave A
- Gør det samme for fjender men med skelet modellen.

![SkeletonIdle.gif](SkeletonIdle.gif)

## Animator kode

## Opgave B

## Lyd
