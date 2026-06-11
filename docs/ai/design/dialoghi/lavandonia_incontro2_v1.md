# Golden Magikarp — Dialogo: incontro in incognito #2 (Lavandonia) — v1

**Scena:** piazzale della Torre Radio di Lavandonia, prima visita del giocatore alla città dopo il Tunnel Roccioso.
**Staging:** una ragazza dai capelli rossi guarda la torre dal basso. **Accanto a lei, un MAROWAK** (sprite overworld — breadcrumb visivo: chi rivedrà quel Marowak alla Lega capirà). Lei non si presenta mai. Trigger: parlarle. Evento one-shot; al termine esce di scena verso sud.
**Note di scrittura:** lei parla di sé al femminile (è visibile: il neutro protegge solo il *nome* FALKER, usato dagli altri NPC). Ogni paragrafo = un box di testo; la formattazione `\n \l \p` si applica in implementazione.

---

???: Sai cosa c'era qui, prima della torre radio?

???: Una torre piena di tombe. La gente saliva piano dopo piano per piangere i POKéMON che non c'erano più.

???: Adesso da qui parte un segnale che arriva in ogni angolo di KANTO, ventiquattr'ore su ventiquattro.

???: Un posto fatto per dire addio che oggi non smette mai di parlare… Non so tu, ma io la trovo una cosa bellissima.

???: È qui che è stata inventata la PIETRARADIO. Le onde della torre, canalizzate dentro una pietra.

???: I POKéMON che per evolversi avevano bisogno di uno scambio… cioè di *qualcun altro*… adesso quel legame se lo portano dietro. In tasca, in pratica.

???: Tieni. Questa è per te.

**[Il giocatore ottiene una PIETRARADIO!]**

???: Non chiedermi dove l'ho presa. Diciamo che… me ne avanzano.

???: Comunque non sono qui per la torre. Mia madre era di LAVANDONIA. E pure io, tecnicamente: ci sono nata.

???: Ce ne andammo che avevo tre anni. Di questa città mi restano due o tre sprazzi… una torre piena di fiori, mi pare. Magari me la sono pure inventata.

???: Mia madre lavorava qui con il signor FUJI. Si prendevano cura dei POKéMON rimasti soli.

???: Fu lei a occuparsi di quel CUBONE… quello famoso, rimasto orfano. La storia forse la conosci.

*(Il MAROWAK accanto a lei fa un passo avanti. Lei gli posa una mano sulla testa, senza commentare. Pausa.)*

???: Sono tornata per vedere se questa città si ricordava di noi. Spoiler: le città non si ricordano di nessuno.

???: Ma va bene così. Possiamo ricordare noi, per due.

???: Comunque. La pietra: usala. Se la trovo ancora nello zaino a far niente, vengo a riprendermela.

*(Si allontana ed esce di scena. Il MAROWAK la segue.)*

---

## Follow-up NPC (vecchietta davanti alla Casa Volontari, dopo la scena)

VECCHIETTA: La PIETRARADIO? L'ha inventata FALKER, insieme a BILL!

VECCHIETTA: Dicono che FALKER è una persona fuori dal comune. Chissà se un giorno passerà da queste parti…

*(Ironia drammatica: il giocatore le ha appena parlato. La vecchietta rispetta la regola del neutro.)*

---

## Note di implementazione

- Flag: `FLAG_INCONTRO_FALKER_2` settata a fine scena (richiamata nel dialogo della Lega: Falker citerà i luoghi degli incontri).
- Item gift: 1× PIETRARADIO (prima copia ottenibile; la vendita ad Aranciopoli si sblocca dopo questa scena).
- La scena non nomina mai chi ha inventato la pietra: l'attribuzione arriva solo dall'NPC dopo.
- Coerenza temporale: i "fiori sulla torre" sono un ricordo pre-T0 (la torre era ancora il cimitero); a T0 la famiglia parte per Quartisola.