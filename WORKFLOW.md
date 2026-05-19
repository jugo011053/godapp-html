# GodApp HTML – Spielplatz mit Regeln

## Zweck

Dieses Repository enthält die Single-File-HTML-Version der GodApp.

`main` bleibt die stabile Version, die über GitHub Pages auf dem iPhone genutzt wird.

Entwicklung passiert in getrennten Branches, damit zwei parallele Chats nicht dieselbe Datei gleichzeitig ruinieren. Kleine Gnade für alle Beteiligten.

---

## Branches

### `main`

Stabile Live-Version.

- Wird von GitHub Pages ausgespielt.
- Nur getestete Änderungen hier hinein mergen.
- Nicht direkt für Experimente nutzen.

### `workflow-a-timeline-core`

Workflow A: Timeline/Core.

Zuständig für:

- Timeline-Block-Modell
- Prioritäten
- Lock-Logik
- Konfliktlösung
- Drag & Drop-Regeln
- Wochenansicht
- wiederkehrende Termine
- Platzierung von Anforderungen in der Timeline

Darf NICHT primär bearbeiten:

- Rezeptdatenbank
- Shoppinglist-Details
- Trainingsübungsdatenbank
- große Profilseiten-Optik

### `workflow-b-meals-training`

Workflow B: Meals/Training/Profile.

Zuständig für:

- Rezeptfilter
- MealMode: Standard, Diät, Masse
- Allergien / No-Gos
- Einkaufsliste
- Packungsgrößen
- Shake- und Snacklogik
- Trainingsprofile
- Übungsdatenbank
- Profil-/Onboarding-Felder

Darf NICHT bearbeiten:

- `buildTimeline()`
- `renderWeekView()`
- `wcDown()` / `wcMove()` / `wcUp()`
- Drag & Drop Kernlogik
- Konfliktresolver / Timeline-Prioritätslogik

---

## Gemeinsame Schnittstellen

Meal und Training sollen nicht final den Tag planen.

Sie liefern Anforderungen:

```js
{
  type: 'prep',
  title: 'Meal Prep',
  preferredDate: 'YYYY-MM-DD',
  durationMin: 90,
  shortDurationMin: 45,
  priority: 3,
  source: 'meal'
}
```

```js
{
  type: 'training',
  title: 'Push Training',
  preferredDate: 'YYYY-MM-DD',
  durationMin: 60,
  shortDurationMin: 40,
  priority: 4,
  source: 'training'
}
```

Die Timeline entscheidet später:

- wann der Block wirklich liegt
- ob Kurzmodus nötig ist
- was verschoben wird
- was locked ist
- was bei Konflikten passiert

---

## Mini-Schritt-Regel

Jeder Chat macht maximal 5 kleine Schritte, dann wird zusammengeführt.

Ein Mini-Schritt soll dokumentieren:

1. Welche Funktionen geändert wurden
2. Welche Datenstruktur geändert wurde
3. Was getestet werden muss
4. Ob Merge-Konflikte zu erwarten sind

---

## Merge-Regel

1. Nie beide Workflows direkt auf `main` entwickeln.
2. Erst Branch A prüfen.
3. Dann Branch B prüfen.
4. Konflikte in `index.html` manuell bewusst lösen.
5. Erst danach nach `main` mergen.
6. Danach iPhone-Link testen:

```text
https://jugo011053.github.io/godapp-html/
```

---

## Aktueller Stand

Ausgangspunkt:

- Single-File-App: `index.html`
- GitHub Pages aktiv auf `main` + root
- Live-Link: `https://jugo011053.github.io/godapp-html/`
- Entwicklungsbranches:
  - `workflow-a-timeline-core`
  - `workflow-b-meals-training`
