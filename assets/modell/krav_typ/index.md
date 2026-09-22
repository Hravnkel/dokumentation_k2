# K-samsök 2 Linked Art-profil: Typspecifika krav

## Persistenta objekt

För följande typer som förekommer som **persistenta objekt**:

- Abstrakta objekt (`PropositionalObject`)
- Aktörer (`Group` eller `Person`)
- Begrepp (`Type`, `Material`, `Language`, `Currency`, eller `MeasurementUnit`)
- Digitala objekt (`DigitalObject`)
- Fysiska objekt (`HumanMadeObject`)
- Händelser (`Period`, `Event`, eller `Activity`)\*
- Motiv (`VisualItem`)
- Platser (`Place`)
- Samlingar och mängder (`Set`)
- Texter (`LinguisticObject`)

…gäller följande minimumattribut:

### Tvingande
- `@context`
- `id` (URI)
- `type`
- *(Proveniens metadata: länk till källan, CC0, osv)*
- *`identified_by`* (ett namn/titel, eller id-nr)
- *För `LinguisticObject`: `language`*†
- *För `VisualItem` och `LinguisticObject`: `subject_to`* (rättighetsmärkning)
	- *(om rättighetmärkningen är InC, InC-Edu, eller CC BY \*) `possessed_by`*


### Rekomenderade

- `_label`
- `classified_as`\*
- *`is_subject_of`* (description)

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad, och begränsar värdet med at leverera posten om den saknas. Den är dessutom tvingande, med minst en länk till en godkänd vokabulärpost, om man vill leverera vidare till Europeana. Om en händelse är av klassen `Event`, eller `Activity` och beskriver ett härkomst (till exempel att ett objekt skapas) eller byte av ägarskap, blir `classified_as` tvingande även då, inte bara rekommenderad. 

† Obs att när språket är okänd/oltalkt, attributet är ändå tvingande, men ska ta värdet [aat:300389645](https://vocab.getty.edu/aat/300389645).

## Icke-persistenta objekt

För följande typer som förekommer som **icke-persistenta objekt**:

- Händelser (`Activity`, `Dissolution`, `Death`, `Destruction`, `Encounter`, `Modification`, eller `Activity`)
- Rättighetsmärkning (`Right`)

…gäller följande minimumattribut:

### Tvingande
- `type`

### Rekomenderade

- `_label`
- `classified_as`\*
- `identified_by`

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad.

---

För följande typer som förekommer som **icke-persistenta objekt**:

- Mått (`Dimension`)
- Belopp (`MonetaryAmount`)

…gäller följande minimumattribut:

### Tvingande

- `type`
- `value`
- `unit` (för `Dimension`)
- `currency`  (för `MonetaryAmount`)

### Rekomenderade

- `_label`
- `classified_as`\*
- `identified_by`

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad.

---

För följande typer som förekommer som **icke-persistenta objekt**:

- Identifierare (`Identifier`)
- Namn (`Name`)
- Texter (`LinguisticObject`)

…gäller följande minimumattribut:

### Tvingande

- `type`
- `content`
- *För `Name` och `LinguisticObject`: `language`*†

### Rekomenderade

- `_label`
- `classified_as`\*
- `identified_by`

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad.

† Obs att när språket är okänd/oltalkt, attributet är ändå tvingande, men ska ta värdet [aat:300389645](https://vocab.getty.edu/aat/300389645).

---

För följande typer som förekommer som **icke-persistenta objekt**:

- Tidspann (`TimeSpan`)

…gäller följande minimumattribut:

### Tvingande

- `type`

### Rekomenderade

- `_label`
- `classified_as`\*
- `identified_by`
- `begin_of_the_begin` (ISO8601 date-time)
- `end_of_the_begin` (ISO8601 date-time)
- `end_of_the_end` (ISO8601 date-time)
- `begin_of_the_end` (ISO8601 date-time)

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad.

## Referenser och länkar.

För följande typer som förekommer som **länkar**:

- Digitala länkar (`VisualItem`, `LinguisticObject`)

…gäller följande minimumattribut:

### Tvingande

- `type`
- För `VisualItem`: `digitally_shown_by`
- För `LinguisticObject`: `digitally_carried_by`
- *`subject_to`* (rättighetsmärkning)
	- *(om rättighetmärkningen är InC, InC-Edu, eller CC BY \*) `possessed_by`*

### Rekomenderade

- För `LinguisticObject`: `language`

---

För följande typer som förekommer som **länkar**:

- Relationer (`AttributeAssignment`)

…gäller följande minimumattribut:

### Tvingande
- `type`
- `assigned`

### Rekomenderade

- `_label`
- `classified_as`\*
- `identified_by`

\* Obs att även om `classified_as` inte är tvingande hos Linked Art, den är *starkt* rekomenderad.

---

 För följande typer som förekommer som **referenser**:

- Referenser till begrepp  (`Type`, `Material`, `Language`, `Currency`, eller `MeasurementUnit`)
- Övriga Referenser

…gäller följande minimumattribut:

### Tvingande

- `id` (URI)
- `type`

### Rekomenderade

- `_label`
