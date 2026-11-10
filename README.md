# Minuvo-Website

Statische Seiten für App Store und TestFlight: Startseite, Hilfe (DE/EN), Datenschutzerklärung (DE/EN), Impressum.
Reines HTML und CSS, kein Build-Schritt, kein JavaScript, keine Cookies, keine externen Quellen (Schrift liegt in
`fonts/`). Entwurf von Claude, 2026-11-10. **Nicht veröffentlicht.**

| Datei | Inhalt |
|---|---|
| `index.html` | Startseite: Name, Versprechen, vier Funktionen, „Bald im App Store / TestFlight“ |
| `support.html` | Hilfe, Deutsch oben, Englisch unter `#en` |
| `datenschutz.html` | Datenschutzerklärung (maßgeblich) |
| `privacy.html` | Privacy Policy (Übersetzung) |
| `impressum.html` | Impressum nach § 5 DDG |
| `style.css` | Farben aus `Shared/Theme/MinuvoTheme.swift`, hell und dunkel über `prefers-color-scheme` |
| `fonts/` | Plus Jakarta Sans (Regular, SemiBold, ExtraBold) aus `Resources/Fonts`, mit `OFL.txt` |
| `img/app-icon.png`, `img/app-icon-dark.png` | App-Icon, 256 px, aus `Resources/AppIcon.icon` mit `ictool` (Icon Composer) exportiert |

## Vor dem Veröffentlichen

1. Platzhalter ersetzen: `grep -n "&lt;" site/*.html` zeigt alle Stellen (Anschrift, E-Mail-Adresse). In
   `support.html` steht die Adresse zweimal im `mailto:`-Link.
2. In `datenschutz.html` und `privacy.html` den Abschnitt „Diese Website“ prüfen: Angaben zu GitHub (Anschrift,
   Data Privacy Framework) vor dem Veröffentlichen auf Aktualität prüfen.
3. Lokal ansehen: `open site/index.html` (alle Links sind relativ und funktionieren auch ohne Server).

## Veröffentlichen mit GitHub Pages (Janek)

**Empfehlung: ein eigenes, öffentliches Repo nur mit dem Inhalt von `site/`.** Gründe:
- GitHub Pages auf dem Haupt-Repo würde das ganze Repo öffentlich machen müssen (interne Doku, Übergabe, Code).
- Pages für private Repos gibt es nur mit einem bezahlten GitHub-Plan.

Schritte:

1. Auf github.com ein neues **öffentliches** Repo anlegen, Name **`minuvo`** (dann passen die URLs in
   `docs/apple/app-store-angaben.md` ohne Änderung). Andere Namen gehen auch, z. B. `minuvo-site`; dann ändert sich
   der Pfad (siehe unten).
2. Den **Inhalt** von `site/` (nicht den Ordner selbst) in dieses Repo kopieren, ohne diese `README.md` oder mit ihr,
   beides geht:
   ```
   mkdir ~/minuvo-web && cp -R site/ ~/minuvo-web/ && cd ~/minuvo-web
   git init -b main && git add . && git commit -m "Website"
   git remote add origin https://github.com/<github-user>/minuvo.git && git push -u origin main
   ```
3. Im Repo: Settings → Pages → „Build and deployment“ → Source „Deploy from a branch“, Branch `main`, Ordner `/ (root)`
   → Save. Nach ein bis zwei Minuten ist die Seite online.
4. Optional eine leere Datei `.nojekyll` anlegen (dann verarbeitet GitHub die Dateien nicht mit Jekyll; hier nicht
   nötig, schadet aber nicht).
5. Alle URLs im Browser öffnen, dann in App Store Connect eintragen.

Ergebnis (Repo `minuvo`):

| Seite | URL |
|---|---|
| Start (Marketing-URL) | `https://<github-user>.github.io/minuvo/` |
| Hilfe (Support-URL) | `https://<github-user>.github.io/minuvo/support.html` (englisch: `…/support.html#en`) |
| Datenschutz (DE) | `https://<github-user>.github.io/minuvo/datenschutz.html` |
| Privacy (EN) | `https://<github-user>.github.io/minuvo/privacy.html` |
| Impressum | `https://<github-user>.github.io/minuvo/impressum.html` |

Bei Repo-Namen `minuvo-site` steht `minuvo-site` statt `minuvo` im Pfad. Mit eigener Domain (Settings → Pages →
Custom domain) ersetzt sie `https://<github-user>.github.io/minuvo`.

**Änderungen später:** Hier in `site/` ändern, dann in das Website-Repo kopieren und pushen. Ändert sich, was die App
an Daten verarbeitet, zuerst `datenschutz.html` und `privacy.html` anpassen (Datum „Stand“ ändern) und das
Datenschutzetikett in App Store Connect.

## Schrift

Die Schrift liegt lokal in `fonts/` (selbst gehostet), damit beim Aufruf keine Daten an Google gehen. Google Fonts wäre
technisch möglich, müsste dann aber in der Datenschutzerklärung stehen; deshalb nicht genutzt. Lizenz: SIL Open Font
License 1.1 (`fonts/OFL.txt`), muss mit veröffentlicht werden.
