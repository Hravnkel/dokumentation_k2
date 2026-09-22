### RecordProvenance: Exempel

Följande exempel visar den minimala formen av den digitala proviniensen (`RecordProvenance`) för ett persistent objekt. Samtliga fält i exemplet är obligatoriska.

```
{
    ✂️ …
    "id" : "https://kulturarvsdata.se/exem/pel/abc",
    "type" : "HumanMadeObject",    
    ✂️ …
    "recordProvenance" : {
        "id" : "https://kulturarvsdata.se/exem/pel/abc/prov",
        "type" "RecordProvenance",
        "license" : "http://creativecommons.org/publicdomain/zero/1.0/",
        "source_record" : {
            "type" : "SourceRecord",
            "url" :  "https://exempel.org/objekt#abc" 
        }
    }
    ✂️ …
}
```

Följande exempel visar en rikare form av digitala proviniens. De två rekommenderade (icke-obligatoriska) fälten `dateCreated` och `dateModified` är angivna. Två icke-obligatoriska fält som RAÄ autogenererar vid skördning — `about` och `provider` —  är också angivna, och korrekt uttryckta som [referenser](Terminologi.md#referens).

```
{
    ✂️ …
    "id" : "https://kulturarvsdata.se/exem/pel/abc",
    "type" : "HumanMadeObject",    
    ✂️ …
    "recordProvenance" : {
        "id" : "https://kulturarvsdata.se/exem/pel/abc/prov",
        "type" "RecordProvenance",
        "license" : "http://creativecommons.org/publicdomain/zero/1.0/",
        "about" : { 
            "id" : "https://kulturarvsdata.se/exem/pel/abc",
            "type" : "HumanMadeObject"
            "_label" : "Referens till objektet som denna proviniensinformation gäller för"
        },
        "provider" : {
            "id" : "https://kulturarvsdata.se/exem",
            "type" : "Group"
            "_label" : "Referens till objektsägaren med ett kulturarvsdata-id"
        }
        "source_record" : {
            "type" : "SourceRecord",
            "dateCreated" : "2021-02-03T00:00:00",
            "dateModified" : "2022-03-04T00:00:00",
            "url" :  "https://exempel.org/objekt#abc" 
        }
    }
    ✂️ …
}
```