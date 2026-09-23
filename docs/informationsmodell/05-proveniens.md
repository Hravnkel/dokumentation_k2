# 5. Proveniens

Det här kapitlet beskriver hur du anger information om postens ursprung: varifrån metadatan kommer, när källposten skapades och ändrades, och under vilka villkor metadatan får återanvändas. Proveniensinformationen beskriver alltså *posten*, inte den kulturarvsresurs som posten handlar om.

## Krav

- Varje objekt som har ett [persistent id](03-identitet-och-referenser.md#översikt) **ska** ha proveniensinformation.
- Proveniensinformation **ska inte** anges på icke-persistenta objekt eller på [referenser](03-identitet-och-referenser.md#referenser-till-andra-objekt).

Proveniensinformationen anges i ett `RecordProvenance`-objekt som är värde för attributet `recordProvenance` på det beskrivna objektet. Termerna för proveniensinformationen definieras i K-samsöks kontext `https://kulturarvsdata.se/resurser/linkedart/v1/raa.json` (se [Serialisering](02-serialisering.md)).

> [!WARNING]
> **Öppen fråga – attributnamn.** Stavningen av attributnamnen skiljer sig åt mellan exemplen, den löpande texten och [Modellreferensen](../referens/modellreferens.md#class-record-provenance):
>
> | Exempel | Modellreferens |
> |---|---|
> | `recordProvenance` | `record_provenance` |
> | `source_record` | `sourceRecord` |
> | `ingested_at` (i tidigare text) | `ingestedAt` |
>
> Vilken form som gäller behöver fastställas mot `raa.json`. Exemplen nedan har inte ändrats.

## Attribut

### `RecordProvenance`

| Attribut | Krav | Beskrivning |
|---|---|---|
| `id` | Obligatoriskt | Det beskrivna objektets `id` följt av `/prov`. Se [Proveniensobjektets id](#proveniensobjektets-id). |
| `type` | Obligatoriskt | Alltid `RecordProvenance`. |
| `license` | Obligatoriskt | Licensen för postens metadata. Värdet är alltid `http://creativecommons.org/publicdomain/zero/1.0/` (CC0). Se [Rättighetsmärkning](06-rattighetsmarkning.md#metadata). |
| `source_record` | Obligatoriskt | Information om källposten. Se nedan. |
| `about` | Behöver inte anges | En referens till det beskrivna objektet. Läggs till av RAÄ vid skördning. Attributet finns inte i Modellreferensen, vilket behöver utredas. |
| `provider` | Ska utelämnas | En referens till den organisation som äger posten. Läggs till av RAÄ vid skördning. |
| `ingested_at` | Ska utelämnas | Tidpunkten då posten skördades. Läggs till av RAÄ vid skördning. |

### `SourceRecord`

| Attribut | Krav | Beskrivning |
|---|---|---|
| `type` | Obligatoriskt | Alltid `SourceRecord`. |
| `url` | Obligatoriskt | Länk till källposten hos datapartnern. |
| `dateCreated` | Rekommenderat | När *källposten* skapades i datapartnerns system. |
| `dateModified` | Rekommenderat | När *källposten* senast ändrades i datapartnerns system. |

`dateCreated` och `dateModified` beskriver källposten, inte den post som levereras till K-samsök. De är inte obligatoriska, men bör anges när det är möjligt.

Den fullständiga definitionen finns i Modellreferensen: [RecordProvenance](../referens/modellreferens.md#class-record-provenance) och [SourceRecord](../referens/modellreferens.md#class-source-record).

## Proveniensobjektets id

`RecordProvenance`-objektet har en förutsägbar identitet: det beskrivna objektets `id` med path-segmentet `/prov` tillagt.

**Exempel:** Om objektets `id` är `https://kulturarvsdata.se/exem/pel/abc` blir proveniensobjektets `id` `https://kulturarvsdata.se/exem/pel/abc/prov`.

## Exempel

### Minimal proveniensinformation

Exemplet visar den minsta tillåtna formen av proveniensinformation för ett persistent objekt. Samtliga fält i exemplet är obligatoriska.

```json
{
    ✂️ …
    "id" : "https://kulturarvsdata.se/exem/pel/abc",
    "type" : "HumanMadeObject",    
    ✂️ …
    "recordProvenance" : {
        "id" : "https://kulturarvsdata.se/exem/pel/abc/prov",
        "type" : "RecordProvenance",
        "license" : "http://creativecommons.org/publicdomain/zero/1.0/",
        "source_record" : {
            "type" : "SourceRecord",
            "url" :  "https://exempel.org/objekt#abc" 
        }
    }
    ✂️ …
}
```

### Utökad proveniensinformation

Exemplet visar en rikare form av proveniensinformation. De rekommenderade fälten `dateCreated` och `dateModified` är angivna. Dessutom visas fälten `about` och `provider`, som RAÄ lägger till vid skördning, uttryckta som [referenser](03-identitet-och-referenser.md#referenser-till-andra-objekt).

```json
{
    ✂️ …
    "id" : "https://kulturarvsdata.se/exem/pel/abc",
    "type" : "HumanMadeObject",    
    ✂️ …
    "recordProvenance" : {
        "id" : "https://kulturarvsdata.se/exem/pel/abc/prov",
        "type" : "RecordProvenance",
        "license" : "http://creativecommons.org/publicdomain/zero/1.0/",
        "about" : { 
            "id" : "https://kulturarvsdata.se/exem/pel/abc",
            "type" : "HumanMadeObject",
            "_label" : "Referens till objektet som denna proviniensinformation gäller för"
        },
        "provider" : {
            "id" : "https://kulturarvsdata.se/exem",
            "type" : "Group",
            "_label" : "Referens till objektsägaren med ett kulturarvsdata-id"
        },
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

> [!NOTE]
> **Utkast.** Det ska beskrivas hur länken till källan anges, både i proveniensinformationen (`/prov`) och som digitalt objekt.
