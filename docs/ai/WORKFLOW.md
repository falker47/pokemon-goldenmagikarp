# WORKFLOW.md — Protocollo AI a tre · Pokémon Golden Magikarp

Contratto operativo tra **Mauri** (direttore), **Claude** (mente) e **Codex** (braccio). Vive in `docs/ai/WORKFLOW.md`. Ogni agente lo rispetta; le modifiche al protocollo le approva Mauri.

## Ruoli

- **Mauri** — direzione creativa e product owner: decide, playtesta, esegue i passi solo-umani (auth, installazioni, boot test), trasporta i file Claude→repo.
- **Claude** — design lead: GDD, dialoghi, brief per Codex, review. Non ha accesso in scrittura al repo; **legge il repo pubblico direttamente da GitHub** (report, diff, commit), quindi la review avviene sui fatti committati.
- **Codex** — implementazione: esegue i brief in WSL nel clone canonico (`/home/falker/pokemon-goldenmagikarp`, branch `dev`), committa, pusha, riporta.

## Struttura

```
docs/
  ai/
    WORKFLOW.md          ← questo file
    STATUS.md            ← stato corrente (aggiornato da Codex a fine sessione)
    briefs/              ← specifiche Claude→Codex (immutabili una volta eseguite)
    reports/             ← report Codex→team (REPORT_<id>.md, build log)
  design/
    GDD.md               ← Game Design Document VIVO (le versioni sono i commit)
    dialoghi/            ← pacchetti dialoghi consegnati da Claude
  CONFIG_GOLDEN.md       ← riferimento permanente config (resta qui)
  TEST_BASELINE_M0.md    ← riferimento permanente baseline test (resta qui)
```

## Ciclo standard

1. **Design:** Mauri e Claude decidono in chat; Claude produce un brief (`<ID>.md`) ed eventuale GDD aggiornato.
2. **Trasporto:** Mauri salva il brief in `docs/ai/briefs/` (e il GDD in `docs/design/GDD.md` se aggiornato).
3. **Lancio:** Mauri incolla a Codex il *launcher* (sotto). **Passo 0 di ogni task: commit del brief**, così la spec entra nella history PRIMA del lavoro.
4. **Esecuzione:** Codex lavora con commit tematici, scrive `docs/ai/reports/REPORT_<ID>.md`, aggiorna `STATUS.md`, pusha su `dev`.
5. **Review:** Mauri scrive a Claude solo «pronto `<ID>`». Claude legge report e diff da GitHub e risponde con verdetto: **CHIUSO** / punch list / change order (= nuovo brief).
6. Nuovo giro.

## Launcher standard (testo da incollare a Codex)

> Leggi `docs/ai/WORKFLOW.md` e rispettalo. Esegui il brief `docs/ai/briefs/<ID>.md`: come passo 0, committa il brief se non è già in history. A fine lavoro scrivi `docs/ai/reports/REPORT_<ID>.md`, aggiorna `docs/ai/STATUS.md`, committa e pusha su `dev`.

## Convenzioni

- **Brief immutabili:** un brief eseguito non si modifica mai; correzioni = nuovo file (`<ID>_v2.md` o change order). Ogni pacchetto è diffabile: range dal commit-brief al commit-report.
- **Branch:** `dev` = lavoro; `main` = specchio di `upstream/no-ql-and-hs`, si aggiorna solo da upstream; **mai** merge `dev`→`main`.
- **Commit:** prefissi `feat/fix/data/docs/ci`, messaggi parlanti, tematici.
- **Qualità:** CI build bloccante e verde; `make check` mai peggiore di `docs/TEST_BASELINE_M0.md` (confronto a fine milestone).
- **Legale:** mai committare `.gba`/`.sav` o ROM; nel repo vive solo il sorgente; la distribuzione futura sarà a patch.
- **GDD:** file vivo; ogni aggiornamento un commit `gdd: v0.N — <sintesi>`.
- **Output dei brief:** ogni nuovo documento prodotto da Codex va in `docs/ai/reports/` anche se il brief cita `docs/<nome>.md` (rimappatura automatica), eccetto i due riferimenti permanenti elencati sopra.

## STATUS.md (formato minimo)

Milestone corrente e stato · ultimo brief eseguito/in corso · blocchi e domande per Mauri o Claude · prossima azione per ciascuno dei tre. Aggiornato da Codex a fine sessione.

## Bootstrap (una tantum, prima adozione)

1. `mkdir -p docs/ai/briefs docs/ai/reports docs/design/dialoghi`
2. `git mv docs/REPORT_M0.md docs/ai/reports/` e `git mv docs/build_log_m0*.txt docs/ai/reports/` (history preservata). `CONFIG_GOLDEN.md` e `TEST_BASELINE_M0.md` restano in `docs/`.
3. Crea `docs/ai/STATUS.md` col formato minimo.
4. Commit: `docs: adotta workflow AI a tre (docs/ai)`.

## Regole d'oro

- Codex si lancia SOLO in WSL nel clone canonico; il workspace Windows è archivio.
- Se bloccato: report onesto e stop — un fallimento documentato vale più di un workaround fragile.
- Le decisioni di design le prende Mauri; Claude propone; Codex implementa. I tre livelli non si scavalcano.