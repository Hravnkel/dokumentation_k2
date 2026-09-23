# Ordlista

Begrepp som används i dokumentationen för K-samsök 2.

| Begrepp | Förklaring |
|---|---|
| **AAT** (Getty Art & Architecture Thesaurus) | En vokabulär med begrepp för kulturarv som förvaltas av Getty Research Institute. Linked Arts och K-samsöks främsta vokabulär. Termer anges ibland förkortat, till exempel `aat:300404670`. Se [Vokabulärer](informationsmodell/09-vokabularer.md). |
| **Bärare** | Det fysiska eller digitala objekt som bär ett innehåll, till exempel en bok, ett fotografi eller en bildfil. Skiljs från själva innehållet (se *VisualItem* och *LinguisticObject*). |
| **CIDOC CRM** | En sektorsövergripande ontologi för kulturarvsinformation. Linked Art är en tillämpningsprofil av CIDOC CRM. |
| **Datamängd** (dataset) | En samling poster som en datapartner levererar till K-samsök. Varje datamängd har ett dataset-id. Se [Beskrivning av datamängder](informationsmodell/11-beskrivning-av-datamangder.md). |
| **Datapartner** | En organisation som levererar data till K-samsök. Varje datapartner har ett datapartner-id som tilldelas av RAÄ. |
| **Icke-persistent objekt** (anonymt objekt) | Ett objekt som saknar `id` eller vars `id` inte är en `http(s)`-URI. Se [Identitet och referenser](informationsmodell/03-identitet-och-referenser.md). |
| **JSON-LD** | Ett format för länkade data som bygger på JSON. K-samsöks format för utbyte av poster. Se [Serialisering](informationsmodell/02-serialisering.md). |
| **Klassificering** | Att ange vad ett objekt är med hjälp av begrepp i kontrollerade vokabulärer, med attributet `classified_as`. Se [Klassificering](informationsmodell/08-klassificering.md). |
| **Kortform** | Ett förenklat uttryck med prefixet `_` som K-samsök expanderar till fullständig Linked Art vid skördning. Se [Kortformer](informationsmodell/10-kortformer.md). |
| **Kulturarvsdata-URI** | En persistent URI i domänen `kulturarvsdata.se` som identifierar en resurs som skördats till K-samsök. Se [Identitet och referenser](informationsmodell/03-identitet-och-referenser.md#kulturarvsdata-urier). |
| **Linked Art** | En modell för länkade öppna data om kulturarv, baserad på CIDOC CRM. K-samsöks informationsmodell bygger på Linked Art. Se [linked.art](https://linked.art/). |
| **LinguisticObject** | Den klass i Linked Art som används för texter, oberoende av vilken bärare de finns på. |
| **Network of Terms** | Den tjänst där K-samsöks rekommenderade vokabulärer och begrepp sammanställs. Se [Vokabulärer](informationsmodell/09-vokabularer.md#rekommenderade-vokabulärer). |
| **Objekt** | I dokumentationen en nod i en JSON-LD-post, det vill säga något som har en `type`. Ett objekt kan vara ett fysiskt föremål men också till exempel en person, en händelse, ett namn eller ett begrepp. |
| **Persistent objekt** | Ett objekt vars `id` är en upplösningsbar `http(s)`-URI som är stabil över tid. Se [Identitet och referenser](informationsmodell/03-identitet-och-referenser.md). |
| **Post** | Ett JSON-LD-dokument med ett rotobjekt som beskriver en kulturarvsresurs. |
| **Proveniens** | Information om en posts ursprung: licens för metadatan och länk till källposten. Se [Proveniens](informationsmodell/05-proveniens.md). |
| **Referens** | En hänvisning till ett annat objekt som bara innehåller `id` och `type`, och eventuellt `_label`, `equivalent` och `notation`. Se [Referenser till andra objekt](informationsmodell/03-identitet-och-referenser.md#referenser-till-andra-objekt). |
| **Rättighetsmärkning** | En licens eller märkning som anger villkoren för att använda ett innehåll. Se [Rättighetsmärkning](informationsmodell/06-rattighetsmarkning.md). |
| **Rotobjekt** | Det yttersta objektet i en post. |
| **Schema** (OpenAPI-schema) | En beskrivning av skördnings-API:et och informationsmodellen i formatet OpenAPI. Se [Skördnings-API](api/README.md#openapi-schema). |
| **Skördning** | När K-samsök hämtar data från en datapartner. |
| **VisualItem** | Den klass i Linked Art som används för visuellt innehåll – motivet – oberoende av vilken bärare det finns på. |
| **Vokabulär** | En kontrollerad samling begrepp, där varje begrepp helst har en URI. Se [Vokabulärer](informationsmodell/09-vokabularer.md). |
