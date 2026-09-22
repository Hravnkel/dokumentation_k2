# Ksamsök 2 LinkedArt-profil: Övergripande krav

## <a id="record_provenance"></a>Digital Proveniens

Samtliga objekt som har ett [persistent id](./identitet.md#persistent) måste också ha digital proveniensinformation. Denna information anges via attributet `recordProvenance` som har ett `RecordProvenance`-objekt som värde.

Proviniensinformation ska ej anges på objekt med [icke-persistenta id:n](./identitet.md#nonpersistent), och ej heller på [referenser](../Terminologi.md#referens).

JSON-LD `@context` för proveniensdatat är `https://kulturarvsdata.se/resurser/linkedart/v1/raa.json` (se [Serialisering](./serialisering)).

De två centrala fälten hos proveniensobjektet som partners *måste* ange är: 
- _Licens_. Fältet `license` anger licensen för postens metadata. Värdet är alltid `http://creativecommons.org/publicdomain/zero/1.0/`. För mer information, se [Rättighetsmärkning](./RightsStatement.md).
- _Länk till källan_. Fältet `sourceRecord` innehåller obligatorisk information om källobjektet, inklusive den obligatoriska länken till källan (`url`). De två fälten `dateCreated` och `dateModified` beskriver när _källobjektet_ skapades respektive senast ändrades; de beskriver alltså inte postens metadata. Dessa två fält är ej obligatoriska, men är starkt rekommenderade att inkludera där möjligt.

👉 Komplett informationsmodell för RecordProvenance: [RecordProvenance](../InformationModelDiagram.md#class-record-provenance)

👉 komplett informationsmodell för SourceRecord: [SourceRecord](../InformationModelDiagram.md#class-source-record)

### <a id="prov_id"></a> Proveniensobjektets id 

`RecordProvenance`-objektet har en förutsägbar lexikal identitet. Identiteten måste vara det beskrivna objektets `id` med det tillagda path-segmentet `/prov`. 

Om det beskrivna objektet's `id` är `https://kulturarvsdata.se/exem/pel` blir proveniensobjektets `id` således `https://kulturarvsdata.se/exem/pel/prov`.

### <a id="autogen"></a> Autogenererade fält

Följande attribut, som förekommer i [schemat](../../Terminologi.md#schema) för `RecordProvenance`-objektet, ska uteslutas från objektet vid leverans. RAÄ lägger till dem under skördningsprocessen.

- `RecordProvenance.ingested_at`
- `RecordProvenance.provider`

### Exempel
Se [exempel/RecordProvenance.md](exempel/RecordProvenance.md).
