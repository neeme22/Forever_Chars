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

## ReforgedHD.dll
Standalone (no WarcraftXL, no AwesomeWotlk, KERNEL32 only). Modules:
- **IndicesGrandes**: removes the 65,535-index limit per `.skin`, so the full HD models fit (retail convention: section start = `level << 16 | indexStart`). Blizzard models (level 0) behave exactly as before.
- **Pies**: low boots (ItemDisplayInfo `GeosetGroup[0] = 0`) switch the bare foot with toes for the HD booted foot. Models without that geoset (Blizzard's, Draenei, Tauren, Troll) are unchanged.
- **MD21**: experimental loader for modern (MD21) models, **disabled** (`MD21=0`). Not needed for this patch.

Before patching, the DLL checks the original bytes of every site; if one does not match (another build, or already patched by something else) it changes nothing and writes it to `ReforgedHD.log`.

## Installation (game closed)
1. Unzip `ReforgedHD.zip` next to `Wow.exe` and run `INSTALL.cmd` once. It first saves an exact copy, `Wow.exe.ReforgedHD.bak`, then adds `ReforgedHD.dll` to the exe's import table. It refuses if the exe is already patched or the backup exists.
2. Copy `patch-H.mpq` into your `Data` folder. **Keep that exact name**: the stock client only loads `patch-<one character>.MPQ`.
3. Delete your `Cache` folder.

**Both files are required.** Without the DLL the HD characters render with broken triangles.

Uninstall: run `UNINSTALL.cmd` (restores `Wow.exe` from the backup) and delete `Data\patch-H.mpq`.
Disable without uninstalling: `ReforgedHD.ini` → `[General] Enabled=0`, or set the environment variable `REFORGEDHD_DISABLE=1`. Only the boots fix: `[Modules] Pies=0`.

## Compatibility
- The patch carries its own `ItemDisplayInfo.dbc` and `HelmetGeosetVisData.dbc` (Blizzard's, changing only what each helmet hides) so long HD hair does not clip through closed helmets. If your server ships its own patch with new items in `ItemDisplayInfo.dbc`, give that patch higher priority.
- Works alongside other DLLs imported by `Wow.exe` (e.g. PetSelectScale), in any install order.

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
