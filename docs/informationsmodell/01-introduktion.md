# 1. Introduktion

Det här kapitlet beskriver vad informationsmodellen bygger på, vilka principer som styr den och hur resten av dokumentationen ska läsas.

## Om informationsmodellen

K-samsöks informationsmodell är baserad på [Linked Art](https://linked.art/), en modell för länkad öppen data som används för att beskriva kulturarv. Linked Art är en tillämpningsprofil av den sektorsövergripande ontologin [CIDOC CRM](https://cidoc-crm.org/), vilket gör den interoperabel med många andra resurser.

Som namnet antyder är Linked Art främst utvecklad för att beskriva konst, men modellen används också för arkiv- och bibliografiskt material. Eftersom K-samsök även innehåller annat material, till exempel fornlämningar, bygger RAÄ ut modellen inom relevanta områden. Resultatet kallas i dokumentationen *RAÄ:s Linked Art-profil*.

Dokumentationen beskriver det som gäller specifikt för K-samsök. För den generella modellen hänvisas till [Linked Arts modelldokumentation](https://linked.art/model/).

> [!NOTE]
> **Öppen fråga.** Vilken version av Linked Art (Model och API) och CIDOC CRM som K-samsök 2 följer ska anges här, liksom versionspolicyn för K-samsöks kontext `raa.json`.

### Avgränsning

Dokumentationen beskriver hur data **levereras** till K-samsök. Hur data hämtas från K-samsök (konsumtion) beskrivs bara översiktligt.

## Grundläggande principer

### K-samsök bygger på Linked Art

K-samsök har valt Linked Art som grundmodell för att underlätta internationell interoperabilitet.

### Objekt identifieras med URI:er

Varje persistent objekt i K-samsök har en beständig URI som unik identifierare. Objektet ska alltid vara nåbart via internet. Läs mer i [Identitet och referenser](03-identitet-och-referenser.md).

### Objekt kan bestå av enbart metadata

Ett objekt behöver inte vara kopplat till en mediefil utan kan bestå av enbart metadata. Ett objekt kan också vara en abstrakt företeelse.

### K-samsök är en kunskapsgraf

K-samsök samlar objekt och relationerna mellan dem i en kunskapsgraf. Relationer kan peka på objekt både inom och utanför grafen.

### Persistenta objekt kan återanvändas över organisationsgränser

Data i K-samsök ska inte betraktas som lokal utan sättas i relation till annan data. Hänvisningar till objekt utanför den egna organisationen är därför både möjliga och uppmuntrade.

### Lokala termer ska så långt som möjligt ersättas med gemensamma vokabulärer

Den viktigaste faktorn för att utveckla data i K-samsök är att använda gemensamma termer. Det stärker kontexten, gör datan rikare och ökar precisionen. Läs mer i [Klassificering](08-klassificering.md) och [Vokabulärer](09-vokabularer.md).

## Så läser du dokumentationen

### Kravnivåer

Dokumentationen använder följande ord för att ange hur bindande en regel är:

| Ord | Betydelse |
|---|---|
| **ska** (obligatorisk, tvingande) | Ett krav. Data som inte uppfyller kravet uppfyller inte K-samsöks informationsmodell. |
| **ska inte** | Ett förbud. |
| **bör** (rekommenderad) | En stark rekommendation. Avsteg är tillåtna men sänker datakvaliteten. |
| **kan** (valfri) | Tillåtet men inte nödvändigt. |

### Exempel

- Exemplen visas som JSON-LD. Symbolen `✂️ …` betyder att delar av posten har utelämnats för att exemplet ska bli kortare. Exempel som innehåller `✂️ …` är därför inte fullständiga poster.
- Exemplen använder den fiktiva datapartnern `exem` och datamängden `pel`, till exempel `https://kulturarvsdata.se/exem/pel/abc`.
- Samtliga exempel finns samlade i [Exempelbanken](../exempel/README.md).

### Skrivsätt

- Attribut och klasser skrivs som kod: `identified_by`, `HumanMadeObject`.
- Termer i Getty AAT anges ibland i förkortad form med prefixet `aat:`. Till exempel står `aat:300404670` för `http://vocab.getty.edu/aat/300404670`. I levererad data ska den fullständiga URI:n användas, om inget annat anges.
- Ordet *objekt* används i dokumentationen om en nod i en JSON-LD-post, det vill säga något som har en `type`. Det behöver inte vara ett fysiskt föremål. Se även [Ordlista](../ordlista.md).
