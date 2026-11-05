# MyOsu

Ein eigener **Offline-osu!-Client**, basiert auf [McOsu](https://github.com/McKay42/McOsu) und [McEngine](https://github.com/McKay42/McEngine) von McKay.
64-bit, DirectX 11, auf hohe FPS getrimmt, dazu ein paar Extras für Relax-Spieler.

> **Offline only.** MyOsu reicht **keine Scores** bei Bancho ein und meldet sich nirgends an.
> Die osu!-API wird nur **lesend** benutzt (Rangliste, Map-Leaderboards).
> Kein offizielles Projekt, nicht verbunden mit ppy / osu! oder McKay.

---

## Download

1. Oben auf **[Actions](../../actions)** gehen und den neuesten **grünen** Build öffnen.
2. Ganz unten bei **Artifacts** auf **`MyOsu`** klicken.
3. Den Inhalt in deinen **McOsu-Ordner** kopieren (`MyOsu.exe`, die DLLs und den Ordner `myosu_shaders`).
4. **`MyOsu.exe`** starten.

**Voraussetzungen:** Windows 10/11 (64-bit) und eine CPU mit AVX2: Intel ab Haswell (2013) oder AMD ab Ryzen (2017).

**Startoptionen** (z. B. über eine Verknüpfung, hinter `MyOsu.exe` eintragen):

| Option | Wirkung |
|---|---|
| `-opengl` | OpenGL statt DirectX 11 |
| `-lowlatency` | **experimentell:** DX11 mit Flip-Modell, Tearing und max. 1 Bild in der Warteschlange |

---

## Features

### Relax
- **Relax als feste Option** unter *Options → Gameplay*: kein Mod, „Reset All Mods“ schaltet es nicht aus.
- **Key-Overlay wie in lazer:** K1/K2 drücken bei Relax automatisch mit. Unter einer einstellbaren Notendichte gibt es nur Single-Taps auf K1, darüber wird K1/K2 abgewechselt. Das gilt auch für Misses und Spinner.
- **Eigene Tasten blocken:** Deine eigenen K1/K2 werden beim Spielen ignoriert, in Pausen und Breaks funktionieren sie.
- **„Hide Relax“:** blendet Relax in Mod-Symbolen und Score-Listen aus.

### Aoy-Modus
Spielen mit **CS 0** (mit HR: 1,5), **AR immer 10,3** und **OD 10** (mit HR: 11), auch mit DT oder HT.
Für Sterne und pp zählen die normalen Werte der Map. Schaltest du den Modus aus, bekommen deine Aoy-Plays wieder ihre echten pp.
Relax wird im Aoy-Modus automatisch versteckt.

### Ranglisten und Leaderboards (osu! API v2)
- **Globaler Rang und Länder-Rang** für deine lokalen pp, über die osu!-Rangliste. Mit einem osudaily-Key auch genau über Platz 10.000 hinaus.
- **Globale Map-Leaderboards:** die Top 50, nur der beste Score pro Spieler und keine reinen lazer-Scores. Bist du außerhalb der Top 50, wird dein eigener Platz zusätzlich angezeigt. Dein Name ist grün, und die Liste wird um deinen Score herum zentriert.
- **Profilbild pro Profil:** liegt unter `avatars/<Name>.png` oder `.jpg`.
- **Rangfarben** und eine **Statistik-Tabelle auf dem Ergebnisbildschirm** wie nach einem Submit in osu!.

### Sonstiges
- **Skin-Suche** in den Optionen.
- **6CE-Modus:** Der Prozess läuft nur auf den gewählten CPU-Kernen, optional mit Echtzeit-Priorität. Standardmäßig automatisch, bei Intel Core Ultra 5 z. B. `0-5` für die 6 P-Kerne eintragen.
- **Low Latency (experimentell):** Mit `-lowlatency` gibt es Flip-Modell, Tearing und höchstens 1 Bild in der Warteschlange.

---

## osu! API einrichten (optional)

1. Auf [osu.ppy.sh](https://osu.ppy.sh) gehen: *Einstellungen → OAuth → Neue OAuth-Anwendung*. Name ist egal, die Callback-URL bleibt leer.
2. **Client ID** und **Client Secret** in MyOsu unter *Options* eintragen.
3. Optional: einen **osudaily.net**-API-Key eintragen, für genaue Ränge über 10.000.

Gib dein Client Secret niemandem und lade es nicht hoch.

---

## Konsolenbefehle

Die Konsole öffnest du mit **F1**. Fast alles davon gibt es auch unter *Options*.

| Befehl | Standard | Beschreibung |
|---|---|---|
| `osu_relax_option` | 0 | Relax als feste Option |
| `osu_relax_hide` | 0 | Relax in Mod-Symbolen und Score-Listen verstecken |
| `osu_relax_block_keys` | 1 | eigene K1/K2 beim Relax-Spielen ignorieren |
| `osu_relax_overlay_autoclick` | 1 | Auto-Klicks im Key-Overlay anzeigen |
| `osu_relax_overlay_alternate_nps` | 5 | ab so vielen Noten pro Sekunde K1/K2 abwechseln |
| `osu_aoy_mode` | 0 | Aoy-Modus |
| `osu_aoy_cs` / `osu_aoy_cs_hr` | 0 / 1.5 | CS im Aoy-Modus |
| `osu_aoy_ar` | 10.3 | AR im Aoy-Modus |
| `osu_aoy_od` / `osu_aoy_od_hr` | 10 / 11 | OD im Aoy-Modus |
| `osu_api_client_id` / `osu_api_client_secret` | – | osu!-API-Zugang |
| `osu_api_osudaily_key` | – | osudaily-Key (optional) |
| `osu_api_country` | – | Ländercode für den Länder-Rang, z. B. `DE` |
| `osu_api_global_leaderboard` | 1 | globale Top 50 anzeigen |
| `osu_cpu_affinity` | leer (automatisch) | erlaubte CPU-Kerne wie im Task-Manager, z. B. `0-5` oder `0,1,4-7` |
| `osu_pcore_affinity` | 1 | CPU-Kerne beim Start festlegen |
| `osu_process_priority_realtime` | 0 | Echtzeit-Priorität (braucht Adminrechte, sonst „Hoch“) |
| `osu_slider_dx11_zflip` | 0 | nur ausprobieren, falls Slider unter DX11 kaputt aussehen |

---

## Selbst bauen

MyOsu wird komplett über **GitHub Actions** gebaut (MSYS2 / MinGW-w64, 64-bit). Lokal ist nichts nötig.

- `patches/myosu-all.patch`: alle Änderungen an McOsu
- `patches/myosu-engine.diff`: Änderungen an McEngine (DX11 mit Low Latency)
- `.github/workflows/build.yml`: lädt McOsu und McEngine, spielt die Patches ein und kompiliert mit `-O3` für `x86-64-v3` (AVX2)

Bei jedem Push startet ein neuer Build. Fork das Repo, ändere die Patches, und unter *Actions* bekommst du deine eigene exe.

---

## Credits und Lizenz

- **[McOsu](https://github.com/McKay42/McOsu)** von McKay: GPL-3.0
- **[McEngine](https://github.com/McKay42/McEngine)** von McKay: MIT
- **BASS / BASS_FX** von [un4seen](https://www.un4seen.com): nur für nicht-kommerzielle Nutzung frei
- osu! ist eine Marke von ppy Pty Ltd.

Weil MyOsu auf McOsu aufbaut, steht MyOsu ebenfalls unter der **GPL-3.0**.
