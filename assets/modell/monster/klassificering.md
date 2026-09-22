# Klassificering

@@@TODO våra förväntningar re klassificering

@@@TODO Referens till LinkedArts Getty-krav

@@@TODO Mönster: objekt med klassificering

@@@TODO Mönster: bild represents_instance_of_type

Se även [Rekommenderade vokabulär](./vokabular.md).

---

## Introduktion
@@@ TODO intro 

## Mappnings- och leveranskrav
@@@ TODO

Att ange `classified_as` som pekar till ett begrepp eller en term mha dess URI är i normalfallet inte ett krav hos K-samsök. Men det är starkt, *starkt* rekommenderat! Datamängder som saknar typer begränsar datats värde, och kommer att få väldigt låga kvalitetsbetyg av just denna anledning. Att ange `language` för textfält är dock ett krav.

`classified_as` och `language` med värden som är URI:er ska alltid formuleras som [referenser](referenser.md).

T.ex. om man vill beskriva ett kamfördral med hjälp av termen hos Getty AAT – [aat:300423476](http://vocab.getty.edu/aat/300423476) "comb cases" (kamfördral):

```
{
✂️…️
"id": "https://kulturarvsdata.se/exem/pel/kfd",
"_label": "Vikingatida kamfördral av ben",
"type": "HumanMadeObject",
"classified_as": [
	{
   		"id": "http://vocab.getty.edu/aat/300423476",
   		"type": "Type",
   		"_label": "Kamfördral"
   	}
],
✂️…️
}
```

Vi rekommenderar i första hand att man använder begrepp som finns med i de rekommenderade vokabulärerna hos Network of Terms. Ifall det specifika begreppet man vill använda saknas, ange istället det närmsta *överordnande* begreppet inom en lämplig hierarki, tillsammans med ett "in-line" singleton instans av begreppet.

T.ex. om man skulle vilja ange att ett föremål i landskapet är av typen "gärdsgård", begreppet "gärdsgård" finns inte hos Getty AAT eller Network of Terms övriga vokabulärer. Då skulle man istället ange det närmsta överordnande begreppet hos AAT – [aat:300005044](http://vocab.getty.edu/aat/300005044) "fences" (staket) – tillsammans med ett engångsbegrepp för "gärdsgård":


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

Har man även en länk till en vokabulärterm som inte förekommer inom Network of Terms är man välkommen att även leverera den tillsammans med – men aldrig istället för – den matchande eller överordnande termen.

Om man t.ex. publicerar ett eget begrepp för "gärdsgård" skulle man kunna göra som i exmplet ovanför, fast även inkludera URI:n till detta begrepp:

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

I vissa fall kommer det inte att finnas någon lämplig term att mappa mot. I sådana fall kan man leverera ett singleton begrepp, in-line och utan någon koppling till ett begrepp med URI, som tillfällig nödlösning. Detta bör dock anses vara ett undantag snarare än regel.

## Mappningskrav för vokabulärer mot K-samsök

@@@ TODO Ställningstagande ang. *mappningskrav*

## Linked Arts krav på vokabulärer

Hos både K-samsök och Linked Art är det som sagt sällan ett krav att ange `classified_as`, men dess fråvaro sänker datans kvalité rejält. Det finns dock vissa krav på *vilka* typer man ska använda för särskilda vanligt förekommande begrepp. T.ex. att det primära namnet för ett objekt skall allltid vara `classified_as` [aat:300404670](http://vocab.getty.edu/aat/300404670). Dessa krav dokumenteras hos Linked Art på [Required Terms](https://linked.art/model/vocab/required/).

Linked Art definierar även motsvarande [Recommended Terms](https://linked.art/model/vocab/recommended/) och [Optional Terms](https://linked.art/model/vocab/optional/) som på samma vis anger vilka termer man borde använda till `classified_as` för olika informationstyper.

## Rekommenderade vokabulärer i Network of Terms

En punkt där K-samsök skiljer sig från Linked Art är plattformens krav på vilka vokabulärer som ska användas. Linked Art förhåller sig mer eller mindre exklusivt till [Getty AAT](https://vocab.getty.edu/aat/). Hos K-samsök föredrar vi även primärt Getty AAT för att så mycket som möjligt behålla kompatibilitet med övriga Linked Art-tillämpningar; men scope:et för K-samsök sträcker sig mycket bredare än Linked Arts fokus på konst, och många viktiga begrepp för kulturarvet i stort och specifika ämnen såsom arkeologi m.fl. saknas. Därför tillåter K-samsök begrepp från övriga rekommenderade vokabulärer, där Getty AAT inte är lämplig. Dessa rekommenderade vokabulärerena och begrepp kureras och sammanställs i tjänsten Network of Terms. Den innehåller för närvarande:

- Rättighetsmärkningar ur [K-samsöks rättighetsmodell](../krav_gen/RightsStatement.md#rättighetsmodell):
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

### Föreslagna vokabulärer till Network of Terms

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
- KulturNav (vilka?)
- Mappningar mellan ovanstående och Wikidata?
