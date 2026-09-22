# Informationsmodell för K-samsök 2.0

Detta dokument beskriver informationsmodellen för K-samsök och de principer som styr hur information struktureras, identifieras, klassificeras och utbyts inom tjänsten. Dokumentet riktar sig främst till utvecklare och informationsförvaltare inom kulturarvsområdet. 

Dokumentationen sammanfattar de krav, mönster och rekommendationer som gäller för datamodellen, inklusive identitet, proveniens, rättighetsmärkning, klassificering och användning av vokabulärer.

Syftet är att ge en sammanhållen beskrivning av hur information uttrycks i K-samsök samt vilka minimikrav som gäller för interoperabilitet och vidareleverans.

## 1. Introduktion

## 2. Grundläggande principer

#### K-samsök bygger på Linked Art

Linked Art är en tillämpningsprofil (application profile) av den sektorsövergripande ontologin CIDOC CRM. K-samsök har valt att tillämpa Linked Art som grundmodell för att underlätta internationell interoperabilitet. 

#### Objekt identifieras med URI:er

Varje persistent objekt i K-samsök (se [Identitet](#intro)) har en beständig URI som unik identifierare. Objektet ska alltid vara nåbart via internet. 

#### Objekt kan bestå av endast metadata

Ett objekt behöver inte vara bärare av en mediafil utan kan bestå av endast metadata. Ett objekt kan vara en abstrakt företeelse. 

#### K-samsök är en kunskapsgraf

K-samsök samlar objekt och relationer mellan dem i en kunskapsgraf. Relationer kan peka på objekt både inom och utanför grafen. 

#### Persistenta objekt kan återanvändas över organisationsgränser

Inom K-samsök ska data inte betraktas som lokal, utan satt i relation med annan data. Det innebär att hänvisningar till andra objekt även utanför den egna organisationen är möjlig och uppmuntrad. 

#### Lokala termer ska ersättas med gemensamma vokabulärer i största möjliga mån

Den viktigaste faktorn för att utveckla data inom K-samsök är att använda gemensamma termer. Det stärker kontext, gör datan rikare och ökar precisionen. 

## 3. Serialiseringsformat

Detta kapitel beskriver hur information uttrycks tekniskt vid utbyte med K-samsök. För att förstå övriga kapitel behöver man känna till att JSON-LD är det primära formatet och att informationsmodellen bygger på Linked Art.

Huvudserialiseringsformatet för poster in och ut hos K-samsök är **[JSON-LD](https://json-ld.org/)**. Ett [OpenAPI schema](../../api/index.md#openapi-schema) definierar dokumentstrukturen för kompatibilitet med generiska JSON-ramverk.

Vid konsumtion av data från K-samsök kan i framtiden även andra anpassade svarsformat förekomma hos utdata, beroende på vilket API man anropar. __Nuvarande dokumentation beskriver endast leverans, ej konsumtion av data.__ 

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

När K-samsöks Linked Art-API anropas sätts `Content-Type` [i linje med Linked Art](https://linked.art/api/1.0/json-ld/#media-type) till strängen `application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"`.

### `Content-Type` och `profile` vid skördning

Eftersom K-samsök introducerar vissa grammatiska specialiseringar vid skördning används en annan `profile` för skördnings-requests. Läs mer om detta i [skördningsspecifikationen](../../api/index.md#specifikation). 

## <a id="kortformer"></a>4. Kortformer

För att göra det lättare för datapartners stödjer vi användandet av _kortformer_ (shortforms): ett förenklat uttryck som expanderas till den fullständiga kanoniska Linked Art-formen när en post skördas. 

Kortformsattribut har prefixet `_` för att markera dem som RAÄ:s transporthjälpmedel, inte kanoniska Linked Art-attribut (undantaget `_label`, som är ett kanoniskt Linked Art-attribut trots prefixet).

Partners kan använda de här attributen i inskickade poster, men poster som publiceras av RAÄ kommer alltid att använda den expanderade kanoniska formen. Notera också att om du skapar en endpoint som kommer eller kan användas av andra konsumenter än RAÄ:s K-samsök 2-skördare bör du inte använda kortformer, eftersom andra inte kommer att kunna expandera dem. 

Kortformer bör inte användas tillsammans med sin expanderade motsvarighet i samma objekt (nod). Om det expanderade värdet redan är tillgängligt kommer kortformsvärdet att ignoreras för det objektet. Om en kortform inte kan tolkas på ett otvetydigt sätt kommer posten fortfarande att accepteras, men kortformen kommer inte att expanderas och utelämnas ur den expanderade formen. 

Kortformer i strängar som stödjer angivande av språk använder suffixformen `text @code`. Tolkningen av `@` som en språktagg sker bara om det föregås av ett mellanslag och avslutar strängen. Till exempel betyder `"Ben Hur @en"` att texten `Ben Hur` är på engelska; `"Ben Hur@en"` betraktas som enbart text. 

Okända språkkoder ignoreras.


## 5. Identitet

Exempel på de identitetsuttryck som beskrivs nedan finns i [Exempelbanken](../exempel/id.md).


### <a id="intro"></a>Introduktion

I K-samsök skiljer vi när det gäller objekts natur och livscykel mellan två huvudsakliga objektstyper: 

- **Persistent objekt**: ett objekt vars id är en upplösningsbar URI. Utfärdaren av den givna URI:n ansvarar för att URI:n är stabil, permanent och beständig över tid, samt att en upplösning av URI:n ger ett meningsfullt svar.

__Exempel:__ fysiska eller digitala objekt/föremål, händelser och aktiviteter, motiv och texter, platser, samlingar, abstrakta företeelser, personer och grupper, begrepp

- **Icke-persistent** (eller 'anonymt') **objekt**: ett objekt som saknar id, eller inte har en URI som id. Inga krav eller förväntningar finns på sådana objekt gällande beständighet.

__Exempel:__ en företeelse som endast har relevans för ETT objekt och som ingen annan behöver hänvisa till. Det kan vara tidpunkten för när ett objekt skapades. 

#### Undertyper till persistenta objekt

De persistenta objekten i sin tur indelas inom K-samsök i två undertyper:

- **Kulturarvsdata-objekt**: Objekt med persistenta URI:er vars domän är `kulturarvsdata.se`. Se [Identitet för Kulturarvsdata-objekt](#kad) nedan. 
- **Andra persistenta objekt**: Objekt med persistenta URI:er som ligger utanför kulturarvsdata-domänen. Se [Identitet för andra persistenta objekt](#ext) nedan. 

### <a id="kad"></a>Identitet för Kulturarvsdata-objekt

Varje kulturarvsresurs som tillhandahålls av en datapartner för skördning till K-samsök tilldelas en persistent kulturarvsdata-URI. 

Kulturarvsdata-URI:er för skördade resurser har följande struktur:
- URI:ns `scheme` är alltid `https`
- URI:ns `domain` är alltid `kulturarvsdata.se`
- URI:n innehåller tre path-segment: 
   1) datapartnerns id i gemener
   2) datasetets id i gemener
   3) resursens id

Givet en datapartner med id `exem` och ett dataset med id `pel` och en resurs med id `abc` blir kulturarvsdata-URI:n således `https://kulturarvsdata.se/exem/pel/abc`

Datapartnern skapar kulturarvsdata-URI:erna enligt ovanstående mönster när ett dataset förbereds för skördning. URI:erna finns alltså med i datasetet när det skördas. Datapartnern använder konsekvent det datapartner-id och dataset-id som tilldelats av RAÄ (dessa finns att tillgå i K-samsök 2:s administrativa gränssnitt). 

Notera: vi rekommenderar starkt att använda endast så kallade "URI-safe" bokstäver (`^[a-zA-Z0-9_-]*$`) i resursens id-segment, det vill säga att id:t är begränsat till a–z, A–Z, siffror, understreck och bindestreck.   

### <a id="ext"></a>Identitet för andra persistenta objekt

K-samsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta. Vid sidan av de kulturarvsdata-URI:er som tilldelas de skördade resurserna förekommer naturligt även referenser till andra persistenta URI:er som ligger utanför kulturarvsdatadomänen. I de flesta fall är dessa URI:er referenser till andra LOD (Linked Open Data) resurser som tillgängliggörs av andra aktörer, till exempel Kungliga Biblioteket, Getty och Wikidata. 

### <a id="nonpersistent"></a>Identitet för icke-persistenta objekt

Eftersom K-samsök 2 tolkar alla objekt vars id:n är `http`- eller `https`-URI:er som persistenta, indikeras ett objekt som icke-persistent genom att helt utelämna id-fältet på objektet, eller genom att ange en godtycklig sträng som inte börjar med `http`- eller `https` som dess värde. Rekommendationen är att utelämna `id` helt. Om ett id ändå behövs (t.ex. för att kunna referera till samma nod flera gånger inom en post) bör det anges som en blank node-identifierare med prefixet `_:`, eftersom en godtycklig sträng annars riskerar att tolkas som en relativ URI av JSON-LD-processorer.


### <a id="ref"></a>Referenser till andra objekt

En *referens* är den av Linked Art [definierade](https://linked.art/api/1.0/shared/reference/), och av RAÄ föreskrivna, metoden för att referera ("länka") till andra objekt utan att behöva ange det refererade objektets innehåll i sin helhet. Ett objekt tolkas som en referens om det endast innehåller attributen `id` och `type`, samt valfritt även `_label`, `equivalent` och `notation`.

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

## 6. Minimum Viable Object - obligatoriska attribut för leverans

K-samsök har ett antal obligatoriska attribut för objekt för enhetlig hantering av data och för att möjliggöra aggregering till Europeana/det gemensamma europeiska dataområdet för kulturarv och andra dataportaler. 

### Obligatoriska attribut för objekt

@@@TODO Obs, listan fortfarande preliminär. Behöver även kollas termmässigt mot LA. På engelska eller svenska? 

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
- language

### Rekommenderade attribut för objekt

- Creator
- Owner - objektets ägare
- Keywords
- Inventory number
- Alternative title
- isPartOf
- isNextInSequence

@@@ TODO MS

### Utifrån detta, MVO på Linked Art:ska för Europeanaleverans

- `id` (URI)
- `identified_by`
- `type`
- `classified_as` *(obs rekommenderad men ej tvingande hos LA/K2 i dagsläget; dock tvingande för Europeana)*
- proveniensmetadata: länk till källan, CC0 osv
- Publisher/Dataprovider – fylls i automatiskt vid skördning
- Description *(obs rekommenderad men ej tvingande hos LA/K2 i dagsläget)*
- Updated *(hos källan – ur proveniensmetadata)*
- Harvested date *(autogenereras vid skördning – ur proveniensmetadata)*
- subject_to *(för visual/linguistic items)*
- isShownAt *(länk till källan – ur proveniensmetadata)*
- isShownBy *(visualised_by för visual/linguistic items)*
- edm:provider (K-samsök) (autogenereras i EDM-mappningen)
- language (för texter)

#### Rekommenderade

- Creator **(hos LA en creation event där en person har varit delaktig)**
- Owner **(hos LA en current owner eller transfer of custody)**
- Keywords **(helst länkar)**
- Inventory number **(identified_by number med classified as)**
- Alternative title **(identified_by name med classified as)**
- isPartOf 
- isNextInSequence *(???)*

## 7. Proveniens

### Introduktion

Detta kapitel beskriver hur information om datats ursprung, ägarskap, licensiering och källsystem uttrycks i K-samsök. Proveniensinformationen gör det möjligt att spåra var metadata kommer från, när den skapades eller uppdaterades samt under vilka villkor den får återanvändas.

#### RecordProvenance: Exempel

Följande exempel visar den minimala formen av den digitala proveniensen (`RecordProvenance`) för ett persistent objekt. Samtliga fält i exemplet är obligatoriska.

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

Följande exempel visar en rikare form av digital proveniens. De två rekommenderade (icke-obligatoriska) fälten `dateCreated` och `dateModified` är angivna. Två icke-obligatoriska fält som RAÄ autogenererar vid skördning — `about` och `provider` —  är också angivna, och korrekt uttryckta som [referenser](#ref).

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

@@@ TODO länk till källan, både i /prov och som digital objekt.

## 8. Rättighetsmärkning

### Introduktion

All information som levereras till K-samsök ska vara försedd med tydlig information om rättigheter och användningsvillkor. Kapitlet beskriver hur licenser uttrycks för både metadata och informationsobjekt samt vilka rättighetsmärkningar som stöds inom K-samsöks rättighetsmodell. 

### Metadata

All metadata ska licensieras enligt [CC0 1.0 Universal](http://creativecommons.org/publicdomain/zero/1.0/).

I och med att sådana rättighetsmärkningar handlar om postens innehåll snarare än den kulturarvsresurs den beskriver, ligger den i proveniensstycket, som beskriver just posten med hjälp av schema.org:

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

All media ska ha en licensmärkning. K-samsök använder [Creative Commons](https://creativecommons.org/) och [Rights Statements](https://rightsstatements.org/) som godkända licenser enligt [K-samsöks rättighetsmodell](#rättighetsmodell).

Detta förekommer inte på bäraren – den fysiska boken/bilden eller den digitala filen – utan på den abstrakta nivån för själva informationsobjektet, dvs `LinguisticObject` för text, `VisualItem` (motivet) för bilder, osv. Om man t.ex. har en digital bild med licensen CC BY beskrivs den som bärare för ett motiv, som i sin tur är föremål för (`subject_to`) en rättighet av typen CC BY:

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

### <a id="rättighetsmodell"></a>K-samsöks rättighetsmodell

#### De licenser/rättighetsmärkningar som finns i K-samsöks rättighetsmodell är:

##### Public Domain Mark

Public Domain Mark (PDM) är en icke juridiskt bindande märkning av material där upphovsrätten har gått ut eller där materialet inte skyddas av upphovsrätten. Märkningen är framtagen av Creative Commons.

URI: [http://creativecommons.org/publicdomain/mark/1.0/](http://creativecommons.org/publicdomain/mark/1.0/)


##### Creative Commons Zero (CC0)

Används om informationsförvaltaren vill avsäga sig alla rättigheter till objektet så att det får återanvändas utan restriktioner.

URI: [http://creativecommons.org/publicdomain/zero/1.0/](http://creativecommons.org/publicdomain/zero/1.0/) 

##### Creative Commons

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

Vill du använda en äldre version än 4.0 går det bra att ange URI:n till den versionen på samma sätt, t.ex. `http://creativecommons.org/licenses/by/3.0/`.

##### Förbehållna rättigheter
Det finns även en möjlighet att leverera metadata om objekt som är helt skyddade av upphovsrätten, med hjälp av RightsStatements.org-licenser. Dessa märks på följande sätt:

__In Copyright (InC)__

Objektet är upphovsrättsskyddat.

URI: [http://rightsstatements.org/vocab/InC/1.0/](http://rightsstatements.org/vocab/InC/1.0/)

__In Copyright – EU Orphan Work (InC-OW-EU)__

Herrelöst verk: objektet är upphovsrättsskyddat, men upphovspersonen är okänd. Obs att för att tillämpa den här licensen ska objektet ha registrerats hos EUIPOs Orphan Works Database genom Patent- och registreringsverket; besök PRVs hemsida för mer information.

URI: [http://rightsstatements.org/vocab/InC-OW-EU/1.0/](http://rightsstatements.org/vocab/InC-OW-EU/1.0/)

__In Copyright – Educational Use Permitted (InC-EDU)__

Objektet är upphovsrättsskyddat, men licensen tillåter bruk inom utbildningssammanhang.

URI: [http://rightsstatements.org/vocab/InC-EDU/1.0/](http://rightsstatements.org/vocab/InC-EDU/1.0/)


## 9. Vanligt förekommande mönster i mappningen

Några vanligt förekommande mönster är att kulturarvsresurser har namn eller id-nummer de refereras till med, att verk har titlar, och beskrivande texter. Namn, titlar och identifierare förekommer som värden på attributet `identified_by`; beskrivande texter uttrycks som egna textobjekt (se [Beskrivningar](#beskrivningar) nedan). Det är i många fall ett krav att något värde för `identified_by` ska förekomma – antingen ett namn eller en identifierare.

### <a id="namn"></a>Namn

Kulturarvsresurser – och andra företeelser! – kan identifieras av namn eller titlar. De har `"type": "Name"`, och något passande `classified_as`, oftast `aat:300404670` för det primära namnet eller titeln på ett verk. Övriga vanliga klassifikationer är:

- `aat:300404670` – primära namn
- `aat:300404669` – visningsnamn
- `aat:300451544` – sorteringsnamn
- `aat:300264273` – alternativa namn
- `aat:300404651` – förnamn på en person
- `aat:300404654` – mellannamn på en person
- `aat:300404652` – efternamn på en person
- `aat:300435719` – f.d. namn
- `aat:300417194` – översatt titel
- `aat:300312006` – underrubrik
- `aat:300404664` – alias
- `aat:300404657` – pseudonym

Namn ska ha ett tillhörande `language`-attribut som anger språket.

Se även [kortformer](#kortformer), där primära namn / preferred terms även kan uttryckas.

### Identifierare

Identifierare funkar på samma sätt som namn, fast primärt icke-lexikala sådana, som t.ex. ett accessionsnummer eller lämningsnummer. De har `"type": "Identifier"`, och något passande `classified_as`. Vanliga klassifikationer är:

- `aat:300312355` – accessionsnummer
- `aat:300435704` – systemnummer; ett autogenererat nummer från t.ex. ett samlingsförvaltningssystem
- `aat:300404621` – lokalt nummer; ett nummer tilldelat av institutionen som är varken accessionsnummer eller systemnummer
- `aat:300311706` – hyllsignum (call number); en identifierare för var ett objekt är fysiskt placerat i samlingen

### <a id="beskrivningar"></a>Beskrivningar

#### `_label`

`_label` (`rdfs:label`) är i flera fall ett krav och annars ett starkt rekommenderat attribut på många noder. Syftet med `_label` är att ge en utvecklare som jobbar med datat ett tecken på vad den aktuella noden handlar om, ofta i fall där något annat namnliknande attribut saknas. Värdet på `_label` ska dock *inte* visas eller synas för slutanvändare på en applikation, webbsida, eller dylikt – den är enbart till för de som granskar datat, som vägledning, inte som innehåll att presenteras.

#### Fritext beskrivning



### Exempel

I följande exempel beskrivs ett föremål som har både ett namn och en identifierare – bägge två som värde för attributet `identified_by` – och en kort beskrivande text på `subject_of`:

```
{
	"@context": "https://linked.art/ns/v1/linked-art.json",
	"id": "https://kulturarvsdata.se/exem/pel/figur",
	"type": "HumanMadeObject",
	"_label": "Arumbayafetisch",
	"classified_as": [
		{
			"id": "http://vocab.getty.edu/aat/300047498",
			"type": "Type",
			"_label": "Fetischfigurer"
		}
	],
	"subject_of": [
		{
			"type": "LinguisticObject",
			"_label": "beskrivande anteckning",
			"content": "Fetischfigur av Arumbayafolket från Sydamerika. Ena örat är sönderslaget."
			"classified_as": [
				{
					"id": "http://vocab.getty.edu/aat/300435416",
					"type": "Type",
					"_label": "descriptive note"
				}
			],
			"language": [
				{
					"id": "http://vocab.getty.edu/aat/300389336",
					"type": "Language",
					"_label": "Svenska"
				}
			]
		}
	],
	"identified_by": [
		{
			"type": "Name",
			"_label": "Namn",
			"content": "Arumbayafetisch",
			"classified_as": [
				{
					"id": "http://vocab.getty.edu/aat/300404670",
					"type": "Type",
					"_label": "preferred terms"
				}
			],
			"language": [
				{
					"id": "http://vocab.getty.edu/aat/300389336",
					"type": "Language",
					"_label": "Svenska"
				}
			]	
		},
		{
			"type": "Identifier",
			"content": "978-0-416-83450-5",
			"_label": "Museets accessionsnummer",
			"classified_as": [
				{
					"id": "http://vocab.getty.edu/aat/300312355",
					"type": "Type",
					"_label": "Accessionsnummer"
				}
			]
		}
	]
}
```

## 10. Klassificering

Att klassificera objekt med hjälp av hänvisningar till URI:er är ett huvudsyfte med all mappning av data för export till K-samsök. Det görs för att underlätta interoperabilitet, ökad tydlighet samt identifiera relationer mellan olika objekt. 

Fördelarna med att arbeta med klassificering via URI:er är flera inom både forskning, intern användning av samlingarna samt underlättar för den som är intresserad av samlingarna. 

I [Nationell strategi för digitalt kulturarv](https://urn.kb.se/resolve?urn=urn:nbn:se:raa:diva-8498) beskrivs detta inom utvecklingsområdet Användbarhet. 

### Mappnings- och leveranskrav

Varje klassificeringsreferens ska minst innehålla:

- `id`, med begreppets fullständiga URI
- `type`, normalt med värdet `Type`

`_label` bör anges för att göra informationen läsbar för utvecklare, men är inte en ersättning för URI:n.

En term från en kontrollerad vokabulär ska anges i `classified_as`, inte i `type`. Omvänt ska informationsmodellens klasser inte användas som värden i `classified_as`.

#### Skillnaden mellan 'type' och 'classified_as'

`type` och `classified_as` fyller olika funktioner. `type` anger objektets grundläggande klass i informationsmodellen, till exempel `HumanMadeObject`, `Person` eller `VisualItem`. `classified_as` används för att precisera vad objektet är med hjälp av ett eller flera begrepp från kontrollerade vokabulärer.

#### Klassificera objekt med hjälp av kontrollerade vokabulär

Att ange `classified_as` som pekar till ett begrepp eller en term mha dess URI är i normalfallet inte ett krav hos K-samsök. Men det är starkt, *starkt* rekommenderat! Datamängder som saknar klassificeringar begränsar datats värde, och kommer att få väldigt låga kvalitetsbetyg av just denna anledning. Att ange `language` för textfält är dock ett krav.

`classified_as` och `language` med värden som är URI:er ska alltid formuleras som [referenser](#ref).

T.ex. om man vill beskriva ett kamfodral med hjälp av termen hos Getty AAT – [aat:300423476](http://vocab.getty.edu/aat/300423476) "comb cases" (kamfodral):

```
{
✂️…️
"id": "https://kulturarvsdata.se/exem/pel/kfd",
"_label": "Vikingatida kamfodral av ben",
"type": "HumanMadeObject",
"classified_as": [
	{
   		"id": "http://vocab.getty.edu/aat/300423476",
   		"type": "Type",
   		"_label": "kamfodral"
   	}
],
✂️…️
}
```

Vi rekommenderar i första hand att man använder begrepp som finns med i de rekommenderade vokabulärerna hos Network of Terms. Ifall det specifika begreppet man vill använda saknas, ange istället det närmaste *överordnade* begreppet inom en lämplig hierarki, tillsammans med en "in-line" singleton-instans av begreppet.

T.ex. om man skulle vilja ange att ett föremål i landskapet är av typen "gärdsgård", begreppet "gärdsgård" finns inte hos Getty AAT eller Network of Terms övriga vokabulärer. Då skulle man istället ange det närmaste överordnade begreppet hos AAT – [aat:300005044](http://vocab.getty.edu/aat/300005044) "fences" (staket) – tillsammans med ett engångsbegrepp för "gärdsgård":


```
{
✂️…️
"id": "https://kulturarvsdata.se/exem/pel/ggd",
"_label": "Gärdsgård längs östra sidan åkern",
"type": "HumanMadeObject",
"classified_as": [
	{
		"id": "http://vocab.getty.edu/aat/300005044",
		"type": "Type",
		"_label": "Staket"
	},
	{
		"type": "Type",
		"_label": "Gärdsgård",
		"identified_by": [
			{
				"type": "Name",
				"content": "Gärdsgård",
				"classified_as": [
					{
						"id": "http://vocab.getty.edu/aat/300404670",
						"type": "Type",
						"_label": "Primära termer"
					}
				],
				"language": [
					{
						"id": "http://vocab.getty.edu/aat/300389336",
						"type": "Language",
						"_label": "Svenska"
					}
				]
			}
		],
		"classified_as": [
			{
				"id": "http://vocab.getty.edu/aat/300435443",
				"type": "Type",
				"_label": "Objekt- eller verkstyp"
			}
		]
	}
],
✂️…️
}
```

Har man även en länk till en vokabulärterm som inte förekommer inom Network of Terms är man välkommen att även leverera den tillsammans med – men aldrig istället för – den matchande eller överordnade termen.

Om man t.ex. publicerar ett eget begrepp för "gärdsgård" skulle man kunna göra som i exemplet ovanför, fast även inkludera URI:n till detta begrepp:

```
{
✂️…️
"id": "https://kulturarvsdata.se/exem/pel/ggd",
"_label": "Gärdsgård längs östra sidan åkern",
"type": "HumanMadeObject",
"classified_as": [
	{
		"id": "http://vocab.getty.edu/aat/300005044",
		"type": "Type",
		"_label": "Staket"
	},
	{
		"id": "https://vocab.exempel.se/ggd123",
		"type": "Type",
		"_label": "Gärdsgård",
		"identified_by": [
			{
				"type": "Name",
				"content": "Gärdsgård",
				"classified_as": [
					{
						"id": "http://vocab.getty.edu/aat/300404670",
						"type": "Type",
						"_label": "Primära termer"
					}
				],
				"language": [
					{
						"id": "http://vocab.getty.edu/aat/300389336",
						"type": "Language",
						"_label": "Svenska"
					}
				]
			}
		],
		"classified_as": [
			{
				"id": "http://vocab.getty.edu/aat/300435443",
				"type": "Type",
				"_label": "Objekt- eller verkstyp"
			}
		]
	}
],
✂️…️
}
```

I vissa fall kommer det inte att finnas någon lämplig term att mappa mot. I sådana fall kan man leverera ett singleton-begrepp, in-line och utan någon koppling till ett begrepp med URI, som tillfällig nödlösning. Detta bör dock anses vara ett undantag snarare än regel.

#### Klassificering av visuellt innehåll

K-samsök och Linked Art skiljer på __avbildningen__ och __själva objektet__ som avbildas. 

Visuellt innehåll är ett objekt av typen `VisualItem`. När motivet föreställer en person eller en bestämd företeelse (exempelvis ett specifikt objekt) används `represents` med en referens till det objektet.

När motivet visar något som kan klassificeras men inte identifieras som en bestämd individ används `represents_instance_of_type`. Egenskapen pekar direkt på den typ av företeelse som bilden visar.

I följande exempel visar motivet ett parasoll, men parasollet har ingen egen identitet och modelleras därför inte som ett separat `HumanMadeObject`.

```json
{
  "id": "https://kulturarvsdata.se/exem/pel/motiv-1",
  "type": "VisualItem",
  "_label": "Bildmotiv med ett parasoll",
  "represents_instance_of_type": [
    {
      "id": "http://vocab.getty.edu/aat/300046218",
      "type": "Type",
      "_label": "Parasoll"
    }
  ]
}
```

Använd:

- `represents` när bilden föreställer en identifierad resurs, till exempel en namngiven person eller en bestämd byggnad
- `represents_instance_of_type` när bilden föreställer en oidentifierad instans av en typ, till exempel ett barn, en cykel eller ett träd
- `about` när ett begrepp är bildens ämne eller innebörd snarare än något som faktiskt avbildas

`represents_instance_of_type` ska uttryckas på ett `VisualItem`, inte direkt på den fysiska eller digitala bärare som visar motivet.

## 11. Rekommenderade vokabulär

### Introduktion

I avsnittet klassificeringar beskrivs de mönster som gäller för att klassificera information. Det ger en viktig grund för att förstå informationsmodellen, men genom att tillämpa klassificeringsmönstren med gemensamma termer / vokabulär möjliggörs en mycket hög grad av interoperabilitet mellan olika datamängder. 

K-samsöks datamodell är uppbyggd kring användning av gemensamma vokabulär. I den bästa av världar ska varje term definieras med hjälp av en URI för termen. Det är ett av de grundläggande kännetecknen för Linked Art och det som gör modellen användbar för aggregering så att kulturarvsdatan i K-samsök blir interoperabel och jämförbar med kulturarvsdata från andra datapartners samt från andra kulturarvsinstitutioner.

Användning av vokabulärer är för tillfället inte ett krav, men att mappa sin data mot vokabulär är den enskilt högst prioriterade insatsen för att höja datakvaliteten i K-samsök. 

### K-samsöks krav på vokabulärer

Hos både K-samsök och Linked Art är det som sagt sällan ett krav att ange `classified_as`, men dess frånvaro sänker datans kvalité rejält. Det finns dock vissa krav på *vilka* typer man ska använda för särskilda vanligt förekommande begrepp. T.ex. att det primära namnet för ett objekt skall alltid vara `classified_as` [aat:300404670](http://vocab.getty.edu/aat/300404670). Dessa krav dokumenteras hos Linked Art på [Required Terms](https://linked.art/model/vocab/required/).

Linked Art definierar även motsvarande [Recommended Terms](https://linked.art/model/vocab/recommended/) och [Optional Terms](https://linked.art/model/vocab/optional/) som på samma vis anger vilka termer man borde använda till `classified_as` för olika informationstyper.

Se även: [Namn](#namn)

### Rekommenderade vokabulärer i K-samsök

En punkt där K-samsök skiljer sig från Linked Art är plattformens krav på vilka vokabulärer som ska användas. Linked Art använder i första hand [Getty AAT](https://vocab.getty.edu/aat/). Hos K-samsök föredrar vi även primärt Getty AAT för att så mycket som möjligt behålla kompatibilitet med övriga Linked Art-tillämpningar; men scope:et för K-samsök sträcker sig mycket bredare än Linked Arts fokus på konst, och många viktiga begrepp för kulturarvet i stort och specifika ämnen såsom arkeologi m.fl. saknas. Därför tillåter K-samsök begrepp från övriga rekommenderade vokabulärer, där Getty AAT inte är lämplig. Dessa rekommenderade vokabulärer och begrepp kureras och sammanställs i tjänsten Network of Terms. Den innehåller för närvarande:

- Rättighetsmärkningar ur [K-samsöks rättighetsmodell](#rättighetsmodell):
	- [PD Mark](http://creativecommons.org/publicdomain/mark/1.0/)
	- [CC0](http://creativecommons.org/publicdomain/zero/1.0/)
	- [CC BY](http://creativecommons.org/licenses/by/4.0/)
	- [CC BY-SA](http://creativecommons.org/licenses/by-sa/4.0/)
	- [CC BY-ND](http://creativecommons.org/licenses/by-nd/4.0/)
	- [CC BY-NC](http://creativecommons.org/licenses/by-nc/4.0/)
	- [CC BY-NC-SA](http://creativecommons.org/licenses/by-nc-sa/4.0/)
	- [CC BY-NC-ND](http://creativecommons.org/licenses/by-nc-nd/4.0/)
	- [In Copyright](http://rightsstatements.org/vocab/InC/1.0/)
	- [In Copyright Orphan Work (EU)](http://rightsstatements.org/vocab/InC-OW-EU/1.0/)
	- [In Copyright Educational Use Permitted](http://rightsstatements.org/vocab/InC-EDU/1.0/)
- [Getty AAT](https://vocab.getty.edu/aat/)
- [PeriodO](https://perio.do/) för periodisering
- [GeoNames](http://www.geonames.org/) för platser och geografiska indelningar
- Runologiska begrepp:
	- [Profilstilar efter Gräslund, Ljung](http://kulturarvsdata.se/resurser/aukt/srdb/profilestyle)
	- [Korsformer efter Lager](http://kulturarvsdata.se/resurser/aukt/srdb/crossform)
	- [Brakteattyper](http://kulturarvsdata.se/resurser/aukt/srdb/bracteatetype)
	- [Runologiska perioder för att informera transliterationsschemat](http://kulturarvsdata.se/resurser/aukt/srdb/period)

#### Föreslagna vokabulärer till K-samsök

@@@ OBS *Marcus utkast på ytterligare vokabulärer som skulle kunna välsignas av staten:*

- RAÄ-vokabulärer för:
	- Lämningstyper (gärna även mappa mot FISH!)
	- Antikvariska bedömningar (gärna även mappa mot FISH!)
	- Uppdragstyper (gärna även mappa mot FISH!)
	- Nummer (RAÄ-nr, lämningsnummer, ärendenr, arkivnr…)
	- Socknar
		- ATA-socken
		- KMR-socken
		- K-samsök-socken
		- …?
	- Mera från Arkivet, BeBR… ???
- DarwinCore (vilka?)
- FISH:
	- [Archaeological Sciences](http://purl.org/heritagedata/schemes/560)
	- [Event Types](http://purl.org/heritagedata/schemes/agl_et)
	- [Evidence](http://purl.org/heritagedata/schemes/eh_evd)
	- ([Resource Description](http://purl.org/heritagedata/schemes/547)?)
	- ([Heritage Subjects and Themes](http://purl.org/heritagedata/schemes/595)?)
	- …?
- [EAGLE](https://www.eagle-network.eu/resources/vocabularies/) (till inskrifter)
- KulturNav (vilka?)
- Mappningar mellan ovanstående och Wikidata?

## 12. Beskrivning av dataset

K-samsök levererar metadata till bl a det gemensamma europeiska dataområdet för kulturarv (Europeana), [Sveriges dataportal](https://www.dataportal.se/) och [European data](https://data.europa.eu/). För att datamängderna som levereras ska vara hittbara för användare krävs information om deras innehåll och proveniens. Beskrivningen är baserad på DCAT-AP SE (och Europeana datasheets ?).

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
