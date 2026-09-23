# Changelog

## 0.6

Typ av ändring: Omstrukturering (+0.1)

Dokumentationen har gjorts om från ett sammanhängande dokument till en uppsättning sidor med en användarorienterad disposition. Innehållet i v0.5 har kompletterats med råmaterial från `assets/` som tidigare inte ingick.

Struktur:

- Ny startsida (`docs/README.md`) med målgrupper och vägval, samt en sida *Kom igång* med arbetsgång och checklista före leverans.
- Informationsmodellen är uppdelad i elva kapitel i fyra delar: Grunder, Krav på levererad data, Modelleringsmönster och Datamängder (`docs/informationsmodell/`).
- Nya referenssidor: Skördnings-API (`docs/api/`), Exempelbank (`docs/exempel/`), Ordlista (`docs/ordlista.md`) och Modellreferens (`docs/referens/modellreferens.md`, oförändrad kopia av den autogenererade `InformationModelDiagram.md`).
- v0.5 och granskningsversionen av v0.5 har flyttats till `archived_versions/`.

Innehåll:

- Nytt avsnitt *Så läser du dokumentationen* med kravnivåer (ska/bör/kan), förklaring av `✂️ …` och skrivsätt.
- Kapitel 3: exemplen från exempelbanken för identitet (`assets/modell/exempel/id.md`) har lagts till. Regeln om riktning för medlemskap i samlingar (från `assets/todo.txt`) har lagts till.
- Kapitel 4 (tidigare *Minimum Viable Object*): de typspecifika kraven (`assets/modell/krav_typ/index.md`) har lagts till som tabeller. Europeana-listan har gjorts om till en tabell med fält i kvalitetsmodellen och motsvarande uttryck i Linked Art.
- Kapitel 5: attributtabeller, regeln för proveniensobjektets id (`/prov`) och fält som genereras vid skördning har lagts till från råmaterialet.
- Kapitel 6: rättighetsmodellen presenteras som tabeller. Den inaktuella hänvisningen till `mediaLicenseUrl` (K-samsök 1) har ersatts.
- Kapitel 10: de tre kortformerna `_primaryName`, `_description` och `_classifications` har dokumenterats utifrån modellreferensen.
- Språkliga korrigeringar från granskningsversionen av v0.5 har förts in.
- Redaktionella anteckningar (`@@@`) har ersatts med enhetligt markerade rutor, **Utkast** och **Öppen fråga**. Personnamn har tagits bort ur anteckningarna.
- Enhetlig stavning: *Linked Art*, *K-samsök*/*K-samsök 2*.

JSON-exempel (endast syntaxrättningar, innehållet är oförändrat):

- Kapitel 3: kommatecken efter `"id" : "_hbtnamn"`; felplacerad `]` i exemplet med både persistenta och icke-persistenta underobjekt.
- Kapitel 5: kolon efter `"type"` i båda exemplen; kommatecken efter `"HumanMadeObject"`, `"Group"` och efter `provider`-objektet.
- Kapitel 7: kommatecken efter `content` i `subject_of`.
- Kodblock med JSON har markerats med `json` för syntaxmarkering.

## 0.5

Typ av ändring: Sprintbaslinje (+0.1)

Ändringar:

- Kapitel 10 Klassificering har omarbetats från arbetsutkast till sammanhängande dokumentation.
- Dokumenterat syftet med klassificering inom K-samsök.
- Dokumenterat skillnaden mellan `type` och `classified_as`.
- Dokumenterat mappnings- och leveranskrav för klassificeringsreferenser.
- Dokumenterat rekommenderad användning av kontrollerade vokabulärer.
- Dokumenterat hantering av lokala begrepp när motsvarande term saknas i rekommenderade vokabulärer.
- Dokumenterat mönster för klassificering av visuellt innehåll.
- Dokumenterat användning av `represents`, `represents_instance_of_type` och `about`.
- Genomfört korrekturändring: `använding` → `användning`.

Observationer för framtida sprintar:

- Rubriken `Mappnings- och leveranskrav` innehåller även modelleringsmönster och kan på sikt delas upp.
- Överlapp mellan kapitel 10 och kapitel 11 bör ses över när vokabulärkapitlet färdigställs.
- Exempeltermernas användning av versaler/gemener kan senare normaliseras.
- Kapitel 10 bedöms i övrigt vara innehållsmässigt stabilt.
