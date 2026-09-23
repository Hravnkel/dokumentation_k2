# Kom igång

Den här sidan ger en översikt över arbetsgången när du förbereder data för leverans till K-samsök 2. Varje steg länkar till det avsnitt i dokumentationen där du hittar detaljerna.

> [!TIP]
> Om du är ny inför Linked Art kan det vara bra att först läsa [Introduktion till informationsmodellen](informationsmodell/01-introduktion.md). Där förklaras de grundläggande principerna och de begrepp som används i resten av dokumentationen.

## Förutsättningar

- Din organisation är registrerad som datapartner hos RAÄ och har tillgång till K-samsök 2:s administrativa gränssnitt.
- Du har tillgång till den data som ska levereras, till exempel via en export från ert samlingsförvaltningssystem.

## Arbetsgång

### 1. Hämta datapartner-id och dataset-id

RAÄ tilldelar varje datapartner ett **datapartner-id** och varje datamängd ett **dataset-id**. Du hittar dem i K-samsök 2:s administrativa gränssnitt. De ingår i alla URI:er som du skapar.

### 2. Beskriv datamängden

Varje datamängd ska beskrivas med bland annat titel, beskrivning och kontaktuppgifter, så att den blir sökbar i dataportaler.

➜ [Beskrivning av datamängder](informationsmodell/11-beskrivning-av-datamangder.md)

### 3. Skapa en URI för varje resurs

Varje kulturarvsresurs som ska skördas ska ha en kulturarvsdata-URI som följer mönstret `https://kulturarvsdata.se/{datapartner-id}/{dataset-id}/{resurs-id}`. Det är du som skapar URI:erna när du förbereder datamängden.

➜ [Identitet och referenser](informationsmodell/03-identitet-och-referenser.md)

### 4. Mappa posterna till Linked Art

För varje resurs väljer du en klass (`type`), till exempel `HumanMadeObject` för ett föremål, och uttrycker därefter informationen med Linked Art-mönster:

- namn, titlar och identifierare med `identified_by` – [Namn, identifierare och beskrivningar](informationsmodell/07-namn-identifierare-och-beskrivningar.md)
- vad resursen är, med `classified_as` och termer från gemensamma vokabulärer – [Klassificering](informationsmodell/08-klassificering.md) och [Vokabulärer](informationsmodell/09-vokabularer.md)
- språk (`language`) på namn och texter

Kontrollera vilka attribut som är obligatoriska för respektive typ av objekt i [Krav på attribut](informationsmodell/04-krav-pa-attribut.md).

### 5. Lägg till proveniens och rättighetsmärkning

- Varje persistent objekt ska ha proveniensinformation med metadatalicens och länk till källposten – [Proveniens](informationsmodell/05-proveniens.md).
- Bilder, texter och annat innehåll ska ha en rättighetsmärkning – [Rättighetsmärkning](informationsmodell/06-rattighetsmarkning.md).

### 6. Serialisera som JSON-LD

Varje post levereras som ett JSON-LD-dokument med både Linked Arts och K-samsöks `@context`.

➜ [Serialisering](informationsmodell/02-serialisering.md)

Vid skördning kan du förenkla vissa vanliga uttryck med [kortformer](informationsmodell/10-kortformer.md).

### 7. Kontrollera och gör datamängden tillgänglig för skördning

Kontrollera posterna mot [OpenAPI-schemat](api/README.md#openapi-schema) och gör dem tillgängliga enligt [skördningsspecifikationen](api/README.md#specifikation).

> [!NOTE]
> **Utkast.** Här ska det beskrivas hur en skördning startas och följs upp i det administrativa gränssnittet, och vilka valideringsverktyg som rekommenderas.

## Checklista före leverans

Använd checklistan som en sista kontroll. Den sammanfattar de krav som beskrivs i dokumentationen.

- [ ] Varje rotobjekt har `@context` med både Linked Arts och K-samsöks kontext.
- [ ] Varje skördad resurs har en kulturarvsdata-URI enligt mönstret ovan.
- [ ] Varje persistent objekt har `id`, `type` och minst ett namn eller en identifierare i `identified_by`.
- [ ] Varje persistent objekt har proveniensinformation med licensen CC0 och en länk till källposten.
- [ ] Varje `VisualItem` och `LinguisticObject` har en rättighetsmärkning (`subject_to`) från [K-samsöks rättighetsmodell](informationsmodell/06-rattighetsmarkning.md#k-samsöks-rättighetsmodell).
- [ ] Namn och texter har `language`.
- [ ] Referenser till begrepp (till exempel i `classified_as` och `language`) har `id` med fullständig URI och `type`.
- [ ] Objekten är klassificerade med termer från [rekommenderade vokabulärer](informationsmodell/09-vokabularer.md) så långt det är möjligt (starkt rekommenderat).
