---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' Experience Platform note sulla versione 10 settembre 2019'
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 5%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 10 settembre 2019**

Aggiornamenti alle funzionalità esistenti in  Adobe Experience Platform:

* [!DNL Data Ingestion](#ingestion)
* [!DNL Data Science Workspace](#dsw)
* [!DNL Query Service](#query)

## [!DNL Data Ingestion] {#ingestion}

 Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati.  Adobe Experience Platform [!DNL Data Ingestion] offre diverse alternative per l’assimilazione dei dati, tra cui API Batch, API Streaming, connettori  Adobe nativi, partner per l’integrazione dei dati o l’interfaccia  Adobe Experience Platform.

**Nuove funzionalità**

| Funzione | Descrizione |
| ----------- | ---------- |
| Nuovo dominio per l’assimilazione in streaming | Il `dcs.data.adobe.net` dominio è stato spostato nel nuovo dominio comune di raccolta dati `dcs.adobedc.net`. Gli utenti devono aggiornare le implementazioni in base alla documentazione aggiornata sull’assimilazione dello streaming di Adobe Experience Platform . Tutta la documentazione relativa &#39;assimilazione dello streaming di Adobe Experience Platform è stata aggiornata per utilizzare il nuovo dominio. |

Per ulteriori informazioni, consulta la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

## [!DNL Data Science Workspace] {#dsw}

 Adobe Experience Platform [!DNL Data Science Workspace] è un servizio completamente gestito all&#39;interno [!DNL Experience Platform] che consente agli esperti di dati di generare informazioni dai dati e dai contenuti attraverso soluzioni  Adobe e sistemi di terze parti, creando e operando modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita end-to-end della scienza dei dati, compresa l&#39;esplorazione e la preparazione di dati XDM, seguito dallo sviluppo e dall&#39;operazionalizzazione di Modelli per arricchire automaticamente [!DNL Real-time Customer Profile] con approfondimenti di apprendimento automatico.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Pianificazione dei servizi tramite l&#39;interfaccia utente | Integrato con il servizio [!DNL Platform] Orchestration per automatizzare la formazione e il punteggio dei modelli con pianificazioni definite dall&#39;utente tramite l&#39;interfaccia utente. |
| [!DNL Service Gallery] | Sfogliate, monitorate e accedete ai servizi di machine learning con la possibilità di pianificare processi di formazione e valutazione automatizzati, il tutto all&#39;interno della nuova progettazione [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Miglioramenti all’interfaccia utente. |

**Problemi noti**

* Al momento non esiste alcun modo accessibile [!DNL Service Gallery] per eliminare un servizio esistente. Nel frattempo, fare riferimento al riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning per eliminare un servizio esistente tramite chiamate API.
* Il servizio [!DNL Service Gallery] non supporta l&#39;impaginazione per filtrare le esecuzioni di formazione e punteggio di un Servizio.
* Quando si configura la formazione programmata o si esegue il punteggio, l’impostazione della frequenza su ogni ora impedisce l’applicazione della pianificazione. [!DNL Service Gallery]

Per ulteriori informazioni, consulta [Panoramica](../../data-science-workspace/home.md)di Data Science Workspace.

## [!DNL Query Service] {#query}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in  Adobe Experience Platform per supportare una serie di casi d&#39;uso di analisi e gestione dei dati. It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. Questi canali possono includere sistemi di punti vendita, web, mobili o CRM.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti a [!DNL Query Editor] | È stata aggiunta una funzione di salvataggio che consente di salvare una query e lavorare su di essa in un secondo momento. È stata aggiunta una scheda &quot;Browse&quot; (Sfoglia) all&#39;interfaccia [!DNL Query Service] utente  Adobe Experience Platform che mostra le query salvate dagli utenti nell&#39;organizzazione. È stato implementato un pannello &quot;Dettagli query&quot; che visualizza utili metadati sulla query visualizzata. |
| Nuove funzioni di attribuzione |  funzioni definite dal Adobe per eseguire una query [!DNL Query Service] per l&#39;attribuzione dei canali con parametri di scadenza. |
| Miglioramenti alla sintassi SQL | Supporto per la sintassi iLike. |
| Generazione di set di dati con uno schema XDM definito | Aggiunta una nuova clausola nelle query Create Table as Select (CTAS) (Crea tabella come Seleziona) che consente di specificare uno schema di destinazione. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).