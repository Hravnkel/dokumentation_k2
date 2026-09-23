# Informationsmodell för K-samsök 2

**Version:** 0.6 (utkast) · [Ändringslogg](changelog.md)

Informationsmodellen beskriver hur information struktureras, identifieras, klassificeras och utbyts i K-samsök 2. Den sammanfattar de krav, mönster och rekommendationer som gäller för data som levereras till tjänsten, och de minimikrav som gäller för interoperabilitet och vidareleverans, till exempel till Europeana.

Modellen är en tillämpning av [Linked Art](https://linked.art/). Dokumentationen beskriver det som är specifikt för K-samsök och hänvisar till Linked Arts dokumentation för det som är gemensamt.

## Innehåll

### Grunder

1. [Introduktion](01-introduktion.md) – Linked Art, grundläggande principer och hur dokumentationen ska läsas
2. [Serialisering](02-serialisering.md) – JSON-LD, `@context` och medietyper

### Krav på levererad data

3. [Identitet och referenser](03-identitet-och-referenser.md) – URI:er, persistenta och icke-persistenta objekt, referenser
4. [Krav på attribut](04-krav-pa-attribut.md) – obligatoriska och rekommenderade attribut per typ av objekt
5. [Proveniens](05-proveniens.md) – information om postens ursprung och källa
6. [Rättighetsmärkning](06-rattighetsmarkning.md) – licenser för metadata och innehåll

### Modelleringsmönster

7. [Namn, identifierare och beskrivningar](07-namn-identifierare-och-beskrivningar.md)
8. [Klassificering](08-klassificering.md) – `type`, `classified_as` och visuellt innehåll
9. [Vokabulärer](09-vokabularer.md) – rekommenderade vokabulärer och Linked Arts termkrav
10. [Kortformer](10-kortformer.md) – förenklade uttryck vid skördning

### Datamängder

11. [Beskrivning av datamängder](11-beskrivning-av-datamangder.md)

### Referens

- [Modellreferens](../referens/modellreferens.md) – alla klasser och attribut i RAÄ:s Linked Art-profil (autogenererad)
- [Exempelbank](../exempel/README.md)
- [Ordlista](../ordlista.md)

## Läsanvisning

- **Informationsförvaltare** rekommenderas att läsa kapitel 1, 3 och 7–9 för att förstå hur data ska struktureras och klassificeras.
- **Utvecklare** som bygger en export bör läsa samtliga kapitel i ordning och använda [Krav på attribut](04-krav-pa-attribut.md) och [Modellreferensen](../referens/modellreferens.md) som uppslagsverk.
