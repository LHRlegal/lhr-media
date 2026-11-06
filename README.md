# lhr-media

Bilder für das Magazin auf lhr-law.de (Beitragsbilder, Anlagen) und der Worker `lhr-media`, der Bilder kurzzeitig im Netz ausliefert.

## Zwei Teile, nicht verbunden

| Teil | Wo | Was |
|---|---|---|
| **Bildablage** | dieses Repo | Fertige Beitragsbilder als PNG. Reine Ablage, kein Build, kein Deploy. |
| **Bild-Host** | Cloudflare Worker `lhr-media` (Konto Service+lhr@daro.de) | Nimmt Bilder per Upload an und liefert sie unter `/m/<key>` aus. |

Es gibt keine Automatik zwischen beiden: Ein Commit hier lädt nichts in den Worker, und der Worker schreibt nichts ins Repo.

## Aufbau des Repos

- `magazin/<JJJJ-MM>/`: Beitragsbilder je Monat der Veröffentlichung. Dateiname `<slug>-v<N>-<stil>-620x326.png` (Stile bisher `klassisch`, `hingucker`, `illustration`, `grafik`). Zu einem Beitrag gibt es meist eine deutsche und eine englische Variante (englischer Slug).
- `2026/10/`: ältere Bilder aus Oktober, Größen `620x326` und `1240x652` (doppelte Auflösung), dazu einzelne Anlagen.
- Commit-Nachricht: `Magazin <slug-des-beitrags>`.

## Der Worker `lhr-media`

- Adresse: `https://lhr-media.service-lhr.workers.dev`
- `GET /m/<key>`: liefert das Bild (Cache 1 Tag, `X-Content-Type-Options: nosniff`). Unbekannter Schlüssel: 404.
- `PUT /upload/<dateiname>` mit `Authorization: Bearer <UPLOAD_TOKEN>` und passendem `Content-Type`: speichert das Bild und antwortet mit `url` und `key`.
  - Erlaubt: `image/png`, `image/jpeg`, `image/webp`, höchstens 10 MB.
  - Der Schlüssel wird aus Zeitstempel und bereinigtem Dateinamen gebildet.
- **Bilder verfallen nach 30 Tagen** (KV-Ablauf). Dauerhaft liegen sie nur in diesem Repo. Für Magazinbeiträge deshalb die Bilder nach WordPress hochladen und nicht auf eine `/m/`-Adresse verlinken.
- Alle anderen Pfade: 404 mit Text `LHR Media`.

### Bindungen und Secrets (nur Namen)

| Name | Art |
|---|---|
| `MEDIA` | KV-Namespace (Bilder mit Ablauf und Metadaten) |
| `UPLOAD_TOKEN` | Secret, Bearer-Token für den Upload |

Der Wert von `UPLOAD_TOKEN` steht nie im Repo. Er liegt im Cloudflare-Dashboard (Worker `lhr-media`, Einstellungen).

### Deploy

Der Worker-Quellcode liegt **nicht** in diesem Repo. Er wurde per API hochgeladen (letzte Änderung 13.10.2026, „Secret Change“). Solange der Code nicht hier liegt, gibt es keinen Git-Deploy und keinen Build-Check. Siehe `STAND.md`.

## Regeln

- Keine Mandantendaten und keine Secrets in Bilder oder Dateinamen.
- Arbeitsweise wie in allen LHR-Repos: eigener Branch im Worktree, PR, Squash-Merge auf `main`, `STAND.md` und `CHANGELOG.md` nachziehen.
