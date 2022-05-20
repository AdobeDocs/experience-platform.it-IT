---
title: Note sulla versione di Adobe Experience Platform - Settembre 2019
description: Le note sulla versione di settembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 10 settembre 2019**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Adobe Experience Platform [!DNL Data Ingestion] fornisce diverse alternative per l’acquisizione dei dati, tra cui API Batch, API Streaming, connettori di Adobe nativi, partner di integrazione dei dati o l’interfaccia utente Adobe Experience Platform.

**Nuove funzioni**

| Funzione | Descrizione |
| ----------- | ---------- |
| Nuovo dominio per l’acquisizione in streaming | La `dcs.data.adobe.net` il dominio è stato spostato nel nuovo dominio di raccolta dati comune `dcs.adobedc.net`. Gli utenti devono aggiornare le proprie implementazioni in base alla documentazione rivista relativa all’acquisizione in streaming di Adobe Experience Platform. Tutta la documentazione relativa all’acquisizione in streaming di Adobe Experience Platform è stata aggiornata per utilizzare il nuovo dominio. |

Per ulteriori informazioni, visita il [Documentazione sull’acquisizione dei dati](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] è un servizio completamente gestito in [!DNL Experience Platform] che consente agli scienziati dei dati di generare facilmente informazioni dai dati e dai contenuti tra soluzioni Adobe e sistemi di terze parti creando e operando modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita completo della scienza dei dati, inclusa l&#39;esplorazione e la preparazione dei dati XDM, seguiti dallo sviluppo e dall&#39;operazionalizzazione dei modelli per arricchire automaticamente [!DNL Real-time Customer Profile] con informazioni sull&#39;apprendimento automatico.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Pianificazione dei servizi tramite l’interfaccia utente | Integrato con [!DNL Platform] Servizio di orchestrazione per automatizzare l&#39;addestramento e il punteggio del modello con pianificazioni definite dall&#39;utente tramite l&#39;interfaccia utente. |
| [!DNL Service Gallery] | Sfogliare, monitorare e accedere ai servizi di apprendimento automatico con la possibilità di pianificare processi di formazione e valutazione automatizzati, il tutto all&#39;interno della riprogettazione [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Miglioramenti all’interfaccia utente. |

**Problemi noti**

* Attualmente non esiste un modo accessibile nel [!DNL Service Gallery] per eliminare un servizio esistente. Nel frattempo, si prega di fare riferimento al [Riferimento API di apprendimento automatico per Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) per eliminare un servizio esistente tramite chiamate API.
* La [!DNL Service Gallery] non dispone del supporto per l’impaginazione per filtrare le esecuzioni di formazione e valutazione di un servizio.
* Durante la configurazione di corsi di formazione o di valutazione pianificati viene eseguito il [!DNL Service Gallery], l’impostazione della frequenza su ogni ora impedisce l’applicazione della pianificazione.

Per ulteriori informazioni, visita il [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform per supportare diversi casi di utilizzo di analisi e gestione dei dati. È uno strumento senza server che ti consente di unire i set di dati dalla [!DNL Data Lake] e acquisisce i risultati della query come nuovo set di dati da utilizzare nel reporting, [!DNL Data Science Workspace]o per l&#39;acquisizione in [!DNL Real-time Customer Profile].

È possibile utilizzare [!DNL Query Service] creare ecosistemi di analisi dei dati, creando un&#39;immagine dei clienti attraverso i loro diversi canali di interazione. Questi canali possono includere sistemi di punti vendita, web, dispositivi mobili o sistemi CRM.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti apportati a [!DNL Query Editor] | È stata aggiunta una funzione di salvataggio che consente di salvare una query e lavorarci in un secondo momento. È stata aggiunta una scheda &quot;Sfoglia&quot; al [!DNL Query Service] interfaccia utente su Adobe Experience Platform che mostra le query salvate dagli utenti dell’organizzazione. Implementato un pannello &quot;Dettagli query&quot; che visualizza metadati utili sulla query visualizzata. |
| Nuove funzioni di attribuzione | Funzioni definite dall&#39;Adobe in [!DNL Query Service] per eseguire una query per l’attribuzione del canale con parametri di scadenza. |
| Miglioramenti alla sintassi SQL | Supporto della sintassi iLike. |
| Generare set di dati con uno schema XDM definito | È stata aggiunta una nuova clausola nelle query Create Table as Select (CTAS) che consente di specificare uno schema di destinazione. |

Per ulteriori informazioni, consulta la [Documentazione del servizio query](../../query-service/home.md).
