# Codex — Golden Magikarp · M1-A v2 (Porting Alpha: dati e sistemi) — CONSOLIDATO

Questo file sostituisce integralmente il precedente M1-A e il Change Order #1. Ambiente: WSL, `/home/falker/pokemon-goldenmagikarp`, branch `dev`. M1 viaggia su due binari: **A = questo file** (dati e sistemi, nessuna dipendenza dai testi) · B = blocchi dialoghi scritti da Claude, che arriveranno con istruzioni di cablaggio proprie. Commit tematici su `dev`, push frequenti.

**Regole permanenti:** CI build verde · `make check`: nessun **nuovo** fallimento rispetto a `docs/TEST_BASELINE_M0.md` (confronto a fine milestone) · niente ROM committate · scelte non specificate: prendile se reversibili e documentate.

## Definition of Done

- [ ] Capipalestra 1-3 e lotte rivale aggiornati (3 varianti starter per ogni lotta rivale)
- [ ] Classe reclute rinominata **CAMORRISTA** (livello classe, non singoli trainer)
- [ ] Sweep Magikarp/Gyarados completo (encounter + trainer) con doc delle sostituzioni
- [ ] Pietraradio v2 implementata: 4 evoluzioni a sola pietra; 13 a pietra+strumento tenuto (consumato); **interfaccia a tre stati**; test di accettazione superati; item non in vendita/loot
- [ ] `docs/PIETRARADIO_ITEMS.md` (censimento disponibilità strumenti) e `docs/RIVAL_FIGHTS.md` (censimento lotte rivale vanilla residue, senza rimozioni)
- [ ] `docs/REPORT_M1A.md` + confronto baseline test

## 1 — Capipalestra (curva v1)

| Trainer | Squadra |
|---|---|
| Brock | RHYHORN L17, ONIX L18 |
| Misty | CLOYSTER L27, STARMIE L28 |
| Lt. Surge | ELECTABUZZ L33, JOLTEON L34, RAICHU L35 |

Niente IV/EV/nature custom alle prime tre palestre (arrivano dalla 4ª, fuori scope).

## 2 — Lotte rivale (starter invertito)

Lo starter del rivale è quello **debole** allo starter del giocatore:

| Giocatore | Rivale |
|---|---|
| CHARMANDER | BULBASAUR |
| SQUIRTLE | CHARMANDER |
| BULBASAUR | SQUIRTLE |

| Lotta | Squadra | Note |
|---|---|---|
| Laboratorio (Biancavilla) | starter L5 | struttura invariata |
| Percorso 22 | SPEAROW L9, starter L9 | come Alpha |
| Celestopoli | PIDGEY L18, MACHOP L18, starter L20 | stadio zero della squadra-firma (→ Pidgeotto/Machoke → Pidgeot/Machamp) |
| S.S. Anna | PIDGEOTTO L29, MACHOKE L29, starter L31 | ultima lotta prima della sparizione |

`docs/RIVAL_FIGHTS.md`: censisci le lotte rivale vanilla rimanenti (Torre di Lavandonia, Silph Co., Percorso 22 bis, Campione) con script/trainer ID e piano di rimozione/sostituzione futuro. **Non rimuoverle ora.**

## 3 — CAMORRISTA

Rename **a livello di classe trainer**: l'etichetta della classe delle reclute Rocket (es. `TRAINER_CLASS_TEAM_ROCKET` / stringa "TEAM ROCKET") diventa **CAMORRISTA**, coprendo ogni recluta del gioco. Verifica resa in lotta e nelle intro ("CAMORRISTA Tizio vuole battersi!") e larghezze textbox. Nomi propri dei singoli trainer invariati per ora. Documenta nel report dove vive la stringa e le occorrenze correlate (musica di classe, prize money: invariati).

## 4 — Sweep Magikarp/Gyarados

Regola di gioco: le due specie sono estinte.
1. **Encounter:** rimuovi MAGIKARP e GYARADOS da ogni tabella (erba, acqua, pesca con ogni amo). Sostituzioni di pari fascia e coerenza di rotta — base acquatica gen 1 (TENTACOOL, GOLDEEN, POLIWAG, KRABBY, HORSEA, PSYDUCK) — documentate per rotta in `docs/SWEEP_MAGIKARP.md`. Vecchio Amo (vanilla 100% Magikarp): placeholder con specie comuni di fascia bassa + TODO ("pesca rifiuti" arriverà con la vetrina ambientale).
2. **Trainer:** grep su tutte le squadre (classe Pescatore in testa), sostituzioni coerenti per tema e livello, elenco nel doc.
3. Verifica finale: `SPECIES_MAGIKARP` e `SPECIES_GYARADOS` devono comparire solo in definizioni di specie (dex/stats), mai in encounter o party.

## 5 — Pietraradio v2

### Regola di gioco
- **Scambio puro → sola PIETRARADIO** (pietra evolutiva standard): KADABRA→ALAKAZAM, MACHOKE→MACHAMP, GRAVELER→GOLEM, HAUNTER→GENGAR.
- **Scambio + strumento → PIETRARADIO mentre il Pokémon tiene lo strumento storico**, che viene **consumato** all'evoluzione:

| Specie | Strumento tenuto (verifica costanti in `include/constants/items.h`) | Esito |
|---|---|---|
| POLIWHIRL | ITEM_KINGS_ROCK | POLITOED |
| SLOWPOKE | ITEM_KINGS_ROCK | SLOWKING |
| ONIX | ITEM_METAL_COAT | STEELIX |
| SCYTHER | ITEM_METAL_COAT | SCIZOR |
| SEADRA | ITEM_DRAGON_SCALE | KINGDRA |
| PORYGON | ITEM_UP_GRADE | PORYGON2 |
| PORYGON2 | ITEM_DUBIOUS_DISC | PORYGON_Z |
| CLAMPERL | ITEM_DEEP_SEA_TOOTH | HUNTAIL |
| CLAMPERL | ITEM_DEEP_SEA_SCALE | GOREBYSS |
| RHYDON | ITEM_PROTECTOR | RHYPERIOR |
| ELECTABUZZ | ITEM_ELECTIRIZER | ELECTIVIRE |
| MAGMAR | ITEM_MAGMARIZER | MAGMORTAR |
| DUSCLOPS | ITEM_REAPER_CLOTH | DUSKNOIR |

### Implementazione (intento; adatta al codice reale)
1. Rinomina l'item Linking Cord in **PIETRARADIO** (nome + descrizione: "Una pietra che canalizza onde radio. Fa evolvere i POKéMON che un tempo si evolvevano solo con lo scambio.").
2. Scambio puro: `EVO_TRADE` delle 4 specie → `EVO_ITEM` con param `ITEM_PIETRARADIO`.
3. Scambio+strumento: metodo evolutivo dedicato (es. `EVO_ITEM_HELD_ITEM`: scatta se l'item usato è la PIETRARADIO **e** il Pokémon tiene l'item nel param; consuma l'item tenuto). Se la versione dell'expansion ha già condizioni evolutive componibili, usale e documenta.
4. **Interfaccia a tre stati** all'uso della PIETRARADIO nel party menu:
   - eleggibile → flusso evoluzione standard;
   - specie da scambio+strumento **senza** lo strumento → **"Serve {NOME STRUMENTO}."** (CLAMPERL senza nessuno dei due: **"Serve {A} o {B}."**);
   - tutte le altre → vanilla "Non avrà effetto" invariato.
   Le nuove stringhe nascono in italiano. Documenta nel report il punto del party menu dove si decide il messaggio.
5. PIETRARADIO **non** in vendita né in loot (sblocco a evento M2): TODO tracciabile.

### Test di accettazione
1. KADABRA + PIETRARADIO → ALAKAZAM.
2. SLOWPOKE senza strumento + PIETRARADIO → "Serve ROCCIA DI RE." (nome item come reso dal gioco), nessuna evoluzione, pietra non consumata.
3. SLOWPOKE con Roccia di Re + PIETRARADIO → SLOWKING, strumento consumato.
4. CLAMPERL: Dente Abissale → HUNTAIL · Squama Abissale → GOREBYSS · senza nulla → messaggio a due rami.
5. PIDGEY + PIETRARADIO → "Non avrà effetto".

### Censimento strumenti (solo report)
Per ogni strumento della tabella: esiste in FR vanilla/Sevii (dove)? è definito nell'expansion ma senza fonte in-game? Tabella in `docs/PIETRARADIO_ITEMS.md`. I piazzamenti nel mondo sono lavoro delle milestone mappe.

## 6 — Report

`docs/REPORT_M1A.md`: cosa fatto per sezione · file toccati · esito test di accettazione Pietraradio · confronto `make check` vs baseline · link run CI · decisioni autonome · domande per il team.