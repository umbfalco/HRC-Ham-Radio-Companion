# HRC – Ham Radio Companion
## HRC-UX – Specifica funzionale dell'interfaccia utente
**Versione:** 1.0  
**Stato:** Bozza progettuale  
**Piattaforma:** Windows 11 – Desktop-first  
**Lingua interfaccia:** Italiano  
**Architettura:** React + TypeScript / FastAPI

---

## 1. Obiettivi UX

L'interfaccia di HRC deve consentire di gestire una stazione radioamatoriale e documentare attività sperimentali senza obbligare l'utente a utilizzare più applicazioni per le operazioni fondamentali.

I principi di progettazione sono:

- **Desktop-first:** ottimizzazione per notebook e monitor.
- **Offline-first:** tutte le operazioni essenziali devono essere disponibili senza Internet.
- **Modularità:** ogni funzionalità appartiene a un modulo autonomo.
- **Coerenza:** stessi comportamenti, pulsanti e convenzioni in tutta l'applicazione.
- **Tracciabilità:** ogni attività sperimentale deve poter essere ricostruita.
- **Efficienza:** le operazioni frequenti devono richiedere pochi passaggi.
- **Estendibilità:** nuovi moduli non devono richiedere la riprogettazione dell'interfaccia generale.

## 2. Struttura generale dell'applicazione

L'interfaccia sarà composta da quattro aree principali:

1. Barra superiore.
2. Menu di navigazione laterale.
3. Area di lavoro centrale.
4. Barra di stato inferiore.

### 2.1 Layout principale

```text
┌──────────────────────────────────────────────────────────────┐
│ HRC  Ham Radio Companion       Ricerca       ⚙ Impostazioni  │
├────────────────┬─────────────────────────────────────────────┤
│                │                                             │
│  DASHBOARD     │                                             │
│                │              AREA DI LAVORO                 │
│  STAZIONE      │                                             │
│  ├ Apparati    │        Contenuto del modulo selezionato     │
│  ├ Antenne     │                                             │
│  └ Postazioni  │                                             │
│                │                                             │
│  LOGBOOK       │                                             │
│                │                                             │
│  FIELD OPS     │                                             │
│                │                                             │
│  DIGITAL LAB   │                                             │
│                │                                             │
│  PROPAGATION   │                                             │
│                │                                             │
│  ANTENNA LAB   │                                             │
│                │                                             │
│  VHF / APRS    │                                             │
│                │                                             │
│  SDR / RF      │                                             │
│                │                                             │
│  REPORTING     │                                             │
│                │                                             │
│  ───────────   │                                             │
│  IMPOSTAZIONI  │                                             │
├────────────────┴─────────────────────────────────────────────┤
│ Offline/Online │ Sync: stato │ Database: OK │ IU8VBG         │
└──────────────────────────────────────────────────────────────┘
```

### 2.2 Barra superiore

Elementi:

- Logo e nome HRC.
- Ricerca globale.
- Pulsante notifiche.
- Accesso alle impostazioni.
- Informazioni sull'utente e sulla stazione attiva.

La ricerca globale dovrà consentire di individuare QSO, apparati, antenne, attività, esperimenti e località.

### 2.3 Menu laterale

Il menu sarà espandibile e comprimibile.

| Sezione | Funzionalità |
|---|---|
| Dashboard | Riepilogo e accesso rapido |
| Station Manager | Stazioni, apparati, antenne, postazioni |
| QSO Logbook | Registro dei collegamenti |
| Field Operations | Attività operative sul campo |
| Digital Modes Lab | Modi digitali |
| Propagation Lab | Analisi della propagazione |
| Antenna Lab | Esperimenti e misure sulle antenne |
| VHF/UHF & APRS | Attività VHF/UHF e APRS |
| SDR & RF Analyzer | Analisi RF e SDR |
| Reporting | Report, esportazioni e statistiche |
| Impostazioni | Configurazione e gestione sistema |

I moduli non ancora disponibili saranno contrassegnati come pianificati e non presenteranno schermate operative incomplete.

## 3. Dashboard

La Dashboard sarà la schermata iniziale.

### 3.1 Obiettivi

Fornire una visione immediata dello stato della stazione e delle attività recenti.

### 3.2 Layout proposto

```text
DASHBOARD

Benvenuto in HRC

┌────────────────┐ ┌────────────────┐ ┌────────────────┐
│ QSO TOTALI     │ │ ATTIVITÀ       │ │ ESPERIMENTI    │
│                │ │                │ │                │
│      0000      │ │      000       │ │      000       │
└────────────────┘ └────────────────┘ └────────────────┘

┌────────────────────────────┐ ┌───────────────────────────┐
│ ULTIMI QSO                 │ │ STAZIONE ATTIVA           │
│                            │ │                           │
│ Callsign  Banda  Modo      │ │ IU8VBG                    │
│ ...                        │ │ Apparati                  │
│ ...                        │ │ Antenna                   │
│ ...                        │ │ Postazione                │
└────────────────────────────┘ └───────────────────────────┘

┌────────────────────────────┐ ┌───────────────────────────┐
│ ATTIVITÀ RECENTI           │ │ SINCRONIZZAZIONE          │
│                            │ │                           │
│ Ultime sessioni            │ │ Stato connessione         │
│ Ultimi esperimenti         │ │ Record in attesa          │
│                            │ │ Ultima sincronizzazione   │
└────────────────────────────┘ └───────────────────────────┘
```

### 3.3 Indicatori

- Numero totale di QSO.
- QSO recenti.
- Attività sul campo.
- Esperimenti in corso.
- Stato del database.
- Stato della sincronizzazione.
- Numero di record non sincronizzati.

I dati saranno aggiornati automaticamente quando cambiano le informazioni locali.

## 4. Station Manager

Questo modulo gestisce la configurazione della stazione radio.

### 4.1 Sottosezioni

- Stazioni.
- Apparati.
- Antenne.
- Installazioni.
- Postazioni operative.
- Configurazioni storiche.

### 4.2 Scheda apparato

Campi principali:

- Marca.
- Modello.
- Numero seriale, facoltativo.
- Tipologia.
- Frequenza minima e massima.
- Potenza massima.
- Modi supportati.
- Interfacce disponibili.
- Note tecniche.
- Allegati e documentazione.

Esempio di apparato: Xiegu G90.

### 4.3 Scheda antenna

Campi principali:

- Nome antenna.
- Tipologia.
- Costruttore.
- Frequenze operative.
- Impedenza nominale.
- Guadagno dichiarato, se disponibile.
- Polarizzazione.
- Potenza massima.
- Alimentazione e adattamento.
- Balun/un-un.
- Lunghezza e dimensioni.
- Note e documentazione.

### 4.4 Installazioni

Una stessa antenna potrà essere utilizzata in installazioni differenti.

Ogni installazione dovrà descrivere:

- Antenna associata.
- Località.
- Coordinate e locator.
- Altezza dal suolo.
- Orientamento.
- Cavo e lunghezza.
- Choke e adattatori.
- Configurazione dei radiali.
- Data di installazione e rimozione.

Questa distinzione consentirà di confrontare la stessa antenna in condizioni operative diverse.

## 5. QSO Logbook

Il Logbook sarà uno dei moduli principali.

### 5.1 Elenco QSO

La schermata presenterà una tabella con:

- Data e ora UTC.
- Callsign.
- Frequenza.
- Banda.
- Modo.
- RST TX.
- RST RX.
- Locator.
- Nome operatore.
- Attività associata.

Funzioni:

- Ricerca per callsign.
- Filtri per banda e modo.
- Filtri temporali.
- Ordinamento colonne.
- Modifica e cancellazione logica.
- Importazione ADIF.
- Esportazione ADIF.

### 5.2 Inserimento QSO

Il modulo di inserimento dovrà essere rapido e organizzato in gruppi.

**Dati del collegamento**
- Callsign.
- Data e ora UTC.
- Frequenza.
- Banda.
- Modo.
- RST TX/RX.

**Dati della stazione corrispondente**
- Nome.
- Locator.
- Paese.
- Note.

**Contesto operativo**
- Stazione utilizzata.
- Apparato.
- Antenna.
- Attività associata.
- Esperimento associato.

I campi non obbligatori non devono rallentare l'inserimento manuale.

### 5.3 Importazione ADIF

Procedura guidata:

1. Selezione del file.
2. Analisi del contenuto.
3. Anteprima dei record.
4. Controllo duplicati.
5. Conferma importazione.
6. Riepilogo degli esiti.

L'importazione non dovrà sovrascrivere automaticamente record esistenti senza una regola esplicita.

## 6. Field Operations

Questo modulo sarà ottimizzato per l'utilizzo durante le attività portable.

### 6.1 Elenco attività

Ogni attività rappresenta una sessione operativa in una determinata località e in un determinato intervallo temporale.

Esempi:

- Attività HF in spiaggia.
- Attivazione POTA.
- Test antenna in campo.
- Sessione di ricezione beacon.
- Prova di propagazione.

### 6.2 Creazione attività

Dati principali:

- Nome attività.
- Tipologia.
- Data e ora di inizio.
- Data e ora di fine.
- Località.
- Coordinate.
- Locator Maidenhead.
- Apparato utilizzato.
- Antenna utilizzata.
- Potenza prevista.
- Bande operative.
- Condizioni ambientali.
- Note.

### 6.3 Diario operativo

La sessione dovrà avere un diario cronologico nel quale registrare:

- Annotazioni.
- Eventi.
- Variazioni di configurazione.
- Problemi riscontrati.
- Misure effettuate.
- Fotografie e allegati.

Ogni annotazione avrà un timestamp.

### 6.4 Modalità operativa rapida

Durante una sessione portable dovranno essere disponibili scorciatoie per:

- Registrare un QSO.
- Inserire una misura.
- Aggiungere una nota.
- Allegare un file.
- Cambiare configurazione antenna.
- Terminare la sessione.

La perdita di connessione Internet non dovrà interrompere nessuna di queste operazioni.

## 7. Digital Modes Lab

Il modulo consentirà di raccogliere e analizzare dati provenienti dai software digitali.

Non sostituirà WSJT-X, JTDX o altri software di decodifica.

### Funzionalità previste

- Configurazione dei software esterni.
- Ricezione eventi UDP da WSJT-X.
- Importazione dati WSPR.
- Associazione degli spot alle attività.
- Statistiche FT8/FT4.
- Analisi dei rapporti SNR.
- Ricerca dei collegamenti per banda e intervallo temporale.

La schermata principale mostrerà gli eventi ricevuti, lo stato dell'integrazione e gli eventuali errori.

## 8. Propagation Lab

Questo modulo sarà dedicato allo studio quantitativo della propagazione.

Funzionalità previste:

- Archivio delle osservazioni.
- Importazione dei dati.
- Analisi per banda.
- Analisi temporale.
- Distribuzione degli SNR.
- Distanze e azimut.
- Confronto tra periodi.
- Grafici e report.

Le osservazioni dovranno mantenere sempre il riferimento alla fonte originale e al timestamp.

## 9. Antenna Lab

Il modulo sarà progettato per documentare esperimenti ripetibili.

### 9.1 Gestione esperimenti

Ogni esperimento avrà:

- Titolo.
- Obiettivo.
- Ipotesi.
- Protocollo.
- Antenne confrontate.
- Apparati.
- Località.
- Bande.
- Parametri controllati.
- Variabili misurate.
- Sessioni sperimentali.
- Risultati e conclusioni.

### 9.2 Gestione sessioni

Ogni sessione potrà contenere più blocchi di trasmissione.

Un blocco identificherà:

- Antenna utilizzata.
- Banda.
- Frequenza.
- Potenza.
- Inizio e fine.
- Configurazione.
- Eventuali anomalie.

### 9.3 Analisi

Le schermate di analisi dovranno supportare:

- Confronti A/B.
- Statistiche descrittive.
- Distribuzioni SNR.
- Analisi per azimut.
- Mappe dei ricevitori.
- Grafici polari.
- Intervalli di confidenza.
- Esportazione dei dati.

Ogni grafico dovrà indicare unità, periodo analizzato, numerosità campionaria e filtri applicati.

## 10. VHF/UHF & APRS

Modulo futuro dedicato a:

- Anagrafica frequenze.
- Ponti ripetitori.
- Beacon.
- Piani di frequenza.
- Importazione dati APRS.
- Archivio delle tracce.
- Statistiche operative.

## 11. SDR & RF Analyzer

Modulo futuro per:

- Importazione dati SDR.
- Archivio scansioni.
- Spettri RF.
- Analisi segnali.
- Importazione misure NanoVNA.
- Grafici SWR.
- Impedenza.
- Frequenza di risonanza.
- Larghezza di banda.

La prima versione non richiederà il controllo diretto degli strumenti.

## 12. Reporting

Il modulo Reporting raccoglierà le funzioni di esportazione e produzione documentale.

Formati previsti:

- PDF.
- CSV.
- JSON.
- ADIF, per il Logbook.

Report iniziali:

- Registro QSO.
- Riepilogo attività portable.
- Scheda configurazione stazione.
- Report esperimento antenna.
- Analisi propagazione.
- Confronto antenne.

Ogni report dovrà indicare data di generazione, periodo analizzato e criteri di selezione dei dati.

## 13. Impostazioni

Le impostazioni saranno suddivise in:

**Generali**
- Lingua.
- Tema chiaro/scuro.
- Formato data e ora.
- Unità di misura.

**Stazione**
- Callsign.
- Locator predefinito.
- Stazione principale.

**Database**
- Percorso archivio.
- Backup.
- Ripristino.
- Verifica integrità.

**Dispositivi**
- Identificativo installazione.
- Nome dispositivo.

**Sincronizzazione**
- Server configurato.
- Stato connessione.
- Ultima sincronizzazione.
- Elementi in attesa.
- Errori e conflitti.

**Integrazioni**
- WSJT-X.
- Hamlib/rigctld.
- NanoVNA.
- SDR.
- Altri software esterni.

## 14. Gestione offline e sincronizzazione

La sincronizzazione deve essere visibile in ogni momento.

### 14.1 Stati dell'applicazione

| Stato | Indicatore |
|---|---|
| Online | Connessione disponibile |
| Offline | Nessuna connessione |
| Sincronizzazione | Trasferimento in corso |
| In attesa | Modifiche locali non inviate |
| Errore | Sincronizzazione non riuscita |
| Conflitto | Necessario intervento |

### 14.2 Regole UX

- L'utente può lavorare senza connessione.
- Le modifiche locali vengono salvate immediatamente.
- La sincronizzazione non deve bloccare l'interfaccia.
- Gli errori devono essere comprensibili.
- I conflitti devono essere mostrati in una schermata dedicata.
- Le cancellazioni e le modifiche devono essere propagate secondo le regole del sistema.
- L'utente deve poter consultare lo storico delle sincronizzazioni.

## 15. Convenzioni grafiche e comportamentali

### Tabelle
- Intestazioni sempre visibili quando si scorre.
- Filtri e ricerca accessibili.
- Colonne configurabili quando utile.
- Paginazione per grandi quantità di dati.

### Moduli di inserimento
- Etichette in italiano.
- Campi obbligatori chiaramente identificati.
- Validazione immediata.
- Messaggi di errore specifici.
- Salvataggio esplicito e conferma dell'esito.

### Grafici
- Legende chiare.
- Unità di misura esplicite.
- Tooltip informativi.
- Possibilità di esportare i dati sottostanti.
- Filtri coerenti con le analisi.

### Notifiche
- Conferme non invasive.
- Errori persistenti fino alla loro risoluzione.
- Nessuna finestra modale per operazioni ordinarie.

## 16. Responsive design

La priorità è il desktop.

L'interfaccia dovrà comunque adattarsi a finestre più strette:

- Menu laterale comprimibile.
- Tabelle con colonne nascondibili.
- Moduli disposti su una o due colonne.
- Grafici ridimensionabili.
- Schermate operative utilizzabili anche su tablet.

Non è previsto, nella prima versione, un client mobile nativo.

## 17. Criteri di accettazione UX

La progettazione sarà considerata sufficientemente definita quando:

1. Tutti i moduli avranno una collocazione nella navigazione.
2. Dashboard e schermate principali saranno definite.
3. Saranno documentati i flussi di inserimento e modifica.
4. Il flusso di una sessione portable sarà completo.
5. La gestione offline sarà esplicita.
6. Gli stati di sincronizzazione saranno definiti.
7. Saranno definite le convenzioni per tabelle, form e grafici.
8. Saranno disponibili wireframe delle schermate prioritarie.

---

## 18. Schermate da progettare nel dettaglio

Prima dello sviluppo, le schermate da completare con wireframe e specifiche dei campi sono:

| Priorità | Schermata |
|---|---|
| P0 | Dashboard |
| P0 | Station Manager – Elenco e scheda apparati |
| P0 | Station Manager – Elenco e scheda antenne |
| P0 | QSO Logbook – Elenco |
| P0 | QSO Logbook – Inserimento |
| P0 | Field Operations – Elenco attività |
| P0 | Field Operations – Sessione operativa |
| P1 | Digital Modes Lab |
| P1 | Antenna Lab |
| P1 | Propagation Lab |
| P2 | VHF/UHF & APRS |
| P2 | SDR & RF Analyzer |
| P1 | Reporting |
| P0 | Impostazioni e stato sincronizzazione |

**Fine documento HRC-UX v1.0**
