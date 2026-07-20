# Gestione Audio Regie — Matrice CCRF

Software **portabile** (senza installazione e **senza server**) per la gestione e
l'**interconnessione audio** delle **3 regie radiofoniche** (Regia B, Regia TV/A,
Regia C) e della **matrice centralizzata** CCRF, con un **Quadro Incroci** in stile
*Dante Controller*.

Tutti i dati — **compresi gli incroci** — risiedono in un unico file `database.json`
dentro una cartella a tua scelta: puoi copiare la cartella su una chiavetta e portartela ovunque.

> Nasce come modulo audio del progetto [Gestione-LAN-e-VOIP](https://github.com/Balux75/Gestione-LAN-e-VOIP),
> qui reso **applicazione autonoma** dedicata solo all'audio.

---

## Avvio rapido

1. Copia in una cartella i file:
   - `GestioneAudio.html` (l'applicazione)
   - `database-esempio.json` (matrice già popolata con ingressi/uscite)
2. Fai **doppio clic** su `GestioneAudio.html` → si apre nel browser (consigliati **Microsoft Edge** o **Google Chrome**).
3. In alto premi **📂 Cartella database**:
   - **Annulla** → *Apri* un database esistente: seleziona `database-esempio.json`.
   - **OK** → *Crea* un nuovo `database.json` nella cartella.
4. Da qui in poi le modifiche vengono salvate direttamente sul file (autosalvataggio attivo).
   Puoi salvare anche a mano con **💾 Salva** o con <kbd>Ctrl</kbd>+<kbd>S</kbd>.

> **Importante:** il file HTML contiene **solo l'applicazione** e la **struttura di
> riferimento** della matrice (dispositivi e canali). Gli **incroci** che imposti stanno
> nel file esterno `database.json`. Tieni i due file nella stessa cartella e fai backup del `.json`.

---

## Cosa contiene la matrice

Importata dal file di cablaggio (foglio *MATRICE CCRF*):

| | Dispositivi | Canali |
|---|---|---|
| **Ingressi** (sorgenti) | MADI 1 (FUTURO RAIWAY), MADI 2 (da Regia B), MADI 3 (da Regia TV), MADI 4 (da Tiepolo), BEALINX (da Regia C), IN DANTE CORE, IN DANTE 2, LOCAL AES IN, LOCAL IN ANALOG | **468** |
| **Uscite** (destinazioni) | MADI 1–4, BEALINX, OUT DANTE 1, OUT DANTE 2, LOCAL AES OUT, LOCAL ANALOG OUT | **496** |

Ogni canale ha: **canale**, **macchina** (segnale), **CH** (L/R/M), **mono/stereo**, **note** e **slot**.

---

## Funzioni principali

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

- **Con Edge/Chrome**: dopo aver collegato la cartella, tutto viene scritto in `database.json`. È il metodo consigliato.
- **Con altri browser (es. Firefox)**: il salvataggio diretto su file non è supportato; i dati
  restano nella memoria del browser. Usa periodicamente **Backup → Esporta JSON** per conservare
  una copia e **Importa JSON** per ricaricarla.

---

## Requisiti

- Un browser moderno. Per il salvataggio diretto su file: **Microsoft Edge** o **Google Chrome**.
- Nessuna connessione a Internet necessaria: l'applicazione funziona completamente offline.
