# volta.codes

Statische Marketing-/Landingpage für volta.codes, eine Berliner Agentur für maßgeschneiderte Software und KI-Lösungen. Bewusst "no build": alles steckt in einer einzigen `index.html`. Betreiber: Dominik Bretsch und Simon Hufeisen (GmbH i. Gr.).

## Aktueller Stand

Die Website ist inhaltlich und technisch überarbeitet. Acht Sektionen (Hero, Warum volta.codes, Für wen wir bauen, Was wir machen, Wie wir arbeiten, Was unsere Software auszeichnet, Die Gründer, Kontakt). Farbrhythmus: hell → hell → blau → hell → dunkel → hell → hell → dunkel.

Texte sind aus dem HTML in `content/site.json` ausgelagert und werden per `fetch()` geladen. Inline-Formatierung über `**bold**` und `==highlight==`. Die `==`-Syntax steuert den Highlight-Pool: pro Sektion werden beim Scrollen 2 zufällige Marks angezeigt, die erst verschwinden wenn die Sektion komplett aus dem Viewport gescrollt ist.

Impressum als Modal (Footer-Button), HRB-Nummer steht noch aus.

## Nächste Schritte

- HRB-Nummer im Impressum-Modal nachtragen (`index.html`, Modal-Div)
- `content/site.json` und `index.html` gemeinsam deployen (JSON muss auf dem Server liegen, `file://` reicht nicht)
- Ggf. Analytics einbinden

## Technisches / Setup

**Repo:** `/Users/ziply/Projekte/volta.codes`

**Git:** https://github.com/Polartag/volta

**Vorschau:** `python3 -m http.server` im Projektverzeichnis, dann auf `localhost:8000` öffnen. Alternativ `index.html` direkt im Browser.

**Aufbau:** Einzige Datei `index.html` mit inline `<style>` und inline `<script>`. Kein Build-Schritt, kein Package Manager, kein Framework.

**Konventionen** (siehe `CLAUDE.md` im Repo):
- Neue Sektionen folgen dem bestehenden `.split`-Pattern
- Keine neuen Observer-Patterns einführen
- User-sichtbarer Text auf Deutsch, Ton "sober, confident, no fluff"

## Entscheidungen

- **Single-File-Ansatz:** HTML, CSS und JS in einer Datei, bewusst ohne Framework oder Build-Tooling. Reduziert Komplexität für ein reines Marketing-Dokument.
- **Impressum als Modal:** Kein eigener Seitenbereich, um den visuellen Fluss der Seite nicht zu unterbrechen.

## Logbuch

### 2026-05-05

Große Überarbeitungs-Session: Inhalte in `content/site.json` ausgelagert (`==highlight==`-Syntax für randomisierte Marks). Seitenstruktur auf 8 Sektionen erweitert, alte Pakete-Sektion entfernt. Design-Iteration: Ghost-Zahlen, Punkt-Marker, Glow-Effekt ausprobiert und wieder verworfen. Finale Lösung: animierte `<mark>`-Highlights, 2 zufällig pro Sektion, verschwinden erst wenn Sektion komplett außer Sicht. Firefox-Kompatibilität gefixt. Dot-Animation auf sauberen Farbwechsel reduziert.

### 2026-05-02

Vault-Datei und Repo-Datei zu einer einheitlichen `projekt.md` zusammengeführt nach festgelegten Konventionen. Datei lebt physisch im Repo, Vault bekommt Symlink.

Vorausgegangene Website-Session: CLAUDE.md aktualisiert (Design-Token-Tabelle, Sektionsübersicht, Observer-Details ergänzt, irrelevanten Tailwind-Workflow-Block entfernt). Impressum als Modal mit Footer-Button implementiert.

### 2026-04-19

Projekt-Root nach `/Users/ziply/Projekte` konsolidiert (neue Konvention).
