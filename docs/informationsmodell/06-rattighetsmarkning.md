# 6. Rättighetsmärkning

All information som levereras till K-samsök ska ha tydlig information om rättigheter och användningsvillkor. Det här kapitlet beskriver hur licenser anges för metadata respektive för innehåll som bilder och texter, och vilka rättighetsmärkningar som ingår i K-samsöks rättighetsmodell.

## Sammanfattning

| Vad | Krav | Var anges det? |
|---|---|---|
| Metadata (själva posten) | Alltid [CC0 1.0](http://creativecommons.org/publicdomain/zero/1.0/) | I [proveniensinformationen](05-proveniens.md) |
| Innehåll (bilder, texter m.m.) | En märkning ur [K-samsöks rättighetsmodell](#k-samsöks-rättighetsmodell) | Med `subject_to` på `VisualItem` eller `LinguisticObject` |

## Metadata

All metadata ska licensieras med [CC0 1.0 Universal](http://creativecommons.org/publicdomain/zero/1.0/).

Eftersom licensen gäller postens innehåll snarare än den kulturarvsresurs som posten beskriver, anges den i proveniensinformationen, som beskriver just posten. I exemplet används schema.org:

```json
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

> [!WARNING]
> **Öppen fråga.** Exemplet ovan uttrycker proveniensinformationen med schema.org (`https://schema.org/DigitalDocument` och `https://schema.org/license` med ett `Type`-objekt som värde). Det stämmer inte med modellen i kapitlet [Proveniens](05-proveniens.md), där `license` är en sträng i ett `RecordProvenance`-objekt. Vilken form som gäller behöver fastställas. Observera också att CC0 och Public Domain Mark är två olika märkningar, trots att exemplet har etiketten "Public Domain".

## Innehåll (bilder, texter m.m.)

Allt innehåll – till exempel bilder och texter – ska ha en rättighetsmärkning. K-samsök använder märkningar från [Creative Commons](https://creativecommons.org/) och [RightsStatements.org](https://rightsstatements.org/) enligt [K-samsöks rättighetsmodell](#k-samsöks-rättighetsmodell).

### Märkningen anges på verket, inte på bäraren

Rättighetsmärkningen anges inte på *bäraren* – den fysiska boken eller bilden, eller den digitala filen – utan på det abstrakta informationsobjektet:

- `VisualItem` (motivet) för bilder
- `LinguisticObject` för texter

En digital bild med licensen CC BY beskrivs alltså som ett `DigitalObject` som visar (`digitally_shows`) ett motiv. Motivet är i sin tur föremål för (`subject_to`) en rättighet (`Right`) som klassificeras med licensens URI:

```json
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

Om rättighetsmärkningen är InC, InC-EDU eller någon av CC BY-licenserna ska rättigheten även ha `possessed_by` (se [Krav på attribut](04-krav-pa-attribut.md#persistenta-objekt)).

> [!NOTE]
> **Utkast.** Vägledning och exempel för texter (`LinguisticObject`), ljud och 3D saknas ännu.

## K-samsöks rättighetsmodell

K-samsöks rättighetsmodell omfattar följande märkningar. Samtliga finns också i [Network of Terms](09-vokabularer.md#rekommenderade-vokabulärer).

### Fri användning

| Märkning | Innebörd | URI |
|---|---|---|
| **Public Domain Mark (PDM)** | En icke juridiskt bindande märkning, framtagen av Creative Commons, för material där upphovsrätten har gått ut eller som inte skyddas av upphovsrätt. | `http://creativecommons.org/publicdomain/mark/1.0/` |
| **Creative Commons Zero (CC0)** | Informationsförvaltaren avsäger sig alla rättigheter, så att materialet får återanvändas utan restriktioner. | `http://creativecommons.org/publicdomain/zero/1.0/` |

### Creative Commons-licenser

En informationsförvaltare kan märka informationen med någon av de sex Creative Commons-licenserna. Standardvalet är CC BY 4.0. Läs mer om licenserna på [creativecommons.se](http://www.creativecommons.se).

| Licens | Villkor vid användning | URI |
|---|---|---|
| **CC BY 4.0** – Attribution | Upphovspersonen ska anges. | `http://creativecommons.org/licenses/by/4.0/` |
| **CC BY-SA 4.0** – Attribution-ShareAlike | Upphovspersonen ska anges. Bearbetningar ska delas under samma villkor. | `http://creativecommons.org/licenses/by-sa/4.0/` |
| **CC BY-ND 4.0** – Attribution-NoDerivatives | Upphovspersonen ska anges. Materialet får inte bearbetas. | `http://creativecommons.org/licenses/by-nd/4.0/` |
| **CC BY-NC 4.0** – Attribution-NonCommercial | Upphovspersonen ska anges. Ingen kommersiell användning. | `http://creativecommons.org/licenses/by-nc/4.0/` |
| **CC BY-NC-SA 4.0** – Attribution-NonCommercial-ShareAlike | Upphovspersonen ska anges. Ingen kommersiell användning. Bearbetningar ska delas under samma villkor. | `http://creativecommons.org/licenses/by-nc-sa/4.0/` |
| **CC BY-NC-ND 4.0** – Attribution-NonCommercial-NoDerivatives | Upphovspersonen ska anges. Ingen kommersiell användning. Materialet får inte bearbetas. | `http://creativecommons.org/licenses/by-nc-nd/4.0/` |

Om du vill använda en äldre version än 4.0 anger du URI:n till den versionen på samma sätt, till exempel `http://creativecommons.org/licenses/by/3.0/`.

### Förbehållna rättigheter

Metadata om material som är skyddat av upphovsrätt kan också levereras. Materialet märks då med en rättighetsmärkning från RightsStatements.org:

| Märkning | Innebörd | URI |
|---|---|---|
| **In Copyright (InC)** | Materialet är upphovsrättsskyddat. | `http://rightsstatements.org/vocab/InC/1.0/` |
| **In Copyright – EU Orphan Work (InC-OW-EU)** | Herrelöst verk: materialet är upphovsrättsskyddat, men upphovspersonen är okänd. Märkningen får bara användas om verket har registrerats i EUIPO:s databas över herrelösa verk (Orphan Works Database) via Patent- och registreringsverket. Mer information finns på PRV:s webbplats. | `http://rightsstatements.org/vocab/InC-OW-EU/1.0/` |
| **In Copyright – Educational Use Permitted (InC-EDU)** | Materialet är upphovsrättsskyddat, men får användas i utbildningssammanhang. | `http://rightsstatements.org/vocab/InC-EDU/1.0/` |
