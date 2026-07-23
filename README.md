# Gestione Audio Regie — Quadro Incroci & Unità operative

Software **portabile** (senza installazione e **senza server**) per la gestione e
l'**interconnessione audio** delle regie radiofoniche, con un **Quadro Incroci** in stile
*Dante Controller*.

L'impianto è organizzato in **Unità operative → Macchine → Ingressi/Uscite**: ogni unità
(regia/postazione) contiene delle macchine, e gli **ingressi/uscite di ogni macchina
popolano il Quadro Incroci**, dove instradi le sorgenti sulle destinazioni.

Tutti i dati — **compresi gli incroci** — risiedono in un unico file `AUDIO_database.json`
dentro una cartella a tua scelta: puoi copiare la cartella su una chiavetta e portartela ovunque.

> Nasce come modulo audio del progetto [Gestione-LAN-e-VOIP](https://github.com/Balux75/Gestione-LAN-e-VOIP),
> qui reso **applicazione autonoma** dedicata solo all'audio.

---

## Avvio rapido

1. Copia in una cartella i file:
   - `GestioneAudio.html` (l'applicazione)
   - `AUDIO_database.json` (già popolato con l'unità «CCRF» e le sue 9 macchine)
2. Fai **doppio clic** su `GestioneAudio.html` → si apre nel browser (consigliati **Microsoft Edge** o **Google Chrome**).
3. In alto premi **📂 Cartella database**:
   - **Annulla** → *Apri* un database esistente: seleziona `AUDIO_database.json`.
   - **OK** → *Crea* un nuovo `AUDIO_database.json` nella cartella.
4. Da qui in poi le modifiche vengono salvate direttamente sul file (autosalvataggio attivo).
   Puoi salvare anche a mano con **💾 Salva** o con <kbd>Ctrl</kbd>+<kbd>S</kbd>.

> **Nota:** al primo avvio (database vuoto) l'app crea automaticamente la stanza **CCRF** con la
> macchina **MATRICE CENTRALIZZATA** e le sue **9 schede di ingresso + 9 di uscita** (MADI 1–4,
> BEALINX, Dante 1/2, AES, Analogico) dai dati del foglio di cablaggio *MATRICE CCRF*.

---

## Struttura dei dati

```
Unità operativa   (la STANZA — es. «CCRF», «Regia A», …)
 └─ Macchina      (es. «MATRICE CENTRALIZZATA», un mixer, un codec…)
     ├─ Schede di INGRESSO   (una scheda per dispositivo: MADI 1, MADI 2, … Dante 1, Dante 2, …)
     │    └─ Canali sorgente        → colonne del Quadro Incroci
     └─ Schede di USCITA     (MADI 1, MADI 2, … Dante 1, Dante 2, …)
          └─ Canali destinazione    → righe del Quadro Incroci
```

Le **schede di ingresso** e di **uscita** sono tenute **separate** e distinte da un **colore**
(azzurro gli ingressi, arancio le uscite). Ogni scheda ha una **tipologia** di segnale
(Analogici / Dante / Digitali / MADI / Bealinx) usata per colorare e filtrare il Quadro Incroci.
Ogni **canale** ha: **canale**, **macchina/segnale**, **CH** (L/R/M), **mono/stereo**, **note** e **slot**.

---

## Funzioni principali

- **🎛️ Quadro Incroci (tipo Dante Controller)** — subito dopo la Dashboard, da solo. Le **colonne**
  sono le **schede di ingresso**, le **righe** le **schede di uscita**. Ogni scheda è
  **comprimibile/espandibile**: da compressa occupa una sola colonna/riga verticale con il
  conteggio degli incroci, da espansa mostra i singoli canali. Con **entrambi i lati espansi**
  clicchi la casella all'incrocio per **instradare** (pallino verde ●). Un'**uscita** può essere
  inviata a **più ingressi**; ogni **ingresso** riceve **una sola** uscita (riclicca per
  staccare). Ogni ingresso e uscita mostra il proprio **numero # di canale**; le intestazioni
  riportano **stanza · macchina · scheda**. Filtri per **tipologia** (Analogici / Dante /
  Digitali / MADI / Bealinx) su ingressi e uscite, ricerca, «solo uscite instradate»,
  espandi/comprimi tutto, evidenziazione riga/colonna, **export Excel**, **stampa** e
  **azzeramento**. Export ed stampa elencano **prima le uscite** e poi gli **ingressi**
  incrociati (con i rispettivi #). Tutto ciò che modifichi nelle schede si riflette qui automaticamente.
- **🏢 Unità operative** — elenco delle stanze. Con **➕ Nuova unità operativa** crei una stanza;
  aprendola vedi le sue **macchine** e con **➕ Nuova macchina** ne aggiungi. Rinomina/elimina
  unità e macchine (con pulizia automatica degli incroci collegati). A livello di unità sono
  disponibili **⤒ Importa**, **⤓ Esporta** e **🖨 Stampa** dell'**intera stanza**: l'export Excel
  ha i fogli *Ingressi*, *Uscite* (con Macchina, Scheda, Tipologia, #, canale…), *Patch*, *Switch*,
  *Pannelli* e *Box*; l'import ricostruisce macchine, schede, patch, switch, pannelli e box dallo
  stesso formato; la stampa produce un documento completo (tutte le schede, i pannelli patch, gli
  switch, i pannelli colorati e le cassette/box).
- **🔌 Patch audio** — dentro ogni stanza puoi creare dei **pannelli patch** a **sviluppo
  orizzontale** (le porte sono le colonne, gli attributi le righe: **Provenienza**, **n° cavo e
  coppia**, **N°**, **Tipologia**, **Segnale**). Aggiungi/elimina porte (o **+8** in blocco),
  con **Importa** (Excel/CSV), **Esporta** e **Stampa** (layout orizzontale). Le patch
  **non entrano** nel Quadro Incroci: servono a documentare i pannelli/cablaggi della stanza.
- **🔀 Switch** — dopo le patch, ogni stanza può contenere degli **switch di rete**: tabella
  verticale delle porte con **Porta, Patch/Stanza, Descrizione, IP, MAC, Subnet, Gateway, VLAN,
  Note, Colore** (schema del file Excel di configurazione). Creando uno switch scegli il numero
  di porte; ogni porta ha un **colore** (bordo colorato). Per ogni switch: **Aggiungi porta**,
  **Importa** (Excel/CSV, riconosce le intestazioni del file switch), **Esporta** e **Stampa**.
- **🎛 Pannelli** — sviluppo orizzontale come le Patch audio, con i campi **Patch** (patch/pannello/box
  di destinazione), **n° cavo e coppia**, **Posizione patch** (la posizione sulla patch di
  destinazione), **Tipologia**, **Segnale** e un **Colore** selezionabile per ogni porta. In cima è
  mostrata la **raffigurazione dei connettori** con forme distinte per tipo — **XLR F** (cerchio
  rosso) / **XLR M** (cerchio blu) / **RJ45** (rettangolo ethernet) / **BNC** (coassiale a doppio
  anello) — con segnale e colore del cavo, come per i Box. **Doppio clic sulla porta** (o sul campo **Patch**, o il pulsante **↗**) apre la
  **patch/pannello/box di destinazione** alla **Posizione patch** indicata, evidenziando la porta di
  arrivo. La lista a discesa del campo **Patch** include **Patch, Pannelli e Box** della stanza.
  Aggiungi/elimina porte (o **+8**), con **Importa** (Excel/CSV), **Esporta** e **Stampa**. I pannelli
  **non entrano** nel Quadro Incroci.
- **📦 Box / Cassette** — cassette secondo lo schema *esempio_cassetta*: creando un box scegli il
  numero di **coppie**; ogni coppia ha **Tipologia** (XLR F / XLR M / RJ45 / BNC / LIBERO), **Nome
  Segnale**, **Colore cavo** e la **destinazione** (**Pannello** + **Posizione pannello**). La vista
  mostra una **raffigurazione del pannello frontale** (interruttore, spia alimentazione, prese
  rete/UPS e i connettori con forme distinte per tipo — XLR F/M, RJ45 ethernet, BNC coassiale — con
  segnale e colore del cavo) più la tabella orizzontale delle coppie. Il campo
  **Pannello destinazione** ha una lista a discesa con **Patch, Pannelli e Box** della stanza e, con
  **doppio clic** (o **↗**), apre la destinazione alla **Posizione pannello** indicata, evidenziando
  la coppia/porta di arrivo (colonna e connettore). Per ogni box: **Aggiungi coppia**, **Importa**
  (Excel/CSV), **Esporta** e **Stampa** (con la raffigurazione).
- **🎛️ Dettaglio macchina** — nome modificabile e due sezioni distinte per colore: **🎙️ Schede di
  ingresso** e **🔊 Schede di uscita**. Con **➕ Nuova scheda ingresso/uscita** aggiungi le schede
  (una per dispositivo: MADI 1, MADI 2, Dante 1…).
- **🎚️ Dettaglio scheda** — nome e **tipologia** modificabili; tabella dei **canali** editabile in
  linea (canale, macchina/segnale, CH, mono/stereo, **patch**, note, slot) con l'indicazione
  dell'**instradamento** sul Quadro Incroci, e i pulsanti **➕ Aggiungi canale**, **⤒ Importa**
  (Excel/CSV), **⤓ Esporta** (Excel) e **🖨 Stampa**. Il campo **Patch** collega il canale a un
  pannello patch della stanza: **doppio clic** sul campo (o il pulsante **↗**) apre la patch
  relativa; il campo ha i suggerimenti dei pannelli/porte della stanza.
- **📊 Dashboard** — riepilogo di incroci attivi, unità, macchine e canali.
- **💽 Backup / Ripristino** — esporta/importa l'intero database in **JSON**, esporta tutto in
  **Excel** (Ingressi, Uscite, Incroci), **⤓ Scarica app (HTML)** per salvare una copia autonoma
  dell'applicazione, **azzera** gli incroci, oppure **⤒ Importa MATRICE CCRF** per (ri)creare
  l'unità «CCRF» e le sue macchine dal foglio Excel di cablaggio.

Tutto l'import/export Excel avviene **offline**, senza librerie né server.

---

## Persistenza dei dati

- **Con Edge/Chrome**: dopo aver collegato la cartella, tutto viene scritto in `AUDIO_database.json`. È il metodo consigliato.
- **Con altri browser (es. Firefox)**: il salvataggio diretto su file non è supportato; usa
  periodicamente **Backup → Esporta JSON** per conservare una copia e **Importa JSON** per ricaricarla.

---

## Requisiti

- Un browser moderno. Per il salvataggio diretto su file: **Microsoft Edge** o **Google Chrome**.
- Nessuna connessione a Internet necessaria: l'applicazione funziona completamente offline.
