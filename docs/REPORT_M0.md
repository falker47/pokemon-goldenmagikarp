# Milestone 0 Report

## Decisions Carried Into M0-ter

- Waiver accepted by Claude: /home/falker/pokemon-goldenmagikarp is compliant because the substantive requirement is Linux filesystem, no spaces, no /mnt/c build path.
- Waiver accepted by Claude: make -j2 is accepted for M0 because higher parallelism was unstable in this environment.
- Smoke-test decision by Claude: headless screenshot is abandoned; boot test is manual on Mauri mGBA Windows.
- Test policy by Claude: make check is not required green for M0. Blocking CI gate is build/release only. Current make check failures are M0 baseline; from M1 onward, no new failure may be introduced relative to the baseline.
- Source of truth by Claude: the WSL clone is canonical. The Windows workspace is no longer used for development.

## Repository

- Canonical workspace: `/home/falker/pokemon-goldenmagikarp`.
- Branch: `dev`.
- Origin: `https://github.com/falker47/pokemon-goldenmagikarp.git`.
- Upstream: `https://github.com/cawtds/pokefirered-expansion.git`, added during M0-ter.
- Branch convention remains: `main` mirrors upstream/no-ql-and-hs; game work lives only on `dev`; never merge dev into main.
- M0-ter code fix commits on `dev`:
  - `62089b27c fix(build): include constants/field_poison.h for poison status constants`
  - `f0130744c fix(build): keep OW_BERRY_COLORS on a legal expansion value`
  - `71b2d6f3a fix(time): guard DNS evening branch for GEN_4 time profiles`
  - `722ded9c6 fix(dex): separate national dex table count from enabled dex count`
- The four code fixes above are candidates for a later upstream PR. No upstream PR was opened in M0.

## Build

- Toolchain path used: modern apt packages in WSL Ubuntu: build-essential, binutils-arm-none-eabi, gcc-arm-none-eabi, libnewlib-arm-none-eabi, git, libpng-dev, pkg-config, python3.
- FireRed build command accepted for M0: `make -j2`.
- Build result: passed; ROM produced at `/home/falker/pokemon-goldenmagikarp/pokefirered.gba`.
- ROM SHA1: `d6e02dee9954026b6a06d2b1946c42f99d7dc173`.
- ROM size: `16777216` bytes.
- Build log committed as `docs/build_log_m0bis.txt`.
- The produced ROM remains ignored and is not committed.

## Technical Build Fixes

- `src/field_control_avatar.c`: included `constants/field_poison.h` for FLDPSN constants.
- `include/config/overworld.h`: kept `OW_BERRY_COLORS` at legal value `GEN_6_ORAS`; `GEN_4` is rejected by berry compile checks.
- `src/overworld.c`: compiled the DNS evening blend branch only when the active time profile has an evening band.
- `include/constants/pokedex.h` and `src/pokemon.c`: added `NATIONAL_DEX_TABLE_COUNT` so the physical National Dex table can remain full while `NATIONAL_DEX_COUNT` reflects enabled Gen 1-4 scope.

## Smoke Test

- Headless screenshot is waived by Claude.
- Partial evidence already acquired in WSL: mGBA loaded the ROM far enough to create `pokefirered.sav`; no save file was committed.
- Manual boot test artifact copied for Mauri: `/mnt/c/Users/Falker/Desktop/golden_magikarp_m0.gba`. SHA1 matches the canonical ROM: `d6e02dee9954026b6a06d2b1946c42f99d7dc173`.
- Manual boot test remains assigned to Mauri on mGBA Windows.

## Gen 4 Config

- Full configuration rationale is in `docs/CONFIG_GOLDEN.md`.
- Gen 1-4 Pokemon gates are enabled; Gen 5+ Pokemon gates are disabled.
- Puntual verification completed in `docs/CONFIG_GOLDEN.md`: Lopunny, Carnivine, Rhyperior, Magmortar, Electivire, Honchkrow, and Darkrai are enabled; Snivy is excluded through `P_GEN_5_POKEMON == FALSE`.
- Fairy support still exists in engine constants/assets as inherited expansion support, but Gen 4 config keeps gameplay exposure out of M0 scope.

## Baseline Tests

- Command run in WSL: `timeout 45m make -j2 check`.
- Result: completed before timeout; make check exited non-zero as expected by the M0 policy.
- Baseline document: `docs/TEST_BASELINE_M0.md`.
- Runner summary: 125 failed-class results, 72 assumption failures, 10 known failing, 625 to-do, 6 expect-failing, 4373 passed, 5211 total.
- Failure-class breakdown: 118 FAIL, 6 INVALID, 1 ERROR.

## CI

- Workflow adjusted in M0-ter: build-firered, build-leafgreen, and release are blocking; make check remains visible but non-blocking.
- New dev push and GitHub Actions verification are pending at this point in the local report flow.

## Reference Cleanup

- Required grep target: README*, .github/, docs/, include/, src/ for Markdown/YAML files.
- Stale repository name references are being corrected to pokemon-goldenmagikarp as part of M0-ter.

## Open Risks

- Upstream tracks multiboot .gba blobs in data/: data/mb_berry_fix.gba, data/mb_colosseum.gba, data/mb_ereader.gba. They are inherited upstream assets and are not removed in M0.
- M0 baseline accepts current make check failures. Any M1+ change should compare against docs/TEST_BASELINE_M0.md.
- Final CI run still needs to be checked after pushing the M0-ter commits.
