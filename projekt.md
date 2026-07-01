# volta.codes

Statische Marketing-/Landingpage für volta.codes, eine Berliner Agentur für maßgeschneiderte Software und KI-Lösungen. Bewusst "no build", ohne Framework: die Startseite ist eine einzige `index.html`, ergänzt um eine eigenständige Projektseite `projekte.html`. Betreiber: Dominik Bretsch und Simon Hufeisen (volta.codes GmbH).

## Aktueller Stand

Die Website ist inhaltlich und technisch überarbeitet. Acht Sektionen (Hero, Warum volta.codes, Für wen wir bauen, Was wir machen, Wie wir arbeiten, Was unsere Software auszeichnet, Die Gründer, Kontakt). Farbrhythmus: hell → hell → blau → hell → dunkel → hell → hell → dunkel.

Seit 2026-06-30 gibt es eine zweite Seite **`projekte.html`** (eigenständig, gleicher Stil/Tokens, von der Nav verlinkt). Sie stellt drei Projekte im Zickzack-Layout vor — **FAMOS** (Fallmanagement- und Organisationssoftware), **VoxDrop** (Dokumente barrierefrei via KI-Agenten, extern auf voxdrop.live verlinkt) und den **KI-Krisenassistenten** (Bevölkerungsschutz). Inhalte als `projekte`-Block in `content/site.json`, gerendert per `fetch()` wie die Startseite. Pro Projekt ein web-optimiertes Bild in `img/projekte/`; beim KI-Krisenassistenten zwei transparent freigestellte Mobile-Screens. Klick vergrößert das jeweilige Bild an Ort und Stelle (kein Overlay); pro Projekt leuchten beim Scrollen 2 von 3 `==`-Markierungen zufällig auf.

Texte sind aus dem HTML in `content/site.json` ausgelagert und werden per `fetch()` geladen. Inline-Formatierung über `**bold**` und `==highlight==`. Die `==`-Syntax steuert den Highlight-Pool: pro Sektion werden beim Scrollen 2 zufällige Marks angezeigt, die erst verschwinden wenn die Sektion komplett aus dem Viewport gescrollt ist.

Schriften (Space Grotesk) werden seit 2026-06-11 **lokal** aus `fonts/` ausgeliefert; die frühere Live-Einbindung von Google Fonts wurde entfernt (DSGVO). Die Seite lädt damit keinerlei Drittanbieter-Ressourcen mehr, setzt keine Cookies und kein Tracking — ein Cookie-Banner ist nicht nötig.

Die Sektion „Die Gründer" zeigt seit 2026-06-16 ein **Gründer-Foto** (S/W, self-hosted in `img/gruender.jpg`, web-optimiert ~165 KB, `loading=lazy`; content-getrieben über `gruender.foto` in `content/site.json`).

Impressum als Modal (Footer-Button); seit 2026-06-15 mit **Handelsregister** (Amtsgericht Charlottenburg, HRB 288375B). Seit 2026-06-11 zusätzlich eine **Datenschutzerklärung** als zweites Modal (Footer-Button „Datenschutz" neben „Impressum"). **Rechtlich offen:** ggf. USt-IdNr.; Datenschutztext und Registerdaten sollten noch rechtlich gegengeprüft werden. Hosting läuft auf GitHub Pages (USA) — im Spannungsverhältnis zur eigenen „Daten in Deutschland"-Positionierung.

## Nächste Schritte

- **Datenschutzerklärung vorhanden** (Modal seit 2026-06-11, Footer-Button „Datenschutz"): deckt Verantwortlicher, Server-Logs/IP (Art. 6 Abs. 1 lit. f), Hosting GitHub Pages USA (Drittlandtransfer / Data Privacy Framework), Kontaktaufnahme per E-Mail, Betroffenenrechte und den Hinweis „keine Cookies/kein Tracking, Schriften lokal" ab. Offen nur noch die rechtssichere Endabnahme (siehe letzter Punkt).
- **Impressum vervollständigen** (`content/site.json` → `impressum`): Registergericht + HRB ✓ (Amtsgericht Charlottenburg, HRB 288375B, 2026-06-15); offen: USt-IdNr. nach § 27a UStG (falls vorhanden), möglichst Telefonnummer als zweiter Kontaktweg (EuGH-Rechtsprechung zur „unmittelbaren Kommunikation").
- **Hosting prüfen:** GitHub Pages (USA) passt nicht zur Datenschutz-Positionierung; Migration auf EU-/DE-Hosting erwägen (vgl. Vault-Notiz zur volta.codes-Migration).
- Falls Analytics gewünscht: nur cookielos/self-hosted, um den No-Cookie-Banner-Vorteil zu erhalten.
- Rechtssichere Endabnahme von Impressum-Registerdaten und Datenschutztext idealerweise anwaltlich bzw. per seriösem Generator gegenprüfen.
- Optional: kompakter **Teaser-Block auf der Startseite**, der zur Projektseite führt (bewusst vertagt). Weitere Projekte lassen sich als Einträge im `projekte`-Block in `content/site.json` ergänzen.

## Technisches / Setup

**Repo:** `/Users/ziply/Projekte/volta.codes`

**Git:** https://github.com/Polartag/volta

**Vorschau:** `index.html` direkt im Browser öffnen. Falls ein lokaler Server nötig ist, vorher in Mission Control einen freien Utility-Port reservieren; `8000` ist fest für Sentinel reserviert.

**Aufbau:** `index.html` (Startseite) und `projekte.html` (Projektseite), jeweils mit inline `<style>` und inline `<script>`. Kein Build-Schritt, kein Package Manager, kein Framework. Beide laden ihre Texte per `fetch()` aus `content/site.json` — für die lokale Vorschau daher ein kleiner Server nötig (`file://` blockiert das `fetch`). Projektbilder liegen in `img/projekte/` (FAMOS/VoxDrop als JPEG/PNG, die zwei Krisenassistent-Phones als transparente WebP).

**Schriften:** Space Grotesk als self-hosted Variable Font in `fonts/` (woff2, `latin` + `latin-ext`), eingebunden per `@font-face` im inline `<style>`. Keine Google-Fonts-Einbindung mehr (DSGVO). Nicht wieder per `<link>` auf `fonts.googleapis.com`/`fonts.gstatic.com` umstellen.

**Hosting:** GitHub Pages (Repo `Polartag/volta`, Branch `main`, CNAME `volta.codes`), Server-Header `GitHub.com` → liegt in den USA.

**Konventionen** (siehe `CLAUDE.md` im Repo):
- Neue Sektionen folgen dem bestehenden `.split`-Pattern
- Keine neuen Observer-Patterns einführen
- User-sichtbarer Text auf Deutsch, Ton "sober, confident, no fluff"

## Entscheidungen

- **Single-File-Ansatz:** HTML, CSS und JS in einer Datei, bewusst ohne Framework oder Build-Tooling. Reduziert Komplexität für ein reines Marketing-Dokument.
- **Impressum als Modal:** Kein eigener Seitenbereich, um den visuellen Fluss der Seite nicht zu unterbrechen.
- **Projekte als eigene Unterseite** (2026-06-30): `projekte.html` statt einer weiteren Sektion auf der Startseite — mehr Raum pro Projekt (großes Bild, Klick-Zoom), ohne den Single-Page-Fluss der Startseite zu stören. No-Build bleibt: zweite statische Datei, gleiche Tokens/Fonts, Inhalte in `content/site.json`.

## Logbuch

### 2026-07-01

**Bug-Fix: Kontakt-Link auf der Projektseite.** Der Nav-Button „Kontakt" zeigte auf
`index.html#kontakt`; weil die Startseite ihre Inhalte per `fetch()` nachlädt, verspringt der
Anker beim Laden und man landet nicht beim Kontakt. Fix: Der Projektseiten-Footer
(„Sprechen wir."-Block) bekam `id="kontakt"`, der Nav-Link zeigt jetzt auf den lokalen Anker
`#kontakt`. Via PR [#2](https://github.com/Polartag/volta/pull/2). Außerdem Doku-Korrektur:
„Aktueller Stand" und „Nächste Schritte" zum Datenschutz nachgezogen — die Erklärung existiert
als zweites Modal bereits seit 2026-06-11, war in der projekt.md aber noch als fehlend vermerkt.

### 2026-06-30

**Projektseite `projekte.html` gebaut** (neue Unterseite, von der Nav verlinkt). Drei Projekte:
FAMOS, VoxDrop (extern, verlinkt auf voxdrop.live) und KI-Krisenassistent. Eigener
`projekte`-Block in `content/site.json`, gerendert per `fetch()` wie die Startseite, gleiche
Tokens/Fonts (DSGVO: keine Drittanbieter-Ressourcen). Zickzack-Layout, große web-optimierte
Bilder in `img/projekte/` (FAMOS/VoxDrop quer; KI-Krisenassistent als **zwei transparent
freigestellte Mobile-Screens** — aus dem Pitch-HTML in 2× gerendert, runde Alpha-Maske,
`drop-shadow` folgt der Phone-Form). Bilder per Klick **an Ort und Stelle** vergrößerbar (kein
Overlay), beim Krisenassistenten jeder Screen einzeln. Pro Projekt 2 von 3 randomisierte
`==`-Highlights beim Scrollen (Mechanik der Startseite, Subline bleibt schlicht). FAMOS-Lead
mit gezieltem Soft-Hyphen (`Schwangerschafts-konfliktberatung`). Bulk-Stand lag bereits auf
`main` (`f7241eb`); finale Politur (Highlights, stärkerer Zoom, Trennung) via PR
[#1](https://github.com/Polartag/volta/pull/1) → Squash-Merge `05628ab`, live über GitHub Pages.

### 2026-06-26

Logo-Punkt-Abstand korrigiert (im Zuge des CI-Baukastens, Repo `volta-ci`). Das Nav-Logo
(`.logo-dot`) bekam einen kleinen optischen Margin (Punkt klebte font-natürlich an „volta"),
und `img/volta_codes_v6.png` (von der CDN-E-Mail-Signatur genutzt) wurde aus der korrigierten
Logo-Geometrie neu gerendert (Punkt saß zu nah an VOLTA). Committet (`5c7b954`) + nach `main`
gepusht → GitHub Pages + jsdelivr aktualisiert. Verbindliche Logo-Geometrie liegt jetzt im
CI-Paket (`/Users/ziply/Projekte/volta-ci`) bzw. Figma „Volta-Logo".

### 2026-06-16

**Gründer-Foto** in die Sektion „Die Gründer" eingebaut (S/W-Studioporträt der beiden Gründer). Self-hosted in `img/gruender.jpg`, von 2,47 MB/3092px auf **165 KB/1500px** web-optimiert (`sips`), `loading=lazy`, 2px-Ecken, Alt-Text. Content-getrieben über neues Feld `gruender.foto` in `content/site.json` + konditionale Render-Zeile/CSS in `index.html`. Lokal auf Mobile + Desktop gerendert/geprüft, dann committet + via GitHub Pages deployt. Full-res-Original liegt lokal als `img/gruender-original.jpg` (nicht im Repo).

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
