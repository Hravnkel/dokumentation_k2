# Backlog – Informationsmodell för K-samsök 2.0 (granskning av v0.5)

Sammanställning av sådant som bedöms kräva större insats än korrektur, eller beslut, och därför inte åtgärdats i granskningsversionen. Kodblock och @@@-stycken har lämnats helt orörda enligt förutsättningarna. Prioritet: **Hög** = påverkar datapartners mappning eller är faktiskt fel; **Medel** = otydlighet/inkonsekvens; **Låg** = polish.

---

## Hög prioritet

### B1. `subject_of` vs `referred_to_by` för beskrivande texter (kap 9)
Linked Art uttrycker inbäddade beskrivningar ("statements") med `referred_to_by` → `LinguisticObject` klassificerad som t.ex. *Description* (`aat:300435416`), och med metatypen *Brief Text* (`aat:300418049`) på klassificeringen. `subject_of` används i Linked Art för externa dokument som *handlar om* objektet (webbsidor, artiklar). Exemplet i kap 9 använder `subject_of` för en inbäddad beskrivande text, vilket avviker.
- **Åtgärd:** Besluta om K-samsök ska följa LA (`referred_to_by`) eller dokumentera avvikelsen uttryckligen. Uppdatera exempel och text i kap 9 samt MVO-listan i kap 6.
- **Ref:** https://linked.art/api/1.0/shared/statement/ , https://linked.art/model/vocab/recommended/#statement-types

### B2. Två oförenliga proveniensmodeller (kap 7 vs kap 8)
Kap 7 använder `recordProvenance` → `RecordProvenance` / `license` / `source_record` → `SourceRecord`. Kap 8 (Metadata) använder `recordProvenance` → `"type": "https://schema.org/DigitalDocument"` och `"https://schema.org/license"` med ett `Type`-objekt som värde. Läsaren kan inte avgöra vilken form som gäller.
- **Åtgärd:** Fastställ en modell, verifiera mot `raa.json`-kontexten och skriv om exemplet i kap 8 så att det stämmer med kap 7 (eller tvärtom). Klargör också om `license` ska vara en sträng-URI eller en referens.

### B3. Kodexempel som inte är giltig JSON
Får inte ändras i denna sprint, men bör rättas innan publicering:
- Kap 7, båda exemplen: `"type" "RecordProvenance"` saknar kolon; kommatecken saknas efter `"type" : "HumanMadeObject"`, `"type" : "Group"` och efter `provider`-objektet.
- Kap 9, exemplet "Arumbayafetisch": kommatecken saknas efter `"content": "..."` i `subject_of`.
- **Åtgärd:** Rätta samt inför automatisk validering av alla exempel (JSON-parse + Linked Art-validator: https://linked.art/software/validator/) i dokumentationsbygget.

### B4. Kap 6 Minimum Viable Object är i huvudsak EDM-termer, inte Linked Art
Listan blandar EDM (isShownAt, isShownBy, edm:provider), DC (Title, Publisher) och LA-attribut. En datapartner kan inte utläsa vilken LA-struktur som faktiskt krävs.
- **Åtgärd:** Gör en mappningstabell *Krav → Linked Art-uttryck → EDM-fält*. Utgå från LA:s krav per endpoint (`@context`, `id`, `type`, `_label` rekommenderat, `identified_by` med Primary Name `aat:300404670`). Notera att LA:s mönster för "hemsida för objektet" (= isShownAt) är `subject_of` → `LinguisticObject` → `digitally_carried_by` → `DigitalObject` klassificerad *Web Page* (`aat:300264578`) med `access_point`.
- **Ref:** https://linked.art/api/1.0/shared/digital/ , https://linked.art/api/1.0/endpoint/physical_object/

### B5. Kap 4 Kortformer saknar själva kortformerna
Kapitlet beskriver principen men listar inga `_`-attribut, inga exempel på expansion och ingen referens till var de definieras.
- **Åtgärd:** Lägg till en tabell *kortform → expanderad form* med minst ett exempel per kortform. Ange språkkodstandard (BCP 47 / ISO 639) för suffixformen `text @code`. Förklara att nycklar som inte finns i kontexten ignoreras vid JSON-LD-expansion (vilket är anledningen till att andra konsumenter "inte kan expandera dem").

### B6. Icke-persistenta objekt och relativa URI:er (kap 5)
En godtycklig sträng som `id` (t.ex. `"id": "abc"`) tolkas av en JSON-LD-processor som en *relativ* IRI mot dokumentets bas-URI och kan därmed bli en fullständig kulturarvsdata-URI. I granskningsversionen har en mening lagts till som rekommenderar att utelämna `id` eller använda blank node-prefix `_:`.
- **Åtgärd:** Verifiera mot skördarens faktiska beteende (sätts `@base`? strippas icke-http-id:n?) och skriv fast regeln i skördningsspecifikationen.

---

## Medel prioritet

### B7. Metatyper ("types of types") – krav eller inte?
Linked Art kräver metatypen *Type of Work* (`aat:300435443`) på objektklassificeringar när den är känd, och *Brief Text* (`aat:300418049`) på statement-klassificeringar. Kap 10:s in-line-exempel använder `300435443`, men exemplet med kamfodral (ren AAT-referens) gör det inte. Kap 9-exemplet saknar `300418049`.
- **Åtgärd:** Besluta om K-samsök kräver, rekommenderar eller ignorerar metatyper, och gör exemplen konsekventa.
- **Ref:** https://linked.art/model/vocab/required/#classification-types

### B8. Licens-URI:er: `http` vs `https`, och etiketter
Dokumentet använder genomgående `http://creativecommons.org/...` (samma som Europeana och rightsstatements.org), medan Linked Art:s egna exempel använder `https://creativecommons.org/...`. Skördaren måste hantera båda.
- Kap 8 Metadata-exemplet sätter `_label: "Public Domain"` på CC0 – CC0 och Public Domain Mark är olika märkningar.
- Kap 8 Metadata-exemplet ger licensen `"type": "Type"` medan media-exemplet använder `Right`/`subject_to`-mönstret.
- **Åtgärd:** Ange kanonisk form (rekommendation: `http://`, i linje med Europeana) och normalisering i skördaren. Rätta etikett och typ i exemplet.

### B9. Rättighetsmodellen (kap 8) – omfattning och ordval
- "Rights Statements ... som godkända licenser": rightsstatements.org-märkningar är inte licenser; kalla dem rättighetsmärkningar.
- Ingen vägledning för `LinguisticObject` (text), ljud, 3D eller för `DigitalObject` som saknar `VisualItem`. Linked Art placerar rätten på *verket* (VisualItem/LinguisticObject), inte på bäraren – texten säger detta men bara med bildexempel.
- InC-OW-EU-stycket refererar till PRV/EUIPO-registrering; verifiera aktuell process. Länken `http://www.creativecommons.se` bör kontrolleras.
- Rättighetsmodellen beskriver enbart 4.0 – klargör hur äldre CC-versioner hanteras i vokabulären (Network of Terms listar bara 4.0).

### B10. `language` – vad exakt är kravet?
Kap 9 och 10 säger att `language` är ett krav för "textfält"/"namn". Oklart om det gäller `Name.content`, `LinguisticObject.content`, `Identifier` (rimligen inte) och `_label` (rimligen inte). Linked Art rekommenderar dessutom `notation` (språkkod) på `Language`-referenser; inget exempel i dokumentet har det, trots att kap 5 tillåter `notation` i referenser.
- **Åtgärd:** Precisera kravet per attribut och lägg till `notation` i språkexemplen. Överväg LA-regeln "högst ett primärt namn per språk".

### B11. Network of Terms – vad, var, hur
Tjänsten nämns i kap 10 och 11 utan länk. Network of Terms är NDE:s (nederländska) verktyg; det bör framgå att det är RAÄ:s instans, med URL, och hur en datapartner slår upp och mappar termer mot den.

### B12. Scheme för kulturarvsdata-URI:er under `/resurser/`
Kap 5 säger att scheme alltid är `https` för skördade resurser; kap 11 listar auktoritets-URI:er under `http://kulturarvsdata.se/resurser/aukt/...`. Klargör kanonisk form för auktoriteter/vokabulärer respektive skördade resurser, och hur `http`/`https` jämställs.

### B13. Kap 12 Beskrivning av dataset
Hela kapitlet är preliminärt. Behöver: val av DCAT-AP-SE-version, mappning till attributen i listan, samt om datasetet även ska uttryckas som Linked Art `Set` (klassificerad *Collection* `aat:300025976`) för att kunna refereras via `member_of` från objekten.

### B14. Versionsangivelser
Ange vilken version av Linked Art (Model 1.0 / API 1.0) och CIDOC CRM (≥ 7.1 krävs för `P199 represents_instance_of_type`) som K-samsök 2 följer, samt versionspolicy för `raa.json`.

### B15. Tomma och motsägande avsnitt
- Kap 1 Introduktion är tom.
- Kap 9 "Fritext beskrivning" är tom (hör ihop med B1).
- Kap 3 säger att dokumentationen "endast beskriver leverans, ej konsumtion" men innehåller ett avsnitt om `Content-Type` vid konsumtion. Besluta om scope.

---

## Låg prioritet

### B16. Externa filreferenser
`../../api/index.md`, `../exempel/id.md`, `Terminologi.md`, `namn.md`, `kortformer.md`, `referenser.md`, `../krav_gen/RightsStatement.md` – dokumentet verkar vara sammanslaget från flera filer. I granskningsversionen har länkarna till avsnitt som numera finns i samma dokument pekats om till interna ankare (`#ref`, `#namn`, `#kortformer`, `#beskrivningar`, `#rättighetsmodell`). Verifiera att övriga relativa länkar finns i målrepot.

### B17. Terminologi och konsekvens
- "objekt" används om JSON-nod, post och kulturarvsresurs; "typ" om både `type` och `classified_as`. En kort ordlista (Terminologi.md?) skulle hjälpa.
- Etiketter i exemplen varierar: "preferred terms" / "Primära termer" / "Primary Name" för samma AAT-term. Harmonisera (kosmetiskt, i kod – ej ändrat).
- "K-samsök 2", "K-samsök 2.0" och "K2" används omväxlande.

### B18. Exemplet "Arumbayafetisch"
Identifieraren `978-0-416-83450-5` är ett ISBN, inte ett accessionsnummer; Linked Art har en egen term för ISBN (`aat:300417443`). Byt till ett realistiskt accessionsnummer (kosmetiskt, i kod – ej ändrat).

---

## Verifierat mot Linked Art – ingen åtgärd behövs
Följande i dokumentet stämmer med gällande Linked Art-dokumentation (kontrollerat 2026-09-22):
- Kontext-URL `https://linked.art/ns/v1/linked-art.json` och media-typ `application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"`.
- Referensdefinitionen: `id` + `type` obligatoriska, `_label` rekommenderat, `equivalent` och `notation` valfria.
- Rättigheter uttrycks med `subject_to` → `Right` klassificerad med licens-URI, placerad på `VisualItem` (verket), inte på bäraren.
- `represents`, `represents_instance_of_type` (CRM P199) och `about` på `VisualItem`.
- `digitally_shows`, `format` på `DigitalObject`; `member_of` → `Set`.
- Samtliga AAT-koder i kap 9 (namn- och identifierartyper), `aat:300435416` (description), `aat:300215302` (digital image), `aat:300389336` (svenska), `aat:300435443` (type of work).

---

## Status efter omstruktureringen (v0.6)

### Åtgärdat
- **B3** – Syntaxfelen i JSON-exemplen är rättade (kap 3, 5 och 7). Automatisk validering i ett dokumentationsbygge saknas fortfarande.
- **B5** – Delvis: kortformerna `_primaryName`, `_description` och `_classifications` är dokumenterade i kap 10 utifrån modellreferensen. Exempel på expansion och språkkodstandard saknas.
- **B15** – Delvis: kap 1 har innehåll. Tomma avsnitt är markerade som **Utkast**.
- **B16** – Alla interna länkar pekar nu på sidor i `docs/`.

### Nya iakttagelser

#### N1. Attributnamn för proveniens skiljer sig mellan exempel, text och modell (Hög)
Exemplen använder `recordProvenance` och `source_record`, råmaterialets text `sourceRecord` och `ingested_at`, medan modellreferensen har `record_provenance`, `sourceRecord` och `ingestedAt`. `about`, som exemplet anger som autogenererat, finns inte i modellreferensens `RecordProvenance`. Markerat som öppen fråga i kap 5. Hänger ihop med B2.

#### N2. `member_of` för medlemskap i `Set` (Hög)
Exemplen i kap 3 använder `member_of` från `HumanMadeObject` och `Person` till ett `Set`. I modellreferensen finns `member_of` bara på `Actor` (medlemskap i grupp), medan `CRMEntity` har `member_of_set`. Linked Art använder `member_of` för båda. Verifiera mot `raa.json` och skördaren.

#### N3. Avvikelser i de typspecifika kraven (Medel)
- `is_subject_of` finns inte i modellen och har tolkats som `subject_of` i kap 4 (hänger ihop med B1).
- `Activity` förekom två gånger i listan över icke-persistenta händelser. Dubbletten är borttagen.
- Europeana-listans *visualised_by* (isShownBy) är inte ett attribut i modellen.

#### N4. Förutsättningar för `possessed_by` (Medel)
Kravet på `possessed_by` för InC, InC-EDU och CC BY-licenser saknar förklaring och exempel. Vad ska anges, och varför inte för InC-OW-EU?

#### N5. Exempel med enbart Linked Arts `@context` (Låg)
Exemplet i kap 7 anger bara Linked Arts kontext, medan kap 2 kräver båda. En kommentar har lagts till under exemplet. Exemplet har inte ändrats.

#### N6. Material som saknas för en användarvänlig dokumentation (Medel)
- Introduktionstext för startsidan (se `assets/prioriterade_underlag.txt`).
- Skillnader mellan K-samsök 1 och K-samsök 2, med konsekvensbeskrivning.
- Hur en skördning startas och följs upp i det administrativa gränssnittet.
- URL till Network of Terms och vägledning för uppslag av termer (B11).
- Kompletta exempelposter för vanliga typer av objekt.
