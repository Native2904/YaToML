# YaToML

Ein Total-Commander-Lister-Plugin (WLX) zum Anzeigen und Bearbeiten von
**YAML**- und **TOML**-Dateien als Baum-plus-Tabellen-Ansicht statt als
reinen Text.

YAML und TOML begegnen einem beim Durchstöbern von Ordnern öfter, als
man denkt – eine `docker-compose.yml` für ein Container-Setup, eine
`Cargo.toml` in einem Rust-Projekt, oder eine `pyproject.toml` für ein
Tool wie `ruff`. Mit diesem Plugin wirft man schnell einen Blick hinein
(und macht kleine Änderungen), ohne Total Commander zu verlassen oder
einen vollwertigen Editor aufzumachen.

## Funktionen

- **Grid-Ansicht**: Baum links (Struktur), Tabelle rechts (Key / Type /
  Value) zeigt die Kinder des ausgewählten Knotens — Klick auf eine
  Map/List-Zeile springt hinein, Doppelklick auf eine Wert-Zeile
  bearbeitet sie.
- **Inline-Bearbeitung**: Doppelklick oder F2 auf einem Skalarwert
  (String, Integer, Float, Bool, Datum/Zeit) öffnet ein Eingabefeld
  direkt in der Tabelle. Enter übernimmt, Escape verwirft.
- **Speichern (Strg+S)**: schreibt Änderungen als *Patch* zurück auf die
  Platte — nur die Bytes der tatsächlich geänderten Werte werden
  ersetzt. Kommentare und Formatierung im restlichen Dokument bleiben
  unangetastet.
  - **TOML**: vollständig unterstützt für alle Skalartypen, inklusive
    Datum/Zeit.
  - **YAML**: unterstützt für einzeilige Plain- und Quoted-Skalare (der
    Alltagsfall). Mehrzeilige Block-Werte (`|`, `>`) und Werte innerhalb
    von Flow-Strukturen (`{...}`/`[...]`) werden erkannt und mit
    Warnung sicher abgelehnt statt geraten — die Datei wird dabei nie
    beschädigt, diese einzelnen Werte werden nur (noch) nicht
    gespeichert.
  - Eine Pflicht-Verifikation parst das Ergebnis nach jedem Speichern
    erneut und bricht ab (schreibt nichts), falls etwas nicht wie
    erwartet aussieht.
- **Kontextmenü** (Rechtsklick oder Umschalt+F10/Menütaste): im Baum
  alles auf-/zuklappen, in der Tabelle Wert bearbeiten/Wert kopieren/
  Schlüssel kopieren, von einer Tabellenzeile zum zugehörigen
  Baum-Knoten springen, sowie Speichern.
- **Statusleiste**: zeigt den Breadcrumb-Pfad des ausgewählten Knotens
  sowie einen Hinweis auf ungespeicherte Änderungen.
- **Dark Mode**: optional, standardmäßig aus. Aktivierung über
  `yatoml.ini` (siehe unten) — unabhängig vom eigenen Farbschema von
  Total Commander.

## Installation

1. `yatoml.wlx64` (64-Bit) und/oder `yatoml.wlx` (32-Bit) in einen
   Ordner eigener Wahl kopieren.
2. In Total Commander: Konfiguration → Optionen → Plugins →
   Lister-Plugins → Konfigurieren → Hinzufügen, und die `.wlx64`/`.wlx`-
   Datei auswählen. Den Endungen `yaml`, `yml`, `toml` zuweisen (oder
   die automatische Erkennung von Total Commander übernehmen lassen).
3. Optional: `yatoml.ini` in denselben Ordner wie die Plugin-DLL legen,
   um Dark Mode zu aktivieren (siehe unten).

## Dark Mode

Nicht an das Farbschema von Total Commander gekoppelt. `yatoml.ini`
neben der Plugin-DLL anlegen oder bearbeiten:

```ini
[Settings]
DarkMode=1
```

`DarkMode=0` (oder gar keine Datei) behält die normale helle
Darstellung bei. Die Einstellung wird bei jedem Öffnen einer Datei neu
gelesen — kein Neustart nötig, einfach das Lister-Fenster schließen und
neu öffnen (oder die nächste Datei öffnen).

## Bekannte Einschränkungen

- YAML: mehrzeilige Block-Werte und Flow-Stil-Werte können angezeigt,
  aber noch nicht gespeichert werden (siehe oben) — eine klare Warnung
  erscheint, nichts wird beschädigt.
- Noch keine reine Textansicht (als zweiter Tab neben dem Grid geplant).
- YAML-Anchors/Aliase werden beim Laden transparent aufgelöst (gezeigt
  wird ihr fertiger Wert); die Alias-Beziehung selbst wird nicht
  angezeigt oder bearbeitet.

## Lizenz

MIT.
