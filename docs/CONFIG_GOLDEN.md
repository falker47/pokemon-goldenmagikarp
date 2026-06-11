# Golden Magikarp M0 Config

Scope: technical foundation only. No maps, text, trainers, or gameplay content were edited.

## Generation Default

| Define | File | Before | After | Reason |
|---|---|---:|---:|---|
| `GEN_LATEST` | `include/config/general.h` | `GEN_9` | `GEN_4` | Make every default config that points at `GEN_LATEST` resolve to Gen 4 mechanics instead of latest-generation expansion behavior. |

This affects the upstream `GEN_LATEST` defaults across battle, Pokemon, item, overworld, fishing, contest, Pokerus, and general config files. Notable affected groups include:

- Battle mechanics: crit chance/multiplier, status odds, damage formulas, type matchup update gates, turn timers, move behavior, ability behavior, weather/terrain, catching, EXP behavior.
- Move data: `B_UPDATED_MOVE_DATA`, `B_UPDATED_MOVE_TYPES`, `B_UPDATED_MOVE_FLAGS`, and `B_PHYSICAL_SPECIAL_SPLIT` now resolve to Gen 4.
- Pokemon data: `P_UPDATED_TYPES`, `P_UPDATED_STATS`, `P_UPDATED_ABILITIES`, `P_UPDATED_EVS`, `P_LVL_UP_LEARNSETS`, breeding, evolution, EV, friendship, and egg-cycle gates now resolve to Gen 4.
- Items/overworld: price/effect gates, Escape Rope behavior, repel behavior, running indoors, poison overworld damage, PC behavior, time of day, and healing egg behavior now resolve to Gen 4.

## Explicit Overrides

| Define | File | Before | After | Reason |
|---|---|---:|---:|---|
| `P_SHOW_TERA_TYPE` | `include/config/pokemon.h` | `GEN_8` | `GEN_4` | Keep summary data aligned with the Gen 4 target and avoid Tera UI exposure. |
| `I_BERRY_PRICE` | `include/config/item.h` | `GEN_7` | `GEN_4` | Use Gen 4 item pricing behavior instead of a later explicit override. |
| `I_EXP_SHARE_ITEM` | `include/config/item.h` | `GEN_5` | `GEN_4` | Keep Exp. Share as a held-item era mechanic; modern party-wide Exp. Share remains inactive. |
| `OW_BERRY_DRAIN_RATE` | `include/config/overworld.h` | `GEN_6_ORAS` | `GEN_4` | Use Gen 4 berry moisture/drain behavior. |
| `OW_BERRY_COLORS` | `include/config/overworld.h` | `GEN_6_ORAS` | `GEN_4` | Avoid ORAS berry color behavior in the Gen 4 baseline. |

## Species And Form Gates

| Define | File | Before | After | Reason |
|---|---|---:|---:|---|
| `P_GEN_5_POKEMON` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Limit enabled Pokemon families to Gen 1-4 for a Gen 4 foundation. |
| `P_GEN_6_POKEMON` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Prevent post-Gen 4 families and default Fairy-type species exposure. |
| `P_GEN_7_POKEMON` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Prevent post-Gen 4 families and mechanics. |
| `P_GEN_8_POKEMON` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Prevent post-Gen 4 families and mechanics. |
| `P_GEN_9_POKEMON` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Prevent post-Gen 4 families and mechanics. |
| `P_MEGA_EVOLUTIONS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Mega Evolution is post-Gen 4. |
| `P_PRIMAL_REVERSIONS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Primal Reversion is post-Gen 4. |
| `P_ULTRA_BURST_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Ultra Burst is post-Gen 4. |
| `P_GIGANTAMAX_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Gigantamax is post-Gen 4. |
| `P_TERA_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Terastallization is post-Gen 4. |
| `P_FUSION_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Fusion forms are post-Gen 4 content/mechanics. |
| `P_REGIONAL_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Regional forms are post-Gen 4. |
| `P_PIKACHU_EXTRA_FORMS` | `include/config/species_enabled.h` | `TRUE` | `FALSE` | Extra Pikachu form groups include post-Gen 4 variants. |
| `P_GEN_6_CROSS_EVOS` | `include/config/species_enabled.h` | `P_CROSS_GENERATION_EVOS` | `FALSE` | Disables Sylveon, preventing Fairy exposure through the Eevee family. |
| `P_GEN_8_CROSS_EVOS` | `include/config/species_enabled.h` | `P_CROSS_GENERATION_EVOS` | `FALSE` | Disable post-Gen 4 cross-generation evolutions. |
| `P_GEN_9_CROSS_EVOS` | `include/config/species_enabled.h` | `P_CROSS_GENERATION_EVOS` | `FALSE` | Disable post-Gen 4 cross-generation evolutions. |

Gen 1-4 Pokemon and Gen 2-4 cross-generation evolutions remain enabled. This keeps Gen 4 evolution families available while preventing later Fairy-only paths such as Sylveon.

## DexNav

| Define | File | Value | Status |
|---|---|---:|---|
| `DEXNAV_ENABLED` | `include/config/dexnav.h` | `FALSE` | Already disabled upstream. |
| `USE_DEXNAV_SEARCH_LEVELS` | `include/config/dexnav.h` | `FALSE` | Already disabled upstream. |
| `DN_FLAG_DEXNAV_GET` | `include/config/dexnav.h` | `0` | Start menu cannot expose DexNav by flag. |

No DexNav config edit was needed.

## Exp Share And Level Caps

| Define | File | Value After M0 | Status |
|---|---|---:|---|
| `I_EXP_SHARE_FLAG` | `include/config/item.h` | `0` | Modern party-wide Exp. Share toggle is not assigned and is inactive. |
| `I_EXP_SHARE_ITEM` | `include/config/item.h` | `GEN_4` | Held-item-era behavior. |
| `B_EXP_CAP_TYPE` | `include/config/caps.h` | `EXP_CAP_NONE` | Level/EXP caps remain inactive for M1 balance decisions. |
| `B_LEVEL_CAP_TYPE` | `include/config/caps.h` | `LEVEL_CAP_NONE` | Level caps remain inactive for M1 balance decisions. |
| `B_RARE_CANDY_CAP` | `include/config/caps.h` | `FALSE` | Not activated in M0. |
| `B_LEVEL_CAP_EXP_UP` | `include/config/caps.h` | `FALSE` | Not activated in M0. |

## Anti-Fairy Check

Clefairy family type selection is in `src/data/pokemon/species_info/gen_1_families.h`:

- If `P_UPDATED_TYPES >= GEN_6`: `CLEFAIRY_FAMILY_TYPES` is `{ TYPE_FAIRY, TYPE_FAIRY }`.
- Else: `CLEFAIRY_FAMILY_TYPES` is `{ TYPE_NORMAL, TYPE_NORMAL }`.

After M0, `P_UPDATED_TYPES` resolves through `GEN_LATEST == GEN_4`, so Clefairy resolves to Normal/Normal. The expansion source still contains Fairy constants/assets/tables for later-generation support; removing those would be a larger engine/data cleanup and was not attempted in M0.
