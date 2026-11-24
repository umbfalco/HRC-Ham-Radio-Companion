# HRC – Ham Radio Companion
## HRC-UX – Wireframe funzionali delle schermate P0

**Versione:** 1.0  
**Stato:** Specifica funzionale preliminare  
**Riferimento:** HRC-UX v1.0

---

# 1. Convenzioni comuni

## 1.1 Struttura dell'applicazione

Tutte le schermate utilizzeranno un layout comune:

```text
┌─────────────────────────────────────────────────────────────┐
│ HRC       Ricerca globale                 Notifiche  Impost. │
├───────────────┬─────────────────────────────────────────────┤
│               │                                             │
│ Dashboard     │                                             │
│               │                                             │
│ Station       │              CONTENUTO                      │
│ Manager       │                                             │
│               │                                             │
│ QSO Logbook   │                                             │
│               │                                             │
│ Field Ops     │                                             │
│               │                                             │
│ Digital Lab   │                                             │
│               │                                             │
│ Propagation   │                                             │
│               │                                             │
│ Antenna Lab   │                                             │
│               │                                             │
│ Reporting     │                                             │
│               │                                             │
│ Impostazioni  │                                             │
├───────────────┴─────────────────────────────────────────────┤
│ Stato connessione | Stato sincronizzazione | IU8VBG         │
└─────────────────────────────────────────────────────────────┘
```

## 1.2 Convenzioni dei pulsanti

- Primario: azione principale, ad esempio Salva.
- Secondario: azione alternativa.
- Pericoloso: cancellazione o operazione irreversibile.
- Link: navigazione verso un'altra schermata.
- Menu contestuale: operazioni secondarie.

## 1.3 Comportamento generale

- Ogni pagina ha un titolo e una descrizione sintetica.
- Le azioni principali sono sempre riconoscibili.
- Le operazioni di inserimento sono accompagnate da validazione.
- La chiusura di una schermata con modifiche non salvate richiede conferma.
- I dati salvati localmente sono disponibili anche offline.
- Nessuna schermata deve richiedere la connessione Internet per funzionare.

---

# 2. Schermata P0-01 – Dashboard

## Obiettivo

Fornire una panoramica immediata della stazione, delle attività e dello stato operativo.

## Wireframe

```text
┌─────────────────────────────────────────────────────────────┐
│ DASHBOARD                                                   │
│ Panoramica della tua attività radioamatoriale               │
│                                                             │
│ [ + Nuova attività ] [ + Nuovo QSO ] [ Apri Logbook ]       │
│                                                             │
│ ┌────────────────┐ ┌────────────────┐ ┌───────────────────┐ │
│ │ QSO TOTALI     │ │ ATTIVITÀ       │ │ ESPERIMENTI       │ │
│ │                │ │                │ │                   │ │
│ │     1.245      │ │      18        │ │        4          │ │
│ └────────────────┘ └────────────────┘ └───────────────────┘ │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │ ULTIMI QSO                │ │ STAZIONE ATTIVA           │ │
│ │                           │ │                           │ │
│ │ Callsign  Banda  Modo     │ │ IU8VBG                    │ │
│ │ IK...     20m    FT8      │ │ Xiegu G90                 │ │
│ │ DL...     40m    SSB      │ │ Antenna: ...              │ │
│ │ ...                       │ │ Postazione: ...           │ │
│ │                           │ │ [Apri stazione]           │ │
│ │ [Vai al Logbook]          │ │                           │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │ ATTIVITÀ RECENTI          │ │ STATO SISTEMA             │ │
│ │                           │ │                           │ │
│ │ Ultima sessione           │ │ Connessione: Offline      │ │
│ │ Ultimo esperimento        │ │ Database: Disponibile     │ │
│ │                           │ │ In attesa sync: 12        │ │
│ │ [Apri attività]           │ │ [Dettagli sincronizzaz.]  │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## Elementi e comportamenti

### Azioni rapide

- Nuovo QSO: apre il modulo di inserimento rapido.
- Nuova attività: avvia la procedura guidata Field Operations.
- Apri Logbook: naviga alla tabella QSO.

### Indicatori

I contatori devono essere calcolati dai dati locali.

### Stazione attiva

Mostra la configurazione selezionata come predefinita. Non implica che il G90 sia collegato fisicamente.

### Stato sistema

Mostra:
- Connessione.
- Stato database.
- Record da sincronizzare.
- Eventuali errori.

## Criterio di accettazione

Dalla Dashboard l'utente deve poter iniziare un QSO o un'attività senza passare da altre schermate.

---

# 3. Schermata P0-02 – Station Manager

## Obiettivo

Gestire le stazioni e le relative configurazioni hardware.

## 3.1 Elenco stazioni

```text
STATION MANAGER

[Stazioni] [Apparati] [Antenne] [Postazioni]

Stazioni

[ + Nuova stazione ]

┌─────────────────────────────────────────────────────────────┐
│ Nome         Callsign    Locator    Stato                   │
├─────────────────────────────────────────────────────────────┤
│ Stazione 1   IU8VBG      JN81...    Principale               │
│ Stazione 2   IU8VBG      JN45...    Secondaria               │
└─────────────────────────────────────────────────────────────┘

Selezionando una stazione:

[Apri] [Modifica] [Imposta come principale]
```

## 3.2 Scheda stazione

```text
DETTAGLIO STAZIONE

Informazioni generali

Nome stazione       [________________________]
Callsign            [________________________]
Locator             [________________________]
Località            [________________________]
Coordinate          [________________________]

Configurazione

Apparati associati  [Seleziona apparati]
Antenne associate   [Seleziona antenne]
Postazioni          [Seleziona postazione]

Note                [________________________]
                    [________________________]

[Annulla]                              [Salva]
```

## 3.3 Elenco apparati

```text
APPARATI

[ + Nuovo apparato ]   [Cerca...]

┌─────────────────────────────────────────────────────────────┐
│ Marca     Modello      Tipo       Potenza    Stato          │
├─────────────────────────────────────────────────────────────┤
│ Xiegu     G90          HF         20 W       Disponibile    │
│ Baofeng   K6           VHF/UHF    ...        Disponibile    │
└─────────────────────────────────────────────────────────────┘
```

## 3.4 Scheda apparato

La schermata sarà organizzata in sezioni.

**Sezione generale**
- Marca.
- Modello.
- Tipologia.
- Identificativo.
- Numero seriale.
- Note.

**Sezione tecnica**
- Frequenze minime e massime.
- Potenza nominale.
- Modi supportati.
- Impedenza.
- Connettori.

**Sezione interfacce**
- CAT.
- Audio.
- USB.
- Seriali.
- Altre interfacce.

**Sezione documentazione**
- Manuale.
- Schede tecniche.
- Fotografie.
- Allegati.

Le specifiche non applicabili a un apparato devono poter rimanere vuote.

## 3.5 Elenco antenne

```text
ANTENNE

[ + Nuova antenna ]   [Cerca...]

┌─────────────────────────────────────────────────────────────┐
│ Nome          Tipo             Frequenze     Potenza        │
├─────────────────────────────────────────────────────────────┤
│ Longwire      EFHW/filare      HF            ...            │
│ Verticale     Verticale        HF            ...            │
│ Loop          Magnetica        HF/VHF        ...            │
└─────────────────────────────────────────────────────────────┘
```

## 3.6 Scheda antenna

**Informazioni generali**
- Nome.
- Tipologia.
- Costruttore.
- Modello.

**Caratteristiche tecniche**
- Frequenze operative.
- Impedenza.
- Guadagno dichiarato.
- Polarizzazione.
- Potenza massima.
- Dimensioni.

**Configurazione**
- Balun/un-un.
- Radiali.
- Contrappesi.
- Alimentazione.
- Cavo.
- Choke.

**Documentazione**
- Manuale.
- Fotografie.
- Misure NanoVNA.
- Note.

## 3.7 Installazioni antenna

Una antenna può avere più installazioni nel tempo o in località diverse.

Ogni installazione deve registrare:
- Antenna.
- Località.
- Locator.
- Coordinate.
- Altezza.
- Orientamento.
- Cavo.
- Choke.
- Configurazione dei radiali.
- Data iniziale e finale.

Il sistema non deve modificare retroattivamente le configurazioni utilizzate in esperimenti precedenti.

## Criterio di accettazione

Deve essere possibile registrare un apparato, un'antenna e una configurazione di installazione senza collegare fisicamente alcun dispositivo.

---

# 4. Schermata P0-03 – QSO Logbook

## Obiettivo

Gestire il registro dei collegamenti in modo semplice, veloce e compatibile con ADIF.

## 4.1 Elenco QSO

```text
QSO LOGBOOK

[ + Nuovo QSO ] [ Importa ADIF ] [ Esporta ADIF ]

Cerca callsign [____________]

Filtri:
Banda [Tutte v]  Modo [Tutti v]  Periodo [Tutti v]

┌─────────────────────────────────────────────────────────────┐
│ Data/UTC   Callsign   Frequenza   Modo   RST   Locator      │
├─────────────────────────────────────────────────────────────┤
│ ...        ...        ...         ...    ...   ...          │
│ ...        ...        ...         ...    ...   ...          │
└─────────────────────────────────────────────────────────────┘

Record: 1.245                  [<] Pagina 1 di 25 [>]
```

### Interazioni

- Click su una riga: apre il dettaglio QSO.
- Doppio click: apre la modifica.
- Menu contestuale: modifica, associa attività, cancellazione logica.
- Filtri: aggiornano la tabella.
- Esportazione: applica i filtri correnti oppure permette di scegliere l'intero archivio.

## 4.2 Inserimento rapido QSO

Questa è una schermata fondamentale: deve essere utilizzabile in pochi secondi.

```text
NUOVO QSO

┌─────────────────────────────────────────────────────────────┐
│ DATI DEL COLLEGAMENTO                                       │
│                                                             │
│ Callsign             [____________________]                 │
│ Data                 [gg/mm/aaaa]                           │
│ Ora UTC              [hh:mm]                                │
│ Frequenza            [__________] MHz                       │
│ Banda                [20 m v]                               │
│ Modo                 [SSB v]                                │
│                                                             │
│ RST TX               [59]       RST RX       [59]           │
│                                                             │
│ ─────────────────────────────────────────────────────────── │
│ DATI OPZIONALI                              [Mostra dettagli]│
│                                                             │
│ Locator              [__________]                            │
│ Nome operatore       [____________________]                 │
│ Paese                [____________________]                 │
│                                                             │
│ CONTESTO OPERATIVO                                          │
│ Attività             [Nessuna v]                            │
│ Stazione             [Stazione principale v]                │
│                                                             │
│ Note                 [____________________________]         │
│                      [____________________________]         │
│                                                             │
│ [Annulla]                             [Salva QSO]            │
└─────────────────────────────────────────────────────────────┘
```

### Regole di funzionamento

- Callsign obbligatorio.
- Data e ora UTC precompilate con l'orario corrente.
- Frequenza e banda coerenti.
- Se viene modificata la frequenza, la banda può essere proposta automaticamente.
- Il modo è selezionabile da un elenco.
- RST precompilato secondo il modo, ma modificabile.
- L'associazione ad attività è facoltativa.
- Salvataggio sempre locale e immediato.
- Il salvataggio non dipende dalla connessione Internet.

La frequenza deve essere memorizzata in Hz, anche se visualizzata in MHz.

## 4.3 Dettaglio avanzato QSO

Il comando Mostra dettagli espande ulteriori campi:

- Nome e QTH.
- Locator.
- Paese.
- QSL ricevuta/inviata.
- POTA/SOTA e riferimenti attività.
- Apparato.
- Antenna.
- Potenza.
- Commenti.
- Fonte del record.
- Identificativo ADIF.

## 4.4 Importazione ADIF

```text
IMPORTAZIONE ADIF

1. Selezione file

[Seleziona file .adi/.adif]

2. Analisi

Record individuati:       250
Record validi:            245
Record potenzialmente duplicati: 3
Record non validi:          2

3. Anteprima

[Visualizza record]

4. Conferma

[Annulla]                    [Importa record validi]
```

L'utente deve poter consultare i record esclusi e il motivo dell'esclusione.

## 4.5 Esportazione ADIF

Opzioni:

- Tutti i QSO.
- QSO filtrati.
- Intervallo temporale.
- Banda.
- Modo.
- Attività.

Il file generato deve rispettare il formato ADIF selezionato.

## Criterio di accettazione

Inserire manualmente un QSO deve essere possibile senza aprire la sezione avanzata.

---

# 5. Schermata P0-04 – Field Operations

## Obiettivo

Gestire attività radioamatoriali in mobilità e sessioni sperimentali, anche completamente offline.

Il modulo avrà due modalità: guidata e libera.

## 5.1 Elenco attività

```text
FIELD OPERATIONS

[ + Nuova attività ]

Filtri:
Periodo [Tutti v]   Tipologia [Tutte v]   Stato [Tutti v]

┌─────────────────────────────────────────────────────────────┐
│ Attività          Località       Data       Stato           │
├─────────────────────────────────────────────────────────────┤
│ Test antenna      ...            ...        Completata      │
│ Portable HF       ...            ...        In corso        │
│ POTA              ...            ...        Pianificata     │
└─────────────────────────────────────────────────────────────┘
```

Stati:
- Pianificata.
- In corso.
- Sospesa.
- Completata.
- Archiviata.

## 5.2 Avvio guidato

La procedura guidata avrà cinque passaggi.

### Passaggio 1 – Informazioni generali

```text
NUOVA ATTIVITÀ                         PASSAGGIO 1 DI 5

Nome attività       [________________________]
Tipologia           [Portable HF v]
Data                [gg/mm/aaaa]
Ora inizio          [hh:mm]

Descrizione         [________________________]
                    [________________________]

[Annulla]                            [Avanti]
```

Tipologie iniziali:
- Portable HF.
- POTA.
- SOTA.
- Test antenna.
- Test propagazione.
- Ricezione.
- Altro.

### Passaggio 2 – Località

```text
LOCALITÀ                              PASSAGGIO 2 DI 5

Nome località       [________________________]
Comune              [________________________]
Provincia           [________________________]
Paese               [Italia]

Locator Maidenhead  [____________]
Latitudine          [____________]
Longitudine         [____________]

[Usa località salvata]

[Indietro]                            [Avanti]
```

Le coordinate e il locator potranno essere inseriti manualmente. La geolocalizzazione automatica sarà una funzione successiva e facoltativa.

### Passaggio 3 – Configurazione radio

```text
CONFIGURAZIONE                        PASSAGGIO 3 DI 5

Stazione            [Stazione principale v]

Apparato            [Xiegu G90 v]
Antenna             [Seleziona antenna v]
Installazione       [Seleziona installazione v]

Potenza prevista    [____] W

Bande operative     [40 m] [20 m] [+ Aggiungi]

Note configurazione [________________________]

[Indietro]                            [Avanti]
```

I valori saranno proposti a partire dalle configurazioni registrate nello Station Manager, ma saranno modificabili per la sessione corrente.

### Passaggio 4 – Parametri e obiettivi

```text
OBIETTIVI                             PASSAGGIO 4 DI 5

Obiettivo           [________________________]
Protocollo          [________________________]

Condizioni meteo    [________________________]
Temperatura         [____] °C
Vento               [________________________]

Variabili da misurare
[ ] SNR
[ ] SWR
[ ] Potenza TX
[ ] Frequenza
[ ] Altro

Note                [________________________]

[Indietro]                            [Avanti]
```

### Passaggio 5 – Riepilogo

```text
RIEPILOGO                             PASSAGGIO 5 DI 5

Attività:       Test antenna
Località:       ...
Data:           ...
Apparato:       Xiegu G90
Antenna:        ...
Bande:          40 m, 20 m

[Modifica]       [Salva e avvia attività]
```

L'utente potrà salvare una sessione pianificata oppure iniziarla immediatamente.

## 5.3 Schermata sessione attiva – Modalità libera

Questa è la schermata più importante del modulo.

```text
SESSIONE ATTIVA – TEST ANTENNA

Stato: IN CORSO
Inizio: 09:35 UTC
Durata: 00:42:18

┌─────────────────────────────────────────────────────────────┐
│ CONFIGURAZIONE ATTUALE                                      │
│ Apparato: Xiegu G90                                         │
│ Antenna: Longwire                                           │
│ Banda: 40 m                                                 │
│ Potenza: 5 W                                                │
│                                                             │
│ [Cambia configurazione]                                     │
└─────────────────────────────────────────────────────────────┘

┌──────────────────────────────┐
│ AZIONI RAPIDE                │
│                              │
│ [ + Registra QSO ]           │
│ [ + Nuova misura ]           │
│ [ + Aggiungi nota ]          │
│ [ + Allegato ]               │
└──────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ DIARIO CRONOLOGICO                                          │
│                                                             │
│ 09:35  Sessione avviata                                     │
│ 09:42  Antenna configurata                                  │
│ 09:51  Misura SWR: ...                                      │
│ 10:05  Nota: ...                                            │
│                                                             │
│ [Visualizza tutto]                                          │
└─────────────────────────────────────────────────────────────┘

[ Sospendi ]                              [ Termina sessione ]
```

### Funzioni operative

**Registra QSO**
Apre il modulo rapido del Logbook con attività già associata.

**Nuova misura**
Permette di inserire:
- Tipo di misura.
- Valore.
- Unità.
- Timestamp.
- Strumento.
- Configurazione.
- Note.

**Aggiungi nota**
Inserisce una voce cronologica con timestamp automatico.

**Allegato**
Consente di associare file e fotografie alla sessione.

**Cambia configurazione**
Registra una nuova configurazione senza sovrascrivere quella precedente.

Ogni cambio deve creare un evento cronologico.

## 5.4 Sospensione e ripresa

Quando si sospende una sessione:
- viene registrato l'orario;
- la sessione rimane salvata;
- l'utente può riprenderla;
- la durata attiva e quella complessiva devono essere distinguibili.

## 5.5 Chiusura attività

```text
TERMINA SESSIONE

Ora fine             [hh:mm]
Sintesi attività     [________________________]

Risultati principali [________________________]

Problemi riscontrati [________________________]

[Annulla]                         [Conferma chiusura]
```

La chiusura non cancella i dati e non impedisce successive annotazioni integrative.

## 5.6 Modalità libera

La modalità libera permette di compilare o modificare i dati senza una procedura guidata.

Sarà disponibile:
- Durante la creazione di un'attività.
- Durante la modifica.
- Nella gestione di sessioni già esistenti.

La procedura guidata sarà una facilitazione, non un vincolo strutturale del modello dati.

## Criterio di accettazione

L'utente deve poter creare un'attività, avviarla, registrare QSO, misure e note e terminarla senza connessione Internet.

---

# 6. Schermata P0-05 – Impostazioni e sincronizzazione

## Obiettivo

Consentire la gestione locale dell'applicazione e rendere trasparente lo stato di sincronizzazione.

## 6.1 Impostazioni generali

```text
IMPOSTAZIONI

[Generali] [Stazione] [Database] [Dispositivi]
[Sincronizzazione] [Integrazioni]

Generali

Lingua                  Italiano
Tema                    Automatico
Formato data            gg/mm/aaaa
Fuso orario             Locale
Orari radio             UTC

[Salva modifiche]
```

## 6.2 Database e backup

```text
DATABASE

Stato database          Disponibile
Percorso archivio       [Visualizza percorso]

Ultimo backup           ...
Dimensione database     ...

[Backup adesso]
[Ripristina backup]
[Verifica integrità]
```

Il ripristino deve richiedere una conferma esplicita e prevedere una copia di sicurezza prima dell'operazione.

## 6.3 Sincronizzazione

```text
SINCRONIZZAZIONE

Stato connessione       Offline
Stato sincronizzazione  In attesa

Record da inviare       12
Record da ricevere      -
Conflitti               0
Errori                  0

Ultima sincronizzazione ...

[Sincronizza adesso]
[Visualizza coda]
[Visualizza storico]
```

La configurazione del server remoto sarà disponibile, ma il funzionamento locale non dovrà dipenderne.

## 6.4 Coda sincronizzazione

```text
CODA SINCRONIZZAZIONE

┌─────────────────────────────────────────────────────────────┐
│ Tipo record    Operazione    Stato        Data              │
├─────────────────────────────────────────────────────────────┤
│ QSO            Inserimento   In attesa    ...               │
│ Activity       Modifica      In attesa    ...               │
│ Measurement    Inserimento   In attesa    ...               │
└─────────────────────────────────────────────────────────────┘
```

## Criterio di accettazione

L'utente deve poter verificare lo stato dei dati locali e della sincronizzazione senza dover conoscere i dettagli tecnici dell'Outbox o delle API.

---

# 7. Flussi operativi principali

## Flusso A – Registrazione QSO

```text
Dashboard
   |
   v
Nuovo QSO
   |
   v
Inserimento dati essenziali
   |
   v
Validazione
   |
   v
Salvataggio SQLite
   |
   v
Conferma QSO salvato
   |
   v
Record in attesa di sincronizzazione
```

## Flusso B – Attività portable

```text
Dashboard
   |
   v
Nuova attività
   |
   v
Procedura guidata
   |
   v
Salvataggio attività
   |
   v
Avvio sessione
   |
   +----> Registra QSO
   |
   +----> Inserisci misura
   |
   +----> Aggiungi nota
   |
   +----> Allega file
   |
   v
Termina sessione
   |
   v
Riepilogo attività
```

## Flusso C – Configurazione stazione

```text
Station Manager
   |
   +----> Crea apparato
   |
   +----> Crea antenna
   |
   +----> Crea postazione
   |
   v
Crea installazione antenna
   |
   v
Associa configurazione alla stazione
   |
   v
Configurazione disponibile nelle attività
```

---

# 8. Regole di navigazione e comportamento

1. La barra laterale rimane sempre disponibile.
2. Ogni schermata deve consentire di tornare alla pagina precedente.
3. Le modifiche non salvate devono essere protette.
4. I dati inseriti in una sessione devono essere salvati localmente.
5. La modalità offline non deve disabilitare le operazioni locali.
6. La sincronizzazione deve essere asincrona e non bloccare l'interfaccia.
7. I dettagli tecnici devono essere nascosti nelle sezioni avanzate, non eliminati.
8. Ogni entità deve poter essere aperta dalla propria schermata e dai riferimenti incrociati.
9. I record cancellati devono essere recuperabili secondo le regole di conservazione definite dal sistema.
10. Le schermate future devono rispettare lo stesso sistema di navigazione.

---

# 9. Questioni progettuali da risolvere prima dello sviluppo

- Definizione definitiva dei campi e delle relazioni del database.
- Gestione delle unità e delle grandezze fisiche.
- Gestione delle installazioni storiche.
- Regole di associazione tra QSO, attività ed esperimenti.
- Gestione degli allegati e dei percorsi dei file.
- Gestione delle identità dei dispositivi.
- Gestione dei conflitti di sincronizzazione.
- Specifica dei permessi e della sicurezza del server remoto.

**Fine documento HRC-UX – Wireframe funzionali P0 v1.0**
