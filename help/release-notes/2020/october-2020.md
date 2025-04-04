---
title: Note sulla versione di Adobe Experience Platform di ottobre 2020
description: Note sulla versione di Adobe Experience Platform di ottobre 2020.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 16%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 14 ottobre 2020**

- [Preparazione dei dati](#data-prep)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)
- [Time to Value](#time-to-value)

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione `is_set` | La funzione `is_set` consente di verificare la presenza di un attributo nei dati di origine. `is_set` può essere utilizzato in combinazione con `is_empty` per verificare sia la presenza dell&#39;attributo che la presenza del valore all&#39;interno dell&#39;attributo. |
| Funzione `get_values` | La funzione `get_values` ti consente di ottenere i valori dalla mappa di input per una determinata chiave. |

Per ulteriori informazioni, leggere la [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con [!DNL Real-Time Customer Profile] è possibile visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. [!DNL Profile] consente di consolidare i dati disparati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiunte API di anteprima profilo | L&#39;API di anteprima profilo (`/previewsamplestatus`) ora include la possibilità di visualizzare un raggruppamento dei frammenti di profilo totali nell&#39;organizzazione e di visualizzare la distribuzione dei frammenti di profilo tra gli spazi dei nomi delle identità. |
| Aggiornamenti della visualizzazione schema di unione | Nell’interfaccia utente di Experience Platform, gli utenti possono trovare più facilmente le informazioni relative a tutti gli schemi e i set di dati che contribuiscono allo schema di unione, nonché gli attributi chiave della superficie, come i campi di identità e relazione. Questi aggiornamenti migliorano la possibilità di risolvere i problemi e di verificare che i profili siano configurati correttamente, che le identità siano unite correttamente e che i dati siano stati acquisiti correttamente. |

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un&#39;interfaccia utente e un&#39;API RESTful che consentono di creare segmenti e generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile]. Questi segmenti vengono configurati e gestiti centralmente in [!DNL Experience Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Rimozione del limite di segmentazione in streaming | Il limite di sette giorni per il periodo di lookback è stato rimosso. |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Experience Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema di gestione delle relazioni con i clienti.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto dell’autenticazione SSH per SFTP | Puoi collegare il tuo account SFTP a [!DNL Experience Platform] utilizzando le chiavi RSA/DSA Open SSH. Per ulteriori informazioni, consulta la [panoramica SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Miglioramenti UX | È possibile abilitare il set di dati per [!DNL Profile] durante il processo di acquisizione dei dati. Per ulteriori informazioni, consulta l&#39;esercitazione sul flusso di lavoro [per l&#39;archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).

## Time to Value {#time-to-value}

Adobe Experience Platform consente ai team che si occupano delle operazioni di marketing di creare una visualizzazione a 360 gradi dei clienti senza richiedere una vasta esperienza di progettazione dei dati. L’obiettivo è quello di accelerare i team e dare valore alla velocità dei dati.

&quot;Time to Value&quot; (Tempo al valore) taglia le persone. I data engineer possono completare le attività in modo efficiente e accelerato con trasparenza dell’attività dei dati, in modo che sia disponibile prima un profilo cliente solido e scalabile in tempo reale. Gli addetti al marketing possono quindi utilizzare il profilo cliente completo e affidabile per la segmentazione e l’attivazione.

### Elementi di rilievo della funzione

#### Schema

Aggiorna l’usabilità e il flusso di lavoro e fornisce informazioni predefinite, standardizzazione e trasparenza dei campi chiave nelle composizioni dello schema. Espone la derivazione dei dati per la combinazione di singoli modelli di dati rappresentati come &quot;schema di unione&quot;, fornendo insight nella struttura e negli ingredienti a Real-Time Customer Profile.

- Aggiornamento flusso di lavoro schema
   - Utilizza le scelte rapide per il tipo più comune di schemi XDM, con impostazioni automatizzate nell’editor schema e consigli per il gruppo di campi dello schema in base agli obiettivi
   - Maggiore efficienza del flusso di lavoro con la funzionalità di selezione e anteprima di più gruppi di campi
   - Fornisci trasparenza sugli attributi chiave della composizione dello schema, inclusi identità, relazione e campi obbligatori e obsoleti
- Trasparenza della derivazione dei dati dello schema di unione e degli attributi chiave

#### Acquisizione e raccolta dei dati

La mappatura automatica, l’anteprima della mappatura e l’aggiornamento dell’usabilità consentono di inserire dati da qualsiasi piattaforma o origine per l’utilizzo in profilo, segmentazione a valle e attivazione. Il sistema è dotato dell&#39;efficienza e dell&#39;intelligenza necessarie per semplificare l&#39;utilizzo di questo processo, anche per utenti esterni all&#39;IT.

- Accesso semplificato alle origini dati con la scheda della pagina del catalogo e l’aggiornamento del modello di azione in linea della tabella dati
- Campo/espressione calcolato per l’acquisizione dei dati
- I consigli sulla mappatura dei dati velocizzano il processo di acquisizione
- Anteprima mappatura e convalide

#### Configurazione profilo

Il visualizzatore di profilo intuitivo e personalizzabile consente di comprendere la composizione di un profilo da utilizzare nei casi di segmentazione, pianificazione e attivazione. Il flusso di lavoro consolidato idrata il profilo in modo controllato ed efficiente fornendo un flusso di lavoro graduale per i criteri di unione.

- Visualizza ogni singolo profilo in un visualizzatore di profili avanzato che visualizza una dashboard con personalizzazione completa, consentendo dati cross-channel raggruppati in base agli obiettivi aziendali dell’addetto al marketing.
- Modificare gli attributi standard e personalizzati nel widget Informazioni di base, in base alle esigenze aziendali.
- Personalizza i widget con attributi dal profilo cliente in tempo reale, utilizzando il selettore schema di unione. Lo schema di unione è derivato dai modelli di dati sottostanti utilizzati nell’acquisizione dei dati di profilo.


#### Monitoraggio

Assicura la trasparenza del flusso di dati e fornisce ad insight informazioni sullo stato del traffico di dati nel sistema dai connettori di origine, fornendo un’actionability più self-service e più rapida per la risoluzione dei problemi.

- Monitora tutte le esecuzioni del flusso e visualizza una vista dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell’esecuzione, l’elenco dei file elaborati, gli errori e la diagnostica actionable
