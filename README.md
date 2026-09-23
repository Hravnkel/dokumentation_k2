# Teknisk dokumentation av K-samsök

Placeholder för den tekniska dokumentationen av K-samsök 2.0. Denna skall migreras till https://github.com/riksantikvarieambetet när dokumentationen är färdig att publiceras. 

Endast öppet för pull-requests från utvecklarteamet av K-samsök i skrivande stund. 

## Struktur

- **[`docs/`](docs/README.md)** – den sammanställda dokumentationen. Börja på [startsidan](docs/README.md).
  - `informationsmodell/` – informationsmodellens kapitel, ändringslogg, backlog och arkiverade versioner
  - `api/` – skördnings-API
  - `exempel/` – exempelbank
  - `referens/` – modellreferens (kopia av den autogenererade `assets/modell/InformationModelDiagram.md`)
  - `ordlista.md`
- **`assets/`** – råmaterial och arbetsanteckningar.

## Redaktionella konventioner

- Sidor som inte är färdiga markeras med rutorna `> [!NOTE]`/`> [!WARNING]` och orden **Utkast** eller **Öppen fråga**, så att de går att söka fram.
- Kravnivåer uttrycks med *ska*, *ska inte*, *bör* och *kan* (se [Introduktion](docs/informationsmodell/01-introduktion.md#kravnivåer)).
- JSON-exempel markeras med ` ```json ` och ändras bara för att rätta syntax.
