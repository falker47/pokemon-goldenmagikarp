# RIVAL_FIGHTS — Residui vanilla rivale M1A

Output M1A spostato in `docs/ai/reports/` secondo `docs/ai/WORKFLOW.md`.

## Sintesi

M1A aggiorna le prime quattro lotte del rivale e inverte la logica starter per coerenza. Le lotte vanilla successive restano in piedi, come richiesto dal brief, ma sono censite qui per una rimozione o sostituzione futura.

## Lotte residue

| Blocco | Script | Trainer ID | Stato M1A | Piano futuro |
|---|---|---|---|---|
| Torre Pokémon, Lavandonia | `data/maps/PokemonTower_2F/scripts.inc` | `TRAINER_RIVAL_POKEMON_TOWER_SQUIRTLE`, `TRAINER_RIVAL_POKEMON_TOWER_BULBASAUR`, `TRAINER_RIVAL_POKEMON_TOWER_CHARMANDER` | Non rimossa; dispatch starter invertito per coerenza | Sostituire o rimuovere nel pacchetto narrativo Lavandonia. |
| Silph Co. 7F | `data/maps/SilphCo_7F/scripts.inc` | `TRAINER_RIVAL_SILPH_SQUIRTLE`, `TRAINER_RIVAL_SILPH_BULBASAUR`, `TRAINER_RIVAL_SILPH_CHARMANDER` | Non rimossa; dispatch starter invertito per coerenza | Sostituire durante rewrite Silph/Rocket. |
| Percorso 22 bis | `data/maps/Route22/scripts.inc` | `TRAINER_RIVAL_ROUTE22_LATE_SQUIRTLE`, `TRAINER_RIVAL_ROUTE22_LATE_BULBASAUR`, `TRAINER_RIVAL_ROUTE22_LATE_CHARMANDER` | Non rimossa; dispatch starter invertito per coerenza | Rimuovere o sostituire con gate late-game quando la nuova curva finale sarà definita. |
| Campione, prima run | `data/maps/PokemonLeague_ChampionsRoom/scripts.inc` | `TRAINER_CHAMPION_FIRST_SQUIRTLE`, `TRAINER_CHAMPION_FIRST_BULBASAUR`, `TRAINER_CHAMPION_FIRST_CHARMANDER` | Non rimossa; dispatch starter invertito per coerenza; Gyarados sostituito nello sweep specie | Rewrite champion in milestone dedicata. |
| Campione, rematch | `data/maps/PokemonLeague_ChampionsRoom/scripts.inc` | `TRAINER_CHAMPION_REMATCH_SQUIRTLE`, `TRAINER_CHAMPION_REMATCH_BULBASAUR`, `TRAINER_CHAMPION_REMATCH_CHARMANDER` | Non rimossa; dispatch starter invertito per coerenza; Gyarados sostituito nello sweep specie | Rewrite champion/rematch in milestone dedicata. |

## Note implementative

- Le tre prime lotte richieste dopo il laboratorio sono aggiornate in `src/data/trainers.party`: Percorso 22, Celestopoli, S.S. Anna.
- La selezione starter nel laboratorio ora assegna al rivale lo starter debole a quello del giocatore: Charmander -> Bulbasaur, Squirtle -> Charmander, Bulbasaur -> Squirtle.
- I residui sopra non sono stati rimossi per rispettare il brief; i loro script sono stati solo allineati alla nuova convenzione starter, così non restano varianti incoerenti nel frattempo.
