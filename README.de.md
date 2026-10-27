[English](README.md) | [Русский](README.ru.md) | [Українська](README.uk.md) | **Deutsch**

# WARDOGS Potato-Grafik-Guide 🥔

Ultra-niedrige („Potato“-)Grafik für **WARDOGS**: Potato-Einstellungen im Spiel, eine Zeile in der `GameUserSettings.ini` und **LOD Bias** über den **NVIDIA Profile Inspector**.

**Kurz gesagt:** Potato-Einstellungen im Spiel → `sg.ShadowQuality=4` in der GameUserSettings.ini (schreibgeschützt) → NVIDIA Profile Inspector mit LOD Bias **+3**. Ergebnis: keine Schatten, deutlich weniger Vegetation und flache, detailarme Texturen.

*Zuletzt aktualisiert: 2026-10-27. Das Spiel bekommt weiterhin Updates, die Einstellungen können sich also ändern.*

![WARDOGS vorher und nachher mit Potato-Grafik](images/before-after.png)

*Der „Nachher“-Screenshot nutzt den maximalen LOD Bias von +15. Empfohlen ist +3 ([warum](#welchen-lod-bias-soll-ich-nehmen)).*

> ⚠️ **Nutzung auf eigene Gefahr.** Die Entwickler haben sich bisher nicht zum NVIDIA Profile Inspector geäußert und könnten ihn in Zukunft verbieten. Falls das passiert, mach alles rückgängig (siehe [Rückgängig machen](#rückgängig-machen)).

---

## Was du brauchst

* Eine **NVIDIA-Grafikkarte**. Der NVIDIA Profile Inspector funktioniert nur mit NVIDIA-Treibern. Die Schritte 1–2 funktionieren mit jeder Grafikkarte.
* **NVIDIA Profile Inspector** (NPI) vom offiziellen GitHub: https://github.com/Orbmu2k/nvidiaProfileInspector/releases
* Etwa 10 Minuten

---

## Schritt 1: Einstellungen im Spiel

Öffne die Grafikeinstellungen im Spiel und stelle alles wie unten ein. **Overall Quality** zeigt dann **Custom** an, das ist so gewollt.

*Die Namen der Einstellungen entsprechen der englischen Spieloberfläche.*

| Einstellung | Wert |
|:--|:--|
| **RESOLUTION QUALITY** | |
| Anti-Aliasing Method | NVIDIA DLSS |
| NVIDIA DLSS | DLAA |
| DLSS-G (DLSS Frame Generation) | Off |
| **GEOMETRY** | |
| Mesh Detail | Potato |
| Nanite Material Visibility Culling | Enabled |
| **ENVIRONMENT** | |
| View Distance | High |
| Shading | Potato |
| **LIGHTING** | |
| Global Illumination | Disabled |
| Shadows | Low *(Schritt 2 schaltet sie komplett ab)* |
| Reflections | Potato |
| **EFFECTS** | |
| Effects | Low |
| Particle Spawn Rate | Potato |
| **POST-PROCESSING** | |
| Post-Processing | Potato |
| Motion Blur | Disabled |
| Depth of Field | Disabled |
| Lens Flare | Disabled |
| Bloom | Disabled |
| **TEXTURES** | |
| World | Potato |
| Character | Potato |
| Effects | Potato |
| Texture Streaming | Potato |

**Übernimm die Einstellungen und schließe das Spiel komplett.** Schritt 2 musst du bei geschlossenem Spiel machen.

---

## Schritt 2: Schatten komplett abschalten (GameUserSettings.ini)

Im Menü ist Low die niedrigste Schattenstufe, über die Konfigurationsdatei geht es aber noch weiter.

1. Stelle sicher, dass WARDOGS **komplett geschlossen** ist. Bearbeite diese Datei nie, während das Spiel läuft.
2. Drücke **Win + R**, füge `%localappdata%\Wardogs\Saved\Config\WindowsClient` ein und drücke **Enter**.
3. **Mach ein Backup:** Kopiere die **GameUserSettings.ini** an einen sicheren Ort, z. B. auf den Desktop.
4. Öffne die **GameUserSettings.ini** im Editor, drücke **Strg + F** und suche nach `sg.ShadowQuality`.
5. Ändere die Zeile zu `sg.ShadowQuality=4`, speichere und schließe den Editor.
6. Rechtsklick auf **GameUserSettings.ini** → **Eigenschaften** → Haken bei **Schreibgeschützt** setzen → **OK**. So kann das Spiel deine Änderung nicht überschreiben.

> 💡 Solange die Datei schreibgeschützt ist, werden Änderungen im Einstellungsmenü des Spiels nicht gespeichert. Wenn du später etwas ändern willst: Schreibschutz entfernen → im Spiel ändern → Spiel schließen → Schritte 4–6 wiederholen.

---

## Schritt 3: NVIDIA Profile Inspector (LOD Bias)

LOD Bias zwingt das Spiel, detailärmere Versionen seiner Texturen zu verwenden. Texturen werden unschärfer und die Vegetation dünnt aus.

Lade NPI über den Link oben herunter, entpacke es und starte `nvidiaProfileInspector.exe`.

### Option A: fertiges Profil importieren (am einfachsten)

1. Lade eines dieser Profile herunter. Öffne die Datei und klicke auf **Download raw file**.
    * [`WARDOGS_potato_LOD3_balanced.nip`](profiles/WARDOGS_potato_LOD3_balanced.nip) (**empfohlen**, LOD Bias +3)
    * [`WARDOGS_potato_LOD15_max.nip`](profiles/WARDOGS_potato_LOD15_max.nip) (maximal Potato, LOD Bias +15, macht die Minimap unbrauchbar)
2. Klicke in NPI in der Werkzeugleiste auf **Import user defined profiles** und wähle die `.nip`-Datei.
3. Klicke auf **Apply changes** (oben rechts).

### Option B: manuell einrichten

1. Gib oben im Feld **Profiles** `WARDOGS` ein und wähle das Profil aus.
    * Kein WARDOGS-Profil vorhanden? Klicke auf **Create new profile** und nenne es `WARDOGS`. Klicke dann auf **Add application to current profile** und wähle `wardogsclient-win64-shipping.exe` aus dem Installationsordner des Spiels. In Steam findest du den Ordner per Rechtsklick auf WARDOGS → Verwalten → Lokale Dateien durchsuchen (Manage → Browse local files).
2. Ändere die drei Einstellungen aus der Tabelle unten. Du kannst den Wert aus der Dropdown-Liste wählen oder den Hex-Wert eintippen.
3. Klicke auf **Apply changes** (oben rechts).
4. Falls das Spiel lief, starte es neu.

| Einstellung | Wert | Hex |
|:--|:--|:--|
| Antialiasing - Transparency Supersampling | AA_MODE_REPLAY_MODE_ALL | `0x00000008` |
| Texture filtering - Driver Controlled LOD Bias | Off | `0x00000000` |
| Texture filtering - LOD Bias | +3 *(siehe unten)* | `0x00000018` |

Die ersten beiden Einstellungen sorgen dafür, dass der Treiber deinen LOD Bias überhaupt anwendet. Ohne sie bewirkt die dritte nichts.

---

## Welchen LOD Bias soll ich nehmen?

| LOD Bias | Hex | Ergebnis |
|:--|:--|:--|
| **+3** | `0x00000018` | **Empfohlen.** Guter Kompromiss zwischen Spielbarkeit und Vorteil. Die Minimap funktioniert weiterhin. |
| +4 bis +15 | — | ❌ Die Minimap wird unbrauchbar. |
| +15 | `0x00000078` | Maximal Potato. Das ist der „Nachher“-Screenshot. |

**Kurz gesagt: Nimm +3**, außer du kommst ohne Minimap klar.

---

## Rückgängig machen

* **NPI:** Profil WARDOGS auswählen → **Restore current profile to NVIDIA defaults** klicken → **Apply changes**.
* **Schatten:** Bei geschlossenem Spiel den Haken bei **Schreibgeschützt** in der GameUserSettings.ini entfernen und dein Backup zurückkopieren.
* **Im Spiel:** Ein beliebiges Preset unter **Overall Quality** wählen.

---

## Bekannte Probleme

* **Minimap unbrauchbar:** Dein LOD Bias liegt über +3. Stell ihn wieder auf +3 (`0x00000018`).
* **Einstellungen im Spiel werden nicht gespeichert:** Die GameUserSettings.ini ist seit Schritt 2 noch schreibgeschützt. Das ist so gewollt.
* **AMD- / Intel-Grafikkarte:** NPI funktioniert nur mit NVIDIA, die Schritte 1–2 aber trotzdem.

---

## Spickzettel

![WARDOGS Potato-Grafik-Spickzettel: alle Einstellungen](images/cheatsheet.png)
