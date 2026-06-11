# REPORT_M1A — Porting Alpha dati e sistemi

## Ambiente e passo 0

- Workflow letto: `docs/ai/WORKFLOW.md` e `docs/ai/STATUS.md`.
- Ambiente verificato: WSL, clone canonico `/home/falker/pokemon-goldenmagikarp`, branch `dev`.
- `git pull --ff-only` eseguito; HEAD di partenza aggiornato a `dc09488bf` o successivo.
- Passo 0: `docs/ai/briefs/M1A_v2.md` era già in history (`c1ff8cb1b`), quindi non è stato ricommittato.
- Bootstrap workflow: già eseguito da Mauri nei commit `c1ff8cb1b` e `dc09488bf`; verificata la struttura `docs/ai/briefs/`, `docs/ai/reports/`, `docs/design/`.

## Cosa è stato fatto

### Capipalestra 1-3

- Brock: `RHYHORN` L17, `ONIX` L18.
- Misty: `CLOYSTER` L27, `STARMIE` L28.
- Lt. Surge: `ELECTABUZZ` L33, `JOLTEON` L34, `RAICHU` L35.
- Nessun IV/mosse/nature custom aggiunto alle prime tre palestre.

File principale: `src/data/trainers.party`.

### Rivale

- Starter invertito in laboratorio: il rivale prende lo starter debole allo starter del giocatore.
- Lotte M1A aggiornate:
  - Laboratorio: starter L5, struttura invariata.
  - Percorso 22 early: `SPEAROW` L9 + starter L9.
  - Celestopoli: `PIDGEY` L18, `MACHOP` L18, starter L20.
  - S.S. Anna: `PIDGEOTTO` L29, `MACHOKE` L29, starter L31.
- I dispatch starter delle lotte vanilla residue sono stati allineati alla nuova convenzione ma non rimossi.

Censimento residue: `docs/ai/reports/RIVAL_FIGHTS.md`.

### CAMORRISTA

- La classe `TRAINER_CLASS_TEAM_ROCKET` ora rende `CAMORRISTA`.
- Stringa in `src/battle_main.c`, tabella `gTrainerClassNames`.
- Musica classe e prize money non modificati.

### Sweep Magikarp/Gyarados

- Rimossi `SPECIES_MAGIKARP` e `SPECIES_GYARADOS` da encounter, party trainer, trainer tower, Battle Frontier, fonti scriptate principali e default Waterfall.
- Le sostituzioni encounter preservano livelli e probabilità; i vecchi slot Old Rod sono placeholder di specie comuni con TODO per la futura “pesca rifiuti”.
- Route 4 gift e Route 12 record ora usano `GOLDEEN`.
- Default Waterfall ora usa `SEADRA`.

Censimento completo: `docs/ai/reports/SWEEP_MAGIKARP.md`.

### Pietraradio v2

- `ITEM_LINKING_CORD` è rinominato in gioco come `PIETRARADIO`; aggiunto alias `ITEM_PIETRARADIO`.
- Descrizione italiana aggiunta nei dati item.
- Evoluzioni da scambio puro convertite a `EVO_ITEM, ITEM_PIETRARADIO`: Kadabra, Machoke, Graveler, Haunter.
- Evoluzioni scambio+strumento convertite a `EVO_ITEM, ITEM_PIETRARADIO` con condition `IF_HOLD_ITEM`: 13 rami su 12 specie base (Poliwhirl, Slowpoke, Onix, Scyther, Seadra, Porygon, Porygon2, Clamperl x2, Rhydon, Electabuzz, Magmar, Dusclops).
- Il consumo dello strumento tenuto usa il percorso esistente `DoesMonMeetAdditionalConditions(..., DO_EVO)`.
- In `src/party_menu.c` è stata aggiunta la UI a tre stati:
  - eleggibile: flusso evoluzione standard;
  - specie da Pietraradio+strumento senza requisito: messaggio `Serve {STRUMENTO}.`;
  - Clamperl senza requisito: messaggio `Serve {A} o {B}.`;
  - altre specie: messaggio vanilla invariato.
- La Pietraradio non risulta in vendita né in loot/eventi mappa nello sweep statico M1A.

Censimento strumenti: `docs/ai/reports/PIETRARADIO_ITEMS.md`.

## File toccati

- Dati trainer e classi: `src/data/trainers.party`, `src/battle_main.c`.
- Script mappe rivale/fonti scriptate: `data/maps/PalletTown_ProfessorOaksLab/scripts.inc`, `data/maps/Route22/scripts.inc`, `data/maps/CeruleanCity/scripts.inc`, `data/maps/SSAnne_2F_Corridor/scripts.inc`, `data/maps/PokemonTower_2F/scripts.inc`, `data/maps/SilphCo_7F/scripts.inc`, `data/maps/PokemonLeague_ChampionsRoom/scripts.inc`, `data/maps/Route4_PokemonCenter_1F/*`, `data/maps/Route12_FishingHouse/*`.
- Encounter e fonti side battle: `src/data/wild_encounters.json`, `src/trainer_tower_sets.c`, `src/frontier_util.c`, `src/data/battle_frontier/*`.
- Pietraradio/evoluzioni: `include/constants/items.h`, `src/data/items.h`, `src/data/pokemon/species_info/gen_1_families.h`, `src/data/pokemon/species_info/gen_3_families.h`, `src/party_menu.c`.
- Fonti scriptate/utility specie: `src/pokemon_size_record.c`, `src/field_move.c`.
- Report: `docs/ai/reports/REPORT_M1A.md`, `docs/ai/reports/PIETRARADIO_ITEMS.md`, `docs/ai/reports/SWEEP_MAGIKARP.md`, `docs/ai/reports/RIVAL_FIGHTS.md`.

## Test di accettazione Pietraradio

Verifica statica + build:

| Caso | Esito |
|---|---|
| Kadabra + Pietraradio | `EVO_ITEM, ITEM_PIETRARADIO -> ALAKAZAM` presente. |
| Slowpoke senza Roccia di Re | Party menu intercetta la specie Pietraradio+strumento e mostra `Serve {STRUMENTO}.` senza avviare evoluzione. |
| Slowpoke con Roccia di Re | `EVO_ITEM, ITEM_PIETRARADIO -> SLOWKING` con `IF_HOLD_ITEM, ITEM_KINGS_ROCK`; il path `DO_EVO` consuma lo strumento. |
| Clamperl | Due rami `DEEP_SEA_TOOTH -> HUNTAIL` e `DEEP_SEA_SCALE -> GOREBYSS`; senza requisito mostra il messaggio a due strumenti. |
| Pidgey + Pietraradio | Nessun ramo Pietraradio; cade sul messaggio vanilla “Non avrà effetto”. |

Non è stato eseguito un playtest manuale mGBA in questa sessione.

## Verifiche

- `make -j`: riuscito, build verde locale.
- `make check -j4`: eseguito; exit non-zero come baseline. Confronto runner:
  - M0 baseline: `FAILED 125`, `KNOWN_FAILING 10`, `ASSUMPTIONS_FAILED 72`, `TO_DO 625`, `EXPECT_FAILING 6`, `PASSED 4373`, `TOTAL 5211`.
  - M1A locale: `FAILED 125`, `KNOWN_FAILING 10`, `ASSUMPTIONS_FAILED 78`, `TO_DO 625`, `EXPECT_FAILING 6`, `PASSED 4373`, `TOTAL 5217`.
  - Nessun aumento del conteggio `FAILED`; le assumption failure aumentano di 6 e sono riportate per review.
- Sweep specie mirato: nessun `SPECIES_MAGIKARP`/`SPECIES_GYARADOS` rimasto in encounter/party/scripted sources toccati. Le occorrenze residue sono definizioni specie/dex/form/easy chat e test battle upstream, non sorgenti encounter o party.
- Pietraradio availability: nessun `ITEM_PIETRARADIO`/`ITEM_LINKING_CORD` trovato in `data/maps`, `data/scripts`, `src/data/shops.h`.

## CI

Build locale verde. Link/run CI GitHub da verificare dopo il push di questo commit su `dev`.

## Decisioni autonome

- Le fonti scriptate Magikarp/Gyarados non esplicitamente “trainer/encounter” ma giocabili sono state sostituite per coerenza con l'estinzione.
- I nomi interni di alcune label storiche (`MagikarpRecord`, ecc.) non sono stati rinominati per evitare churn non richiesto.
- I rami `ITEM_LINKING_CORD` su specie fuori scope o disabilitate da config GEN_5+ non sono stati riscritti, salvo casi GEN 1-4 richiesti.
- Dove il brief chiedeva `docs/<nome>.md`, i documenti sono stati creati in `docs/ai/reports/` secondo `WORKFLOW.md`.

## Domande per review

- Confermare se in M2 la Pietraradio va introdotta come evento unico, ricorrente, o premio narrativo.
- Decidere se i nomi degli strumenti storici vadano italianizzati in modo sistematico prima dei playtest lunghi.
- Decidere se i residui vanilla del rivale vanno rimossi tutti insieme o pacchettizzati per arco narrativo.
