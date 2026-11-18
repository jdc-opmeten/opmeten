# Formaat opmeting (POST bij "Einde meting")

De opmeet-app stuurt bij "Einde meting" een HTTP POST naar het adres in de link (`?srv=...`).
- `Content-Type: text/plain;charset=utf-8` (geen preflight; Apps Script leest `e.postData.contents`), body = JSON.
- `meting_id` is uniek per meting: de server moet dubbele zendingen negeren (de app probeert opnieuw tot de server `{"ok":true}` antwoordt).
- Antwoord van de server: JSON `{"ok":true}` (of `{"ok":false,"fout":"..."}`).

```json
{
  "versie": 1,
  "meting_id": "333-mwm1iz0j",
  "dnw": "333",
  "werf": "Straatnaam 1, Kontich",
  "datum": "2026-11-18",
  "tijd_start": "12:31",
  "tijd_einde": "13:05",
  "verstuurd_op": "2026-11-18T12:05:00.000Z",
  "sleuven": [
    {
      "nr": 1,
      "start":  { "lat": 51.158, "lng": 4.445 },
      "meetpunten": [ { "lat": 51.1581, "lng": 4.4451, "zijde": "Rechts" } ],
      "einde":  { "lat": 51.1584, "lng": 4.4454 },
      "zijde_begin": "Rechts",
      "zijde_einde": "Links",
      "meters": 12.5,
      "bovenbouw": "Asfalt",
      "leidingen": [ { "partij": "Fluvius", "type": "LS", "aantal": 2 } ],
      "bijzonderheden": ["Doorsteek"],
      "opmerking": "",
      "doorsteek": true,
      "doorsteek_segmenten": [ { "van": 2, "tot": 3, "meters_gps": 8 } ]
    }
  ]
}
```

Regels
- Een sleuf is een eigen lijn: teken `start` → `meetpunten` (in volgorde) → `einde`. Sleuven worden nooit met elkaar verbonden.
- `zijde`: "Links" | "Midden" | "Rechts" (kant van de weg, in looprichting).
- Doorsteek = twee opeenvolgende punten (start, meetpunten, einde in die volgorde, index 0 = start) met Links ↔ Rechts. `doorsteek_segmenten.van/tot` zijn indexen in die lijst; `meters_gps` is de GPS-afstand.
- `meters` is het meetwiel-getal (of `null`), niet de GPS-afstand.
- `einde` kan ontbreken niet: de app plaatst bij "Einde meting" nog een einde als een sleuf liep.
