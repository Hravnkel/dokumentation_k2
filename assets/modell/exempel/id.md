# Exempel: Identitet (id)


## <a id="id_1"></a> Persistenta rotobjekt med icke-persistenta underobjekt

I exemplet nedan har rotobjektet (`Person`) ett persistent kulturarvsdata-id, och ett av underobjekten (`Name`) är icke-persistent, vilket signaleras via avsaknaden av ett `id` på `Name`-instansen. 

```
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : {
	  "type" : "Name",
	  "content" : "Harald Blåtand",
	  "language" : {
  	   ✂️ …	    
	  }
	}
	✂️ …
	
}
```

Exemplet nedan visar en variation av ovan, där icke-persistensen hos `Name`-objektet istället signaleras via att ett `id` anges som inte är en http(s) URI. Detta mönster tillåts i RAÄ's Linked Art-profil av bakåtkompatibilitetsskäl. Det generellt rekommenderade mönstret är dock att utelämna `id`-attributet helt på icke-persistenta objekt. RAÄ garanterar inte att angivna icke-persistenta id:n kommer att behållas. 

```
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : [{
	  "type" : "Name",
	  "id" : "_hbtnamn"
	  "content" : "Harald Blåtand",
	  "language" : {
  	   ✂️ …	    
	  }
	}]
	✂️ …
	
}
```

## <a id="id_2"></a> Persistent rotobjekt med både icke-persistenta (anonyma) och persistenta underobjekt

Exemplet nedan visar ett persistent `Person`-objekt där underobjektet `Name` är icke-persistent. En referens till ett persistent objekt anges i `Name`-objektets `language`-attribut.

```
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"identified_by" : [{
	  "type" : "Name",
	  "content" : "Harald Blåtand",
	  "language" : {
  	   "id" : "http://vocab.getty.edu/aat/300389336",
	   "type" : "Language",
	   "_label" : "svenska"
	  }]
	}
	✂️ …
	
}
```

Exemplet nedan visar ett persistent `Person`-objekt som deklareras som medlem i en persistent kollektion (`Set`). Kollektionen är i detta fall inte en referens, eftersom det innehåller fler attribut än `id`, `type` och `_label`.

```
{
	✂️ …
	"id" : "https://kulturarvsdata.se/exem/pel/hbt",
	"type" : "Person",
	✂️ …
	"member_of" : {
	  "type" : "Set",
	  "id" : "https://kulturarvsdata.se/exem/pel/vikingar",
	  "_label" : "Kollektionen 'Kända vikingar'",
	  "title" : [✂️ …],
	  "about" : [✂️ …],
	  ✂️ …  
	}
	✂️ …	
}
```

## <a id="prov"></a> URI-mönster för `RecordProvenance`-objektets id

@@@TODO

## <a id="vi"></a> URI-mönster för `VisualItem`-objektets id

@@@TODO
