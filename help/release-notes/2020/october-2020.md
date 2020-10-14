---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform ottobre, 2020'
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: bf4271cec6126de3b5d9f98df280afdcc798589d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: Ottobre 2020**

- [Preparazione dei dati](#data-prep)
- [Profilo cliente in tempo reale](#profile)
- [Origini](#sources)

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