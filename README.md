# Pokemon Golden Magikarp

Pokemon Golden Magikarp is a FireRed decomp hack based on `cawtds/pokefirered-expansion`, using the `no-ql-and-hs` branch as its Milestone 0 base.

Credits and upstream foundations:

- `cawtds/pokefirered-expansion`
- `rh-hideout/pokeemerald-expansion`
- `pret/pokefirered`

## Build

1. Read `INSTALL.md`; it is the source of truth for toolchain setup.
2. Install the documented ARM toolchain and host dependencies.
3. Run `make -j$(nproc)` on Linux/WSL, or the platform equivalent from `INSTALL.md`.
4. The expected artifact is `pokefirered.gba`.
5. Do not commit ROMs, save files, or original game images.
