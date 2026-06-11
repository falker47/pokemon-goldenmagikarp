# STATUS — Pokémon Golden Magikarp

*Ultimo aggiornamento: 11/06/2026 — redatto da Codex dopo esecuzione M1A.*

## Milestone corrente

- **M0 — Fondamenta: CHIUSA.** Base `cawtds/pokefirered-expansion` branch `no-ql-and-hs`; build WSL riuscita; config GEN_4 verificata; baseline test in `docs/TEST_BASELINE_M0.md`; report in `docs/ai/reports/REPORT_M0.md`.
- **M1 — Porting Alpha: APERTA.** Binario A (Codex): `docs/ai/briefs/M1A_v2.md` eseguito e in attesa review Claude. Binario B (Claude): pacchetti dialoghi in ordine di storia, primo pacchetto `M1B_01` in preparazione.

## Ultimo brief eseguito / in review

- Eseguito: `M1A_v2.md` — trainer 1-3, prime lotte rivale, CAMORRISTA, sweep Magikarp/Gyarados, Pietraradio v2.
- Report: `docs/ai/reports/REPORT_M1A.md`.
- Censimenti collegati: `docs/ai/reports/SWEEP_MAGIKARP.md`, `docs/ai/reports/PIETRARADIO_ITEMS.md`, `docs/ai/reports/RIVAL_FIGHTS.md`.

## Blocchi e azioni umane pendenti (Mauri)

- Nessun blocco Codex attivo su M1A.
- Dopo push su `dev`, dire a Claude: «pronto M1A».
- Facoltativo ma utile: smoke test manuale in mGBA della Pietraradio e delle prime tre lotte rivale.
- Operativo non bloccante: rinomina della cartella Windows archivio quando l'IDE non la tiene aperta.

## Prossima azione per ciascuno

- **Mauri:** avvisare Claude per review M1A; poi decidere eventuale change order o passaggio a M1B.
- **Codex:** attendere review o nuovo brief; non toccare contenuti fuori brief.
- **Claude:** leggere report e diff GitHub di M1A; rispondere con CHIUSO / punch list / change order; proseguire con `M1B_01_biancavilla`.

## Qualità e promemoria

- `make -j`: verde locale su M1A.
- `make check -j4`: non-zero come baseline; `FAILED` resta 125, `ASSUMPTIONS_FAILED` passa da 72 a 78.
- CI GitHub: da verificare dopo push.
- Convenzioni permanenti: brief committato prima del lavoro; `main` solo specchio upstream; niente `.gba`/`.sav` nel repo; `make check` mai peggiore della baseline M0.
