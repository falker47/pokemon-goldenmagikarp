# Golden Magikarp Alpha — Inventario tecnico della ROM

## Identità
- Base: Pokémon FireRed US, BPRE rev. 0 (v1.0) — la versione standard per gli offset noti
- Dimensione: 16 MB, MD5 `106439db9922d007e4ff0e8c692d7670`

## Testi
- 777 stringhe italiane uniche (~12.200 parole, ~71.000 caratteri), vedi file dialoghi
- Distribuzione: script di gioco 0x172000–0x1CFFFF (traduzione in-place + ripuntamenti XSE),
  più blocchi tradotti tra i testi enciclopedici (0x3D0000–0x490000: Pokédex/descrizioni) e Sevii (0x71xxxx)
- La traduzione copre la storia all’incirca fino a Lavandonia; oltre, testo inglese vanilla

## Trainer (tabella gTrainers @0x23EAC8, 742 entry parsate)
Capipalestra modificati rispetto a vanilla:
- #414 BROCK: **RHYHORN L17, ONIX L18**  (vanilla: GEODUDE L12, ONIX L14)
- #415 MISTY: **CLOYSTER L27, STARMIE L28**  (vanilla: STARYU L18, STARMIE L21)
- #416 LT. SURGE: **ELECTABUZZ L36, JOLTEON L37, RAICHU L38**  (vanilla: VOLTORB L21, PIKACHU L18, RAICHU L24)
- Da ERIKA (#417) in poi: squadre identiche a vanilla FR (verificato su Koga, Sabrina, Blaine, Giovanni, Superquattro 1°/2° giro)
- Reclute Team Rocket rinominate **POKéMAFIOSO** (trainer #352–356) — seme dell’idea Camorra già presente
- Rivale (entry dati `TERRY`, il nome reale è custom da naming screen): primi scontri ritoccati (SPEAROW al posto di PIDGEY)

## Free space / dati inseriti
- 0xD00000–0xEB2000 (~1,7 MB): grafica compressa LZ77 (~3.860 blocchi) — con ogni probabilità un ROM base di tileset/sprite applicato all’epoca
- 0xF03000–0xF0D000 (~28 KB) e 0xFFF000–fine: dati ripuntati (mappe AdvanceMap / script)

## Implicazioni per il porting su decomp (pret/pokefirered)
- Dialoghi → reinserire nelle `scripts.inc`/`text.inc` delle mappe corrispondenti (gli offset seguono l’ordine di storia, il mapping è quasi meccanico)
- Squadre trainer → `src/data/trainers.h` + `src/data/trainer_parties.h` (Brock/Misty/Surge già pronti da questo inventario)
- Pokédex/descrizioni tradotte → `src/data/pokemon/pokedex_text.h` e affini
- Grafica del ROM base: da reinserire solo se la riconosci e la vuoi; altrimenti si riparte da tileset puliti in Porymap