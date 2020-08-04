---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic: labels
translation-type: tm+mt
source-git-commit: 5e65c843c3c612b657ebe915c53f14f0b8d7f541
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Panoramica delle etichette di utilizzo dei dati

 Adobe Experience Platform [!DNL Data Governance] consente di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati in [!DNL Experience Platform]. Prima di leggere questa guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più robusta al framework sulla governance dei dati.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono ingeriti [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform].

Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione.

[!DNL Platform] fornisce diverse etichette di utilizzo dei dati di base pronte all&#39;uso, che coprono un&#39;ampia gamma di limitazioni comuni applicabili alla governance dei dati. Per ulteriori informazioni su queste etichette e sui criteri di utilizzo che rappresentano, consultare la guida sulle etichette [di utilizzo dei dati di](reference.md)base.

Oltre alle etichette fornite da  Adobe, potete anche definire etichette personalizzate per l&#39;organizzazione. Per ulteriori informazioni, vedere la sezione sulla [gestione delle etichette](#manage-labels) .

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [servizio](../../segmentation/home.md) di segmentazione Adobe Experience Platform ereditano le etichette di utilizzo dei set di dati corrispondenti. Questo consente alle applicazioni integrate [!DNL Experience Platform] (come [!DNL Real-time Customer Data Platform]) di fornire l&#39;applicazione automatica dei criteri di utilizzo dei dati durante l&#39;attivazione dei segmenti nelle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. A seconda del modo in cui l’applicazione [!DNL Platform]basata sui segmenti utilizza i segmenti, è possibile specificare quali campi vengono utilizzati, impedendo al segmento di ereditare le etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in CDP in tempo reale, consulta la panoramica sulla governance dei [dati in CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)in tempo reale.

### Ereditarietà dai controlli di esportazione dei dati  Adobe Audience Manager

[!DNL Experience Platform] è in grado di condividere segmenti con  Adobe Audience Manager. Eventuali controlli di esportazione dei dati applicati  segmenti di Audience Manager vengono convertiti in etichette equivalenti e azioni di marketing riconosciute da [!DNL Experience Platform][!DNL Data Governance].

Per un riferimento alla modalità in cui specifici controlli di esportazione dei dati vengono mappati sulle etichette di utilizzo dei dati in [!DNL Platform], consultare la documentazione [](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Gestione delle etichette di utilizzo dei dati in [!DNL Experience Platform] {#manage-labels}

È possibile gestire le etichette di utilizzo dei dati utilizzando [!DNL Experience Platform] le API o l&#39;interfaccia utente. Per informazioni dettagliate su ciascuna sezione, fare riferimento alle sottosezioni riportate di seguito.

### Utilizzo dell’interfaccia

L’ **[!UICONTROL Policies]** area di lavoro nell’ [!DNL Experience Platform] interfaccia utente consente di visualizzare e gestire le etichette di base e personalizzate per l’organizzazione. L&#39; **[!DNL Datasets]** area di lavoro consente di applicare etichette a set di dati e campi. Per ulteriori informazioni, consultare la guida [utente relativa alle](user-guide.md)etichette.

### Utilizzo delle API

L&#39; `/labels` endpoint nell&#39;API [di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) Policy Service consente di gestire le etichette di utilizzo dei dati a livello di programmazione, compresa la creazione di etichette personalizzate. Per ulteriori informazioni, consultare la guida [all&#39;endpoint delle](../api/labels.md) etichette.

L&#39;API [del servizio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) DataSet viene utilizzata per gestire le etichette per i set di dati e i campi. Per ulteriori informazioni, vedere la guida sulla [gestione delle etichette](./dataset-api.md) dei set di dati.

## Passaggi successivi

Questo documento ha fornito un&#39;introduzione alle etichette di utilizzo dei dati e al loro ruolo all&#39;interno del framework di governance dei dati. Per ulteriori informazioni sulla gestione delle etichette in [!DNL Experience Platform], consulta la documentazione collegata a questa guida.