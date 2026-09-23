# 8. Klassificering

Att klassificera objekt med hänvisningar till URI:er för begrepp är ett av huvudsyftena med all mappning av data till K-samsök. Klassificering ökar tydligheten, gör data från olika datapartner jämförbar och gör det möjligt att hitta relationer mellan objekt. Det gynnar forskning, organisationens egen användning av samlingarna och alla andra som är intresserade av samlingarna.

I [Nationell strategi för digitalt kulturarv](https://urn.kb.se/resolve?urn=urn:nbn:se:raa:diva-8498) beskrivs detta inom utvecklingsområdet Användbarhet.

## `type` och `classified_as`

`type` och `classified_as` fyller olika funktioner:

| Attribut | Anger | Värde | Exempel |
|---|---|---|---|
| `type` | Objektets grundläggande klass i informationsmodellen | En klass i modellen | `HumanMadeObject`, `Person`, `VisualItem` |
| `classified_as` | Vad objektet är, mer precist | En eller flera referenser till begrepp i kontrollerade vokabulärer | *kamfodral* (`aat:300423476`) |

- En term från en kontrollerad vokabulär **ska** anges i `classified_as`, inte i `type`.
- Informationsmodellens klasser **ska inte** användas som värden i `classified_as`.

## Krav på klassificeringar

Att ange `classified_as` är i normalfallet inte obligatoriskt i K-samsök, men det är **starkt** rekommenderat. Poster utan klassificering har begränsat värde och får mycket låga kvalitetsbetyg. I vissa fall är `classified_as` obligatoriskt, se [Krav på attribut](04-krav-pa-attribut.md#om-classified_as).

Varje klassificering som hänvisar till ett begrepp med URI **ska** vara en [referens](03-identitet-och-referenser.md#referenser-till-andra-objekt) med:

- `id` – begreppets fullständiga URI
- `type` – normalt `Type`

`_label` bör anges för att göra informationen läsbar för utvecklare, men ersätter inte URI:n. Samma sak gäller `language`: värden som är URI:er ska alltid anges som referenser.

**Exempel:** Ett kamfodral klassificeras med termen [`aat:300423476`](http://vocab.getty.edu/aat/300423476) *comb cases* (kamfodral) i Getty AAT:

```json
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

## Så väljer du term

1. **Använd en term från de rekommenderade vokabulärerna** i Network of Terms om det finns en som passar. Se [Vokabulärer](09-vokabularer.md).
2. **Om termen saknas:** ange det närmaste *överordnade* begreppet i en lämplig hierarki, tillsammans med en inbäddad engångsinstans (*singleton*) av det specifika begreppet. Se [Exempel: begrepp som saknas](#exempel-begrepp-som-saknas).
3. **Om du har en egen URI** för begreppet, eller en URI i en vokabulär utanför Network of Terms, kan du ange den *tillsammans med* – men aldrig *i stället för* – den matchande eller överordnade termen. Se [Exempel: egen URI](#exempel-egen-uri).
4. **Om det inte finns någon lämplig term alls** kan du som tillfällig nödlösning leverera ett inbäddat engångsbegrepp utan koppling till ett begrepp med URI. Det ska vara ett undantag, inte regel.

### Exempel: begrepp som saknas

Du vill ange att ett föremål i landskapet är en *gärdsgård*, men begreppet finns inte i Getty AAT eller i någon annan vokabulär i Network of Terms. Ange då det närmaste överordnade begreppet i AAT – [`aat:300005044`](http://vocab.getty.edu/aat/300005044) *fences* (staket) – tillsammans med ett engångsbegrepp för *gärdsgård*:

```json
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

### Exempel: egen URI

Om du publicerar ett eget begrepp för *gärdsgård* gör du som i föregående exempel, men anger även begreppets URI:

```json
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

> [!NOTE]
> **Öppen fråga.** Linked Art kräver metatypen *Type of Work* ([`aat:300435443`](http://vocab.getty.edu/aat/300435443)) på objektklassificeringar när den är känd. Den används i exemplen med gärdsgård men inte i exemplet med kamfodralet. Det behöver beslutas om K-samsök kräver, rekommenderar eller bortser från metatyper.

## Klassificering av visuellt innehåll

K-samsök och Linked Art skiljer mellan **avbildningen** och **det som avbildas**. Visuellt innehåll – motivet – är ett objekt av typen `VisualItem`. Vad motivet föreställer anges med något av följande attribut:

| Attribut | Används när bilden … | Exempel |
|---|---|---|
| `represents` | föreställer en identifierad resurs. Värdet är en referens till resursen. | En namngiven person, en bestämd byggnad, ett specifikt föremål |
| `represents_instance_of_type` | föreställer något som kan klassificeras men inte identifieras som en bestämd individ. Värdet är en referens till typen. | Ett barn, en cykel, ett träd |
| `about` | har ett begrepp som ämne eller innebörd, snarare än något som faktiskt avbildas. | |

`represents_instance_of_type` ska anges på `VisualItem`, inte direkt på den fysiska eller digitala bärare som visar motivet.

**Exempel:** Motivet visar ett parasoll. Parasollet har ingen egen identitet och beskrivs därför inte som ett separat `HumanMadeObject`:

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
