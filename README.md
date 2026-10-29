# Reforged HD Characters for WoW 3.3.5a

HD player-race models from **WoW Forever (Classic beta)** for a **3.3.5a (build 12340) client**, with the **full Forever mesh** (hair, beards and clothing are not simplified) and a small standalone DLL, **ReforgedHD**, that lets the stock client load them.

> **ReforgedHD.dll is required.** The full HD models are bigger than the stock 3.3.5a client can draw (more than 65,535 indices per model). Installing only `patch-H.mpq` without the DLL gives characters with broken, stretched triangles.

Download **both** files from the [latest release](../../releases/latest): `patch-H.mpq` and `ReforgedHD.zip`.

## What's included
- **All 10 playable races, male and female**: Human, Dwarf, Gnome, Night Elf, Draenei, Orc, Undead, Tauren, Troll and Blood Elf.
- **Customization is the stock 3.3.5a one.** Every race keeps exactly the same options as the original client (skins, faces, hairstyles, hair colors and facial features, same count and same IDs). Each option shows its HD equivalent using Blizzard's own legacy-to-modern conversion table. **No server changes are needed**: it works on any 3.3.5a server with stock DBCs, and existing characters keep their look, now in HD.
- **NPCs that use player models are HD too**, with their 13,547 baked textures remapped to the HD body.
- **Helmets, shoulders and weapons fit** like on the original models; same size as Blizzard's models, also on the character select and creation screens.
- Boots, gloves and robes hide and show the right body parts. With low boots the bare toes are hidden (ReforgedHD `Pies` module).
- **Death Knight eyes** with the modern glow.

## ReforgedHD.dll (1.5.1)
Standalone (no WarcraftXL, no AwesomeWotlk, KERNEL32 only). **Optional load:** the patched `Wow.exe` tries to load `ReforgedHD.dll` at startup; if the DLL is missing the game still starts normally, just without the improvements. Modules:
- **IndicesGrandes**: removes the 65,535-index limit per `.skin`, so the full HD models fit (retail convention: section start = `level << 16 | indexStart`). Blizzard models (level 0) behave exactly as before.
- **Pies**: low boots (ItemDisplayInfo `GeosetGroup[0] = 0`) switch the bare foot with toes for the HD booted foot. Models without that geoset (Blizzard's, Draenei, Tauren, Troll) are unchanged.
- **Cascos** (helmets): fits every helmet to the HD heads using `Interface\ReforgedHD\cascos.csv` inside `patch-H.mpq` (per race/sex fit taken from Blizzard's own Forever re-fitted helmets, plus per-helmet rows checked against all 5,438 helmet/race combinations). The original 3.3.5a helmet models are used; helmets from other servers get the race/sex fit. 1.5.1 fixes the per-helmet rows, which 1.5 never applied (it always used the race/sex fit).
- **MD21**: experimental loader for modern (MD21) models, **disabled** (`MD21=0`). Not needed for this patch.

Before patching, the DLL checks the original bytes of every site; if one does not match (another build, or already patched by something else) it changes nothing and writes it to `ReforgedHD.log`.

## Installation (game closed)
1. Unzip `ReforgedHD.zip` next to `Wow.exe` and run `INSTALL.cmd` once (or drag your `Wow.exe` onto `INSTALL.cmd`). The patcher is a readable PowerShell script, `PatchReforgedHD.ps1` (an `.exe` patcher was flagged by antivirus heuristics as a false positive). It first saves an exact copy, `Wow.exe.ReforgedHD.bak`, sets Large Address Aware and adds a tiny optional loader. The exe size and `SizeOfImage` do not change. An older ReforgedHD install (1.0-1.3) is upgraded in place.
2. Copy `patch-H.mpq` into your `Data` folder. **Keep that exact name**: the stock client only loads `patch-<one character>.MPQ`.
3. Delete your `Cache` folder.

**Both files are required for the HD characters.** With `patch-H.mpq` but without the DLL the game starts, but the HD characters render with broken triangles.

Uninstall: run `UNINSTALL.cmd` (restores `Wow.exe` from the backup) and delete `Data\patch-H.mpq`.
Disable without uninstalling: `ReforgedHD.ini` → `[General] Enabled=0`, or set the environment variable `REFORGEDHD_DISABLE=1`. Only the boots fix: `[Modules] Pies=0`.

## Compatibility
- The patch carries its own `ItemDisplayInfo.dbc` and `HelmetGeosetVisData.dbc` (Blizzard's, changing only what each helmet hides) so long HD hair does not clip through closed helmets; open helmets keep the hairstyle exactly as on Blizzard's models. If your server ships its own patch with new items in `ItemDisplayInfo.dbc`, give that patch higher priority.
- Works alongside other DLLs loaded by `Wow.exe`. The loader does not use the import table and does not touch the startup hook used by the AwesomeWotlk / WotLKExtensions loaders (0x40B7D0 / 0x4E5CB0).
- St0ny's AIO WoW.exe Patcher: none of its patches touch the sites ReforgedHD patches (checked by reading its source), and the ReforgedHD loader avoids every file range St0ny writes (including its watermark). **Order:** run St0ny's patcher first, then ReforgedHD. St0ny refuses an exe changed by other tools, so to change St0ny patches later: run `UNINSTALL.cmd`, use St0ny, then install ReforgedHD again. Tested with St0ny's patches simulated byte by byte, not with his script itself.

## Known limitations
- Only the stock 3.3.5a options exist. Modern extras (face shapes, eye colors, extra hairstyles and jewelry) are not included.
- Draenei always have the short tail. Night elf females have fixed eyebrows; human females have eyebrows in the face texture.
- Undead mouth variations are baked as meshes (Forever deforms the jaw bones instead).
- Some hair colors and skin tones have no exact Forever equivalent: the closest one is used.
- With robes or skirts the foot is drawn with the skirt and may look slightly bigger than Blizzard's.
- Goblin and high elf are not included (not playable in 3.3.5a).

## Credits & disclaimer
Converted by the Reforged community project. All models, textures and game data are property of Blizzard Entertainment. This is a free, non-commercial fan project, not affiliated with or endorsed by Blizzard. You need your own legitimate copy of the game.

---

## Español (resumen)
Modelos HD de WoW Forever para las 10 razas jugables (hombre y mujer) en un cliente 3.3.5a (12340), con la malla completa de Forever. **Necesita el DLL independiente ReforgedHD**: los modelos completos pasan del límite de índices del cliente original, y sin el DLL salen con triángulos rotos. Las opciones de personalización son exactamente las del 3.3.5a, así que **no hay que tocar el servidor** y los personajes que ya existen conservan su aspecto, ahora en HD.

**Instalación (juego cerrado):** descomprime `ReforgedHD.zip` junto a `Wow.exe` y ejecuta `INSTALL.cmd` una vez (guarda antes `Wow.exe.ReforgedHD.bak`); copia `patch-H.mpq` a `Data` con ese nombre exacto; borra la carpeta `Cache`. Hacen falta los dos: sin el DLL los personajes salen con triángulos rotos.
**Quitarlo:** `UNINSTALL.cmd` y borrar `Data\patch-H.mpq`. **Desactivar:** `Enabled=0` en `ReforgedHD.ini`.

Todo el arte es propiedad de Blizzard Entertainment. Proyecto de comunidad sin ánimo de lucro, no afiliado a Blizzard.
