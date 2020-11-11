---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform ottobre, 2020'
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e2b0048703816dc481eb9486310d86a8f2483af2
workflow-type: tm+mt
source-wordcount: '1028'
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

Data Prep consente agli ingegneri di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione  di `is_set` | La `is_set` funzione consente di verificare la presenza di un attributo all&#39;interno dei dati di origine. `is_set` può essere utilizzato in combinazione con `is_empty` per verificare sia la presenza dell&#39;attributo che la presenza del valore all&#39;interno dell&#39;attributo. |
| Funzione  di `get_values` | La `get_values` funzione permette di ottenere i valori dalla mappa di input per ogni chiave. |

Per ulteriori informazioni, consulta la panoramica [Prep](../../data-prep/home.md)dati.

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi online, offline, CRM e dati di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiunte API di anteprima profilo | L&#39;API di anteprima profilo (`/previewsamplestatus`) ora include la possibilità di visualizzare una suddivisione dei frammenti di profilo totali nell&#39;organizzazione IMS, nonché di visualizzare la distribuzione dei frammenti di profilo negli spazi dei nomi delle identità. |
| Aggiornamenti della visualizzazione dello schema dell&#39;unione | Nell&#39;interfaccia utente del Experience Platform di , gli utenti possono trovare più facilmente informazioni su tutti gli schemi e i set di dati che contribuiscono allo schema unione, nonché attributi di chiave di superficie quali i campi di identità e relazione. Questi aggiornamenti migliorano la capacità di risolvere eventuali problemi e convalidare la corretta configurazione dei profili, la corretta unione delle identità e l’acquisizione dei dati. |

Per ulteriori informazioni [!DNL Real-time Customer Profile], comprese esercitazioni e best practice per l’utilizzo dei [!DNL Profile] dati, consulta la panoramica [Profilo cliente](../../profile/home.md)in tempo reale.

## Servizio di segmentazione {#segmentation}

Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione  Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Rimozione del limite di segmentazione in streaming | Il limite di sette giorni per il periodo di lookback è stato rimosso. |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la panoramica sulla [segmentazione](../../segmentation/home.md)

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappatura gerarchica | Durante il processo di assimilazione dei dati è possibile visualizzare l&#39;anteprima di un file di origine gerarchico, ad esempio JSON o Parquet. |
| Supporto dell&#39;autenticazione SSH per SFTP | Puoi collegare il tuo account SFTP a [!DNL Platform] utilizzando le chiavi SSH RSA/DSA Open. Per ulteriori informazioni, consulta la panoramica [](../../sources/connectors/cloud-storage/ftp-sftp.md) SFTP. |
| Miglioramenti UX | È possibile abilitare il set di dati per [!DNL Profile] durante il processo di assimilazione dei dati. Per ulteriori informazioni, consulta l’esercitazione sul flusso di lavoro [del flusso di lavoro per l’archiviazione](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) cloud. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).

## Time to Value {#time-to-value}

Adobe Experience Platform consente ai team delle operazioni di marketing di creare una visualizzazione a 360 gradi dei propri clienti senza richiedere un&#39;ampia esperienza di progettazione dei dati. L&#39;obiettivo è quello di accelerare i team e valutare la velocità dei dati.

&quot;Time to Value&quot; taglia tra le persone. Gli ingegneri dei dati possono completare le attività in modo efficiente e accelerato grazie alla trasparenza dell&#39;attività dei dati, in modo da rendere disponibile prima un profilo cliente in tempo reale affidabile e scalabile. Gli addetti al marketing possono quindi utilizzare un profilo cliente completo e affidabile per la segmentazione e l&#39;attivazione.

### Funzioni principali

#### Schema

Consente di aggiornare usabilità e flusso di lavoro e fornisce approfondimenti pratici, standardizzazione e trasparenza dei campi chiave all&#39;interno delle composizioni di schema. Espone la linea di dati per la combinazione di singoli modelli di dati rappresentati come &quot;schema unione&quot;, fornendo informazioni sulla struttura e gli ingredienti del profilo cliente in tempo reale.

- Aggiornamento del flusso di lavoro dello schema
   - Utilizzate i collegamenti per il tipo più comune di schemi XDM, con le impostazioni automatizzate nell&#39;editor di schemi e le raccomandazioni di mixin base agli obiettivi prefissati
   - Maggiore efficienza del flusso di lavoro grazie alla selezione e alla funzionalità di anteprima dei mixer
   - Trasparenza sugli attributi chiave della composizione dello schema, inclusi identità, relazione e campi obbligatori e obsoleti
- Trasparenza di proprietà e attributi chiave dello schema unione

#### Ingestione e raccolta dati

La mappatura automatica, l&#39;anteprima della mappatura e l&#39;aggiornamento dell&#39;usabilità consentono di inserire dati da qualsiasi piattaforma o origine da utilizzare in profili, segmentazione a valle e attivazione. Il sistema ha l&#39;efficienza e l&#39;intelligenza necessarie per semplificare l&#39;utilizzo di questo processo, anche per le persone esterne all&#39;IT.

- Accesso più semplice alle origini dati con scheda della pagina del catalogo e modello di azione in linea della tabella dati
- Campo/espressione calcolata per l&#39;assimilazione dei dati
- Le raccomandazioni di mappatura dei dati velocizzano il processo di assimilazione
- Anteprima e convalide mappatura

#### Configurazione profilo

Il visualizzatore di profili intuitivo per gli esperti di marketing con la personalizzazione consente di comprendere la composizione di un profilo da usare nei casi di segmentazione, pianificazione e attivazione. Il flusso di lavoro consolidato idrata il profilo in modo controllato ed efficiente fornendo un flusso di lavoro graduale per i criteri di unione.

- Visualizzate ogni singolo profilo in un visualizzatore di profili avanzato che visualizza una dashboard con personalizzazione completa, consentendo la condivisione di dati multicanale raggruppati in base agli obiettivi aziendali degli esperti di marketing.
- Modificate gli attributi standard e personalizzati nel widget Informazioni di base, in base alle esigenze aziendali.
- Potete personalizzare i widget con gli attributi del profilo cliente in tempo reale utilizzando il selettore dello schema unione. Lo schema unione è derivato dai modelli di dati sottostanti utilizzati nell&#39;assimilazione dei dati del profilo.


#### Monitoraggio

Garantisce la trasparenza del flusso di dati e fornisce informazioni sullo stato del traffico dei dati nel sistema dai connettori di origine, fornendo maggiore self-service e maggiore facilità di utilizzo per la risoluzione di problemi.

- Monitorate tutte le esecuzioni del flusso e visualizzate una visualizzazione dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell&#39;esecuzione, l&#39;elenco dei file elaborati, gli errori e la diagnostica utilizzabile