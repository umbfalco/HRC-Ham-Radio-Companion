# HRC – Ham Radio Companion
## Specificazione tecnica e piano di realizzazione – Versione 1.0

**Data:** 24 novembre 2026  
**Stato:** Progettazione approvata – sviluppo non ancora avviato  
**Piattaforma principale:** Windows 11  
**Lingua interfaccia:** Italiano

---

# 1. Descrizione generale

HRC (Ham Radio Companion) è un'applicazione desktop destinata alla gestione delle attività radioamatoriali e alla sperimentazione tecnica in ambito RF.

Il progetto nasce con l'obiettivo di integrare in un unico ambiente:

- Gestione della stazione radio.
- Registrazione dei QSO.
- Attività radio portatili.
- Gestione degli apparati e delle antenne.
- Integrazione con software per modi digitali.
- Acquisizione e analisi dei dati WSPR.
- Analisi della propagazione.
- Misurazioni e sperimentazione sulle antenne.
- Gestione di dati SDR e VHF/UHF.
- Produzione di documentazione tecnica.

HRC non intende sostituire integralmente i software specializzati esistenti, ma coordinarne i dati e aggiungere funzionalità di gestione, analisi e documentazione.

## 1.1 Obiettivi strategici

1. Realizzare un'applicazione utilizzabile realmente durante le attività radio.
2. Garantire il funzionamento senza connessione Internet.
3. Consentire la sincronizzazione dei dati tra installazioni.
4. Integrare apparati e software radioamatoriali.
5. Sviluppare strumenti di analisi quantitativa.
6. Documentare gli esperimenti in maniera ripetibile.
7. Costruire progressivamente un laboratorio software personale.

## 1.2 Principi progettuali

- Offline-first.
- Modularità.
- Separazione delle responsabilità.
- Persistenza locale affidabile.
- Sincronizzazione differita.
- Tracciabilità delle modifiche.
- Conservazione dei dati originali.
- Testabilità.
- Estensibilità.

---

# 2. Perimetro funzionale

Il progetto sarà sviluppato progressivamente.

Non tutti i moduli saranno disponibili nella prima versione.

## 2.1 Moduli previsti

| Modulo | Descrizione | Priorità |
|---|---|---|
| HRC Core | Servizi condivisi, database, configurazione | P0 |
| Station Manager | Apparati, antenne e postazioni | P0 |
| QSO Logbook | Gestione comunicazioni e ADIF | P0 |
| Field Operations | Attività portable e diario operativo | P0 |
| Digital Modes Lab | FT8, FT4, WSPR e integrazioni | P1 |
| Propagation Lab | Analisi della propagazione | P1 |
| Antenna Lab | Caratterizzazione e confronto antenne | P1 |
| VHF/UHF & APRS | Gestione attività VHF/UHF | P2 |
| SDR & RF Analyzer | Analisi spettrale e segnali IQ | P2 |
| Desktop Packaging | Distribuzione Windows tramite Tauri | P1 |

P0: indispensabile per il primo prodotto utilizzabile.  
P1: estensione funzionale successiva.  
P2: funzionalità avanzate.

## 2.2 Funzionalità escluse dalla prima versione

- Decodifica proprietaria FT8.
- Implementazione autonoma del protocollo WSPR.
- Software SDR completo.
- Server cloud proprietario immediatamente operativo.
- Sincronizzazione in tempo reale.
- Controllo automatico di tutti gli apparati.
- Applicazione mobile nativa.

---

# 3. Architettura tecnologica

## 3.1 Stack approvato

| Livello | Tecnologia | Utilizzo |
|---|---|---|
| Frontend | React | Interfaccia utente |
| Linguaggio frontend | TypeScript | Tipizzazione |
| UI | Componenti React | Interfaccia modulare |
| Backend | Python | Logica applicativa |
| API | FastAPI | Comunicazione frontend/backend |
| ORM | SQLAlchemy | Accesso ai dati |
| Database | SQLite | Persistenza locale |
| Migrazioni | Alembic | Evoluzione schema DB |
| Analisi | NumPy, Pandas, SciPy | Elaborazione dati |
| Statistica | Statsmodels | Analisi avanzata |
| Grafici | Plotly | Visualizzazioni |
| Mappe | Leaflet | Visualizzazione geografica |
| Test backend | Pytest | Test automatici |
| Test frontend | Vitest | Test automatici |
| Desktop | Tauri 2 | Packaging |
| Versionamento | Git | Controllo versioni |
| Repository | GitHub | Gestione progetto |

## 3.2 Architettura logica

L'applicazione sarà organizzata secondo il modello Modular Monolith, utilizzando principi Clean Architecture.

Livelli:

1. Presentation: interfaccia React.
2. API: endpoint FastAPI.
3. Application: servizi e casi d'uso.
4. Domain: entità e regole di business.
5. Infrastructure: database e file system.
6. Adapters: integrazione con software e hardware esterni.

Le dipendenze devono essere orientate verso il dominio applicativo.

I moduli non devono accedere direttamente alle tabelle di altri moduli: devono utilizzare servizi o interfacce condivise.

## 3.3 Architettura di esecuzione

Durante lo sviluppo:

- React sarà eseguito tramite il proprio server di sviluppo.
- FastAPI sarà eseguito come processo locale.
- SQLite conserverà i dati sul notebook.
- Il frontend comunicherà con il backend tramite API HTTP locali.

Nella versione desktop:

- Tauri gestirà la finestra applicativa.
- Il backend Python sarà avviato come processo secondario.
- Il database rimarrà locale.
- Le integrazioni radio saranno gestite dal backend o da adapter dedicati.

Il packaging definitivo richiederà una gestione esplicita del ciclo di vita del processo Python e delle porte di comunicazione locali.

---

# 4. Architettura offline e sincronizzazione

La sincronizzazione è un requisito architetturale iniziale.

## 4.1 Modello operativo

HRC dovrà essere utilizzabile anche in assenza completa di connessione Internet.

Ogni installazione avrà un database locale.

La sincronizzazione sarà effettuata attraverso API dedicate, senza condividere direttamente il file SQLite.

## 4.2 Componenti

- Local Database: archivio operativo.
- Sync Engine: motore di sincronizzazione.
- Outbox: coda delle modifiche locali.
- Remote API: interfaccia del servizio remoto.
- Remote Database: archivio sincronizzato.
- Conflict Resolver: gestione delle modifiche concorrenti.
- Attachment Sync: trasferimento degli allegati.

## 4.3 Identificazione e versionamento

Ogni record sincronizzabile dovrà contenere:

- UUID.
- created_at.
- updated_at.
- deleted_at, quando applicabile.
- version.
- origin_device_id.
- sync_status.

Gli orari saranno memorizzati in UTC.

Le cancellazioni saranno inizialmente logiche (soft delete), in modo da poter propagare correttamente le modifiche tra dispositivi.

## 4.4 Gestione delle modifiche

Ogni operazione locale dovrà essere registrata in una coda transazionale.

La modifica del record e l'inserimento dell'evento Outbox dovranno avvenire nella stessa transazione SQLite.

Stati previsti:

- PENDING.
- IN_PROGRESS.
- SYNCED.
- FAILED.
- CONFLICT.

## 4.5 Risoluzione conflitti

Strategia iniziale:

- Dati anagrafici: rilevamento conflitti e risoluzione esplicita.
- QSO: inserimento idempotente tramite identificativo stabile e controllo duplicati.
- Spot WSPR: deduplicazione basata su identificativi e chiavi composite.
- Misurazioni: conservazione degli eventi originali.
- Allegati: sincronizzazione separata dal record descrittivo.
- Cancellazioni: tombstone e propagazione.

Non sarà utilizzato un semplice criterio globale di ultima modifica vincente per tutti i dati, perché potrebbe causare perdita di informazioni.

## 4.6 Sicurezza

- Comunicazioni remote HTTPS.
- Autenticazione tramite token.
- Identità distinta per installazione.
- Nessuna password memorizzata in chiaro.
- Backup prima delle operazioni di ripristino.
- Validazione dei dati ricevuti.
- Gestione degli errori e retry.

La sincronizzazione cloud sarà implementata dopo la stabilizzazione del Core, ma i requisiti e le strutture necessarie saranno presenti fin dalla prima versione del database.

---

# 5. Modello dati

## 5.1 Entità principali

| Entità | Descrizione |
|---|---|
| Station | Postazione radio |
| Equipment | Apparato o strumento |
| Antenna | Anagrafica antenna |
| AntennaInstallation | Configurazione fisica |
| Location | Località e locator |
| Activity | Attività radio |
| QSO | Comunicazione |
| Measurement | Misurazione |
| Observation | Osservazione tecnica |
| Experiment | Esperimento |
| ExperimentSession | Sessione sperimentale |
| TransmissionBlock | Blocco di trasmissione |
| WSPRSpot | Rapporto WSPR |
| Attachment | Allegato |
| Device | Installazione HRC |
| SyncOperation | Operazione di sincronizzazione |

## 5.2 Relazioni principali

- Una Station può contenere più Equipment.
- Una Station può avere più Location operative.
- Una Activity può contenere più QSO.
- Una Activity può essere collegata a un Experiment.
- Un Experiment può contenere più ExperimentSession.
- Una ExperimentSession può contenere più TransmissionBlock.
- Un TransmissionBlock identifica antenna, banda, potenza e intervallo temporale.
- Una sessione può generare più Measurement e WSPRSpot.
- Le entità principali possono essere associate ad Attachment.

## 5.3 Convenzioni database

- Chiavi primarie UUID.
- Date in UTC.
- Unità di misura esplicite.
- Potenza in dBm o W, con unità dichiarata.
- Frequenze in Hz.
- Distanze in metri o chilometri, con unità dichiarata.
- Azimut in gradi.
- Coordinate geografiche WGS84.
- Locator Maidenhead conservato anche come dato originale.

Le unità non dovranno essere interpretate implicitamente.

---

# 6. Requisiti funzionali

## 6.1 HRC Core

- FR-CORE-001: avvio applicazione.
- FR-CORE-002: configurazione generale.
- FR-CORE-003: gestione database locale.
- FR-CORE-004: logging applicativo.
- FR-CORE-005: backup e ripristino.
- FR-CORE-006: identificazione dispositivo.
- FR-CORE-007: predisposizione sincronizzazione.

## 6.2 Station Manager

- FR-STA-001: inserimento apparati.
- FR-STA-002: inserimento antenne.
- FR-STA-003: configurazione postazioni.
- FR-STA-004: associazione apparati e antenne.
- FR-STA-005: storico delle configurazioni.

## 6.3 QSO Logbook

- FR-QSO-001: inserimento manuale QSO.
- FR-QSO-002: modifica e cancellazione logica.
- FR-QSO-003: ricerca e filtri.
- FR-QSO-004: importazione ADIF.
- FR-QSO-005: esportazione ADIF.
- FR-QSO-006: statistiche per banda e modo.
- FR-QSO-007: associazione a sessioni operative.

## 6.4 Field Operations

- FR-FLD-001: creazione attività.
- FR-FLD-002: registrazione località.
- FR-FLD-003: configurazione apparati e antenne.
- FR-FLD-004: diario operativo.
- FR-FLD-005: registrazione misure.
- FR-FLD-006: allegati.
- FR-FLD-007: utilizzo offline.

## 6.5 Digital Modes Lab

- FR-DIG-001: acquisizione dati WSJT-X.
- FR-DIG-002: importazione spot WSPR.
- FR-DIG-003: associazione spot alle sessioni.
- FR-DIG-004: statistiche FT8/FT4.
- FR-DIG-005: esportazione dati.

## 6.6 Antenna Lab

- FR-ANT-001: definizione esperimento.
- FR-ANT-002: configurazione antenne.
- FR-ANT-003: registrazione installazioni.
- FR-ANT-004: gestione blocchi A/B.
- FR-ANT-005: importazione WSPR.
- FR-ANT-006: calcolo distanza e azimut.
- FR-ANT-007: confronto SNR appaiato.
- FR-ANT-008: analisi statistica.
- FR-ANT-009: diagrammi polari.
- FR-ANT-010: esportazione relazione tecnica.

---

# 7. Requisiti non funzionali

## 7.1 Affidabilità

- Nessuna perdita di dati in caso di chiusura ordinata.
- Transazioni database.
- Backup ripristinabili.
- Gestione degli errori.
- Conservazione dei dati grezzi.

## 7.2 Prestazioni

L'applicazione dovrà essere utilizzabile su un normale notebook Windows 11.

Gli obiettivi iniziali saranno:

- Apertura dashboard entro pochi secondi.
- Ricerca QSO senza ritardi percepibili.
- Importazione di archivi di grandi dimensioni con feedback di avanzamento.
- Elaborazioni statistiche eseguite senza bloccare l'interfaccia.

I valori saranno misurati durante il collaudo e formalizzati successivamente.

## 7.3 Usabilità

- Interfaccia italiana.
- Navigazione modulare.
- Messaggi di errore comprensibili.
- Indicazione dello stato offline/online.
- Indicazione della sincronizzazione.
- Funzionamento con mouse e tastiera.
- Visualizzazione adattabile alle dimensioni del notebook.

## 7.4 Manutenibilità

- Codice modulare.
- Test automatici.
- Documentazione tecnica.
- Migrazioni database.
- Separazione frontend/backend.
- Versionamento Git.

---

# 8. Integrazioni hardware e software

## 8.1 Xiegu G90

Integrazione CAT attraverso Hamlib/rigctld.

Funzioni previste:

- Lettura frequenza.
- Lettura modo.
- Lettura stato apparato.
- Eventuale controllo frequenza e modo.
- Associazione QSO alla configurazione radio.

Il collegamento audio e CAT tramite DE-19 sarà verificato separatamente.

## 8.2 WSJT-X

Integrazione UDP.

HRC potrà acquisire gli eventi pubblicati dal software, elaborarli e associarli ai QSO e alle sessioni.

WSJT-X resterà responsabile della decodifica e generazione dei modi digitali.

## 8.3 NanoVNA

Prima fase: importazione dei file di misura, compresi i formati compatibili come Touchstone.

Fase successiva: analisi di SWR, impedenza, frequenza di risonanza e banda.

## 8.4 SDR

L'integrazione sarà definita in funzione del dispositivo scelto.

HRC dovrà inizialmente poter importare misure e dati generati da software esterni.

## 8.5 Baofeng K6

Gestione anagrafica, frequenze, piani canali e attività. Il controllo CAT non sarà requisito della prima versione.

---

# 9. Specifica WSPR Antenna Lab

## 9.1 Obiettivo

Confrontare il comportamento trasmissivo di due o più antenne mediante l'analisi degli spot WSPR ricevuti da stazioni remote.

Il risultato sarà un diagramma relativo di prestazione osservata, non un diagramma assoluto di radiazione.

## 9.2 Protocollo sperimentale

- Trasmettitore invariato.
- Potenza costante e misurata.
- Banda invariata.
- Frequenza invariata.
- Postazione documentata.
- Configurazione antenna documentata.
- Alternanza A/B.
- Sequenza ABBA.
- Sessioni ripetute in giornate diverse.

## 9.3 Raccolta dati

Per ogni spot:

- Timestamp UTC.
- Nominativo TX.
- Locator TX.
- Nominativo RX.
- Locator RX.
- SNR.
- Frequenza.
- Potenza dichiarata.
- Antenna.
- Sessione.
- Blocco di trasmissione.
- Distanza.
- Azimut.

## 9.4 Analisi

- Deduplicazione.
- Validazione.
- Calcolo geodetico.
- Suddivisione in settori.
- Statistiche descrittive.
- Confronto appaiato.
- Bootstrap a cluster.
- Intervalli di confidenza.
- Analisi dell'interazione antenna/settore.

## 9.5 Output

- Mappa ricevitori.
- Diagramma polare.
- Diagramma comparativo.
- Box plot.
- Heatmap azimut/orario.
- Tabella statistiche.
- Relazione tecnica PDF.

## 9.6 Limiti scientifici

I risultati dipendono anche da propagazione, ricevitori remoti, antenne riceventi, rumore e condizioni ambientali.

L'assenza di uno spot non rappresenta un SNR pari a zero.

Le conclusioni dovranno riportare numero di ricevitori, copertura geografica, incertezza e limiti sperimentali.

---

# 10. Organizzazione del repository

ham-radio-companion/

- frontend/
  - src/components/
  - src/layouts/
  - src/modules/
  - src/services/
  - src/types/
  - tests/

- backend/
  - app/api/
  - app/domain/
  - app/application/
  - app/infrastructure/
  - app/adapters/
  - tests/

- database/
  - migrations/

- docs/
  - requirements/
  - architecture/
  - experiments/
  - user-guide/

- scripts/
- README.md
- .gitignore

I nomi delle classi, delle funzioni, delle tabelle e delle API saranno in inglese. L'interfaccia utente sarà in italiano.

---

# 11. Piano di sviluppo

## Fase 0 – Progettazione

Deliverable:
- Specifica tecnica.
- Requisiti.
- Modello dati.
- Architettura.
- Wireframe.

## Fase 1 – Ambiente

Deliverable:
- Ambiente Python.
- Ambiente Node.js.
- IDE.
- Git.
- Backend avviabile.
- Frontend avviabile.

## Fase 2 – Core

Deliverable:
- SQLite.
- SQLAlchemy.
- Alembic.
- API.
- Logging.
- Identificazione dispositivo.
- Outbox e predisposizione sincronizzazione.

## Fase 3 – Station Manager

Deliverable:
- Apparati.
- Antenne.
- Postazioni.
- Configurazioni.

## Fase 4 – Logbook

Deliverable:
- QSO.
- ADIF.
- Ricerca.
- Statistiche.

## Fase 5 – Field Operations

Deliverable:
- Attività portable.
- Località.
- Diario.
- Allegati.

## Fase 6 – Digital Modes

Deliverable:
- WSJT-X.
- FT8/FT4.
- WSPR.

## Fase 7 – Antenna e Propagation Lab

Deliverable:
- Importazione dati.
- Analisi statistica.
- Grafici.
- Report.

## Fase 8 – VHF/UHF e SDR

Deliverable:
- Ripetitori.
- APRS.
- Analisi RF.
- Integrazione SDR.

## Fase 9 – Distribuzione

Deliverable:
- Tauri.
- Installer Windows.
- Backup.
- Ripristino.
- Sincronizzazione remota.

---

# 12. Criteri di accettazione del primo prodotto

La prima versione utilizzabile dovrà consentire di:

1. Avviare HRC senza Internet.
2. Configurare almeno una stazione radio.
3. Registrare almeno un apparato e un'antenna.
4. Creare un'attività portable.
5. Registrare QSO.
6. Importare ed esportare ADIF.
7. Conservare note e misure.
8. Effettuare backup.
9. Ripristinare il database.
10. Mantenere i dati locali pronti per la sincronizzazione futura.

La prima versione non richiede ancora l'integrazione automatica del G90 o l'analisi WSPR.

---

# 13. Metodo di lavoro e apprendimento

Lo sviluppo sarà anche un percorso di apprendimento Python.

Ogni fase dovrà comprendere:

- Spiegazione dei concetti.
- Teoria architetturale.
- Esempi guidati.
- Implementazione progressiva.
- Test.
- Verifica del funzionamento.
- Documentazione.

Non si passerà alla fase successiva senza aver compreso e verificato i risultati della precedente.

Il codice dovrà essere leggibile, documentato e coerente con le competenze già acquisite nello sviluppo enterprise.

---

# 14. Stato del progetto

**Specificazione tecnica v1.0: approvata come baseline progettuale.**

Non è stato ancora avviato lo sviluppo.

Le successive modifiche dovranno essere documentate come nuove versioni della specifica.

Il primo documento operativo da produrre sarà la progettazione dettagliata dell'interfaccia e del modello dati, seguita dal piano di installazione e configurazione dell'ambiente Windows 11.

**Obiettivo finale:** realizzare un laboratorio radioamatoriale software personale, offline-first, sincronizzabile e scientificamente orientato, capace di accompagnare le attività radio e trasformarle in dati, misure e conoscenza tecnica.
