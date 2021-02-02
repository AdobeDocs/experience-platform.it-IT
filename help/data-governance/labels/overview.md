---
keywords: ' Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dei dati api;API del servizio criteri;descrizione delle etichette di utilizzo dei dati'
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic: labels
description: Adobe Experience Platform Data Governance consente di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle etichette di utilizzo dei dati nel  Experience Platform.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Panoramica delle etichette di utilizzo dei dati

Adobe Experience Platform [!DNL Data Governance] consente di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati in [!DNL Experience Platform]. Prima di leggere questa guida, consultare la [Panoramica sulla governance dei dati](../home.md) per un&#39;introduzione più robusta al framework di governance dei dati.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono trasferiti in [!DNL Experience Platform] o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform].

Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione.

[!DNL Platform] fornisce diverse etichette di utilizzo dei dati di base pronte all&#39;uso, che coprono un&#39;ampia gamma di limitazioni comuni applicabili alla governance dei dati. Per ulteriori informazioni su queste etichette e sui criteri di utilizzo che rappresentano, vedere la guida sulle [etichette di utilizzo dei dati di base](reference.md).

Oltre alle etichette fornite da  Adobe, potete anche definire etichette personalizzate per l&#39;organizzazione. Per ulteriori informazioni, vedere la sezione relativa alla [gestione delle etichette](#manage-labels).

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ereditano le etichette di utilizzo dei set di dati corrispondenti. Questo consente  Experience Platform di fornire l&#39;applicazione automatica dei criteri di utilizzo dei dati quando si attivano i segmenti alle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. Pertanto, è possibile identificare più facilmente gli attributi da escludere dai segmenti e impedire loro di ereditare etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell&#39;applicazione automatica in Piattaforma, vedere la panoramica sull&#39; [applicazione automatica dei criteri](../enforcement/auto-enforcement.md).

### Ereditarietà dai controlli di esportazione dei dati di Adobe Audience Manager

[!DNL Experience Platform] è in grado di condividere segmenti con Adobe Audience Manager. Tutti i controlli di esportazione dei dati applicati  segmenti di Audience Manager vengono convertiti in etichette equivalenti e azioni di marketing riconosciute da [!DNL Experience Platform] [!DNL Data Governance].

Per un riferimento alla mappatura di controlli specifici sull&#39;esportazione dei dati sulle etichette di utilizzo dei dati in [!DNL Platform], fare riferimento alla [documentazione  Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gestione delle etichette di utilizzo dei dati in [!DNL Experience Platform] {#manage-labels}

Potete gestire le etichette di utilizzo dei dati utilizzando le [!DNL Experience Platform] API o l&#39;interfaccia utente. Per informazioni dettagliate su ciascuna sezione, fare riferimento alle sottosezioni riportate di seguito.

### Utilizzo dell’interfaccia

L&#39;area di lavoro **[!UICONTROL Policies]** nell&#39;interfaccia utente di [!DNL Experience Platform] consente di visualizzare e gestire le etichette di base e personalizzate per l&#39;organizzazione. L&#39;area di lavoro **[!DNL Datasets]** consente di applicare etichette a set di dati e campi. Per ulteriori informazioni, consultare la [guida utente delle etichette](user-guide.md).

### Utilizzo delle API

L&#39;endpoint `/labels` in [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) consente di gestire a livello di programmazione le etichette di utilizzo dei dati, inclusa la creazione di etichette personalizzate. Per ulteriori informazioni, fare riferimento alla [guida dell&#39;endpoint delle etichette](../api/labels.md).

L&#39; [API del servizio DataSet](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) viene utilizzata per gestire le etichette per i set di dati e i campi. Per ulteriori informazioni, vedere la guida sulla [gestione delle etichette dei set di dati](./dataset-api.md).

## Passaggi successivi

Questo documento ha fornito un&#39;introduzione alle etichette di utilizzo dei dati e al loro ruolo all&#39;interno del framework di governance dei dati. Per ulteriori informazioni sulla gestione delle etichette in [!DNL Experience Platform], consultare la documentazione collegata a questa guida.