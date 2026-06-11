# STATUS — Pokémon Golden Magikarp

*Ultimo aggiornamento: 11/06/2026 — redatto da Claude (versione iniziale; da qui in poi lo aggiorna Codex a fine sessione).*

## Milestone corrente

- **M0 — Fondamenta: CHIUSA.** Base `cawtds/pokefirered-expansion` branch `no-ql-and-hs` · build WSL riuscita (ROM `pokefirered.gba`, SHA1 `d6e02dee9954026b6a06d2b1946c42f99d7dc173`) · config GEN_4 verificata (Folletto assente, gen 1-4 ON / 5+ OFF) · CI: build/release bloccanti verdi, test non bloccante (run finale `27364310618`) · baseline test in `docs/TEST_BASELINE_M0.md` · 4 fix di build committati (candidati a PR upstream).
- **M1 — Porting Alpha: APERTA.** Binario A (Codex): brief `docs/ai/briefs/M1A_v2.md` — **non ancora eseguito**. Binario B (Claude): pacchetti dialoghi in ordine di storia — primo pacchetto (Biancavilla, `M1B_01`) **in preparazione**.

## Ultimo brief eseguito / in coda

- Eseguito: M0-ter (chiusura M0) — report in `docs/ai/reports/REPORT_M0.md` (post-migrazione cartelle).
- In coda: `M1A_v2.md` (trainer 1-3, lotte rivale, CAMORRISTA, sweep Magikarp/Gyarados, Pietraradio v2 + interfaccia a tre stati).
- Bootstrap workflow (`docs/ai/WORKFLOW.md`, sezione Bootstrap): **da eseguire** al prossimo lancio di Codex. Nota: questo STATUS.md esiste già — al bootstrap va solo aggiornato, non creato.

## Blocchi e azioni umane pendenti (Mauri)

1. Commit dei file di fondazione consegnati in chat: `docs/design/GDD.md` (v0.9 consolidato) · `docs/ai/WORKFLOW.md` · `docs/ai/briefs/M1A_v2.md` · `docs/design/dialoghi/lavandonia_incontro2_v1.md` · `docs/design/alpha/` (dialoghi estratti + inventario ROM) · questo file in `docs/ai/STATUS.md`.
2. Boot test manuale di `golden_magikarp_m0.gba` (sul Desktop) in mGBA Windows — ultima casella aperta della DoD di M0.
3. Rinomina della cartella Windows in `Pokemon Golden Magikarp_ARCHIVE` (era bloccata dall'IDE aperto).

## Prossima azione per ciascuno

- **Mauri:** punti 1-3 sopra; poi lancio di Codex col launcher standard su `M1A_v2`.
- **Codex:** bootstrap workflow + esecuzione `M1A_v2` → `docs/ai/reports/REPORT_M1A.md`, aggiornamento di questo file, push su `dev`.
- **Claude:** alla parola «pronto M1A», review di report e diff da GitHub; in parallelo, consegna del pacchetto dialoghi `M1B_01_biancavilla` (nella nuova chat).

## Promemoria convenzioni

Brief committato **prima** del lavoro · `main` solo specchio di upstream, mai merge da `dev` · niente `.gba`/`.sav` nel repo · `make check` mai peggiore della baseline M0.