# 2. Serialisering

Det här kapitlet beskriver hur information uttrycks tekniskt vid utbyte med K-samsök.

## JSON-LD

Poster till och från K-samsök serialiseras som **[JSON-LD](https://json-ld.org/)**. Ett [OpenAPI-schema](../api/README.md#openapi-schema) beskriver dokumentstrukturen, så att posterna även kan hanteras med vanliga JSON-verktyg.

När data hämtas från K-samsök kan det i framtiden finnas andra svarsformat, beroende på vilket API som anropas och vilka `Accept`-headers som anges vid API-anrop eller URI-upplösning.

## JSON-LD-kontext (`@context`)

Varje rotobjekt ska innehålla både [Linked Arts `@context`](https://linked.art/ns/v1/linked-art.json) och [K-samsöks `@context`](https://kulturarvsdata.se/resurser/linkedart/v1/raa.json). Det första fältet i varje rotobjekt ser därför alltid ut så här:

```json
{
    "@context": [
      "https://linked.art/ns/v1/linked-art.json",
      "https://kulturarvsdata.se/resurser/linkedart/v1/raa.json"
    ]
    ✂️ …
}
```

Nästlade objekt (objekt som inte är rotobjekt) behöver inte ha `@context`, så länge de inte inför termdefinitioner utöver dem som finns i de två kontexterna ovan.

> [!IMPORTANT]
> JSON-LD tillåter att `@context` anges i en HTTP-header ("out of band"). K-samsök kräver ändå att `@context` anges i själva dokumentet, både i data som levereras och i data som hämtas.

## Medietyp (`Content-Type`) och `profile`

### Vid skördning

K-samsök inför vissa grammatiska specialiseringar vid skördning, till exempel [kortformer](10-kortformer.md). Därför används en annan `profile` för skördningsanrop än för Linked Art-API:et. Läs mer i [skördningsspecifikationen](../api/README.md#specifikation).

### Vid hämtning från K-samsök

När K-samsöks Linked Art-API anropas sätts `Content-Type` [i enlighet med Linked Art](https://linked.art/api/1.0/json-ld/#media-type) till:

```
application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"
```
