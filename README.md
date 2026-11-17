# Opmeten

Digitaal opmeetformulier voor de werf, gemaakt voor gebruik op de gsm. Het vervangt het papieren
formulier (sleufnr, meters, boordstenen, berm, bitumen, + diepe, stab, beton, stutten,
opbinden kabel, droogzuiging, verv. grond, EAN).

## Wat het doet
- Per opmeting: DNW, datum, gemeente, straat, fase, aannemer en een notitie.
- Per sleuf de hoeveelheden per post, met automatisch de totalen.
- **Posten** zijn aan te passen: naam, eenheid, volgorde, toevoegen en verwijderen.
- **CSV-export** (puntkomma, komma als decimaal, opent zo in Excel en Google Sheets).
  Bestandsnaam: `datum_uur_opmeting-DNW-straat.csv`.
- **Delen**: stuurt een leesbare samenvatting met de CSV als bijlage via mail, WhatsApp en zo verder.
- **Back-up** (JSON) om alles naar een ander toestel over te zetten.

Gegevens worden enkel lokaal op het toestel bewaard (browseropslag).

## Gebruik
Open `index.html` in de browser. Het is één bestand, er is geen installatie nodig.
