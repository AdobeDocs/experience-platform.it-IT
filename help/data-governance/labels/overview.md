---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;servizio criteri api;panoramica etichette di utilizzo dati
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
description: Scopri come le etichette di utilizzo dei dati vengono utilizzate per contribuire a rafforzare la conformità alla governance dei dati in Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Panoramica delle etichette di utilizzo dei dati {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Descrizione"
>abstract=""

Adobe Experience Platform consente di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendoli in categorie in base ai [criteri di governance dei dati](../policies/overview.md) e [criteri di controllo dell’accesso](../../access-control/abac/ui/policies.md).

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati in [!DNL Experience Platform].

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati ti consentono di categorizzare set di dati e campi in base ai criteri di governance applicabili a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform].

Le etichette di utilizzo dei dati applicate a livello di set di dati vengono propagate a tutti i campi del set di dati. Le etichette possono anche essere applicate direttamente ai singoli campi (intestazioni di colonna) in un set di dati, senza propagazione.

[!DNL Platform] fornisce diverse etichette di utilizzo dei dati &quot;core&quot; pronte all’uso, che coprono un’ampia varietà di restrizioni comuni applicabili alla governance dei dati. Per ulteriori informazioni su queste etichette e sui criteri di governance che rappresentano, consulta la guida su [etichette di utilizzo dei dati core](reference.md).

Oltre alle etichette fornite dall’Adobe, puoi anche definire etichette personalizzate per la tua organizzazione. Consulta la sezione su [gestione delle etichette](#manage-labels) per ulteriori informazioni.

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md) eredita le etichette di utilizzo dei set di dati corrispondenti. Questo consente agli Experienci Platform di fornire l’applicazione automatica delle policy durante l’attivazione dei segmenti nelle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. Pertanto, puoi identificare più facilmente quali attributi devono essere esclusi dai segmenti e impedire loro di ereditare le etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in Platform, consulta la panoramica su [applicazione automatica delle policy](../enforcement/auto-enforcement.md).

### Ereditarietà da controlli esportazione dati Adobe Audience Manager

[!DNL Experience Platform] ha la possibilità di condividere segmenti con Adobe Audience Manager. Tutti i Controlli sull’esportazione dei dati applicati ai segmenti Audience Manager vengono tradotti in etichette equivalenti e le azioni di marketing riconosciute da [!DNL Experience Platform] Governance dei dati.

Per informazioni sulla mappatura di specifici controlli sull’esportazione dei dati alle etichette di utilizzo dei dati in [!DNL Platform], fare riferimento al [Documentazione di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gestione delle etichette di utilizzo dei dati in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Istruzioni"
>abstract=""

Puoi gestire le etichette di utilizzo dei dati utilizzando [!DNL Experience Platform] API o interfaccia utente. Per informazioni dettagliate su ciascuno di essi, consulta le sottosezioni seguenti.

### Utilizzo dell’interfaccia utente

Il **[!UICONTROL Criteri]** area di lavoro in [!DNL Experience Platform] L’interfaccia utente ti consente di visualizzare e gestire le etichette core e personalizzate per la tua organizzazione. È possibile utilizzare **[!UICONTROL Schemi]** area di lavoro a [applicare etichette agli schemi Experience Data Model (XDM)](../../xdm/tutorials/labels.md), oppure puoi utilizzare il **[!DNL Datasets]** area di lavoro a [applicare etichette ai set di dati](./user-guide.md) invece.

>[!NOTE]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se tenti di creare criteri di accesso per i dati, devi applicare etichette allo schema su cui si basa il set di dati. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

### Utilizzo delle API

Il `/labels` endpoint nella [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) consente di gestire in modo programmatico le etichette di utilizzo dei dati, inclusa la creazione di etichette personalizzate. Consulta la sezione [guida dell’endpoint &quot;labels&quot;](../api/labels.md) per ulteriori informazioni.

Il [API servizio set di dati](https://www.adobe.io/experience-platform-apis/references/dataset-service/) viene utilizzato per gestire le etichette per set di dati e campi. Consulta la guida su [gestione delle etichette dei set di dati](./dataset-api.md) per ulteriori informazioni.

>[!NOTE]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se si desidera creare criteri di accesso per i dati, è necessario [applica etichette allo schema](../../xdm/tutorials/labels.md) su cui si basa il set di dati. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce un’introduzione alle etichette di utilizzo dei dati e al loro ruolo all’interno del framework di governance dei dati. Per ulteriori informazioni su come gestire le etichette in, consulta la documentazione accessibile dai collegamenti presenti in questa guida. [!DNL Experience Platform].
