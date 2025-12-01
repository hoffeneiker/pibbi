# Klangunterstützung für Urinkontrollen

PISSHILFE ist eine kleine Webanwendung, die durch Wasser- und Flüssigkeitsgeräusche Menschen bei Urinkontrollen unterstützt – insbesondere im Kontext von Suchterkrankungen und/oder schüchterner Blase (Paruresis).

Die Oberfläche kombiniert bewusst eine verspielte Retro-Optik (Windows‑95-/Netscape-Vibes) mit einem fachlich ernst gemeinten, einfühlsamen Text.

------

## Ziel der Anwendung

Urinkontrollen sind in der Suchthilfe und -therapie verbreitet, werden von vielen Betroffenen jedoch als:

- emotional belastend,
- schambesetzt,
- stark mit Druck- und Versagensängsten verbunden

erlebt – insbesondere, wenn das Wasserlassen unter Beobachtung stattfinden muss oder eine sogenannte „schüchterne Blase“ (Paruresis) vorliegt.

PISSHILFE möchte in dieser Situation helfen, indem:

- Wasser-/Pinkelgeräusche als „klangliche Unterstützung“ bereitgestellt werden,
- innere Anspannung reduziert,
- der Fokus sanft nach innen verlagert,
- und Blockaden beim Wasserlassen etwas gelockert werden können.

------

## Features

- 12 klickbare Bild-Buttons (PNG mit transparentem Hintergrund)
- 12 zugehörige Audio-Dateien (`.m4a`) mit Wasser-/Pinkelgeräuschen
- Zufällige Zuordnung bei jedem Seitenaufruf:
  - Icons werden im Grid neu gemischt
  - Sounds werden neu den Icons zugeordnet
- Weiches Crossfading:
  - Wechsel zwischen Sounds wird überblendet (kein harter Cut)
- Fallback-Mechanismus:
  - Wenn der Web Audio API-Pfad scheitert, werden HTML-Audio-Elemente verwendet
- Mobile-Unterstützung:
  - AudioContext wird nach erstem Touch aktiviert (Browser-Sicherheitsvorgaben)
- Retro-UI:
  - Fensterrahmen, Titelzeile, farbige Statusbar
  - Comic-Neue-Schriftart
  - Ernsthafter, psychologisch sensibler Einleitungstext

------

## Live-Nutzung

Die Webanwendung ist als reine HTML/CSS/JS-Seite konzipiert:

1. `index.html` im Browser öffnen (am besten über einen simplen Webserver, z. B. GitHub Pages oder irgendeinen statischen Hoster).
2. Die Icons anklicken/tippen, um Sounds abzuspielen.
3. Auf Mobilgeräten:
  - Evtl. benötigt der Browser einen ersten Tipp irgendwo auf die Seite, um Audio zu erlauben.
  - Danach funktionieren die Bild-Buttons wie gewohnt.

Es wird keinerlei Backend, Build-Prozess oder zusätzliche Runtime benötigt.

------

## Projektstruktur

Erwartete Struktur im Repository:

```

.
├─ index.html
├─ sounds/
│ ├─ sound1.m4a
│ ├─ sound2.m4a
│ ├─ ...
│ └─ sound12.m4a
└─ images/
  ├─ piss1.png
  ├─ piss2.png
  ├─ ...
  └─ piss12.png
```

- `index.html`: komplette App (Markup, Styling, Logik)
- `sounds/`: Audio-Dateien mit Wasser-/Pinkelgeräuschen
- `images/`: PNG-Icons, die als „Buttons“ dienen

Die Dateinamen (`sound1.m4a` – `sound12.m4a`, `piss1.png` – `piss12.png`) sind im JavaScript fest verdrahtet.

------

## Funktionsweise (technisch kurz)

- HTML:
  - Ein zentrales „Fenster“ (`.screen-frame`) mit Titelzeile, Einleitungstext, Button-Grid und Statusbar.
- CSS:
  - Grid-Layout für die Buttons
  - Responsive Anpassung auf schmalen Screens (3 Spalten statt 4)
  - Hover-/Active-Effekte: Icons werden größer und etwas heller
- JavaScript:
  - Web Audio API:
    - Laden der 12 Sounds in Buffer (`AudioContext.decodeAudioData`)
    - Crossfading mittels `GainNode`
  - Fallback über `<audio>`-Elemente, falls Buffer nicht verfügbar
  - Fisher–Yates-Shuffle, um:
    - eine zufällige Reihenfolge der Bild-Icons zu erzeugen
    - eine zufällige Reihenfolge/Zuordnung der Sounds zu erzeugen
  - Mobile-Hack:
    - Erster `touchstart` resümiert den `AudioContext`, falls dieser noch im `suspended`-State ist.

------

## Verwendung im Browser

- Repository klonen oder herunterladen

- Sicherstellen, dass:

  - `index.html` vorhanden ist,
  - `sounds/` und `images/` wie oben beschrieben befüllt sind.

- ```
 index.html
 ```

 über einen Webserver ausliefern (z. B.:

  - GitHub Pages,
  - Netlify,
  - irgendein anderer statischer Webhoster,
  - oder lokaler Dev-Server deiner Wahl).

Viele Browser blockieren Audios von `file://`-URLs oder handhaben CORS bei direktem Dateiöffnen restriktiv – deshalb ist ein „echter“ Webkontext sinnvoll.

------

## Hinweise zur Gestaltung / Inhalt

- Die Oberfläche ist visuell leicht, verspielt und retro – die Texte sind bewusst seriös und einfühlsam formuliert.
- Der Einleitungstext richtet sich direkt an die nutzende Person und:
  - benennt Scham, Druck und Blockaden,
  - ermutigt zur Selbstfürsorge,
  - setzt das Tool in einen sensiblen Kontext (Urinkontrolle bei Suchterkrankungen).

------

## Sicherheit & Datenschutz

- Reine Frontend-Anwendung: keine Datenspeicherung, kein Login, kein Tracking im Code.
- Alle Ressourcen (Bilder, Sounds) werden statisch vom Webserver geladen.
- Es werden keine personenbezogenen Daten erfasst oder übertragen (sofern nicht durch das Hosting-Setup ergänzt).

------

## Lizenz

```
Dieses Projekt steht unter der GNU General Public License Version 3 (GPL-3.0).

Das bedeutet insbesondere:
- Du darfst den Code ausführen, untersuchen, verändern und weitergeben.
- Wenn du veränderte Versionen oder abgeleitete Werke veröffentlichst oder verteilst, müssen diese ebenfalls unter der GPL-3.0 stehen (Copyleft).
- Der Quellcode muss zugänglich gemacht werden, wenn du das Programm verbreitest.

Den vollständigen Lizenztext findest du in der Datei `LICENSE` in diesem Repository oder online bei der Free Software Foundation:
https://www.gnu.org/licenses/gpl-3.0.html

Copyright (c) 2025 Dein Name
```