# 3. Identitet och referenser

Det här kapitlet beskriver hur objekt identifieras i K-samsök, hur du skapar URI:er för de resurser du levererar och hur du hänvisar till andra objekt.

## Översikt

K-samsök skiljer mellan två slags objekt utifrån deras natur och livscykel:

| | Persistent objekt | Icke-persistent (anonymt) objekt |
|---|---|---|
| **Definition** | Ett objekt vars `id` är en upplösningsbar URI. | Ett objekt som saknar `id`, eller vars `id` inte är en URI. |
| **Så anges det** | `id` är en `http`- eller `https`-URI. | `id` utelämnas (rekommenderas) eller är en sträng som inte börjar med `http` eller `https`. |
| **Krav på beständighet** | Utfärdaren av URI:n ansvarar för att den är stabil och beständig över tid och att en upplösning av den ger ett meningsfullt svar. | Inga krav eller förväntningar. |
| **Exempel** | Fysiska eller digitala föremål, händelser och aktiviteter, motiv och texter, platser, samlingar, abstrakta företeelser, personer och grupper, begrepp. | En företeelse som bara är relevant för *ett* objekt och som ingen annan behöver hänvisa till, till exempel tidpunkten när ett föremål tillverkades. |

De persistenta objekten delas i sin tur in i två undertyper:

- **Kulturarvsdata-objekt** – objekt vars URI ligger i domänen `kulturarvsdata.se`. Se [Kulturarvsdata-URI:er](#kulturarvsdata-urier).
- **Andra persistenta objekt** – objekt vars URI ligger utanför `kulturarvsdata.se`. Se [Andra persistenta objekt](#andra-persistenta-objekt).

## Kulturarvsdata-URI:er

Varje kulturarvsresurs som en datapartner levererar för skördning ska ha en persistent kulturarvsdata-URI.

### Så är URI:n uppbyggd

```
https://kulturarvsdata.se/{datapartner-id}/{dataset-id}/{resurs-id}
```

| Del | Värde |
|---|---|
| Schema | Alltid `https` |
| Domän | Alltid `kulturarvsdata.se` |
| Första path-segmentet | Datapartnerns id, med gemener |
| Andra path-segmentet | Datamängdens id, med gemener |
| Tredje path-segmentet | Resursens id |

**Exempel:** En datapartner med id `exem`, en datamängd med id `pel` och en resurs med id `abc` ger URI:n `https://kulturarvsdata.se/exem/pel/abc`.

### Så skapar du URI:erna

1. Hämta ert datapartner-id och dataset-id i K-samsök 2:s administrativa gränssnitt. Använd alltid de id:n som RAÄ har tilldelat.
2. Välj ett resurs-id för varje resurs, till exempel ert interna post-id.
3. Sätt ihop URI:n enligt mönstret ovan och ange den som `id` på resursen när du förbereder datamängden. URI:erna ska alltså finnas med i datamängden när den skördas.

> [!TIP]
> Använd bara så kallade URI-säkra tecken i resurs-id:t, det vill säga a–z, A–Z, siffror, understreck och bindestreck (`^[a-zA-Z0-9_-]*$`). Det rekommenderas starkt.

> [!NOTE]
> **Öppen fråga.** Vissa auktoriteter och vokabulärer under `kulturarvsdata.se/resurser/` använder schemat `http` (se [Vokabulärer](09-vokabularer.md)). Det behöver förtydligas vilken form som är kanonisk för dem och hur `http` och `https` jämställs.

## Andra persistenta objekt

K-samsök 2 tolkar alla objekt vars `id` är en `http`- eller `https`-URI som persistenta. Utöver de kulturarvsdata-URI:er som tilldelas skördade resurser förekommer därför även referenser till persistenta URI:er utanför `kulturarvsdata.se`. Oftast är det länkade öppna data (LOD) som tillgängliggörs av andra aktörer, till exempel Kungliga biblioteket, Getty och Wikidata.

## Icke-persistenta objekt

Eftersom alla `http`- och `https`-URI:er tolkas som persistenta anger du att ett objekt är icke-persistent på något av följande sätt:

- **Utelämna `id`** (rekommenderas).
- Ange som `id` en godtycklig sträng som inte börjar med `http` eller `https`. Det tillåts av bakåtkompatibilitetsskäl, men RAÄ garanterar inte att sådana id:n behålls.

Se [exemplen](#exempel) nedan.

## Referenser till andra objekt

En *referens* är det sätt som Linked Art [definierar](https://linked.art/api/1.0/shared/reference/), och RAÄ föreskriver, för att hänvisa ("länka") till ett annat objekt utan att ange hela dess innehåll.

Ett objekt tolkas som en referens om det **enbart** innehåller:

| Attribut | Krav |
|---|---|
| `id` | Obligatoriskt |
| `type` | Obligatoriskt |
| `_label` | Rekommenderat |
| `equivalent` | Valfritt |
| `notation` | Valfritt |

Om objektet innehåller fler attribut än dessa tolkas det inte som en referens utan som en (partiell) beskrivning av objektet.

Följande exempel visar hur en referens används för att ange att ett objekt ingår i en samling:

```json
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

### Medlemskap i samlingar

Medlemskap i en samling (`Set`) eller annan kollektion ska anges från medlemmen till samlingen, som i exemplet ovan. K-samsök förbehåller sig rätten att vända på relationen om den anges i motsatt riktning.

## Exempel

### Persistent rotobjekt med icke-persistent underobjekt

Rotobjektet (`Person`) har ett persistent kulturarvsdata-id. Underobjektet (`Name`) är icke-persistent, vilket framgår av att det saknar `id`.

```json
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : {
	  "type" : "Name",
	  "content" : "Harald Blåtand",
	  "language" : {
  	   ✂️ …	    
	  }
	}
	✂️ …
	
}
```

Samma sak, men här anges icke-persistensen hos `Name` med ett `id` som inte är en `http(s)`-URI. Mönstret tillåts av bakåtkompatibilitetsskäl, men det rekommenderade mönstret är att utelämna `id` helt.

```json
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : [{
	  "type" : "Name",
	  "id" : "_hbtnamn",
	  "content" : "Harald Blåtand",
	  "language" : {
  	   ✂️ …	    
	  }
	}]
	✂️ …
	
}
```

> [!NOTE]
> **Öppen fråga.** En JSON-LD-processor tolkar en sträng som `_hbtnamn` i `id` som en *relativ* URI mot dokumentets bas-URI. Det behöver fastställas hur skördaren hanterar sådana id:n.

### Persistent rotobjekt med både icke-persistenta och persistenta underobjekt

Underobjektet `Name` är icke-persistent. Dess `language` är en referens till ett persistent objekt (termen *svenska* i Getty AAT).

```json
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : [{
	  "type" : "Name",
	  "content" : "Harald Blåtand",
	  "language" : {
  	   "id" : "http://vocab.getty.edu/aat/300389336",
	   "type" : "Language",
	   "_label" : "svenska"
	  }
	}]
	✂️ …
	
}
```

### Persistent objekt som är medlem i en samling

`Person`-objektet är medlem i en persistent samling (`Set`). Samlingen är här *inte* en referens, eftersom den innehåller fler attribut än `id`, `type` och `_label`.

```json
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"member_of" : {
	  "type" : "Set",
	  "id" : "https://kulturarvsdata.se/exem/pel/vikingar",
	  "_label" : "Kollektionen 'Kända vikingar'",
	  "title" : [✂️ …],
	  "about" : [✂️ …],
	  ✂️ …  
	}
	✂️ …	
}
```

> [!NOTE]
> **Utkast.** Exempel på URI-mönster för `id` på `RecordProvenance` finns i [Proveniens](05-proveniens.md#proveniensobjektets-id). Exempel på URI-mönster för `id` på `VisualItem` ska läggas till.
