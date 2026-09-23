# 7. Namn, identifierare och beskrivningar

Kulturarvsresurser har ofta namn eller id-nummer som de refereras till med, verk har titlar och många resurser har beskrivande texter. Det här kapitlet beskriver hur de uttrycks.

- **Namn, titlar och identifierare** anges i attributet `identified_by`. I många fall är det obligatoriskt att ange minst ett namn eller en identifierare (se [Krav på attribut](04-krav-pa-attribut.md)).
- **Beskrivande texter** anges som egna textobjekt (se [Beskrivningar](#beskrivningar)).

## Namn

Kulturarvsresurser – och andra företeelser – kan identifieras med namn eller titlar. Ett namn har `"type": "Name"` och en lämplig klassificering i `classified_as`. Det primära namnet, eller titeln på ett verk, klassificeras nästan alltid med `aat:300404670`.

Ett namn **ska** ha attributet `language`, som anger namnets språk.

### Vanliga klassificeringar av namn

| Term | Används för |
|---|---|
| [`aat:300404670`](http://vocab.getty.edu/aat/300404670) | Primärt namn eller titel |
| [`aat:300404669`](http://vocab.getty.edu/aat/300404669) | Visningsnamn |
| [`aat:300451544`](http://vocab.getty.edu/aat/300451544) | Sorteringsnamn |
| [`aat:300264273`](http://vocab.getty.edu/aat/300264273) | Alternativt namn |
| [`aat:300404651`](http://vocab.getty.edu/aat/300404651) | Förnamn på en person |
| [`aat:300404654`](http://vocab.getty.edu/aat/300404654) | Mellannamn på en person |
| [`aat:300404652`](http://vocab.getty.edu/aat/300404652) | Efternamn på en person |
| [`aat:300435719`](http://vocab.getty.edu/aat/300435719) | Tidigare namn |
| [`aat:300417194`](http://vocab.getty.edu/aat/300417194) | Översatt titel |
| [`aat:300312006`](http://vocab.getty.edu/aat/300312006) | Underrubrik |
| [`aat:300404664`](http://vocab.getty.edu/aat/300404664) | Alias |
| [`aat:300404657`](http://vocab.getty.edu/aat/300404657) | Pseudonym |

> [!TIP]
> Vid skördning kan det primära namnet anges med kortformen `_primaryName`. Se [Kortformer](10-kortformer.md).

## Identifierare

Identifierare fungerar på samma sätt som namn, men är i första hand icke-språkliga, till exempel ett accessionsnummer eller ett lämningsnummer. En identifierare har `"type": "Identifier"` och en lämplig klassificering i `classified_as`.

### Vanliga klassificeringar av identifierare

| Term | Används för |
|---|---|
| [`aat:300312355`](http://vocab.getty.edu/aat/300312355) | Accessionsnummer |
| [`aat:300435704`](http://vocab.getty.edu/aat/300435704) | Systemnummer – ett automatiskt genererat nummer, till exempel från ett samlingsförvaltningssystem |
| [`aat:300404621`](http://vocab.getty.edu/aat/300404621) | Lokalt nummer – ett nummer som institutionen har tilldelat och som varken är accessionsnummer eller systemnummer |
| [`aat:300311706`](http://vocab.getty.edu/aat/300311706) | Hyllsignum (*call number*) – anger var ett objekt är fysiskt placerat i samlingen |

## Beskrivningar

### `_label`

`_label` (`rdfs:label`) är i vissa fall obligatoriskt och annars starkt rekommenderat på många noder. Syftet är att ge den som arbetar med datan en ledtråd om vad noden handlar om, ofta när något annat namnliknande attribut saknas.

> [!IMPORTANT]
> Värdet i `_label` ska **inte** visas för slutanvändare i en applikation, på en webbsida eller liknande. Det är enbart avsett som vägledning för dem som granskar datan, inte som innehåll att presentera. Använd `identified_by` för namn som ska visas.

### Beskrivande text

> [!NOTE]
> **Utkast.** Avsnittet om beskrivande fritext ska skrivas.

> [!WARNING]
> **Öppen fråga.** Exemplet nedan anger den beskrivande texten med `subject_of`. I Linked Art anges inbäddade beskrivande texter normalt med `referred_to_by`, medan `subject_of` används för externa dokument som *handlar om* objektet. Även kortformen `_description` (se [Kortformer](10-kortformer.md)) expanderas till `referred_to_by`. Vilket mönster som gäller i K-samsök behöver fastställas.

## Exempel

Föremålet i exemplet har både ett namn och en identifierare i `identified_by`, och en kort beskrivande text i `subject_of`:

```json
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
			"content": "Fetischfigur av Arumbayafolket från Sydamerika. Ena örat är sönderslaget.",
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

> [!NOTE]
> Exemplet anger bara Linked Arts `@context`. En levererad post ska även ha K-samsöks kontext, se [Serialisering](02-serialisering.md#json-ld-kontext-context).
