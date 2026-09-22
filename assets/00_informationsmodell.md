# Ksamsök 2 LinkedArt-profil: informationsmodell

## Introduktion
@@@ TODO övergripande intro till linked.art, ref till linked.art/model

K-samsöks informationmodell är baserad på [LinkedArt](https://linked.art/), en länkad öppen data-modell för att beskriva kulturarv. LinkedArt är en anpassning av CIDOC-CRM, vilket gör den interoperabel med många andra resurser. Som namnet antyder är LinkedArt främst utvecklad för att beskriva konst men också arkiv- och bibliografiskt material. Då K-samsök även innehåller annat material, ex. fornlämningar, bygger vi även ut modellen på relevanta [områden](./krav_gen/index.md) (placeholder).



## Ksamsök 2 LinkedArt-profil: Generella krav

K-samsök har ett antal obligatoriska attribut för objekt för enhetlig hantering av data och för att möjliggöra aggregering till Europeana/det gemensamma europeiska dataområdet för kulturarv och andra dataportaler. 

### Obligatoriska attribut för objekt

@@@ TODO Agnieszka. Obs, listan fortfarande preliminär. Behöver även kollas termmässigt mot LA. På engelska eller svenska? 

- Title
- URI 
- Publisher - partnern som bidrar med objektet
- DataProvider - partnern som äger datan (ev. samma som utgivare?)
- Description 
- Updated - datum när posten uppdaterades
- Harvested date - autogenereras vid skördning
- Type 
- Classification - för Europeana 
- Rights
- isShownAt (Link to istutionen) - (auto?)
- isShownBy (Link to file)
- edm:provider (K-samsök) - i EDM-mappningen?

#### Rekommenderade attribut för objekt

- Creator
- Owner - objektets ägare
- Keywords
- Inventory number
- Alternative title
- isPartOf
- isNextInSequence

### Utifrån detta, MVO på Linked Art:ska för Europeanaleverans

- identified_by
- id (URI)
- type
- classified_as *(obs rekomenderad men ej tvingande hos LA/K2 i dagsläget)*
- proveniensmetadata: länk till källan, CC0 osv
- Publisher/Dataprovider – fylls i automatiskt vid skördning
- Description *(obs rekomenderad men ej tvingande hos LA/K2 i dagsläget)*
- Updated *(hos källan – ur proveniensmetadata)*
- Harvested date *(autogenereras vid skördning – ur proveniensmetadata)*
- subject_to *(för visual/linguistic items)*
- isShownAt *(länk till källan – ur proveniensmetadata)*
- isShownBy *(visualised_by för visual/linguistic items)*
- edm:provider (K-samsök) (autogenereras i EDM-mappningen)

#### Rekommenderade

- Creator **(hos LA en creation event där en person har varit delaktig)**
- Owner **(hos LA en current owner eller transfer of custody)**
- Keywords **(helst länkar)**
- Inventory number **(identified_by number med classified as)**
- Alternative title **(identified_by name med classified as)**
- isPartOf 
- isNextInSequence *(???)*





## Identitet

Exempel på de identitetsuttryck som beskrivs nedan finns i [Exempelbanken](../exempel/id.md).


### <a id="intro"></a>Introduktion

I Ksamsök skiljer vi när det gäller objekts natur och livscykel mellan två huvudsakliga objektstyper: 

- **Persistent objekt**: ett objekt vars id är en upplösningsbar URI. Utställaren av den givna URIn ansvarar för att URI:n är stabil, permanent och beständig över tid, samt att en upplösning av URI:n ger ett meningsfullt svar.
- **Icke-persistent** (eller 'anonymt') **objekt**: ett objekt som saknar id, eller inte har en URI som id. Inga krav eller förväntningar finns på sådana URI:er gällande beständighet.

De persistenta objekten i sin tur indelas inom Ksamsök i två underttyper:

- **Kulturarvsdata-objekt**: Objekt med persistenta URI:er vars domän är `kulturarvsdata.se`. Se [Identitet för Kulturarvsdata-objekt](#kad) nedan. 
- **Andra persistenta objekt'**: Objekt med persistenta URI:er som ligger utanför kulturarvsdata-domänen. Se [Identitet för andra persistenta objekt](#ext) nedan. 

### <a id="kad"></a>Identitet för Kulturarvsdata-objekt

Varje kulturarvsresurs som tillhandahålls av en datapartner för skördning till Ksamsök tilldelas en persistent kulturarvsdata-URI. 

Kulturarvsdata-URI:er för skördade resurser har följande struktur:
- URI:ns `scheme` är alltid `https`
- URI:ns `domain` är alltid `kulturarvsdata.se`
- URI:n innehåller tre path-segment: 
   1) datapartnerns id i gemener
   2) datasetets id i gemener
   3) resursens id

Givet en datapartner med id `exem` och ett dataset med id `pel` och en resurs med id `abc` blir kulturarvsdata-URI:n således `https://kulturarvsdata.se/exem/pel/abc`

Datapartnern skapar kulturarvsdata-URI:erna enligt ovanstående mönster när ett dataset förbereds för skördning. URI:erna finns alltså med i datasetet när det skördas. Datapartnern använder konsekvent det datapartner-id och dataset-id som tilldelats av RAÄ (dessa finns att tillgå i Ksamsök 2's administrativa gränssnitt). 

Notera: vi rekommenderar starkt att använda endast så kallade "URI-safe" bokstäver (`^[a-zA-Z0-9_-]*$`) i resursens id-segment, det vill säga att id:t är begränsat till a-z, siffror, understreck och bindestreck.   

### <a id="ext"></a>Identitet för andra persistenta objekt

Ksamsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta. Vid sidan av de kulturarvsdata-URI:er som tilldelas de skördade resurserna förekommer naturligt även referenser till andra persistenta URI:er som ligger utanför kulturarvsdatadomänen. I de flesta fall är dessa URI:er referenser till andra LOD (Linked Open Data) resurser som tillgängliggörs av andra aktörer, till exempel Kungliga Biblioteket, Getty och Wikidata. 

### <a id="nonpersistent"></a>Identitet för icke-persistenta objekt

Eftersom Ksamsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta, indikeras ett objekt som icke-persistent genom att helt utelämna id-fältet på objektet, eller genom att ange en godtycklig sträng som inte börjar med `http`- eller `https` som dess värde.


Exempel på de identitetsuttryck som beskrivs ovan finns i [Exempelbanken](../exempel/id.md).




## Ksamsök 2 LinkedArt-profil: Övergripande krav

### <a id="record_provenance"></a>Digital Proveniens

Samtliga objekt som har ett [persistent id](./identitet.md#persistent) måste också ha digital proveniensinformation. Denna information anges via attributet `recordProvenance` som har ett `RecordProvenance`-objekt som värde.

Proviniensinformation ska ej anges på objekt med [icke-persistenta id:n](./identitet.md#nonpersistent), och ej heller på [referenser](../Terminologi.md#referens).

JSON-LD `@context` för proveniensdatat är `https://kulturarvsdata.se/resurser/linkedart/v1/raa.json` (se [Serialisering](./serialisering)).

De två centrala fälten hos proveniensobjektet som partners *måste* ange är: 
- _Licens_. Fältet `license` anger licensen för postens metadata. Värdet är alltid `http://creativecommons.org/publicdomain/zero/1.0/`. För mer information, se [Rättighetsmärkning](./RightsStatement.md).
- _Länk till källan_. Fältet `sourceRecord` innehåller obligatorisk information om källobjektet, inklusive den obligatoriska länken till källan (`url`). De två fälten `dateCreated` och `dateModified` beskriver när _källobjektet_ skapades respektive senast ändrades; de beskriver alltså inte postens metadata. Dessa två fält är ej obligatoriska, men är starkt rekommenderade att inkludera där möjligt.

👉 Komplett informationsmodell för RecordProvenance: [RecordProvenance](../InformationModelDiagram.md#class-record-provenance)

👉 komplett informationsmodell för SourceRecord: [SourceRecord](../InformationModelDiagram.md#class-source-record)

#### <a id="prov_id"></a> Proveniensobjektets id 

`RecordProvenance`-objektet har en förutsägbar lexikal identitet. Identiteten måste vara det beskrivna objektets `id` med det tillagda path-segmentet `/prov`. 

Om det beskrivna objektet's `id` är `https://kulturarvsdata.se/exem/pel` blir proveniensobjektets `id` således `https://kulturarvsdata.se/exem/pel/prov`.

#### <a id="autogen"></a> Autogenererade fält

Följande attribut, som förekommer i [schemat](../../Terminologi.md#schema) för `RecordProvenance`-objektet, ska uteslutas från objektet vid leverans. RAÄ lägger till dem under skördningsprocessen.

- `RecordProvenance.ingested_at`
- `RecordProvenance.provider`

#### Exempel
Se [exempel/RecordProvenance.md](exempel/RecordProvenance.md).






## Rättighetsmärkning

### Metadata

All metadata ska licensieras enligt [CC0 1.0 Universal](http://creativecommons.org/publicdomain/zero/1.0/).

Iom att sådana rättighetsmärkningar handlar om postens innehåll snarare än den kulturarvsresursen den beskriver, ligger den i proveniensstycket, som beskriver just posten mha schema.org:

```
✂️…️
"recordProvenance": {
   	"id": "https://kulturarvsdata.se/exem/pel/lic/prov",
   	"type": "https://schema.org/DigitalDocument",
   	✂️…️
   	"https://schema.org/license": {
   		"id": "http://creativecommons.org/publicdomain/zero/1.0/",
   		"type": "Type",
   		"_label": "Public Domain"
   	}
}
✂️…️
```

### Media

All media ska ha en licensmärkning. K-samsök använder  [Creative Commons](https://creativecommons.org/) och [Rights Statements](https://rightsstatements.org/) som godkända licenser enligt [K-samsöks rättighetsmodell](#rättighetsmodell).

Detta förekommer inte på bäraren – den fysiska boken/bilden eller den digitala filen – utan på den abstrakta nivån för själva informationsobjektet, dvs `LinguisticObject` för text, `VisualItem` (motivet) för bilder, osv. Om man t.ex. har en digital bild med licensen CC BY, den beskrivs som bärare för ett motiv, som har rättigheter av typen CC BY:

```
{
	✂️…️
	"id": "https://kulturarvsdata.se/exem/pel/motlic",
	"type": "DigitalObject",
	"_label": "Digitalt foto",
	"classified_as": [
		{
			"id": "http://vocab.getty.edu/aat/300215302",
			"type": "Type",
			"_label": "Digital Image"
		}
	],
	"format": "image/jpeg",
	"digitally_shows": [
		{
			"id": "https://kulturarvsdata.se/exem/pel/motlic/vi001",
			"type": "VisualItem",
			"_label": "Fotomotivet",
			"subject_to": [
				{
					"type": "Right",
					"identified_by": [
						{
							"type": "Name",
							"content": "CC BY"
						}
					],
					"classified_as": [
						{
							"id": "http://creativecommons.org/licenses/by/4.0/",
							"type": "Type",
							"_label": "CC BY 4.0"
						}
					]
				}
			],
			✂️…️
		}
	],
	✂️…️
}
```






## Serialiseringsformat

Huvudserialiseringsformatet för poster in och ut hos K-samsök är **[JSON-LD](https://json-ld.org/)**. Ett [OpenAPI schema](../../api/index.md#openapi-schema) definierar dokumentstrukturen för kompatibilitet med generiska JSON-ramverk.

Vid konsumtion från Ksamsök kan i framtiden även andra anpassade svarsformat förekomma hos utdata, beroende på vilket API man anropar och vilka `Accept` headers som anges vid API-anrop eller URI-upplösning.

### JSON-LD context

Rot-JSON-LD objekten ska innehålla både [Linked Arts `@context`](https://linked.art/ns/v1/linked-art.json) och [K-samsöks `@context`](https://kulturarvsdata.se/resurser/linkedart/v1/raa.json). Det betyder att det första fältet i varje rotobjekt alltid ser ut så här: 

```
{
    "@context": [
      "https://linked.art/ns/v1/linked-art.json",
      "https://kulturarvsdata.se/resurser/linkedart/v1/raa.json"
    ]
    ✂️ …
}
```

Nestade objekt (icke-rotobjekt) behöver inte innehålla `@context`-fältet under förutsättningen att objektet inte introducerar termdefinitioner bortom de som ingår i de två ovanstående kontexterna.

Obs att medan JSON-LD tillåter att `@context` kan förekomma som en http-header ("out of band"), kräver K-samsök för både in- och utdata att `@context` explicit anges i dokumentinnehållet.


### `Content-Type` och `profile` vid konsumtion

När Ksamsöks LinkedArt API anropas sätts `Content-Type` [i linje med Linked Art](https://linked.art/api/1.0/json-ld/#media-type) till strängen `application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"`.

### `Content-Type` och `profile` vid skördning

Eftersom Ksamsök introducerar vissa grammatiska specialiseringar vid skördning används en annan `profile` för skördnings-requests. Läs mer om detta i [skördningsspecifikationen](../../api/index.md#specifikation). 






## Beskrivning av datamängder

K-samsök levererar metadata till bl a det gemensamma europeiska dataområdet för kulturarv (Europeana), [Sveriges dataportal](https://www.dataportal.se/) och [European data](https://data.europa.eu/). För att datamängderna som levereras ska vara hittbara för användare krävs information om deras innehåll och proviniens. Beskrivningen är baserad på DCAT-AP SE (och Europeana datasheets ?).

### Kom igång

@@@ TODO Beskrivning av hur man fyller i informationen i adminportalen

### Obligatoriska attribut
@@@ Preliminär lista, behöver dubbelkollas och anpasses till LA-termer

- Title
- Publisher
- Description
- Harvest date
- Language(s)
- Email address
- Rights - alltid CC0

@@@ Identifierare frivillig i DCAT-AP SE, MG starkt mot uri för datamängd

### Rekommenderade attribut
@@@ Preliminär lista, behöver dubbelkollas och anpassas till LA-termer

- Access - var kommer jag åt datamängden 
- Keywords - från vokabulär (?)
- Phone numbre
- Address
- Website








# Appendix 1 - K-samsöks rättighetsmodell

### De licenser/rättighetsmärkningar som finns i K-samsöks rättighetsmodell är:

#### Public Domain Mark

Public Domain Mark (PDM) är en icke juridiskt bindande märkning av material där upphovsrätten har gått ut eller där materialet inte skyddas av upphovsrätten. Märkningen är framtagen av Creative Commons.

URI: [http://creativecommons.org/publicdomain/mark/1.0/](http://creativecommons.org/publicdomain/mark/1.0/)


#### Creative Commons Zero (CC0)

Används om informationsförvaltaren vill avsäga sig alla rättigheter till objektet så att det får återanvändas utan restriktioner.

URI: [http://creativecommons.org/publicdomain/zero/1.0/](http://creativecommons.org/publicdomain/zero/1.0/) 

#### Creative Commons

En informationsförvaltare kan märka upp informationen med de sex Creative Commons licenserna där ”Creative Commons Attribution 4.0 International (CC BY 4.0)” är satt som standard. Läs mer om Creative Commons på http://www.creativecommons.se. 

Licenserna är:

__Creative Commons Attribution 4.0 International (CC BY 4.0)__

Upphovsperson ska anges vid användning.

URI: [http://creativecommons.org/licenses/by/4.0/](http://creativecommons.org/licenses/by/4.0/) 

__Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)__

Upphovsperson ska anges vid användning, bearbetningar delas med samma villkor.

URI: [http://creativecommons.org/licenses/by-sa/4.0/](http://creativecommons.org/licenses/by-sa/4.0/)

__Creative Commons Attribution-NoDerivatives 4.0 International (CC BY-ND 4.0)__

Upphovsperson ska anges vid användning, objektet får inte bearbetas.

URI: [http://creativecommons.org/licenses/by-nd/4.0/](http://creativecommons.org/licenses/by-nd/4.0/)

__Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)__

Upphovsperson ska anges vid användning, ej kommersiell användning.

URI: [http://creativecommons.org/licenses/by-nc/4.0/](http://creativecommons.org/licenses/by-nc/4.0/)

__Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)__

Upphovsperson ska anges vid användning, ej kommersiell användning, bearbetningar delas med samma villkor.

URI: [http://creativecommons.org/licenses/by-nc-sa/4.0/](http://creativecommons.org/licenses/by-nc-sa/4.0/)

__Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)__

Upphovsperson ska anges vid användning, ej kommersiell användning, objektet får inte bearbetas.

URI: [http://creativecommons.org/licenses/by-nc-nd/4.0/](http://creativecommons.org/licenses/by-nc-nd/4.0/)

Vill du använda en äldre version än standard 4.0 så går det bra skriva URL till denna mellan mediaLicenseUrl– och/eller itemLicenseURL, t ex: <mediaLicenseUrl rdf:resource="http://creativecommons.org/licenses/by/3.0"/>

#### Förbehållna rättigheter
Det finns även en möjlighet att leverera metadata om objekt som är helt skyddade av upphovsrätten, med hjälp av RightsStatements.org-licenser. Dessa märks på följande sätt:

__In Copyright (InC)__

Objektet är upprovsrättsskyddat.

URI: [http://rightsstatements.org/vocab/InC/1.0/](http://rightsstatements.org/vocab/InC/1.0/)

__In Copyright – EU Orphan Work (InC-EU-OW)__

Herrelöst verk: objektet är upprovsrättsskyddat, men upphovspersonen är okänd. Obs att för att tillämpa den här licensen ska objektet ha registrerats hos EUIPOs Orphan Works Database genom Patent- och registreringsverket; besök PRVs hemsida för mer information.

URI: [http://rightsstatements.org/vocab/InC-OW-EU/1.0/](http://rightsstatements.org/vocab/InC-OW-EU/1.0/)

__In Copyright – Educational Use Permitted (InC-EDU)__

Objektet är upprovsrättsskyddat, men licensen tillåter bruk inom utbildningssammanhang.

URI: [http://rightsstatements.org/vocab/InC-EDU/1.0/](http://rightsstatements.org/vocab/InC-EDU/1.0/)

'''

