# Milestone 0 Report

## Repository

- Source cloned with full history from `https://github.com/cawtds/pokefirered-expansion`.
- Branch comparison on 2026-06-11:
  - `origin/master`: `cbc3a79b6`, 2026-05-31 15:24:03 +0200, "update toolchain variable".
  - `origin/no-ql-and-hs`: `d31e1ff5c`, 2026-05-31 16:55:01 +0200, "Merge branch 'master' into no-ql-and-hs".
  - Distance `origin/master...origin/no-ql-and-hs`: master-only `0`, no-ql-only `88`.
- Decision: base is `no-ql-and-hs`, because it is not behind `master` and already removes quest log/help system.
- Local branches created: `main` from `origin/no-ql-and-hs`, `dev` from `main`.
- GitHub remote repo creation is blocked in this environment: `gh` is not installed, the available GitHub connector cannot create repositories, and `https://github.com/falker47/golden-magikarp.git` does not exist.

## Build

- Build not completed locally. See `docs/build_log_m0.txt`.
- `make` is not available in PowerShell.
- WSL has no distro installed.
- `C:\devkitPro` is absent.
- MSYS2 exists but initially lacks `make`, `gcc`, and `arm-none-eabi-gcc`.
- Cygwin exists with `gcc 11.4.0`, but lacks `make` and ARM toolchain.
- One documented alternative was attempted: installing MSYS2/MinGW64 packages for modern `arm-none-eabi` build. It failed because the pacman database/mirrors are stale and the cache write ended with `Permission denied`.
- Per guardrail, the build system was not rewritten.

## Smoke Test

- Not executed: no `.gba` artifact was produced.
- `mgba` is not installed or not available in PATH in this environment.
- No title-screen screenshot was captured.
- Manual smoke test remains assigned after a successful build artifact exists.

## Gen 4 Config

- Applied in `include/config/general.h`, `include/config/pokemon.h`, `include/config/item.h`, `include/config/overworld.h`, and `include/config/species_enabled.h`.
- Full config rationale is in `docs/CONFIG_GOLDEN.md`.
- `GEN_LATEST` now resolves to `GEN_4`, bringing the expansion defaults down from latest-generation behavior.
- Explicit post-Gen 4 species/forms/gimmicks were disabled to avoid Fairy exposure and later-generation mechanics.

## Anti-Fairy Verification

- Empirical source check passed for Clefairy:
  - `src/data/pokemon/species_info/gen_1_families.h` uses Fairy only when `P_UPDATED_TYPES >= GEN_6`.
  - With M0 config, `P_UPDATED_TYPES == GEN_4`, so Clefairy resolves to `TYPE_NORMAL`.
- Caveat: the expansion still contains `TYPE_FAIRY` constants, type info, icons, and later-gen data in source. Those are inherited engine support and were not removed in M0.

## DexNav

- DexNav exists in the codebase (`src/dexnav.c`, `src/start_menu.c`, `include/config/dexnav.h`).
- It is already disabled:
  - `DEXNAV_ENABLED FALSE`
  - `USE_DEXNAV_SEARCH_LEVELS FALSE`
  - `DN_FLAG_DEXNAV_GET 0`
- No edit needed.

## Escape Rope Risk Map

`ITEM_ESCAPE_ROPE` appears in early/general shops:

- `SHOP_ID_PEWTER_CITY_MART`
- `SHOP_ID_CERULEAN_CITY_MART`
- `SHOP_ID_LAVENDER_TOWN_MART`
- `SHOP_ID_SAFFRON_CITY_MART`
- `SHOP_ID_CINNABAR_ISLAND_MART`
- `SHOP_ID_THREE_ISLAND_MART`
- `SHOP_ID_FOUR_ISLAND_MART`
- `SHOP_ID_SIX_ISLAND_MART`
- Shared Seven Island stock used by `SHOP_ID_SEVEN_ISLAND_MART` and `SHOP_ID_TRAINER_TOWER_LOBBY`

M0 did not remove it. Decision deferred to M1.

## Linking Cord Recon

- Item constant: `include/constants/items.h`, `ITEM_LINKING_CORD = 796`.
- Item data/name: `src/data/items.h`, display name "Linking Cord".
- Evolution method enum: `include/constants/pokemon.h`, `EVO_TRADE` and `EVO_ITEM`.
- Trade evolutions that also accept Linking Cord are encoded as `EVO_ITEM, ITEM_LINKING_CORD` in species data, including:
  - `src/data/pokemon/species_info/gen_1_families.h`: Alakazam, Machamp, Golem, Gengar.
  - Later disabled families also contain examples in gen 5/6 files.
- M1 rebrand target for PIETRARADIO is therefore item data/name plus species evolution entries.

## Music Branch

`origin/dppt-hgss-music` is 3 commits ahead and 0 behind `master` as of 2026-05-31. It converts/adds DPPt/HGSS audio assets (`convert dppt/hgss aif -> wav`). It is thematically attractive for a Gen 4-feel hack, but M0 should not adopt it: merging it now would add asset churn and audio risk before the base build is green.

## Hygiene And CI

- `.gitignore` now ignores `*.gba`, `*.gb`, `*.gbc`, `*.sav`, `*.srm`, `baserom*`, and `roms/`.
- Removed the previous `!data/*.gba` exception from `.gitignore`.
- Important repo conflict: upstream tracks three `.gba` files in `data/`:
  - `data/mb_berry_fix.gba`
  - `data/mb_colosseum.gba`
  - `data/mb_ereader.gba`
- Those files are directly included by assembly via `.incbin`, so deleting them in M0 would likely break the upstream build. This conflicts with the project rule "no .gba committed"; team decision needed.
- Existing GitHub Actions workflow was adapted to push branches `main` and `dev`, plus manual `workflow_dispatch`.
- CI could not be observed green because the GitHub repository could not be created/pushed from this environment.

## Open Risks

- Local toolchain is not usable until WSL distro/devkitPro/MSYS2 packages are repaired.
- Remote repository creation/push requires GitHub CLI, credentials, or a tool with repo-create permission.
- Upstream tracked `.gba` multiboot blobs conflict with the legal hygiene rule.
- Fairy engine support remains in source even though Gen 4 config and species gates should prevent gameplay exposure.
- `include/config/caps.h` contains a duplicated `B_EV_CAP_VARIABLE` define inherited from upstream; untouched in M0 because EV caps are inactive.

## Questions For Team

- Should the inherited multiboot `.gba` blobs be removed and replaced with source-buildable assets, external artifacts, or accepted as upstream-required binary blobs?
- Should post-Gen 4 Pokemon be completely disabled as done here, or should later species be allowed if manually remapped away from Fairy and later mechanics?
- Should `dppt-hgss-music` be evaluated in M1 after the base build is green?
- Who will create `falker47/golden-magikarp` if this environment remains without GitHub repo-create capability?
