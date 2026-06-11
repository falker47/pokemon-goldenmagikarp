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

- Pushed dev commit checked by GitHub Actions: `1b4d546d1edeb1e989c2833aefddc04ecdced916`.
- Run status: completed success.
- Run link: https://github.com/falker47/pokemon-goldenmagikarp/actions/runs/27362915540
- Blocking jobs: build-firered success, build-leafgreen success, release success, gate build success.
- Non-blocking baseline job: test completed failure, accepted by M0 policy and documented in `docs/TEST_BASELINE_M0.md`.

## Reference Cleanup

- Required grep target: README*, .github/, docs/, include/, src/ for Markdown/YAML files.
- Result: no residual old hyphenated repository-name references in the required Markdown/YAML targets after cleanup.

## Open Risks

- Upstream tracks multiboot .gba blobs in data/: data/mb_berry_fix.gba, data/mb_colosseum.gba, data/mb_ereader.gba. They are inherited upstream assets and are not removed in M0.
- M0 baseline accepts current make check failures. Any M1+ change should compare against docs/TEST_BASELINE_M0.md.

## M0 CHIUSO

- [x] Canonical work happened in WSL clone `/home/falker/pokemon-goldenmagikarp`; path accepted by Claude waiver.
- [x] Origin and upstream remotes configured correctly.
- [x] Branch convention preserved: work on `dev`, no dev to main merge.
- [x] Toolchain installed and documented; modern gcc-arm-none-eabi route used.
- [x] FireRed ROM build passed in Linux filesystem; `make -j2` accepted by Claude waiver.
- [x] ROM SHA1 recorded: `d6e02dee9954026b6a06d2b1946c42f99d7dc173`.
- [x] ROM artifact not committed; manual smoke-test copy placed at `/mnt/c/Users/Falker/Desktop/golden_magikarp_m0.gba`.
- [x] Smoke-test screenshot waived; manual mGBA Windows boot test assigned to Mauri; WSL mGBA .sav creation recorded as partial evidence.
- [x] Gen 4 species verification completed for Lopunny, Carnivine, Rhyperior, Magmortar, Electivire, Honchkrow, Darkrai, plus negative Snivy check.
- [x] Reference cleanup completed: no required Markdown/YAML target still contains the old hyphenated repository name.
- [x] make check baseline completed and documented; failure is accepted baseline, not M0 blocker.
- [x] CI adjusted to build/release blocking gate and verified green on GitHub Actions run 27362915540.
- [x] Four build/time/dex fixes committed separately and marked as later upstream PR candidates.
- [x] M0 report, config, build log, and test baseline committed on dev.

M0 is formally closed. M1 can start from dev after the Windows workspace archive step is completed.
