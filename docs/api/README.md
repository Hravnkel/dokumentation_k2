# Skördnings-API

K-samsök 2 skördar data från datapartner via ett API. Den här sidan hänvisar till de tekniska specifikationerna.

## OpenAPI-schema

Ett [OpenAPI](https://www.openapis.org)-schema som beskriver skördnings-API:et och informationsmodellen finns på:

<https://k2.kulturarvsdata.se/resurser/linkedart/openapi/1.0/>

Schemat finns i två versioner:

| Version | Innehåll | Så hämtar du den |
|---|---|---|
| Standard | Enbart skördnings-API:et | Anropa adressen ovan utan parametrar. |
| Fullständig | Skördnings-API:et och hela informationsmodellen | Lägg till parametern `full=true`. |

> [!TIP]
> Det fullständiga schemat är stort och kan ta lång tid att läsa in i vissa klienter.

## Specifikation

Specifikationen för skördnings-API:et finns på:

<https://k2.kulturarvsdata.se/resurser/linkedart/v1/api/doc>

Där beskrivs bland annat vilken medietyp och `profile` som används vid skördning (se även [Serialisering](../informationsmodell/02-serialisering.md#medietyp-content-type-och-profile)).
