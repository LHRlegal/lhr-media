# Stand

06.11.2026

## Läuft

- Bildablage im Repo (Magazin-Beitragsbilder, 38 Dateien).
- Worker `lhr-media` live, antwortet auf `GET /` mit 404 und Text `LHR Media` (so im Code vorgesehen).

## Offen

- Worker-Quellcode fehlt im Repo (nur live im Konto Service+lhr@daro.de). Sollte als `src/index.js` mit `wrangler.toml` und Workers Builds ins Repo geholt werden. Dafür den Code aus dem Live-Worker exportieren und gegen die ausgelieferte Version prüfen, nicht aus dem Gedächtnis nachbauen.
- Der Worker setzt nur `X-Content-Type-Options`. Die übrigen Sicherheits-Header laut Arnos Regel (HSTS, CSP, X-Frame-Options, Referrer-Policy, Permissions-Policy) fehlen. `workers.dev` ist nicht von der Cloudflare-Regel für lhr-law.de erfasst. An Helfer-Agent 03 (Sicherheits-Header) gemeldet.
- Wer lädt Bilder in den Worker hoch und wofür (Magazin oder Mandanten-Anlagen)? Bisher nicht dokumentiert, beim Magazin-Chat nachfragen.

## Bekannte Probleme

Keine.
