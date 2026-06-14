
# Diablo4AssetBrowser v1.0

A standalone Diablo IV asset browser and 3D **wardrobe / mount studio**. It reads
your installed game directly (CASC), decodes textures, and previews/exports
character appearances, armor sets, mounts and pets as animated `.glb` models —
with skin tone, hair/eye colour, makeup, markings, facial hair, dyes and
animations. Keep in mind, this is vibe-coded slop that I'm actually unhappy with as I ended up filling it with bloat. I highly recommend D4Analyzer as it's the cleanest, fastest, and most well made tool for getting Diablo 4's Assets; if you need the rigged versions and weights use my other tool which is just a .bat file that will generate a rigged .glb version of the .gltf's extracted from D4Analyzer.

> Not affiliated with or endorsed by Blizzard. For personal use with a copy of
> Diablo IV that you own. No game assets are included in this repository.

---

## Features

- **Asset Gallery** — browse every appearance with rendered 3D icons.
- **Models** — D4Analyzer-style appearance browser with a live 3D preview and PBR.
- **Wardrobe** — build a full character (class + gender, face, hair, facial hair,
  armor by slot, weapons, jewelry), tint skin/hair/dye, pick eye colour, makeup
  and markings, play animations, and export the combined model.
- **Stable** — the same for mounts and pets (bodies, armor, trophies).
- **Textures** / **StringLists** — decode and browse textures and translations.
- Reads the **live game** (always matches your installed patch), with on-demand
  decryption via TACT keys.

---

## Previews

<img width="2844" height="1369" alt="python_4UXR66RHCA" src="https://github.com/user-attachments/assets/fdf27b51-365f-4455-815a-c509bd375c47" />
<img width="2560" height="1369" alt="python_KM3xu8d76n" src="https://github.com/user-attachments/assets/e547d671-1ff4-48a8-b888-e73ca989d976" />
<img width="2560" height="1369" alt="python_6FsqgtvP0Z" src="https://github.com/user-attachments/assets/2f5d57a8-eba7-4095-8291-1cdea7b39648" />
<img width="2560" height="1369" alt="python_IohgGOw6Dj" src="https://github.com/user-attachments/assets/0b58935b-6e6f-43f5-a061-d6346d31506f" />
<img width="2560" height="1369" alt="python_MjDe7DVPSW" src="https://github.com/user-attachments/assets/af950351-1a49-4749-8ac7-fe9284987a78" />

---

## Plans
I'm actually not very happy with this version of the tool as I've ended up taking it beyond the scope of it what it should be for. I'm burnt out trying to get things to work properly and plan on starting fresh all over again later on.
- Wardrobe Tab is slow as hell
- Stable Tab sucks
- Removing D4Extract as a dependency

---

## Known Issues

- Facial Hair is buggy
- Paladin animations are misssing, probably encrypted
- Warlock models are bugged and or missing, probably encrypted
- Horse armor isn't rigged to the skeleton
- Stable models don't have proper transparency

---

## Requirements

- **Windows**
- **Python 3.11+** on your PATH — <https://python.org> (tick "Add to PATH")
- A **Diablo IV** installation (Battle.net or Steam)
- Internet on first run (to fetch Python packages + the data dependencies)

---

## Quick start

1. Download/clone this repository and unzip it anywhere (it's fully portable —
   everything lives in the one folder).
2. Double-click **`run.bat`**. The first run installs the Python packages into
   `deps\py` automatically (portable — nothing touches your system Python).
3. In the app:
   - **File → Settings** — set your **Diablo IV game folder**.
   - **File → Dependencies…** — download **d4data** (game metadata) and
     **d4extract** (the model exporter). One click each.
   - **File → Update TACT Keys** — fetch the current decryption keys.
4. Open the **Wardrobe** (or any tab) and build a character.

Manual launch (instead of `run.bat`):

```bat
pip install -r requirements.txt
set PYTHONPATH=src
python -m d4ab2.gui.main
```

---

## Portability

The whole tool is self-contained in its folder: Python packages vendor into
`deps\py`, and the data dependencies (`deps\d4data`, `deps\d4extract`), TACT keys
(`tactkeys\`) and all caches/logs (`userdata\`) are created next to it. Delete the
folder to remove everything. None of those generated folders are part of this
repository — the app downloads or builds them on first use.

---

## Project layout (what's in the repo)

```
Diablo4AssetBrowser/
├── run.bat                  ← launch (auto-installs Python deps)
├── check.bat                ← self-check (compile + import smoke test)
├── requirements.txt         ← Python dependencies
├── src/d4ab2/               ← the application
├── data/                    ← bundled name/attribute tables (required)
├── tools/                   ← diagnostics (diag_*.py, data_audit.py, check.py)
├── README.md
├── DEVELOPMENT.md           ← edit/test guide
└── PIPELINE_INVARIANTS.md   ← how the extract→merge→render pipeline must behave
```

Created at runtime (NOT in the repo): `deps/`, `userdata/`, `tactkeys/`,
`bin/`, `plugins/`, `translations/`.

---

## Troubleshooting

- **"python not found"** — install Python 3.11+ and re-run `run.bat`.
- **Nothing loads / "d4data not configured"** — File → Settings (game folder)
  and File → Dependencies (download d4data + d4extract).
- **A new collab item is missing** — File → Update TACT Keys; some brand-new
  encrypted content only unlocks once Blizzard decrypts it in a later patch.
- **Verify an install** — run `check.bat`; it writes `userdata\check_report.txt`.

---

## Credits

Builds on the Diablo IV community tooling: **d4data** (DiabloTools), **d4extract**
(narascode), and the community **TACT keys**. This project bundles none of them —
they're downloaded on demand.
