# Kortformer

För att göra det lättare för datapartners stödjer vi användandet av _shortforms_: ett anpassat/skräddarsytt(??) uttryck (struket: a harvest-time-only) som expanderas till den fullständinga kanoniska/korrekta (??) Linked ART-formen när en post skördas. 

Kortformsattribut(??) har prefixet `_` för att markera dem som RAA transport conveniences(??), inte kanoniska Linked Art-attribut(?).

Partners kan använda de här attributen i inskickade poster men poster som visas upp(??) av RAÄ kommer alltid att använda den expanderade kanoniska formen. Notera också att om du skapar en endpoint(??) som kommer eller kan användas av andra användare än RAÄ:s K2-sköradare bör du inte använda kortformer eftersom andra inte kommer att kunna expandera dem. 

Kortformer bör inte användas tillsammans med sin expanderade motsvarighet i samma objekt. Om det expanderade värdet redan är tillgängligt kommer kortformsvärdet att ignoreras för det objektet. (Objekt = post här??) Om en kortform inte kan tolkas på ett otvetydigt sätt kommer posten fortfarande att accepteras och (men??) kortformen kommer att utelämnas från den expanderade formen/kommer inte att expanderas(??). 

Kortformer i strängar som stödjer angivande av språk anväder suffixformen `text @code`. Tolkningen av `@`som en språktagg händer bara om den föregås av ett mellanrum och avslutar en sträng. Till exempel, `"Ben Hur @en"` betyder att texten `Ben Hur` är på engelska; `"Ben Hur@en"` betraktas som enbart text. 

Okända språkkoder ignoreras.

## Shortforms

As a convenience for data providers, we support the use of the _shortforms_: a harvest-time-only
custom expression that is expanded to the full canonical Linked ART form when the record is
harvested.

Shortform fields are prefixed with `_` to mark them as RAA transport conveniences, not canonical
Linked Art properties.

Providers may use these fields in submitted records, but records exposed by
RAÄ will always use the expanded canonical form. Note also: if you are creating an endpoint that
will or may be exposed to other consumers than RAÄ's K2 harvester, you should not use shortforms as
other consumers will not recognize them.

Shortforms should not be used together with their expanded counterpart on the same object. If the
expanded value is already present, the shortform value is ignored for that object. If a shortform
cannot be interpreted unambiguously, the record is still accepted and the shortform is left out of
the expanded form.

String shortforms that support language use the suffix form `text @code`. The `@` is interpreted as
a language tag only when it is preceded by whitespace and appears at the end of the string. For
example, `"Ben Hur @en"` means text `Ben Hur` in English; `"Ben Hur@en"` is treated as literal text.
Unknown language codes are ignored.