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
  staccare). Filtri per **tipologia** (Analogici / Dante /
  Digitali / MADI / Bealinx) su ingressi e uscite, ricerca, «solo uscite instradate»,
  espandi/comprimi tutto, evidenziazione riga/colonna, **export Excel** e **azzeramento**.
  Tutto ciò che modifichi nelle schede si riflette qui automaticamente.
- **🏢 Unità operative** — elenco delle stanze. Con **➕ Nuova unità operativa** crei una stanza;
  aprendola vedi le sue **macchine** e con **➕ Nuova macchina** ne aggiungi. Rinomina/elimina
  unità e macchine (con pulizia automatica degli incroci collegati).
- **🎛️ Dettaglio macchina** — nome modificabile e due sezioni distinte per colore: **🎙️ Schede di
  ingresso** e **🔊 Schede di uscita**. Con **➕ Nuova scheda ingresso/uscita** aggiungi le schede
  (una per dispositivo: MADI 1, MADI 2, Dante 1…).
- **🎚️ Dettaglio scheda** — nome e **tipologia** modificabili; tabella dei **canali** editabile in
  linea (canale, macchina/segnale, CH, mono/stereo, note, slot) con l'indicazione
  dell'**instradamento** sul Quadro Incroci, e i pulsanti **➕ Aggiungi canale**, **⤒ Importa**
  (Excel/CSV), **⤓ Esporta** (Excel) e **🖨 Stampa**.
- **📊 Dashboard** — riepilogo di incroci attivi, unità, macchine e canali.
- **💽 Backup / Ripristino** — esporta/importa l'intero database in **JSON**, esporta tutto in
  **Excel** (Ingressi, Uscite, Incroci), **azzera** gli incroci, oppure **⤒ Importa MATRICE
  CCRF** per (ri)creare l'unità «CCRF» e le sue 9 macchine dal foglio Excel di cablaggio.

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
