# Serialiseringsformat

Huvudserialiseringsformatet för poster in och ut hos K-samsök är **[JSON-LD](https://json-ld.org/)**. Ett [OpenAPI schema](../../api/index.md#openapi-schema) definierar dokumentstrukturen för kompatibilitet med generiska JSON-ramverk.

Vid konsumtion från K-samsök kan i framtiden även andra anpassade svarsformat förekomma hos utdata, beroende på vilket API man anropar och vilka `Accept` headers som anges vid API-anrop eller URI-upplösning.

## JSON-LD context

Rot-JSON-LD objekten ska innehålla både [Linked Arts `@context`](https://linked.art/ns/v1/linked-art.json) och [K-samsöks `@context`](https://kulturarvsdata.se/resurser/linkedart/v1/raa.json). Det betyder att det första fältet i varje rotobjekt alltid ser ut så här: 

```
{
    "@context": [
      "https://linked.art/ns/v1/linked-art.json",
      "https://kulturarvsdata.se/resurser/linkedart/v1/raa.json"
    ]
    ✂️ …
}
```

Nestade objekt (icke-rotobjekt) behöver inte innehålla `@context`-fältet under förutsättningen att objektet inte introducerar termdefinitioner bortom de som ingår i de två ovanstående kontexterna.

Obs att medan JSON-LD tillåter att `@context` kan förekomma som en http-header ("out of band"), kräver K-samsök för både in- och utdata att `@context` explicit anges i dokumentinnehållet.


## `Content-Type` och `profile` vid konsumtion

När K-samsöks LinkedArt API anropas sätts `Content-Type` [i linje med Linked Art](https://linked.art/api/1.0/json-ld/#media-type) till strängen `application/ld+json;profile="https://linked.art/ns/v1/linked-art.json"`.

## `Content-Type` och `profile` vid skördning

Eftersom K-samsök introducerar vissa grammatiska specialiseringar vid skördning används en annan `profile` för skördnings-requests. Läs mer om detta i [skördningsspecifikationen](../../api/index.md#specifikation). 
