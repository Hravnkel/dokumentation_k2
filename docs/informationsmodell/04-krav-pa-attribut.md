# 4. Krav på attribut

Det här kapitlet sammanfattar vilka attribut som är obligatoriska och rekommenderade för olika typer av objekt. Kraven finns för att data ska kunna hanteras enhetligt och för att den ska kunna levereras vidare till Europeana och andra dataportaler.

Använd kapitlet som uppslagsverk när du mappar data. Hur respektive attribut används beskrivs i de kapitel som tabellerna länkar till. Samtliga attribut som får förekomma för en viss klass finns i [Modellreferensen](../referens/modellreferens.md).

> [!WARNING]
> **Utkast.** Kraven är preliminära och kan komma att ändras.

## Krav per typ av objekt

Vilka krav som gäller beror på om objektet är persistent, icke-persistent, en länk eller en referens. Se [Identitet och referenser](03-identitet-och-referenser.md) för definitionerna.

### Persistenta objekt

Gäller följande klasser när de förekommer som persistenta objekt:

| Typ av objekt | Klass |
|---|---|
| Abstrakta objekt | `PropositionalObject` |
| Aktörer | `Group`, `Person` |
| Begrepp | `Type`, `Material`, `Language`, `Currency`, `MeasurementUnit` |
| Digitala objekt | `DigitalObject` |
| Fysiska objekt | `HumanMadeObject` |
| Händelser | `Period`, `Event`, `Activity` |
| Motiv | `VisualItem` |
| Platser | `Place` |
| Samlingar och mängder | `Set` |
| Texter | `LinguisticObject` |

**Obligatoriska attribut**

| Attribut | Gäller | Kommentar |
|---|---|---|
| `@context` | Rotobjekt | Se [Serialisering](02-serialisering.md#json-ld-kontext-context). |
| `id` | Alla | En URI. Se [Identitet och referenser](03-identitet-och-referenser.md). |
| `type` | Alla | |
| Proveniens | Alla | Metadatalicens (CC0) och länk till källposten. Se [Proveniens](05-proveniens.md). |
| `identified_by` | Alla | Minst ett namn, en titel eller ett id-nummer. Se [Namn, identifierare och beskrivningar](07-namn-identifierare-och-beskrivningar.md). |
| `language` | `LinguisticObject` | Se [Språk](#språk-language). |
| `subject_to` | `VisualItem`, `LinguisticObject` | Rättighetsmärkning. Se [Rättighetsmärkning](06-rattighetsmarkning.md). |
| `possessed_by` på rättigheten | `VisualItem`, `LinguisticObject` | Om rättighetsmärkningen är InC, InC-EDU eller någon av CC BY-licenserna. |
| `classified_as` | `Event`, `Activity` | Om händelsen beskriver en tillkomst (till exempel att ett föremål tillverkas) eller ett ägarbyte. |

**Rekommenderade attribut**

| Attribut | Kommentar |
|---|---|
| `_label` | Se [`_label`](07-namn-identifierare-och-beskrivningar.md#_label). |
| `classified_as` | Starkt rekommenderat. Se [Om `classified_as`](#om-classified_as). |
| `subject_of` | Beskrivande text. Se [Beskrivningar](07-namn-identifierare-och-beskrivningar.md#beskrivningar). |

### Icke-persistenta objekt

| Typ av objekt | Klass | Obligatoriska | Rekommenderade |
|---|---|---|---|
| Händelser | `Activity`, `Dissolution`, `Death`, `Destruction`, `Encounter`, `Modification` | `type` | `_label`, `classified_as`, `identified_by` |
| Rättighetsmärkning | `Right` | `type` | `_label`, `classified_as`, `identified_by` |
| Mått | `Dimension` | `type`, `value`, `unit` | `_label`, `classified_as`, `identified_by` |
| Belopp | `MonetaryAmount` | `type`, `value`, `currency` | `_label`, `classified_as`, `identified_by` |
| Identifierare | `Identifier` | `type`, `content` | `_label`, `classified_as`, `identified_by` |
| Namn | `Name` | `type`, `content`, `language` | `_label`, `classified_as`, `identified_by` |
| Texter | `LinguisticObject` | `type`, `content`, `language` | `_label`, `classified_as`, `identified_by` |
| Tidsspann | `TimeSpan` | `type` | `_label`, `classified_as`, `identified_by`, `begin_of_the_begin`, `end_of_the_begin`, `begin_of_the_end`, `end_of_the_end` |

Tidpunkterna på `TimeSpan` anges som datum och tid enligt ISO 8601.

### Länkar

| Typ av objekt | Klass | Obligatoriska | Rekommenderade |
|---|---|---|---|
| Digitala länkar | `VisualItem` | `type`, `digitally_shown_by`, `subject_to` (och i vissa fall `possessed_by`, se ovan) | |
| Digitala länkar | `LinguisticObject` | `type`, `digitally_carried_by`, `subject_to` (och i vissa fall `possessed_by`, se ovan) | `language` |
| Relationer | `AttributeAssignment` | `type`, `assigned` | `_label`, `classified_as`, `identified_by` |

### Referenser

Gäller referenser till begrepp (`Type`, `Material`, `Language`, `Currency`, `MeasurementUnit`) och alla övriga referenser.

| Obligatoriska | Rekommenderade |
|---|---|
| `id` (URI), `type` | `_label` |

Se [Referenser till andra objekt](03-identitet-och-referenser.md#referenser-till-andra-objekt).

### Om `classified_as`

Även om `classified_as` sällan är obligatoriskt, varken i Linked Art eller i K-samsök, är det **starkt** rekommenderat. Poster som saknar klassificering har begränsat värde och får låga kvalitetsbetyg. För vidareleverans till Europeana är `classified_as` obligatoriskt, med minst en länk till en term i en godkänd vokabulär. Se [Klassificering](08-klassificering.md).

### Språk (`language`)

`language` är obligatoriskt på namn och texter (`Name` och `LinguisticObject`). Om språket är okänt eller inte går att fastställa ska attributet ändå anges, med värdet [`aat:300389645`](http://vocab.getty.edu/aat/300389645).

> [!NOTE]
> **Öppen fråga.** Det behöver preciseras om kravet på `language` även gäller andra textfält, till exempel `Identifier` och `_label` (rimligen inte).

## Krav för vidareleverans till Europeana

K-samsök levererar data vidare till Europeana, det gemensamma europeiska dataområdet för kulturarv. Tabellen visar vilka fält i K-samsöks kvalitetsmodell som krävs för det, och hur de motsvaras i Linked Art. Flera av fälten fylls i automatiskt vid skördning.

> [!WARNING]
> **Utkast.** Listan är preliminär och behöver stämmas av mot Linked Arts termer. Det är också oklart om fältnamnen ska anges på engelska eller svenska.

### Obligatoriska fält

| Fält i kvalitetsmodellen | Uttryck i Linked Art / K-samsök | Kommentar |
|---|---|---|
| URI | `id` | |
| Title | `identified_by` | Namn eller titel. |
| Type | `type` | |
| Classification | `classified_as` | Rekommenderat men inte obligatoriskt i Linked Art och K-samsök. Obligatoriskt för Europeana. |
| Description | Beskrivande text | Rekommenderat men inte obligatoriskt i Linked Art och K-samsök. |
| Rights | Proveniens (CC0 för metadata) och `subject_to` (för `VisualItem` och `LinguisticObject`) | |
| Publisher – partnern som bidrar med objektet | – | Fylls i automatiskt vid skördning. |
| DataProvider – partnern som äger datan | – | Fylls i automatiskt vid skördning. Kan vara samma som Publisher. |
| Updated – när posten senast uppdaterades | `dateModified` i proveniensinformationen | Avser källposten. |
| Harvested date | Proveniensinformationen | Genereras automatiskt vid skördning. |
| isShownAt – länk till posten hos institutionen | Länk till källposten i proveniensinformationen | |
| isShownBy – länk till fil | Digital representation av `VisualItem` eller `LinguisticObject` | I underlaget benämnt *visualised_by*, som inte är ett attribut i modellen. Behöver fastställas. |
| edm:provider (K-samsök) | – | Genereras automatiskt i mappningen till EDM. |
| language | `language` | För texter. |

### Rekommenderade fält

| Fält i kvalitetsmodellen | Uttryck i Linked Art / K-samsök |
|---|---|
| Creator | En tillkomsthändelse (*creation event*) där en person har medverkat. |
| Owner – objektets ägare | Nuvarande ägare, eller en överföring av besittning (`TransferOfCustody`). |
| Keywords | Helst länkar till termer i vokabulärer. |
| Inventory number | `identified_by` med ett `Identifier` och lämplig `classified_as`. |
| Alternative title | `identified_by` med ett `Name` och lämplig `classified_as`. |
| isPartOf | *Ej fastställt.* |
| isNextInSequence | *Ej fastställt.* |
