# Teknisk dokumentation för K-samsök 2

> [!WARNING]
> **Utkast.** Dokumentationen är under arbete och kan ändras utan föregående meddelande. Avsnitt som ännu inte är färdiga är markerade med **Utkast** eller **Öppen fråga**.

K-samsök är Riksantikvarieämbetets (RAÄ) tjänst för att samla, länka och tillgängliggöra information om kulturarv från många olika organisationer. I K-samsök 2 beskrivs all information med en gemensam informationsmodell som bygger på [Linked Art](https://linked.art/), och informationen utbyts som [JSON-LD](https://json-ld.org/).

Dokumentationen beskriver hur du som datapartner strukturerar, märker upp och levererar data till K-samsök 2.

> [!NOTE]
> **Utkast – introtext.** En mer utförlig introduktion till K-samsök (bakgrund, syfte och användningsområden) ska skrivas. Underlag kan eventuellt hämtas från dokumentationen för K-samsök 1.

## Vem vänder sig dokumentationen till?

| Du är … | … och vill | Börja här |
|---|---|---|
| **Informationsförvaltare** eller samlingsansvarig | förstå vad som krävs av er data och hur den ska klassificeras | [Introduktion till informationsmodellen](informationsmodell/01-introduktion.md) |
| **Utvecklare** som bygger en export eller mappning | veta exakt hur en post ska se ut i JSON-LD | [Kom igång](kom-igang.md) |
| Redan insatt och vill **slå upp** en detalj | hitta krav, attribut eller en term | [Krav på attribut](informationsmodell/04-krav-pa-attribut.md), [Modellreferens](referens/modellreferens.md), [Ordlista](ordlista.md) |

## Dokumentationens delar

- **[Kom igång](kom-igang.md)** – en översikt över stegen från befintlig data till en skördningsbar datamängd.
- **[Informationsmodellen](informationsmodell/README.md)** – principer, krav och modelleringsmönster. Detta är dokumentationens huvuddel.
- **[Skördnings-API](api/README.md)** – OpenAPI-schema och specifikation för skördning.
- **[Exempelbank](exempel/README.md)** – samtliga exempel i dokumentationen samlade på ett ställe.
- **[Modellreferens](referens/modellreferens.md)** – autogenererad förteckning över alla klasser och attribut i RAÄ:s Linked Art-profil.
- **[Ordlista](ordlista.md)** – begrepp som används i dokumentationen.
- **[Ändringslogg](informationsmodell/changelog.md)** – vad som har ändrats mellan versioner.

## Skillnader mot K-samsök 1

> [!NOTE]
> **Utkast.** Här ska det finnas en sammanställning av skillnaderna mellan K-samsök 1 och K-samsök 2 i mappningen, med en beskrivning av vilka konsekvenser ändringarna får för datapartner.
