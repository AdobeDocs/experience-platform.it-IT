---
title: Note sulla versione di Adobe Experience Platform di settembre 2019
description: Note sulla versione di settembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
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

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Adobe Experience Platform [!DNL Data Ingestion] fornisce diverse alternative per l’acquisizione dei dati, tra cui API Batch, API Streaming, connettori Adobi nativi, partner di integrazione dei dati o interfaccia utente di Adobe Experience Platform.

**Nuove funzioni**

| Funzione | Descrizione |
| ----------- | ---------- |
| Nuovo dominio per acquisizione in streaming | Il `dcs.data.adobe.net` è stato spostato nel nuovo dominio di raccolta dati comune `dcs.adobedc.net`. Gli utenti devono aggiornare le proprie implementazioni in base alla versione rivista della documentazione di acquisizione in streaming di Adobe Experience Platform. Tutta la documentazione relativa all’acquisizione in streaming di Adobe Experience Platform è stata aggiornata per l’utilizzo del nuovo dominio. |

Per ulteriori informazioni, visitare il [Documentazione sull’acquisizione dei dati](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] è un servizio completamente gestito all’interno di [!DNL Experience Platform] che consente ai data scientist di generare senza interruzioni informazioni da dati e contenuti tra soluzioni Adobe e sistemi di terze parti tramite la creazione e l’operazionalizzazione di modelli di apprendimento automatico. [!DNL Data Science Workspace] è strettamente integrato con [!DNL Platform] e potenzia il ciclo di vita della data science end-to-end, inclusa l&#39;esplorazione e la preparazione dei dati XDM, seguita dallo sviluppo e dall&#39;operazionalizzazione di modelli per l&#39;arricchimento automatico [!DNL Real-Time Customer Profile] con Approfondimenti apprendimento automatico.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Pianificazione dei servizi tramite l’interfaccia utente | Integrato con [!DNL Platform] Servizio di orchestrazione per automatizzare l’apprendimento e il punteggio dei modelli con pianificazioni definite dall’utente tramite l’interfaccia utente. |
| [!DNL Service Gallery] | Sfoglia, monitora e accedi ai servizi di apprendimento automatico con la possibilità di pianificare processi di formazione automatizzati e di valutazione, il tutto all’interno del [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Miglioramenti all’interfaccia utente. |

**Problemi noti**

* Al momento non è disponibile alcuna modalità accessibile in [!DNL Service Gallery] per eliminare un servizio esistente. Nel frattempo, si prega di fare riferimento al [Riferimento API di apprendimento automatico di Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) per eliminare un servizio esistente tramite chiamate API.
* Il [!DNL Service Gallery] non dispone del supporto per l’impaginazione per filtrare le esecuzioni di apprendimento e punteggio di un servizio.
* Durante la configurazione dell’apprendimento o del punteggio pianificato viene eseguito [!DNL Service Gallery], l&#39;impostazione della frequenza su oraria impedisce l&#39;applicazione della pianificazione.

Per ulteriori informazioni, visitare il [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] consente di utilizzare istruzioni SQL standard per eseguire query sui dati in Adobe Experience Platform per supportare diversi casi di utilizzo di analisi e gestione dei dati. Si tratta di uno strumento serverless che consente di unire set di dati da [!DNL Data Lake] e acquisiscono i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, [!DNL Data Science Workspace], o per l’acquisizione in [!DNL Real-Time Customer Profile].

È possibile utilizzare [!DNL Query Service] creare ecosistemi di analisi dei dati, creando un quadro dei clienti attraverso i loro vari canali di interazione. Questi canali possono includere sistemi POS, web, mobili o sistemi CRM.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti a [!DNL Query Editor] | È stata aggiunta una funzione di salvataggio che consente di salvare una query e lavorarci in un secondo momento. È stata aggiunta una scheda &quot;Sfoglia&quot; al [!DNL Query Service] interfaccia utente di Adobe Experience Platform che mostra le query salvate dagli utenti dell’organizzazione. È stato implementato un pannello &quot;Dettagli query&quot; che visualizza metadati utili sulla query visualizzata. |
| Nuove funzioni di attribuzione | Funzioni definite dall&#39;Adobe in [!DNL Query Service] per eseguire una query per l’attribuzione del canale con parametri di scadenza. |
| Miglioramenti alla sintassi SQL | Supporto per la sintassi iLike. |
| Generare set di dati con uno schema XDM definito | È stata aggiunta una nuova clausola nelle query Create Table as Select (CTAS) che consente di specificare uno schema di destinazione. |

Per ulteriori informazioni, consulta [Documentazione di Query Service](../../query-service/home.md).
