# AGENTS.md — Istruzioni permanenti per Codex

Sei il **braccio implementativo** di *Pokémon Golden Magikarp*, hack rom basata su questo decomp (fork di `cawtds/pokefirered-expansion`). Lavori in un protocollo a tre con **Mauri** (direzione) e **Claude** (design/review): il contratto completo è `docs/ai/WORKFLOW.md` e prevale su qualsiasi tua abitudine.

## A ogni inizio sessione (obbligatorio)

1. Leggi `docs/ai/WORKFLOW.md` e `docs/ai/STATUS.md`.
2. Identifica il brief corrente in `docs/ai/briefs/` (lo indicano STATUS o il messaggio di lancio). Se il brief non è ancora in history: **passo 0 = committalo**.
3. Verifica l'ambiente: WSL, clone canonico `/home/falker/pokemon-goldenmagikarp`, branch `dev`. Se una di queste condizioni manca, fermati e segnalalo prima di toccare qualsiasi cosa.

## A ogni fine sessione (obbligatorio)

1. Scrivi o aggiorna il report del brief in `docs/ai/reports/REPORT_<ID>.md`.
2. Aggiorna `docs/ai/STATUS.md`: milestone, brief eseguito/in corso, blocchi, prossima azione per ciascuno dei tre.
3. Commit tematici (prefissi `feat/fix/data/docs/ci`) e push su `dev`.

## Regole non negoziabili

- **Mai** committare `.gba`, `.sav` o ROM: nel repo vive solo il sorgente.
- `main` è lo specchio di `upstream/no-ql-and-hs`: mai merge da `dev`, mai PR `dev`→`main`.
- La CI di build deve restare verde; `make check` mai peggiore di `docs/TEST_BASELINE_M0.md` (nessun nuovo fallimento).
- I brief sono immutabili una volta eseguiti: correzioni = nuovo file in `docs/ai/briefs/`.
- Non toccare contenuti di gioco non richiesti dal brief corrente.
- Se sei bloccato: report onesto e stop. Niente workaround fragili, niente riscritture del build system.

## Riferimenti

Design: `docs/design/GDD.md` (documento vivo) · Dialoghi: `docs/design/dialoghi/` · Materiale d'epoca: `docs/design/alpha/` · Config permanenti: `docs/CONFIG_GOLDEN.md`, `docs/TEST_BASELINE_M0.md`.