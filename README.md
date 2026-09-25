# Condemned Gunplay

An experimental gunplay mod and weapon switcher for the Steam version of
**Condemned: Criminal Origins**.

## Current milestone: EnemyGuns-M1

This is the first in-game validated enemy-gun milestone.

- Automatically gives a Colt .45 to 70% of newly initialized generic AI.
- Uses the game's native AI initialization and update events.
- Performs no heap scanning or periodic memory scanning.
- Does not require the player to guess when enemies spawn or press a refresh key.
- Keeps the existing player weapon switcher and normal-capacity ammo refill.
- Safely supports switching weapons while the player is unarmed.
- `Ctrl+Alt+9` toggles automatic enemy guns; it is enabled by default.

The automatic AI logic waits for the model instance to become valid and then
performs the weapon change outside the AI callback stack. This avoids the
initialization crash found in earlier prototypes.

## Download

Download [`Condemned-Gunplay-EnemyGuns-M1.zip`](./Condemned-Gunplay-EnemyGuns-M1.zip).
It contains the tested binaries, matching source snapshot, build script,
milestone notes, and SHA-256 checksums.

Archive SHA-256:

```text
A46376F35CF51E4E52FBF42D1B9E5396ED114F378E47E5797AC0E14A7DB1EEC9
```

## Installation

1. Fully exit Condemned before replacing an older DLL.
2. Extract the archive.
3. Keep the EXE and DLL together. If automatic launch cannot find the game,
   place both files beside `Condemned.exe` in the game directory.
4. Run the switcher and click **Launch / Inject Condemned**.
5. Load a checkpoint or enter a level. Enemy gun assignment is automatic.

## Compatibility

The current build targets only:

- Steam game version `1.0.314.0`
- `GameServer.dll` timestamp `0x43FCFFA5`
- `GameServer.dll` image size `0x0028B000`

Other releases are rejected instead of calling unverified game addresses.

## Known limitation

The probability roll currently applies to generic `CAI`. Friendly or scripted
AI may also be affected. Keep a backup save while testing experimental builds.

## Antivirus notice

The tool injects its companion DLL into the running game process so it can call
the game's native inventory and AI functions. Security products may flag this
behavior heuristically. The matching source snapshot and reproducible build
script are included so the binaries can be inspected and rebuilt.
