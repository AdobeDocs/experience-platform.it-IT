---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 10 settembre 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 10 settembre 2019**

Aggiornamenti alle funzionalità esistenti in Adobe Experience Platform:

* [Ingestione dati](#ingestion)
* [Area di lavoro Data Science](#dsw)
* [Servizio query](#query)

## Ingestione dati {#ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. L’inserimento dei dati in Adobe Experience Platform offre diverse alternative per l’assimilazione dei dati, tra cui API per batch, API per lo streaming, connettori Adobe nativi, partner per l’integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

**Nuove funzionalità**

| Funzione | Descrizione |
| ----------- | ---------- |
| Nuovo dominio per l’assimilazione in streaming | Il `dcs.data.adobe.net` dominio è stato spostato nel nuovo dominio comune di raccolta dati `dcs.adobedc.net`. Gli utenti devono aggiornare le implementazioni in base alla documentazione aggiornata sull’assimilazione dei flussi della piattaforma Adobe Experience Platform. Tutta la documentazione relativa all’assimilazione dei flussi in Adobe Experience Platform è stata aggiornata per utilizzare il nuovo dominio. |

Per ulteriori informazioni, consulta la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

## Area di lavoro Data Science {#dsw}

Adobe Experience Platform Data Science Workspace è un servizio completamente gestito all&#39;interno della piattaforma Experience che consente agli esperti di dati di generare in modo semplice informazioni dai dati e dai contenuti tra le soluzioni Adobe e i sistemi di terze parti, creando e operando modelli di apprendimento automatico. Data Science Workspace è strettamente integrato con la Piattaforma e migliora il ciclo di vita completo della scienza dei dati, compresa l&#39;esplorazione e la preparazione di dati XDM, seguita dallo sviluppo e dall&#39;operazionalizzazione di modelli per arricchire automaticamente il profilo cliente in tempo reale con informazioni sull&#39;apprendimento automatico.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Pianificazione dei servizi tramite l&#39;interfaccia utente | Integrato con Platform Orchestration Service per automatizzare la formazione e il punteggio dei modelli con pianificazioni definite dall&#39;utente tramite l&#39;interfaccia utente. |
| Raccolta servizi | Sfogliate, monitorate e accedete ai servizi di machine learning con la possibilità di pianificare processi di formazione e valutazione automatizzati, il tutto all&#39;interno della nuova Galleria dei servizi. |
| JupyterLab 5.0.0 | Miglioramenti all’interfaccia utente di JupyterLab. |

**Problemi noti**

* Nella Raccolta servizi non è attualmente disponibile alcun modo accessibile per eliminare un servizio esistente. Nel frattempo, fare riferimento al riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning per eliminare un servizio esistente tramite chiamate API.
* La Galleria servizi non supporta l&#39;impaginazione per filtrare le esecuzioni di formazione e punteggio di un Servizio.
* Durante la configurazione della formazione programmata o del punteggio, l&#39;impostazione della frequenza su ogni ora impedisce l&#39;applicazione della pianificazione tramite la Galleria servizi.

Per ulteriori informazioni, consulta [Panoramica](../../data-science-workspace/home.md)di Data Science Workspace.

## Servizio query {#query}

Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform per supportare diversi casi di utilizzo di analisi e gestione dei dati. Si tratta di uno strumento senza server che consente di unire set di dati dal Data Lake e acquisire i risultati della query come nuovo set di dati da utilizzare nei report, in Data Science Workspace o per l&#39;inserimento in Real-time Customer Profile.

È possibile utilizzare il servizio Query per creare ecosistemi di analisi dei dati, creando un&#39;immagine dei clienti attraverso i loro diversi canali di interazione. Questi canali possono includere sistemi di punti vendita, web, mobili o CRM.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Miglioramenti all&#39;Editor query | È stata aggiunta una funzione di salvataggio che consente di salvare una query e lavorare su di essa in un secondo momento. È stata aggiunta una scheda &quot;Browse&quot; (Sfoglia) all&#39;interfaccia utente del servizio di query in Adobe Experience Platform che mostra le query salvate dagli utenti nell&#39;organizzazione. È stato implementato un pannello &quot;Dettagli query&quot; che visualizza utili metadati sulla query visualizzata. |
| Nuove funzioni di attribuzione | Funzioni definite da Adobe in Query Service per eseguire query per l&#39;attribuzione dei canali con parametri di scadenza. |
| Miglioramenti alla sintassi SQL | Supporto per la sintassi iLike. |
| Generazione di set di dati con uno schema XDM definito | Aggiunta una nuova clausola nelle query Create Table as Select (CTAS) (Crea tabella come Seleziona) che consente di specificare uno schema di destinazione. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).