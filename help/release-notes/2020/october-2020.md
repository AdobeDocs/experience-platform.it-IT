---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform ottobre, 2020'
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 9%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: Ottobre 2020**

- [Preparazione dei dati](#data-prep)
- [Origini](#sources)

## Preparazione dei dati {#data-prep}

Data Prep consente agli ingegneri di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzione  di `is_set` | La `is_set` funzione consente di verificare la presenza di un attributo all&#39;interno dei dati di origine. `is_set` può essere utilizzato in combinazione con `is_empty` per verificare sia la presenza dell&#39;attributo che la presenza del valore all&#39;interno dell&#39;attributo. |
| Funzione  di `get_values` | La `get_values` funzione permette di ottenere i valori dalla mappa di input per ogni chiave. |

Per ulteriori informazioni, consulta la panoramica [Prep](../../data-prep/home.md)dati.

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