# Polaris 2.0 Hub

Die öffentliche Website von **Polaris Client 2.0**: Home, Skin Gallery, Themes, Crosshairs, Ressourcen, Plugins, Community, Profile, Leaderboard, News, Changelog, Downloads, Dokumentation, Support, Bug Reports, Vorschläge, Konto und Admin Panel.

## Aufbau

- Statische Single-Page-App ohne Build-Schritt (`index.html`, `hub.css`, `hub.js`), Hash-Routing (`#/skins`, `#/item/<id>`, `#/profiles/<kirka-id>`, `#/u/<name>`).
- **Snapshot-Modus:** Ohne erreichbares Backend zeigt der Hub den Stand aus `data/content.json`. Die Datei wird im Hauptrepository mit `node scripts/hub-snapshot.js` aus einem laufenden Polaris-Backend erzeugt und dann hierher committet. Der Hub sagt im Footer offen, dass er einen Snapshot zeigt.
- **Live-Modus:** Ist in den Site-Einstellungen (`site.apiUrl`) eine öffentliche **https**-Adresse des Polaris-Backends hinterlegt und erreichbar, lädt der Hub Live-Daten. Dann gehen Registrierung, Anmeldung, Bewertungen, Favoriten, Kommentare, Einreichungen, Bug Reports, Vorschläge und der Download-Verlauf.
- **Admin Panel (`#/mod`):** Nur sichtbar für Konten mit der Rolle `moderator` oder `admin`. Die Rollen vergibt ausschließlich der Owner über die signierte Owner-API. Jede Aktion wird **serverseitig** gegen Rolle und Berechtigungen geprüft und protokolliert. Das Ausblenden des Buttons ist keine Sicherheitsmaßnahme.
- Profilstile (Titel, Abzeichen, Farbverläufe) stammen aus der Polaris-Datenbank und sind nur in Polaris und diesem Hub sichtbar. Original-Kirka.io-Profile werden nicht verändert.
- Im Code liegen keine Schlüssel oder Tokens.

## Veröffentlichung

`.github/workflows/pages.yml` veröffentlicht bei jedem Push auf `main` über GitHub Pages.

## Lokal testen

```bash
python3 -m http.server 8000      # im Hub-Ordner, dann http://localhost:8000
node test/run-e2e.js             # im Monorepo: Snapshot- und Live-Modus (Chromium via Playwright)
HUB_URL=https://… node test/run-e2e.js   # gegen eine veröffentlichte URL
```
