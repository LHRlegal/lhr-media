# lhr-media

Bilddateien für die Magazinbeiträge auf lhr-law.de/magazin (Titelbilder, Grafiken). Eine Datei pro Beitrag und Größe, abgelegt nach Monat.

## Aufbau

| Pfad | Inhalt |
|---|---|
| `2026/10/`, `magazin/2026-10/`, `magazin/2026-11/` | PNG-Bilder je Beitrag |
| `.claude/settings.json` | erlaubt den Magazin-Läufen den Abruf von rv.hessenrecht.hessen.de (Rechtsprechung) |

Namensschema: `<beitrags-slug>-<variante>-<breite>x<höhe>.png`, z. B. `kuendigungsbutton-login-bgh-v5-grafik-620x326.png`. Varianten: `v1-klassisch`, `v3-illustration`, `v4-hingucker`, `v5-grafik`. Englische (`…-zh-…` chinesische) Fassungen tragen den englischen Slug. Standardgröße 620×326, Titelbild 1240×652.

## Deploy

Kein Deploy. Das Repo ist nur Ablage. Die Beiträge selbst entstehen mit dem Skill `lhr-magazinbeitrag` und werden in WordPress veröffentlicht. Wie die Bilder von dort aus eingebunden werden, ist hier nicht dokumentiert (offen, siehe `STAND.md`).

## Secrets

Keine. Keine Zugangsdaten ins Repo legen.
