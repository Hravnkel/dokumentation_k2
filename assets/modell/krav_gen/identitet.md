# Identitet

Exempel på de identitetsuttryck som beskrivs nedan finns i [Exempelbanken](../exempel/id.md).


## <a id="intro"></a>Introduktion

I K-samsök skiljer vi när det gäller objekts natur och livscykel mellan två huvudsakliga objektstyper: 

- **Persistent objekt**: ett objekt vars id är en upplösningsbar URI. Utställaren av den givna URI:n ansvarar för att URI:n är stabil, permanent och beständig över tid, samt att en upplösning av URI:n ger ett meningsfullt svar.

__Exempel:__ fysiska eller digitala objekt/föremål, händelser och aktiviteter, motiv och texter, platser, samlingar, abstrakta företeelser, personer och grupper, begrepp

- **Icke-persistent** (eller 'anonymt') **objekt**: ett objekt som saknar id, eller inte har en URI som id. Inga krav eller förväntningar finns på sådana objekt gällande beständighet.

__Exempel:__ en företeelse som endast har relevans för ETT objekt och som ingen annan behöver hänvisa till. Det kan vara tidpunkten för när ett objekt skapades. 

### Undertyper till persistenta objekt

De persistenta objekten i sin tur indelas inom K-samsök i två underttyper:

- **Kulturarvsdata-objekt**: Objekt med persistenta URI:er vars domän är `kulturarvsdata.se`. Se [Identitet för Kulturarvsdata-objekt](#kad) nedan. 
- **Andra persistenta objekt'**: Objekt med persistenta URI:er som ligger utanför kulturarvsdata-domänen. Se [Identitet för andra persistenta objekt](#ext) nedan. 

## <a id="kad"></a>Identitet för Kulturarvsdata-objekt

Varje kulturarvsresurs som tillhandahålls av en datapartner för skördning till K-samsök tilldelas en persistent kulturarvsdata-URI. 

Kulturarvsdata-URI:er för skördade resurser har följande struktur:
- URI:ns `scheme` är alltid `https`
- URI:ns `domain` är alltid `kulturarvsdata.se`
- URI:n innehåller tre path-segment: 
   1) datapartnerns id i gemener
   2) datasetets id i gemener
   3) resursens id

Givet en datapartner med id `exem` och ett dataset med id `pel` och en resurs med id `abc` blir kulturarvsdata-URI:n således `https://kulturarvsdata.se/exem/pel/abc`

Datapartnern skapar kulturarvsdata-URI:erna enligt ovanstående mönster när ett dataset förbereds för skördning. URI:erna finns alltså med i datasetet när det skördas. Datapartnern använder konsekvent det datapartner-id och dataset-id som tilldelats av RAÄ (dessa finns att tillgå i K-samsök 2's administrativa gränssnitt). 

Notera: vi rekommenderar starkt att använda endast så kallade "URI-safe" bokstäver (`^[a-zA-Z0-9_-]*$`) i resursens id-segment, det vill säga att id:t är begränsat till a-z, siffror, understreck och bindestreck.   

## <a id="ext"></a>Identitet för andra persistenta objekt

K-samsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta. Vid sidan av de kulturarvsdata-URI:er som tilldelas de skördade resurserna förekommer naturligt även referenser till andra persistenta URI:er som ligger utanför kulturarvsdatadomänen. I de flesta fall är dessa URI:er referenser till andra LOD (Linked Open Data) resurser som tillgängliggörs av andra aktörer, till exempel Kungliga Biblioteket, Getty och Wikidata. 

## <a id="nonpersistent"></a>Identitet för icke-persistenta objekt

Eftersom K-samsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta, indikeras ett objekt som icke-persistent genom att helt utelämna id-fältet på objektet, eller genom att ange en godtycklig sträng som inte börjar med `http`- eller `https` som dess värde.


Exempel på de identitetsuttryck som beskrivs ovan finns i [Exempelbanken](../exempel/id.md).


