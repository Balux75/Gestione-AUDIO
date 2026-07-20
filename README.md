# Gestione Audio Regie — Matrice CCRF

Software **portabile** (senza installazione e **senza server**) per la gestione e
l'**interconnessione audio** delle **3 regie radiofoniche** (Regia B, Regia TV/A,
Regia C) e della **matrice centralizzata** CCRF, con un **Quadro Incroci** in stile
*Dante Controller*.

Tutti i dati — **compresi gli incroci** — risiedono in un unico file `AUDIO_database.json`
dentro una cartella a tua scelta: puoi copiare la cartella su una chiavetta e portartela ovunque.

> Nasce come modulo audio del progetto [Gestione-LAN-e-VOIP](https://github.com/Balux75/Gestione-LAN-e-VOIP),
> qui reso **applicazione autonoma** dedicata solo all'audio.

---

## Avvio rapido

1. Copia in una cartella i file:
   - `GestioneAudio.html` (l'applicazione)
   - `AUDIO_database.json` (matrice già popolata con ingressi/uscite)
2. Fai **doppio clic** su `GestioneAudio.html` → si apre nel browser (consigliati **Microsoft Edge** o **Google Chrome**).
3. In alto premi **📂 Cartella database**:
   - **Annulla** → *Apri* un database esistente: seleziona `AUDIO_database.json`.
   - **OK** → *Crea* un nuovo `AUDIO_database.json` nella cartella.
4. Da qui in poi le modifiche vengono salvate direttamente sul file (autosalvataggio attivo).
   Puoi salvare anche a mano con **💾 Salva** o con <kbd>Ctrl</kbd>+<kbd>S</kbd>.

> **Importante:** il file HTML contiene **solo l'applicazione** e la **struttura di
> riferimento** della matrice (dispositivi e canali). Gli **incroci** che imposti stanno
> nel file esterno `AUDIO_database.json`. Tieni i due file nella stessa cartella e fai backup del `.json`.

---

## Cosa contiene la matrice

Importata dal file di cablaggio (foglio *MATRICE CCRF*):

| | Dispositivi | Tipologia | Canali |
|---|---|---|---|
| **Ingressi** (sorgenti) | MADI 1 (FUTURO RAIWAY), MADI 2 (da Regia B), MADI 3 (da Regia TV), MADI 4 (da Tiepolo) | MADI | **256** |
| | BEALINX (da Regia C) | Bealinx | 64 |
| | IN DANTE CORE, IN DANTE 2 | Dante | 128 |
| | LOCAL AES IN | Digitali | 32 |
| | LOCAL IN ANALOG | Analogici | 16 |
| **Uscite** (destinazioni) | MADI 1–4, BEALINX, OUT DANTE 1/2, LOCAL AES OUT, LOCAL ANALOG OUT | MADI/Bealinx/Dante/Digitali/Analogici | **496** |

Ogni **dispositivo** ha una **tipologia** (Analogici / Dante / Digitali / MADI / Bealinx) usata
per suddividere e filtrare il Quadro Incroci. Ogni **canale** ha: **canale**, **macchina**
(segnale), **CH** (L/R/M), **mono/stereo**, **note** e **slot**.

---

## Funzioni principali

- **🏢 Unità / Regie**: sezione per censire le **regie** (o postazioni) dell'impianto. Con
  **➕ Nuova unità / regia** crei un'unità; ognuna ha un **nome**, una **descrizione** e tre
  tabelle indipendenti gestite a schede:
  - **🎙️ Ingressi** — sorgenti della regia (Sorgente/Segnale, Tipo, Connettore/Presa, CH, Mono/Stereo, Livello, Note)
  - **🔊 Uscite** — destinazioni della regia (stessi campi)
  - **🔌 Patch audio** — pannello patch (Porta, Etichetta/Segnale, Normalizzazione, Destinazione, Note, **Colore**)

  Ogni tabella ha **aggiungi/elimina riga** ed editing in linea (con suggerimenti per Tipo,
  Mono/Stereo e Normalizzazione); da ogni unità puoi fare l'**export Excel** (fogli Ingressi,
  Uscite, Patch). Questa sezione è **indipendente** dal Quadro Incroci / matrice CCRF.
- **🎛️ Quadro Incroci (tipo Dante Controller)**: gli **ingressi** (sorgenti) sono sulle
  **colonne**, le **uscite** (destinazioni) sulle **righe**. Ogni dispositivo è
  **comprimibile/espandibile**: da compresso occupa una sola colonna/riga verticale con il
  **conteggio degli incroci attivi**, da espanso mostra i singoli canali. Con **entrambi i
  lati espansi** clicchi la casella all'incrocio per **instradare** l'ingresso verso
  l'uscita (pallino verde ●); ogni uscita riceve **una sola** sorgente (riclicca per
  staccare). Le celle di riepilogo mostrano il numero di collegamenti fra due dispositivi
  (clic = espandi). Sono disponibili: filtri di ricerca su ingressi e uscite, «**solo uscite
  instradate**», **espandi/comprimi tutto**, evidenziazione riga/colonna, **export Excel**
  degli instradamenti e **azzeramento** rapido.
  I dispositivi sono **suddivisi per tipologia** di segnale — **Analogici / Dante / Digitali
  (AES) / MADI / Bealinx** — con codifica a colori (pallino e bordo sull'intestazione di ogni
  dispositivo) e due filtri a tendina («Ingressi» e «Uscite») per mostrare solo una tipologia
  per asse. Gli ingressi/uscite provengono direttamente dalla matrice CCRF: **ogni modifica
  fatta in «Regie & Matrice»** (rinomina, aggiunta/eliminazione canale, cambio tipologia) **si
  riflette immediatamente sul Quadro Incroci**.
  > Suggerimento: la matrice parte tutta compressa (veloce). Espandi solo i dispositivi che
  > ti servono; l'espansione totale di tutti i 9+9 dispositivi genera decine di migliaia di
  > incroci ed è pesante da disegnare.
- **🎚️ Regie & Matrice**: elenco dei **dispositivi di ingresso e uscita** (una scheda per
  dispositivo, con numero di canali e instradamenti attivi). Aprendo un dispositivo
  vedi/modifichi la **tabella canali** (canale, macchina, CH L/R, mono/stereo, note, slot),
  con **aggiungi/elimina canale** e la colonna che mostra gli instradamenti collegati.
- **📊 Dashboard**: riepilogo di incroci attivi, dispositivi e canali, con la distribuzione
  per dispositivo.
- **💽 Backup / Ripristino**: esporta/importa l'intero database in **JSON**, esporta la
  matrice in **Excel** (fogli Ingressi, Uscite, Incroci), **azzera** gli incroci o
  **ripristina** la struttura di ingressi/uscite dai dati di riferimento (mantenendo gli incroci).

Tutto l'import/export Excel avviene **offline**, senza librerie né server.

---

## Persistenza dei dati

- **Con Edge/Chrome**: dopo aver collegato la cartella, tutto viene scritto in `AUDIO_database.json`. È il metodo consigliato.
- **Con altri browser (es. Firefox)**: il salvataggio diretto su file non è supportato; i dati
  restano nella memoria del browser. Usa periodicamente **Backup → Esporta JSON** per conservare
  una copia e **Importa JSON** per ricaricarla.

---

## Requisiti

- Un browser moderno. Per il salvataggio diretto su file: **Microsoft Edge** o **Google Chrome**.
- Nessuna connessione a Internet necessaria: l'applicazione funziona completamente offline.
