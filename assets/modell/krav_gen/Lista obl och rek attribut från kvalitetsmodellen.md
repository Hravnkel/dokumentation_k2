# Lista på obligatoriska och rekommenderade fält från kvalitetsmodellen

## Introduktion
K-samsök har ett antal obligatoriska attribut för objekt för enhetlig hantering av data och för att möjliggöra aggregering till Europeana/det gemensamma europeiska dataområdet för kulturarv och andra dataportaler. 

## Obligatoriska attribut för objekt

@@@ TODO Agnieszka. Obs, listan fortfarande preliminär. Behöver även kollas termmässigt mot LA. På engelska eller svenska? 

- Title
- URI 
- Publisher - partnern som bidrar med objektet
- DataProvider - partnern som äger datan (ev. samma som utgivare?)
- Description 
- Updated - datum när posten uppdaterades
- Harvested date - autogenereras vid skördning
- Type 
- Classification - för Europeana 
- Rights
- isShownAt (Link to istutionen) - (auto?)
- isShownBy (Link to file)
- edm:provider (K-samsök) - i EDM-mappningen?
- language

## Rekommenderade attribut för objekt

- Creator
- Owner - objektets ägare
- Keywords
- Inventory number
- Alternative title
- isPartOf
- isNextInSequence

@@@ TODO MS

## Utifrån detta, MVO på Linked Art:ska för Europeanaleverans

- `id` (URI)
- `identified_by`
- `type`
- `classified_as` *(obs rekomenderad men ej tvingande hos LA/K2 i dagsläget; dock tvingande för Europeana)*
- proveniensmetadata: länk till källan, CC0 osv
- Publisher/Dataprovider – fylls i automatiskt vid skördning
- Description *(obs rekomenderad men ej tvingande hos LA/K2 i dagsläget)*
- Updated *(hos källan – ur proveniensmetadata)*
- Harvested date *(autogenereras vid skördning – ur proveniensmetadata)*
- subject_to *(för visual/linguistic items)*
- isShownAt *(länk till källan – ur proveniensmetadata)*
- isShownBy *(visualised_by för visual/linguistic items)*
- edm:provider (K-samsök) (autogenereras i EDM-mappningen)
- language (för texter)

### Rekommenderade

- Creator **(hos LA en creation event där en person har varit delaktig)**
- Owner **(hos LA en current owner eller transfer of custody)**
- Keywords **(helst länkar)**
- Inventory number **(identified_by number med classified as)**
- Alternative title **(identified_by name med classified as)**
- isPartOf 
- isNextInSequence *(???)*
