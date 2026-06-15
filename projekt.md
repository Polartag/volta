# volta.codes

Statische Marketing-/Landingpage für volta.codes, eine Berliner Agentur für maßgeschneiderte Software und KI-Lösungen. Bewusst "no build": alles steckt in einer einzigen `index.html`. Betreiber: Dominik Bretsch und Simon Hufeisen (volta.codes GmbH).

## Aktueller Stand

Die Website ist inhaltlich und technisch überarbeitet. Acht Sektionen (Hero, Warum volta.codes, Für wen wir bauen, Was wir machen, Wie wir arbeiten, Was unsere Software auszeichnet, Die Gründer, Kontakt). Farbrhythmus: hell → hell → blau → hell → dunkel → hell → hell → dunkel.

Texte sind aus dem HTML in `content/site.json` ausgelagert und werden per `fetch()` geladen. Inline-Formatierung über `**bold**` und `==highlight==`. Die `==`-Syntax steuert den Highlight-Pool: pro Sektion werden beim Scrollen 2 zufällige Marks angezeigt, die erst verschwinden wenn die Sektion komplett aus dem Viewport gescrollt ist.

Schriften (Space Grotesk) werden seit 2026-06-11 **lokal** aus `fonts/` ausgeliefert; die frühere Live-Einbindung von Google Fonts wurde entfernt (DSGVO). Die Seite lädt damit keinerlei Drittanbieter-Ressourcen mehr, setzt keine Cookies und kein Tracking — ein Cookie-Banner ist nicht nötig.

Impressum als Modal (Footer-Button); seit 2026-06-15 mit **Handelsregister** (Amtsgericht Charlottenburg, HRB 288375B). **Rechtlich offen:** ggf. USt-IdNr.; eine **Datenschutzerklärung fehlt komplett**. Hosting läuft auf GitHub Pages (USA) — im Spannungsverhältnis zur eigenen „Daten in Deutschland"-Positionierung.

## Nächste Schritte

- **Datenschutzerklärung erstellen** (Art. 13 DSGVO) und als eigenen, klar benannten Link neben dem Impressum einbinden — Pflicht, fehlt aktuell ganz. Inhalte: Verantwortlicher, Server-Logs/IP (Art. 6 Abs. 1 lit. f), Hosting GitHub Pages USA (Drittlandtransfer / Data Privacy Framework), Kontaktaufnahme per E-Mail, Betroffenenrechte, Speicherdauer, Hinweis „keine Cookies/kein Tracking, Schriften lokal".
- **Impressum vervollständigen** (`content/site.json` → `impressum`): Registergericht + HRB ✓ (Amtsgericht Charlottenburg, HRB 288375B, 2026-06-15); offen: USt-IdNr. nach § 27a UStG (falls vorhanden), möglichst Telefonnummer als zweiter Kontaktweg (EuGH-Rechtsprechung zur „unmittelbaren Kommunikation").
- **Hosting prüfen:** GitHub Pages (USA) passt nicht zur Datenschutz-Positionierung; Migration auf EU-/DE-Hosting erwägen (vgl. Vault-Notiz zur volta.codes-Migration).
- Falls Analytics gewünscht: nur cookielos/self-hosted, um den No-Cookie-Banner-Vorteil zu erhalten.
- Rechtssichere Endabnahme von Impressum-Registerdaten und Datenschutztext idealerweise anwaltlich bzw. per seriösem Generator gegenprüfen.

## Technisches / Setup

**Repo:** `/Users/ziply/Projekte/volta.codes`

**Git:** https://github.com/Polartag/volta

**Vorschau:** `index.html` direkt im Browser öffnen. Falls ein lokaler Server nötig ist, vorher in Mission Control einen freien Utility-Port reservieren; `8000` ist fest für Sentinel reserviert.

**Aufbau:** Einzige Datei `index.html` mit inline `<style>` und inline `<script>`. Kein Build-Schritt, kein Package Manager, kein Framework.

**Schriften:** Space Grotesk als self-hosted Variable Font in `fonts/` (woff2, `latin` + `latin-ext`), eingebunden per `@font-face` im inline `<style>`. Keine Google-Fonts-Einbindung mehr (DSGVO). Nicht wieder per `<link>` auf `fonts.googleapis.com`/`fonts.gstatic.com` umstellen.

**Hosting:** GitHub Pages (Repo `Polartag/volta`, Branch `main`, CNAME `volta.codes`), Server-Header `GitHub.com` → liegt in den USA.

**Konventionen** (siehe `CLAUDE.md` im Repo):
- Neue Sektionen folgen dem bestehenden `.split`-Pattern
- Keine neuen Observer-Patterns einführen
- User-sichtbarer Text auf Deutsch, Ton "sober, confident, no fluff"

## Entscheidungen

- **Single-File-Ansatz:** HTML, CSS und JS in einer Datei, bewusst ohne Framework oder Build-Tooling. Reduziert Komplexität für ein reines Marketing-Dokument.
- **Impressum als Modal:** Kein eigener Seitenbereich, um den visuellen Fluss der Seite nicht zu unterbrechen.

## Logbuch

### 2026-06-15

Impressum um die **Handelsregister-Angabe** ergänzt: „Amtsgericht Charlottenburg, HRB 288375B" (neues Feld `handelsregister` in `content/site.json`, konditionale Render-Zeile im Impressum-Modal von `index.html`). Damit ist die GmbH-Pflichtangabe nach § 5 DDG erfüllt. Offen bleiben USt-IdNr. und die Datenschutzerklärung. Committet + via GitHub Pages deployt.

### 2026-06-11

Google Fonts entfernt und Space Grotesk self-hosted ausgeliefert (`fonts/`, Variable Font, woff2 `latin` + `latin-ext`). Grund: Live-Einbindung von Google Fonts überträgt Besucher-IPs ohne Einwilligung an Google — abmahnfähiger DSGVO-Verstoß (LG München I, 3 O 17493/20). Fix committet (`d13313f`), gepusht, live verifiziert (0 Google-Requests, Optik identisch). Gleiche Umstellung in `angebot-famos.html` (nicht in Git). Allgemeine Self-Hosting-Regel global verankert (`~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`).

Anschließend Compliance-Check der Website: lädt keine Drittanbieter-Ressourcen, keine Cookies, kein Tracking (kein Cookie-Banner nötig), Kontakt nur per `mailto`. Offene Pflicht-Punkte unter „Nächste Schritte" dokumentiert: fehlende Datenschutzerklärung, unvollständiges Impressum (HRB/USt-IdNr.), US-Hosting (GitHub Pages).

### 2026-06-01

Alten Vorschau-Hinweis auf `localhost:8000` entfernt, weil `8000` im Portplan Sentinel gehört. Die statische Seite wird direkt per Datei geöffnet oder bekommt bei Bedarf einen neu reservierten Utility-Port.

### 2026-05-05 (2)

Seite auf GitHub gepusht. Repo: https://github.com/Polartag/volta, Branch `main`. CNAME `volta.codes` war bereits im Remote vorhanden. Alte Upload-History in der Git-History behalten (merge mit `--allow-unrelated-histories`). Alle Texte ab sofort ausschließlich über `content/site.json` editierbar.

### 2026-05-05

Große Überarbeitungs-Session: Inhalte in `content/site.json` ausgelagert (`==highlight==`-Syntax für randomisierte Marks). Seitenstruktur auf 8 Sektionen erweitert, alte Pakete-Sektion entfernt. Design-Iteration: Ghost-Zahlen, Punkt-Marker, Glow-Effekt ausprobiert und wieder verworfen. Finale Lösung: animierte `<mark>`-Highlights, 2 zufällig pro Sektion, verschwinden erst wenn Sektion komplett außer Sicht. Firefox-Kompatibilität gefixt. Dot-Animation auf sauberen Farbwechsel reduziert.

### 2026-05-02

Vault-Datei und Repo-Datei zu einer einheitlichen `projekt.md` zusammengeführt nach festgelegten Konventionen. Datei lebt physisch im Repo, Vault bekommt Symlink.

Vorausgegangene Website-Session: CLAUDE.md aktualisiert (Design-Token-Tabelle, Sektionsübersicht, Observer-Details ergänzt, irrelevanten Tailwind-Workflow-Block entfernt). Impressum als Modal mit Footer-Button implementiert.

### 2026-04-19

Projekt-Root nach `/Users/ziply/Projekte` konsolidiert (neue Konvention).
