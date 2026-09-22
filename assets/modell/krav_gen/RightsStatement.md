# Rättighetsmärkning

## Metadata

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

## Media

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

## <a id="rättighetsmodell"></a>K-samsöks rättighetsmodell

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

