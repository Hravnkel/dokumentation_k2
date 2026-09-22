# Referenser till andra objekt

Den av LinkedArt [definierade](https://linked.art/api/1.0/shared/reference/), och av RAÄ föreskrivna, metoden för att referera ("länka") till andra objekt utan att behöva ange det refererade objektets innehåll i sin helhet. Ett objekt kommer tolkas som en referens om det endast innehåller attributen `id` och `type`, samt valfritt även `_label`, `equivalent` och `notation`.

Nedan exempel visar hur en referens används för att ange att ett objekt ingår i en samling. 

```
{
    "id" : "https://kulturarvsdata.se/exem/pel/abc",
    "type" : "HumanMadeObject",    
    ✂️ …
    "member_of" : {
        "id" : "https://kulturarvsdata.se/exem/pel/samlingen",
        "type" : "Set",
        "_label": "Referens till samlingen som abc ingår i"
    }
    ✂️ …
}
```