# 10. Kortformer

För att göra det enklare för datapartner kan vissa vanliga uttryck anges med *kortformer* (*shortforms*). En kortform är ett förenklat uttryck som K-samsök expanderar till den fullständiga Linked Art-formen när posten skördas.

## Så fungerar kortformer

- Kortformer har prefixet `_`, som markerar att de är ett hjälpmedel vid överföring till RAÄ och inte Linked Art-attribut. (Undantaget är `_label`, som är ett vanligt Linked Art-attribut trots prefixet.)
- Du kan använda kortformer i poster som skördas av K-samsök. Poster som RAÄ publicerar använder alltid den expanderade formen.
- Om samma objekt innehåller både en kortform och motsvarande expanderade värde, ignoreras kortformen.
- Om en kortform inte kan tolkas entydigt accepteras posten ändå, men kortformen expanderas inte och utelämnas.

> [!IMPORTANT]
> Använd inte kortformer i data som kan hämtas av andra än K-samsök 2:s skördare, till exempel i ett öppet API. Andra konsumenter känner inte till kortformerna och kan inte expandera dem.

## Tillgängliga kortformer

| Kortform | Värde | Expanderas till |
|---|---|---|
| `_primaryName` | En sträng, högst en per objekt | Ett `Name` i `identified_by`, klassificerat som primärt namn ([`aat:300404670`](http://vocab.getty.edu/aat/300404670)). Om objektet redan har ett namn med den klassificeringen ignoreras kortformen. |
| `_description` | En sträng, högst en per objekt | Ett `LinguisticObject` i `referred_to_by`, klassificerat som beskrivning ([`aat:300435416`](http://vocab.getty.edu/aat/300435416)). Om objektet redan har en text med den klassificeringen ignoreras kortformen. |
| `_classifications` | En lista med strängar | En `Type`-referens i `classified_as` för varje värde. Värdena ska vara fullständiga URI:er eller förkortningar med prefixet `aat:` (Getty AAT). Ogiltiga värden ignoreras. Om objektet redan har värden i `classified_as` ignoreras kortformen. |

Den fullständiga definitionen finns i [Modellreferensen](../referens/modellreferens.md#property-index).

## Språk i kortformer

I kortformer som stöder språk (`_primaryName` och `_description`) anges språket med ett suffix i formen `text @kod`:

- `@` tolkas som början på en språkkod bara om det föregås av ett eller flera mellanslag och står sist i strängen.
- `"Ben Hur @en"` betyder att texten `Ben Hur` är på engelska.
- `"Ben Hur@en"` tolkas som texten `Ben Hur@en`, utan språk.
- Okända språkkoder ignoreras.

> [!NOTE]
> **Öppen fråga.** Vilken standard språkkoderna följer (till exempel BCP 47 eller ISO 639) behöver anges.
