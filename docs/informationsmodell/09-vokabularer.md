# 9. Vokabulärer

[Klassificering](08-klassificering.md) beskriver *hur* information klassificeras. Det här kapitlet beskriver *vilka* termer och vokabulärer som ska användas. Det är när klassificeringsmönstren tillämpas med gemensamma termer som olika datamängder blir verkligt interoperabla.

## Varför gemensamma vokabulärer?

K-samsöks informationsmodell är uppbyggd kring gemensamma vokabulärer. Helst ska varje term definieras med en URI. Det är ett av Linked Arts grundläggande kännetecken och det som gör modellen användbar för aggregering: kulturarvsdatan i K-samsök blir interoperabel och jämförbar med data från andra datapartner och från andra kulturarvsinstitutioner.

> [!TIP]
> Att använda vokabulärer är i dagsläget inte ett krav. Men att mappa sin data mot vokabulärer är den enskilt viktigaste insatsen för att höja datakvaliteten i K-samsök.

## Termer som Linked Art kräver

Även om det sällan är obligatoriskt att ange `classified_as` finns det krav på *vilka* termer som ska användas för vissa vanligt förekommande begrepp. Det primära namnet på ett objekt ska till exempel alltid klassificeras med [`aat:300404670`](http://vocab.getty.edu/aat/300404670) (se [Namn](07-namn-identifierare-och-beskrivningar.md#namn)).

Linked Art dokumenterar termerna i tre nivåer:

- [Required Terms](https://linked.art/model/vocab/required/) – termer som ska användas
- [Recommended Terms](https://linked.art/model/vocab/recommended/) – termer som bör användas
- [Optional Terms](https://linked.art/model/vocab/optional/) – termer som kan användas

## Rekommenderade vokabulärer

Här skiljer sig K-samsök från Linked Art. Linked Art använder i första hand [Getty AAT](https://vocab.getty.edu/aat/). K-samsök föredrar också Getty AAT, för att behålla så stor kompatibilitet som möjligt med andra Linked Art-tillämpningar. Men K-samsök omfattar mycket mer än Linked Arts fokus på konst, och många viktiga begrepp för kulturarvet i stort och för ämnen som arkeologi saknas i AAT. Därför tillåter K-samsök begrepp från andra rekommenderade vokabulärer där Getty AAT inte räcker till.

De rekommenderade vokabulärerna och begreppen sammanställs i tjänsten **Network of Terms**, som för närvarande innehåller:

| Vokabulär | Används för |
|---|---|
| [Getty AAT](https://vocab.getty.edu/aat/) | Allmänna begrepp, i första hand |
| [PeriodO](https://perio.do/) | Perioder |
| [GeoNames](http://www.geonames.org/) | Platser och geografiska indelningar |
| [K-samsöks rättighetsmodell](06-rattighetsmarkning.md#k-samsöks-rättighetsmodell) | Rättighetsmärkningar: PDM, CC0, de sex CC BY-licenserna, InC, InC-OW-EU och InC-EDU |
| [Profilstilar efter Gräslund, Ljung](http://kulturarvsdata.se/resurser/aukt/srdb/profilestyle) | Runologi |
| [Korsformer efter Lager](http://kulturarvsdata.se/resurser/aukt/srdb/crossform) | Runologi |
| [Brakteattyper](http://kulturarvsdata.se/resurser/aukt/srdb/bracteatetype) | Runologi |
| [Runologiska perioder](http://kulturarvsdata.se/resurser/aukt/srdb/period) | Runologi – perioder som styr transliterationsschemat |

> [!NOTE]
> **Utkast.** Här ska det framgå var Network of Terms finns (URL), att det är RAÄ:s instans av tjänsten, och hur en datapartner slår upp och mappar termer mot den.

## Vokabulärer under diskussion

> [!WARNING]
> **Utkast – internt underlag.** Följande vokabulärer är förslag som diskuteras för att eventuellt ingå i Network of Terms. De ingår inte i de rekommenderade vokabulärerna.

- RAÄ-vokabulärer för:
	- lämningstyper (gärna även mappade mot FISH)
	- antikvariska bedömningar (gärna även mappade mot FISH)
	- uppdragstyper (gärna även mappade mot FISH)
	- nummer (RAÄ-nummer, lämningsnummer, ärendenummer, arkivnummer …)
	- socknar (ATA-socken, KMR-socken, K-samsök-socken …)
	- mer från arkivet, BeBR …
- DarwinCore (vilka delar?)
- FISH:
	- [Archaeological Sciences](http://purl.org/heritagedata/schemes/560)
	- [Event Types](http://purl.org/heritagedata/schemes/agl_et)
	- [Evidence](http://purl.org/heritagedata/schemes/eh_evd)
	- eventuellt [Resource Description](http://purl.org/heritagedata/schemes/547)
	- eventuellt [Heritage Subjects and Themes](http://purl.org/heritagedata/schemes/595)
- [EAGLE](https://www.eagle-network.eu/resources/vocabularies/) (för inskrifter)
- KulturNav (vilka delar?)
- Mappningar mellan ovanstående och Wikidata
