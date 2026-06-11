# PIETRARADIO_ITEMS — Censimento strumenti M1A

Output M1A spostato in `docs/ai/reports/` secondo `docs/ai/WORKFLOW.md`.

## Sintesi

La Pietraradio e gli strumenti storici sono definiti nell'expansion. Solo una parte degli strumenti ha una fonte garantita in FR/LG o Sevii nello stato attuale del repo; i piazzamenti mancanti restano lavoro delle milestone mappe/eventi.

La Pietraradio è `ITEM_LINKING_CORD` rinominato via dati item più alias `ITEM_PIETRARADIO`; non risulta in vendita né in loot/eventi mappa nello sweep statico M1A.

## Tabella

| Strumento | Costante | Stato dati | Fonte garantita trovata | Nota M1A |
|---|---|---|---|---|
| Pietraradio | `ITEM_PIETRARADIO` (`ITEM_LINKING_CORD`) | Definita e rinominata | Nessuna in `data/maps`, `data/scripts`, `src/data/shops.h` | Sblocco evento M2; prezzo 0. |
| Roccia di Re | `ITEM_KINGS_ROCK` | Definita | `data/scripts/item_ball_scripts.inc` (`SevenIsland_SevaultCanyon_EventScript_ItemKingsRock`); Battle Frontier Exchange Service Corner, 64 BP | Fonte Sevii + BP. |
| Metalcoperta | `ITEM_METAL_COAT` | Definita | `data/scripts/item_ball_scripts.inc` (`FiveIsland_MemorialPillar_EventScript_ItemMetalCoat`) | Fonte Sevii. |
| Squama Drago | `ITEM_DRAGON_SCALE` | Definita | `data/scripts/item_ball_scripts.inc` (`SixIsland_WaterPath_EventScript_ItemDragonScale`) | Fonte Sevii. |
| Upgrade | `ITEM_UP_GRADE` / `ITEM_UPGRADE` | Definita | `data/scripts/item_ball_scripts.inc` (`FiveIsland_RocketWarehouse_EventScript_ItemUpGrade`) | Fonte Sevii. |
| Dubbiodisco | `ITEM_DUBIOUS_DISC` | Definita | Nessuna fonte garantita trovata | Da piazzare in milestone mappe/eventi. |
| Dente Abissale | `ITEM_DEEP_SEA_TOOTH` | Definita | Nessuna fonte garantita trovata | Presente anche come wild held item in dati specie; non conta come pickup/shop garantito. |
| Squama Abissale | `ITEM_DEEP_SEA_SCALE` | Definita | Nessuna fonte garantita trovata | Presente anche come wild held item in dati specie; non conta come pickup/shop garantito. |
| Copertura | `ITEM_PROTECTOR` | Definita | Nessuna fonte garantita trovata | Da piazzare in milestone mappe/eventi. |
| Elettritore | `ITEM_ELECTIRIZER` | Definita | Nessuna fonte garantita trovata | Presente anche come wild held item in dati specie; non conta come pickup/shop garantito. |
| Magmatore | `ITEM_MAGMARIZER` | Definita | Nessuna fonte garantita trovata | Presente anche come wild held item in dati specie; non conta come pickup/shop garantito. |
| Terrorpanno | `ITEM_REAPER_CLOTH` | Definita | Nessuna fonte garantita trovata | Da piazzare in milestone mappe/eventi. |

## Grep usati

- `git grep -n -E 'ITEM_(PIETRARADIO|LINKING_CORD|KINGS_ROCK|METAL_COAT|DRAGON_SCALE|UP_GRADE|UPGRADE|DUBIOUS_DISC|DEEP_SEA_TOOTH|DEEP_SEA_SCALE|PROTECTOR|ELECTIRIZER|MAGMARIZER|REAPER_CLOTH)' -- data/maps data/scripts src/data/shops.h src/data/pokemon/species_info src/data/items.h include/constants/items.h`
- `git grep -n -E 'ITEM_PIETRARADIO|ITEM_LINKING_CORD' -- data/maps data/scripts src/data/shops.h`
