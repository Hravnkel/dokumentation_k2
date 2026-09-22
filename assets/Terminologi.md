# Terminologi

## <a id="referens"></a>Referens

En länk till ett annat objekt. Se [Referenser](./modell/monster/referenser.md).

## <a id="schema"></a>Schema

Ett [OpenAPI](https://www.openapis.org) schema som beskriver skörde-API:et samt informationsmodellen. 

Schemat finns tillgängligt på addressen [https://k2.kulturarvsdata.se/resurser/linkedart/openapi/1.0/](https://k2.kulturarvsdata.se/resurser/linkedart/openapi/1.0/).

Notera att schemat finns i två versioner: en som endast definierar skörde-API:et, och en som definierar både skörde-API:et och hela informationsmodellen. Det sistnämnda schemat är stort och kan ta lång tid att ladda i klienter. 

Som default returneras det förstnämnda mindre schemat. Det kompletta schemat erhålls genom att i anropet ange requestparametern `full` med värdet `true`. 



