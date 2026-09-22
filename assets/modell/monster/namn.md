# Namn, titlar, identifierare, och beskrivningar

Några vanligt förekommande mönster är att kulturarvsresurser har namn eller id-nummer de refererast till med, att verk har titlar, och beskrivande texter. Dessa förekommer som värden på attributet `identified_by`. Det är i många fall ett krav att något värde för `identified_by` ska förekomma – antingen ett namn eller en identifierare.

## Namn

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

Se även [kortformer](kortformer.md), där primära namn / preferred terms kan även uttryckas på detta vis.

## Identifierare

Identifierare funkar på samma sätt som namn, fast primärt icke-lexikala sådana, som t.ex. ett accessionsnummer eller lämningsnummer. De har `"type": "Identifier"`, och något passande `classified_as`. Vanliga klassifikationer är:

- `aat:300312355` – accesionsnummer
- `aat:300435704` – systemnummer; ett autogenererat nummer från t.ex. ett samlingsförvaltningssystem
- `aat:300404621` – lokalt nummer; ett nummer tilldelat av institutionen som är varken accessionsnummer eller systemnummer
- `aat:300311706` – lokalsigum; en indentifierare för var ett objekt är fysiskt placerad i samlingen

## Beskrivningar

### `_label`

`_label` (`rdfs:label`) är i flera fall ett krav och annars ett starkt rekommenderat attribut på många noder. Syftet med `_label` är att ge en utvecklare som jobbar med datat ett tecken på vad den aktuella noden handlar om, ofta i fall där nägot annat namnliknande attribut saknas. Värdet på `_label` ska dock *inte* visas eller synas för slutanvändare på en applikation, webbsida, eller dylikt – den är enbart till för de som granskar datat, som vägledning, inte som innehåll att prestenteras.

### Fritext beskrivning



## Exempel

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
