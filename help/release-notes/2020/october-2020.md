---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2020
description: Le note sulla versione di ottobre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 4%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 14 ottobre 2020**

- [Preparazione dei dati](#data-prep)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)
- [Time to Value](#time-to-value)

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione  di `is_set` | La `is_set` consente di controllare la presenza di un attributo all&#39;interno dei dati di origine. `is_set` può essere utilizzato in combinazione con `is_empty` per verificare sia la presenza dell’attributo sia la presenza del valore all’interno dell’attributo. |
| Funzione  di `get_values` | La `get_values` consente di ottenere i valori dalla mappa di input per una determinata chiave. |

Per ulteriori informazioni, leggere il [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-Time Customer Profile], puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiunte API di anteprima del profilo | API di anteprima del profilo (`/previewsamplestatus`) ora include la possibilità di visualizzare una suddivisione dei frammenti di profilo totali nell’organizzazione e di visualizzare la distribuzione dei frammenti di profilo tra i namespace identità. |
| Aggiornamenti della visualizzazione dello schema dell&#39;unione | Nell’interfaccia utente di Experience Platform, gli utenti possono trovare più facilmente informazioni su tutti gli schemi e i set di dati che contribuiscono allo schema dell’unione, nonché attributi chiave di superficie come i campi di identità e relazione. Questi aggiornamenti migliorano la possibilità di risolvere e convalidare la corretta configurazione dei profili, la corretta unione delle identità e il corretto inserimento dei dati. |

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], incluse esercitazioni e best practice per l’utilizzo di [!DNL Profile] dati, leggere [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal proprio [!DNL Real-Time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione di Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Rimozione del limite di segmentazione in streaming | Il limite di sette giorni per il periodo di lookback è stato rimosso. |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto dell’autenticazione SSH per SFTP | Puoi collegare il tuo account SFTP a [!DNL Platform] utilizzo delle chiavi SSH aperte RSA/DSA. Consulta la sezione [Panoramica SFTP](../../sources/connectors/cloud-storage/sftp.md) per ulteriori informazioni. |
| Miglioramenti UX | Puoi abilitare il set di dati per [!DNL Profile] durante il processo di inserimento dei dati. Consulta la sezione [flusso di lavoro flusso di lavoro per l’archiviazione cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) esercitazione per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).

## Time to Value {#time-to-value}

Adobe Experience Platform consente ai team delle operazioni di marketing di creare una visione a 360 gradi dei propri clienti senza richiedere un&#39;ampia esperienza di ingegneria dei dati. L&#39;obiettivo è accelerare i team e valutare la velocità dei dati.

&quot;Time to Value&quot; taglia tra le persone. I data engineer possono completare le attività in modo efficiente e accelerato grazie alla trasparenza delle attività dati, in modo che sia disponibile prima un profilo cliente in tempo reale affidabile e scalabile. Gli addetti al marketing possono quindi utilizzare un profilo cliente completo e affidabile per la segmentazione e l’attivazione.

### Funzioni principali

#### Schema

Aggiorna usabilità e flusso di lavoro e fornisce informazioni predefinite, standardizzazione e trasparenza dei campi chiave nelle composizioni degli schemi. Espone la derivazione dei dati per la combinazione di singoli modelli di dati rappresentati come &quot;schema di unione&quot;, fornendo informazioni sulla struttura e gli ingredienti del Profilo del cliente in tempo reale.

- Aggiornamento del flusso di lavoro dello schema
   - Utilizza le scelte rapide per il tipo più comune di schemi XDM, con impostazioni automatizzate nell’editor di schemi e raccomandazioni per i gruppi di campi di schema in base agli obiettivi
   - Maggiore efficienza del flusso di lavoro grazie alla selezione e alla funzionalità di anteprima di più gruppi di campi
   - Fornire trasparenza sugli attributi chiave della composizione dello schema, compresi identità, relazione e campi obbligatori ed obsoleti
- Trasparenza di attributi chiave e linee di dati schema dell’unione

#### Acquisizione e raccolta dei dati

La mappatura automatica, l’anteprima della mappatura e l’aggiornamento dell’usabilità consentono di importare dati da qualsiasi piattaforma o sorgente da utilizzare in profili, segmentazione downstream e attivazione. Il sistema ha l&#39;efficienza e l&#39;intelligenza necessarie per semplificare l&#39;utilizzo di questo processo, anche per le persone al di fuori dell&#39;IT.

- Accesso più semplice alle origini dati con scheda della pagina di catalogo e aggiornamento del modello di azione in linea della tabella dati
- Campo/espressione calcolata per l’acquisizione dei dati
- Le raccomandazioni di mappatura dei dati velocizzano il processo di acquisizione
- Anteprima mappatura e convalide

#### Configurazione del profilo

Un visualizzatore di profili intuitivo per gli addetti al marketing con funzioni di personalizzazione ti aiuta a comprendere la composizione di un profilo da utilizzare nei casi di segmentazione, pianificazione e attivazione. Il flusso di lavoro consolidato idrata il profilo in modo controllato ed efficiente fornendo un flusso di lavoro graduale per i criteri di unione.

- Visualizza ogni singolo profilo in un visualizzatore di profili avanzato che visualizza una dashboard con personalizzazione completa, abilitando dati raggruppati tra canali in base agli obiettivi aziendali dell’addetto al marketing.
- Modifica gli attributi standard e personalizzati nel widget Informazioni di base, in base alle esigenze aziendali.
- Personalizzare i widget con gli attributi del profilo cliente in tempo reale utilizzando il selettore dello schema di unione. Lo schema di unione viene derivato dai modelli di dati sottostanti utilizzati nell’inserimento dei dati di profilo.


#### Monitoraggio

Garantisce la trasparenza del flusso di dati e fornisce informazioni sullo stato del traffico di dati nel sistema dai connettori di origine, fornendo maggiore self-service e più rapida actionability per le situazioni di risoluzione dei problemi.

- Monitora tutte le esecuzioni del flusso e visualizza una visualizzazione dettagliata di ciascuna esecuzione, tra cui lo stato di completamento, la durata dell&#39;esecuzione, l&#39;elenco dei file elaborati, gli errori e la diagnostica actionable
