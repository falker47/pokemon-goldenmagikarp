# Pokémon Golden Magikarp — Game Design Document

**Versione 0.9 — CONSOLIDAMENTO INTEGRALE.** Questo documento fonde le versioni v0.1→v0.8 in un unico testo completo e autosufficiente: nessuna decisione nuova. Da qui in poi vive in `docs/design/GDD.md` come documento unico; le versioni successive saranno sempre file completi sostitutivi e i diff li traccia git.

Legenda: `[APERTO]` = decisione da prendere · `[BOZZA]` = proposta da bilanciare · `[PROPOSTA]` = scelta di Claude applicata salvo veto.

---

## 1. Pitch e linea temporale

Hack rom di Pokémon Rosso Fuoco ambientata **16 anni dopo** gli eventi del gioco originale, in **continuità canonica con Oro/Argento**. Kanto, Johto e Hoenn attraversano una grave crisi ambientale che ha decimato molte specie, portandone alcune all'estinzione — tra cui i Magikarp. **La causa di fondo è il cambiamento climatico**: il gioco sensibilizza trasponendo sul mondo Pokémon effetti reali, presenti e futuri. Il protagonista indaga insieme a un Prof. Oak vecchio, tossicodipendente e in bancarotta, alla Prof.ssa Vera e a una galleria di personaggi nuovi e storici. Tono: commedia satirica sulle dinamiche fallaci del mondo Pokémon, condita di attualità. Target: giocatori esperti.

**Timeline:**
- **T−3** — nasce Falker a Lavandonia.
- **T0** — eventi di Rosso Fuoco. La famiglia di Falker si trasferisce a Quartisola (la madre porta con sé il Cubone orfano). Disastro Master Ball/Rattata del futuro rivale.
- **T3** — eventi di Oro/Argento: **l'eroe di GSC è canonico** (`[APERTO: nome — proposta attiva: Ethan]`) e smantella i resti del Team Rocket alla Torre Radio di Fiordoropoli; Torre Pokémon di Lavandonia → Torre Radio; eruzione e distruzione di Isola Cannella; Blue capopalestra a Smeraldopoli; Lance campione; Rocket sciolto definitivamente.
- **T8** — programma di reintroduzione di specie da Hoenn guidato da Vera.
- **~T14-15** — Falker, eletta da Red (ultimo campione), rifonda la Lega.
- **T16** — Golden Magikarp. Falker ha 19 anni; l'eroe di GSC ~24-25; il rivale ~15-16.

**Regola assoluta di coerenza:** **Magikarp e Gyarados non esistono in gioco** — nessun selvatico, nessun trainer, nessun boss. Unica eccezione: il Magikarp Dorato (§8). Conseguenze: bonifica encounter (inclusa la pesca), rework dei trainer Pescatore, Blue usa **Blastoise**.

## 2. Pilastri di design

1. **La comicità sta nei dialoghi.** Voice bible: i testi della Alpha (`golden_magikarp_dialoghi_estratti.md`).
2. **Il mistero Falker** — identità celata via scrittura al neutro, incontri in incognito, indizio opzionale dal padre.
3. **Difficoltà expert** — boss con strumenti tenuti, IV/EV e nature dalla 4ª palestra; IA avanzata sui boss finali.
4. **Estetica FR pulita** (tileset da zero, ROM base della Alpha scartato), **meccaniche gen 4**, Folletto OFF.
5. **Lore e gameplay si giustificano a vicenda** — MN, Pietraradio, fauna di Hoenn, crisi climatica.
6. **Continuità GSC:** i macro-fatti sono vincolanti; la Lega è stata rifondata da Falker → composizione libera.
7. **Divulgazione scientifica reale** (§12), con la disinformazione come bersaglio satirico.

## 3. Stack tecnico e governance

- **Base:** `cawtds/pokefirered-expansion`, branch `no-ql-and-hs`. Repo: `falker47/pokemon-goldenmagikarp` (`main` = specchio upstream, `dev` = gioco, mai merge dev→main).
- **Config:** split fisico/speciale ON; dati mosse/abilità/statistiche/evoluzioni a GEN_4; specie gen 1-4 ON, gen 5+ OFF; Folletto OFF (verificato: Clefairy = Normale); exp share moderno e level cap documentati, attivazione in bilanciamento.
- **Qualità:** CI build bloccante; `make check` mai peggiore di `docs/TEST_BASELINE_M0.md`.
- **Processo:** `docs/ai/WORKFLOW.md` (Mauri direzione · Claude design/dialoghi/brief/review · Codex implementazione).
- **Strumenti:** Porymap per le mappe; brief in `docs/ai/briefs/`, report in `docs/ai/reports/`.

## 4. Personaggi

### Prof. Oak
Vecchio, tossicodipendente, in bancarotta **per piano deliberato della Camorra** (§5): tramite il nipote gli hanno smantellato l'impero economico. Detonatore già scritto nella Alpha: il nipote usò la sua unica Master Ball (2 mln di Pokédollari) per catturare un Rattata, poi liberato. **Arco di redenzione:** si rende conto del tracollo, passa il testimone a Falker e si ritira con **Agatha** — coetanei e rivali di gioventù nel canone FRLG, quindi la **romance senile** è canon-compatibile. `[PROPOSTA]` Centro anziani = Casa Volontari di Fuji a Lavandonia. Partecipa al WPT (§9).

### La famiglia Oak (motore satirico)
Nonno Oak; **Daisy** (superquattro); **Blue** (8° capopalestra, canon GSC); il **rivale**, terzogenito e pecora nera. La battuta di Daisy ("Kanto è una repubblica fondata sulla raccomandazione") rende la satira sul nepotismo autoconsapevole, rafforzata da Janine che eredita la palestra dal padre.

### Il Rivale
- **Identità:** fratello minore di Blue e Daisy, nipote di Oak, nato dopo T0 (~15-16 anni). Nome custom da naming screen (entry dati `TERRY`; nei testi Alpha parla col placeholder `É:` → buffer del nome).
- **Arco:** Atto 1 inetto comico → **sparizione dopo la 2ª medaglia** (subito dopo l'ultima lotta sulla S.S. Anna); un assistente di Oak ad Aranciopoli chiede di lui → **covo di Azzurropoli** (ex Team Rocket, acquisito dalla Camorra): finto rapimento, il giocatore lo libera, lui ringrazia e sparisce di nuovo → **resa dei conti post-7ª medaglia alla Terra dei Fuochi**: reveal, monologo, boss fight → **redenzione**: capisce gli sbagli; nel post-game è l'informatore che aiuta a smascherare il Presidente `[BOZZA]`.
- **Monologo del reveal (v1.1, testo di Mauri con fix di genere):**
  > "Secondo te posso davvero essere così scemo? È sempre stato tutto un piano per liberarmi dalle pressioni della mia famiglia e vivere come voglio io! Non ne potevo più di vivere all'ombra dei miei fratelli, Blue capopalestra e Daisy superquattro, e dovermi sentir dire da mio nonno: «[nome rivale], ma quando diventi un allenatore Pokémon anche tu? Appena hai una squadra ti trovo il posto fisso come capopalestra di Plumbeopoli. Così è la volta buona che tolgono l'immunità parlamentare a Brock e lo sbattono in galera.» Ma a me non me ne frega nulla di tutto ciò, si tenesse la palestra quel pedofilo! Io volevo solo avere una villa a Primisola e chillare nell'idromassaggio con un Gardevoir, Lopunny e Vaporeon. Ma per fare questo servono i cash. Ed è per questo che ho stretto accordi con la Camorra, ho smantellato l'impero economico di mio nonno, conquistandomi la fiducia del boss. Sono a un passo dal mio sogno, e tu non mi fermerai!"
- **Lotte e squadre** (3 varianti: il suo starter è quello **debole** allo starter del giocatore — l'inetto ha sbagliato perfino la scelta del giorno uno):

| Lotta | Squadra |
|---|---|
| Laboratorio (Biancavilla) | starter L5 |
| Percorso 22 | SPEAROW L9, starter L9 |
| Celestopoli | PIDGEY L18, MACHOP L18, starter L20 |
| S.S. Anna (ultima prima della sparizione) | PIDGEOTTO L29, MACHOKE L29, starter L31 |
| Resa dei conti (Terra dei Fuochi) `[BOZZA livelli]` | starter L56, MACHAMP L55, GARDEVOIR L55, VAPOREON L54, PIDGEOT L54, LOPUNNY L53 |

Letture di design: tre stadi visibili della squadra-firma (Pidgey/Machop → Pidgeotto/Machoke → Pidgeot/Machamp: l'unica cosa che ha sempre fatto bene è allenare quei due); il trio del sogno (Gardevoir/Lopunny/Vaporeon) comprato coi soldi della Camorra; Machamp implica l'uso della Pietraradio.

### Prof.ssa Vera (= May, figlia di Birch)
Professoressa brillante da Hoenn. Autrice del **programma di reintroduzione (T8, riuscito)**: specie di Hoenn importate per stabilizzare gli ecosistemi — giustificazione in-world della fauna gen 3 (le "zone risanate" sono gli habitat gen 3). **Unico punto debole: i Carnivine** (gen 4, invasivi) hanno infestato il Percorso 9 `[BOZZA: quest di contenimento]`. Nel post-game guida il progetto di ripopolamento dei Magikarp e partecipa al WPT.

### Falker
Campionessa, 19 anni, ginger, ricercatrice nello sviluppo tecnologico contro i disastri climatici. Con Bill ha inventato la **Pietraradio** e potenziato le **MN**; ha rifondato la Lega.
- **Backstory:** nata a **Lavandonia** a T−3; la madre lavorava con **Fuji** alla Casa Volontari e si prese cura del **Cubone orfano** (madre Marowak uccisa dal Team Rocket). A T0 la famiglia si trasferisce a **Quartisola**; Cubone non volle separarsi e li seguì. La madre morì quando Falker era piccola (nella casa vive solo il padre). Falker e Cubone sono cresciuti prendendosi cura l'uno dell'altra: è il suo primo Pokémon, oggi il **Marowak** in squadra. **Non ha ricordi di Lavandonia se non sprazzi** ("una torre piena di fiori") → il ritorno è poetico (dialogo: `docs/design/dialoghi/lavandonia_incontro2_v1.md`).
- **Formazione:** a Quartisola conobbe **Red**, suo maestro; università di Smeraldopoli; eletta da Red alla rifondazione della Lega.
- **Regola del neutro (vincolante fino alla Lega):** gli NPC che parlano di FALKER non usano mai pronomi o accordi di genere — solo il **nome ripetuto** o formule con "persona" ("Falker è davvero brillante", "Falker è una persona piena di risorse"). Le due righe maschili della Alpha (`0x17ef89`, `0x194180`) vanno corrette. Lei, in scena, parla di sé al femminile (è visibile: il neutro protegge il nome, non la ragazza).
- **Incontri in incognito:** 1) **Celestopoli** — è lì per le voci sull'avvistamento di un Magikarp. 2) **Lavandonia** — spiega che lì è nata la Pietraradio (senza attribuirsela: lo fanno altri NPC), ne regala una, rivela le radici della madre e la storia del Cubone; **il Marowak è in scena accanto a lei** (breadcrumb visivo). 3) **Isola Cannella** — la lezione di vulcanologia climatica (§12), scena separata da quella di Alex.
- **Indizio opzionale:** la casa del padre a Quartisola (edificio normale, non obbligato): gli manca la moglie, è più solo da quando la figlia studia a Smeraldopoli, lo consola che "il suo MAROWAK è lì con lei", è orgoglioso del suo lavoro contro i disastri climatici.
- **Squadra campionessa (74-80, asso 80 `[BOZZA: Dragonite]`):** Marowak, Lapras, Charizard, Primeape, Dragonite, Snorlax — eco voluta del Red di Oro: è la sua allieva.

### Red
Ultimo campione prima di Falker. Vive nel Settipelago, ritiratosi sempre più al largo negli anni `[PROPOSTA: casa a Settisola — località post-game]`; da giovane viveva nei pressi di Quartisola, dove conobbe Falker bambina. **Evento post-game:** Falker vuole fondare il WPT e convincerlo a partecipare; chiede al giocatore di sfidarlo come argomento di persuasione; **a prescindere dall'esito, Red accetta**. `[BOZZA]` Squadra (~85-88), base GSC: Pikachu, Espeon, Snorlax, Venusaur, Charizard, Blastoise. La sua vecchia casa a Biancavilla: la madre, sola `[BOZZA: battuta sul figlio lontano]`.

### Lega (ordine di sfida) e capipalestra notevoli
- **Alex** (1°, 63-65) — archeologo appassionato di storia. Team fossili: Aerodactyl, Kabutops, Omastar, Armaldo, Cradily (i due di Hoenn via amicizia con **Rocco/Steven** e programma Vera; amico anche di **Camilla/Cynthia**). Incontri pre-Lega: (a) `[PROPOSTA: Monte Luna]` reindirizza all'acquisizione di un fossile e alla rigenerazione (→ università di Smeraldopoli, il lab di Cannella è distrutto); (b) **Isola Cannella**, scavo tra le rovine del vecchio laboratorio. Battuta NPC: Agatha non è più superquattro, Alex ha preso il suo posto — "Era ora! Pure i Pokémon fossile di Alex sono più giovani di Agata!"
- **Daisy Oak** (2ª, 66-68) — Venusaur, Hypno, Tauros, Magmortar, Poliwrath. Battuta sulla "repubblica fondata sulla raccomandazione".
- **Lance** (3°, 68-70) — Dragonite, Kingdra, Flygon, Salamence, Altaria. Ex campione GSC → battuta sul declassamento a "2° superquattro più forte" (punge doppio).
- **Bill** (4°, 71-73) — Vaporeon, Jolteon, Flareon, Umbreon, Espeon. Co-inventore della Pietraradio. **Requisito: IA al massimo livello** + strumenti/set ottimizzati, per giustificare la battuta di Lance.
- **Blue** — 8° capopalestra a Smeraldopoli (canon GSC), fratello maggiore del rivale. `[BOZZA]` Squadra (54-60): Pidgeot 55, Alakazam 56, Exeggutor 55, Arcanine 57, **Rhyperior 57** (il Rhydon di GSC evoluto con la Pietraradio), **Blastoise 60** (asso, al posto di Gyarados).
- **Janine** — 5ª capopalestra a Fucsiapoli (Koga promosso e uscito di scena: battuta disponibile).
- **Blaine** — tornato nella **palestra ricostruita a Isola Cannella**.

## 5. Antagonisti

- **La Camorra** — sostituisce il Team Rocket. **Modello di business: ecomafia** — smaltimento illecito a basso costo dei rifiuti delle grandi aziende — più malavita classica. Non causa il cambiamento climatico: ne è acceleratore locale e profittatrice. **Piano strategico:** controllare Kanto spodestando l'influenza di Oak (bancarotta orchestrata tramite il rivale). Strutture: reclute di classe **CAMORRISTA** (rename a livello classe), covo di Azzurropoli (ex Rocket, acquisito), discarica della Terra dei Fuochi.
- **Il vero boss: il Presidente della Silph Co.** Parodia archetipica dei CEO big-tech (nessun nome reale in gioco; in main story è solo "il Presidente" — nome-parodia `[APERTO]`). Controlla Camorra **e** grandi aziende. **Mai mostrato nella main story**; foreshadowing diffuso (container Silph alla Terra dei Fuochi, voci, "il boss" del monologo). Reveal e confronto **solo post-game**.
- **Giovanni:** assente (canon GSC).

## 6. Struttura della storia

- **Apertura — Biancavilla:** tre case + laboratorio (casa di Red con la madre; casa della famiglia Oak; **nuova casa del protagonista**). Oak in rovina, backstory Master Ball, consegna starter.
- **Atto 1 (badge 1-3):** lotte rivale (Lab, P.22), Brock; Monte Luna (incontro Alex #1); Celestopoli: Misty, lotta rivale, **incontro Falker #1**, **glimpse dorato** `[PROPOSTA]` — un lampo dorato nell'acqua visto dal ponte, non interattivo (struttura da monster movie); S.S. Anna: Vera a bordo, **ultima lotta rivale**; **sparizione** e assistente di Oak ad Aranciopoli; Surge; Tunnel Roccioso.
- **Lavandonia:** evento Torre Radio — origine della **Pietraradio** (onde radio della torre canalizzate da Falker e Bill) + **incontro Falker #2** (regalo Pietraradio + radici). La **vendita** ad Aranciopoli si sblocca dopo questo evento.
- **Atto 2 (badge 4-7):** Erika; **covo di Azzurropoli** (finto rapimento); Janine; **Zona Safari** (biomi, osservazione, adozioni); Sabrina; Percorso 9 infestato dai Carnivine; **Settipelago 1-4** (fix rotte traghetto: isole 1-4 pre-Lega, 5-7 post-Lega) con casa del padre a Quartisola e **Ghiacciaia in scioglimento** (beat climatico visivo); **Isola Cannella:** Blaine, incontro Alex #2, **incontro Falker #3** (scene separate).
- **Resa dei conti (post-7ª) — "Terra dei Fuochi":** nuova area-discarica costiera sui **Percorsi 12-13** (le rotte di pesca: i Magikarp lì sono morti per primi; container marchiati Silph = foreshadowing). Dungeon, boss fight rivale, monologo, innesco redenzione. Zafferanopoli/Silph resta intatta per il post-game.
- **Atto 3:** comunicazione della causa climatica, smantellamento dell'operazione rifiuti, Blue (università visibile a Smeraldopoli), Strada Vittoria, **Lega** — il reveal di Falker è il primo momento in cui nome e volto si uniscono.
- **Vetrina ambientale diffusa:** acque svuotate, zone degradate, NPC testimoni; **Old Rod** `[BOZZA]`: nelle acque morte pesca rifiuti (item-spazzatura marchiati) — le acque rinascono nell'epilogo.

## 7. Curva (v1)

| Tappa | Range |
|---|---|
| Brock | 17–18 |
| Misty | 27–28 |
| Rivale (S.S. Anna) | 29–31 |
| Lt. Surge | 33–35 |
| Erika | 38–40 |
| Janine | 43–45 |
| Sabrina | 47–49 |
| Blaine | 51–53 |
| Rivale (resa dei conti) | 53–56 |
| Blue | 54–60 (asso 60) |
| Alex | 63–65 |
| Daisy | 66–68 |
| Lance | 68–70 |
| Bill | 71–73 |
| Falker | 74–80 (asso 80) |

Sostenibilità: exp share moderno + level cap configurabili; boss con strumenti/IV/EV/nature dalla 4ª palestra; modalità SET consigliata di default.

## 8. Meccaniche

### Gen 4 via config
Split, dati mosse, learnset e abilità a Platino/HGSS; specie gen 1-4 (lista curata delle gen 4 `[APERTO]`); nuove abilità gen 4 implementate solo se usate dal cast `[APERTO: lista]`.

### Pietraradio (v2 — regola attuale)
Principio in-world: **le onde radio sostituiscono il viaggio dello scambio, non il corredo.** Origine: onde della Torre Radio di Lavandonia, tecnologia "redenta" dagli esperimenti Rocket del Lago d'Ira (Gyarados Rosso, canon GSC).
- **Scambio puro → sola Pietraradio:** Kadabra, Machoke, Graveler, Haunter.
- **Scambio + strumento → Pietraradio mentre il Pokémon tiene lo strumento storico**, che viene **consumato**: Poliwhirl/Slowpoke (Roccia di Re), Onix/Scyther (Metalcoperture), Seadra (Squamadrago), Porygon (Upgrade), Porygon2, Clamperl (Dente Abissale → Huntail / Squama Abissale → Gorebyss), Rhydon, Electabuzz, Magmar, Dusclops (rispettivi strumenti gen 4).
- **Interfaccia a tre stati** all'uso della pietra: evoluzione standard per gli eleggibili · **"Serve {strumento}."** per chi non tiene lo strumento richiesto (a due rami per Clamperl) · "Non avrà effetto" vanilla per gli altri.
- Gli strumenti-scambio storici restano contenuto di gioco; quelli gen 4 vanno piazzati nel mondo `[APERTO: piazzamenti — censimento in M1]`.
- Vendita ad Aranciopoli sbloccata dall'evento di Lavandonia; una copia in regalo da Falker (incontro #2).

### Magikarp Dorato (leggendario, Grotta di Celestopoli)
Forma/specie unica: aspetto dorato (shiny), **non evolve**, typing **Acqua/Drago** (con Folletto OFF: una sola debolezza), BST 600 — PS 100 / Att 70 / Dif 100 / AttSp 125 / DifSp 80 / Vel 125. Moveset originale `[BOZZA: sessione dedicata]`. Scena post-lotta (cattura o sconfitta): Bill e Falker arrivano estasiati → teletrasporto (tecnologia di Bill) all'università di Smeraldopoli → estrazione dati e mutazioni → avvio del ripopolamento. Respawn in caso di sconfitta `[APERTO: config]`.

### Zona Safari (overhaul)
Lato con **macro-aree a biomi** per far crescere le specie a rischio prima del rilascio. **Niente cattura**: osservazione e registrazione Pokédex. **Receptionist delle adozioni:** Pokémon rari ottenibili a condizioni `[BOZZA: condizioni per specie]`. Post-evento Dorato: un'area si popola di Magikarp.

### MN potenziate (firma di Falker) `[BOZZA]`
Taglio 75/100 con crit alto · Volo 90/95 · Surf invariata · Forza 100/100 · Flash acc 100 e Precisione nemica −2 · Spaccaroccia 60/100 con 50% Dif −1 · Cascata +20% flinch (standard gen 4).

### Specie estinte
Magikarp e Feebas assenti dalle encounter table fino all'epilogo.

## 9. Post-game

1. **Grotta di Celestopoli:** Magikarp Dorato → università → **avvio ripopolamento** (Safari ripopolata, acque che rinascono, Old Rod torna a pescare pesci).
2. **Il Presidente Silph:** indagine col rivale redento come informatore `[BOZZA]` → scalata della Silph a Zafferanopoli → confronto col burattinaio.
3. **WPT — World Pokémon Tournament.** Falker fonda il campionato mondiale: i 16 migliori di Kanto, Johto, Hoenn e Sinnoh per il titolo definitivo (trigger narrativo: evento di reclutamento di Red). Nel canone il formato nasce solo in gen 5: nel nostro continuum **lo inventa Falker**.
   - **Roster definitivo (16/16):** Protagonista · Lance · Falker · Red · Blue · Bill · Prof. Oak · Vera · Karen · Ethan · Cynthia · Palmer · Tobias · Steven · Brendan · Wally. (Bilancio: Kanto 6 · Johto 3 · Hoenn 4 · Sinnoh 3 — i padroni di casa sono sovrarappresentati → gag delle **wildcard degli organizzatori**.)
   - **Strutture del tabellone:** quattro generazioni di protagonisti (Red T0, Ethan T3, Brendan era RSE, Protagonista T16); **Red vs Blue** come dream match `[BOZZA: seeding semi-scriptato]`; rapporto personaggi-di-storia/cameo = 8/8.
   - **Note partecipanti:** Tobias = deep cut anime (Darkrai/Latios; gag: "nessuno ha mai visto gli altri quattro…"); Oak = omaggio ai dati di lotta inutilizzati di Rosso/Blu (Tauros, Exeggutor, Arcanine, starter + Gyarados→sostituire `[BOZZA: Lapras o Dragonite]`); Karen con la battuta canonica sui Pokémon forti e deboli; Vera ("il progetto sopravvivrà una settimana senza di me"); Blue in stile GSC ("i tornei sono per chi ha qualcosa da dimostrare" — detto partecipando).
   - **Club dei non qualificati** (gag opzionale `[APERTO]`): Daisy, Janine, Alex, rivale. Ruolo alternativo per Daisy: **telecronista del torneo** `[APERTO]`.
   - `[BOZZA]` **Formato:** eliminazione diretta a 16, il giocatore disputa 4 turni, resto del tabellone simulato con esiti variabili → **rigiocabile** (è anche la battle facility del post-game). Livelli ~80-85, SET. 16 squadre in sessione dedicata `[APERTO]`. **Sede** `[APERTO: proposta Altopiano Blu rinnovato]`.
4. **Red superboss** (vedi scheda; esito-indipendente per la storia, durissimo per la gloria).
5. **Parcheggio (esplicitamente NON ora):** esplorazione delle altre regioni con palestre ed eventi; criminalità organizzata regionale ('ndrangheta, cosa nostra, cartello messicano).

`[APERTO — chiusura poetica]` Post-ripopolamento, l'ultimissima immagine del gioco può essere un Gyarados che riemerge dall'acqua?

## 10. Mappe nuove o modificate (inventario Porymap)

Biancavilla: + casa del protagonista, madre di Red nella vecchia casa · Smeraldopoli: **università** (esterni + interni; rigenerazione fossili) · Percorsi 12-13: **Terra dei Fuochi** · Lavandonia: Torre Radio (evento), Casa Volontari/centro anziani (epilogo) · Isola Cannella: ricostruzione parziale, rovine-scavo di Alex, palestra di Blaine · Zona Safari: biomi + reception adozioni · Percorso 9: infestazione Carnivine · Settipelago: casa del padre a Quartisola, Ghiacciaia "in scioglimento", casa di Red `[PROPOSTA: Settisola]` · Arena WPT `[APERTO]` · Ponte di Celestopoli: punto-glimpse · Rimozione rival fight della Torre di Lavandonia (slot all'evento Torre Radio).

## 11. Piano di porting dalla Alpha

1. **Testi** (777 stringhe italiane, ~12.200 parole, estratte e consegnate): non trapianto meccanico ma **riscrittura forward** — Claude scrive i dialoghi finali per mappa usando la Alpha come voice bible (binario B), Codex li cabla. Revisione espansiva: i testi furono compressi dai limiti di byte.
2. **Trainer:** Brock e Misty come Alpha; Surge ricalibrato 33-35; classe CAMORRISTA; lotte rivale come §4.
3. **Fix puntuali:** le due righe maschili su Falker; la battuta di Vera con "BG. MAGIKARP" (vecchio rename di Biancavilla "Borgo Magikarp" — il nome città resta originale); riga Bellossom rimossa.
4. **Grafica ROM base Alpha (~1,7 MB):** scartata, si riparte da tileset puliti.
5. **Bonifica Magikarp/Gyarados** totale (encounter, pesca, Pescatori).

## 12. Scienza del gioco (canone divulgativo)

- **Cannella (canone):** l'intensificarsi delle **piogge estreme** infiltra l'edificio vulcanico, aumenta la pressione nei pori e può innescare eruzioni — ipotesi pubblicata su Nature (2020) per il Kīlauea 2018. Cannella, isola vulcanica tropicale flagellata da piogge senza precedenti, fu **il primo segnale forte** del cambiamento.
- **Contesto globale:** sui vulcani coperti dai ghiacci, lo scioglimento riduce il carico e favorisce eruzioni più esplosive (effetto "coperchio"/bottiglia di soda; parallelo con la deglaciazione di 26.000-18.000 anni fa).
- **Eruzioni quasi simultanee = causa comune,** non connessione fisica: lo stesso forzante globale agisce ovunque con meccanismi locali diversi ("correlazione senza connessione") — cuore della lezione di Falker a Cannella.
- L'ipotesi dei "vulcani collegati sottoterra" è **eliminata dal canone** e non compare in gioco.

## 13. Milestone

- **M0 — Fondamenta: CHIUSA.** Fork `no-ql-and-hs`, build WSL verde (ROM sha1 `d6e02de…`), config gen 4 verificata, CI build bloccante, baseline test (`docs/TEST_BASELINE_M0.md`), workflow a tre adottato.
- **M1 — Porting Alpha (in corso):** binario A (Codex: trainer, sweep, Pietraradio v2, curva 1-3) + binario B (Claude: blocchi dialoghi in ordine di storia, a partire da Biancavilla).
- **M2 — Lavandonia:** evento Torre Radio/Pietraradio + Erika + badge 5 + piazzamenti strumenti.
- **M3 — Atto 2:** arco Camorra (covo, finto rapimento), incontri Falker, Settipelago 1-4, Cannella.
- **M4 — Resa dei conti e Lega:** Terra dei Fuochi, atto 3, Blue, Superquattro, Falker.
- **M5 — MN potenziate, vetrina ambientale, epilogo, bilanciamento, betatest.**
- **M6 — Post-game:** grotta/Dorato/università, Presidente Silph, WPT, Red.

## 14. Registro decisioni aperte

**Bloccanti per i dialoghi:** nessuna (l'unica bloccante storica — età di Falker — è chiusa: 19).

**Design (sessioni dedicate):** 16 squadre WPT + formato fine e sede · moveset e respawn del Magikarp Dorato · condizioni adozioni Safari · lista curata specie gen 4 e abilità gen 4 implementate · piazzamento strumenti gen 4 · livelli definitivi della lotta finale del rivale.

**Conferme leggere (proposte attive):** nome dell'eroe GSC = Ethan · casa di Red = Settisola · Daisy telecronista · club dei non qualificati · ritorno dei Gyarados come ultimissima immagine post-ripopolamento.

**Eventuali:** nome-parodia del Presidente (al design del post-game).