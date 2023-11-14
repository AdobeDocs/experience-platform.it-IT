---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;servizio criteri api;panoramica etichette di utilizzo dati
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
description: Scopri come le etichette di utilizzo dei dati vengono utilizzate per contribuire a rafforzare la conformità alla governance dei dati in Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 15%

---

# Panoramica delle etichette di utilizzo dei dati {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Controllare l’accesso ai dati sensibili e protetti"
>abstract="<h2>Descrizione</h2><p>Controllare l’accesso ad attributi di dati e/o segmenti specifici consente di progettare flussi di lavoro flessibili per i vari utenti tipo e team coinvolti nei casi d’uso di Experience Platform.</p>"

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

[!DNL Experience Platform] ha la possibilità di condividere segmenti con Adobe Audience Manager. Tutti i Controlli sull’esportazione dei dati applicati ai segmenti Audienci Manager vengono tradotti in etichette equivalenti e le azioni di marketing riconosciute da [!DNL Experience Platform] Governance dei dati.

Per informazioni sulla mappatura di specifici controlli sull’esportazione dei dati alle etichette di utilizzo dei dati in [!DNL Platform], fare riferimento al [Documentazione di Audienci Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gestione delle etichette di utilizzo dei dati in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Istruzioni"
>abstract="<ul><li>Etichetta i segmenti e i campi XDM per classificare i campi e i segmenti a cui desideri limitare l’accesso.</li><li>Etichetta i ruoli: l’aggiunta di etichette a un ruolo consente di definire le etichette relative alle limitazioni a cui devono essere soggetti gli utenti a cui è stato assegnato questo ruolo.</li><li>Crea i criteri: un criterio crea una relazione tra le etichette applicate agli oggetti etichettati, come segmenti e campi XDM, e le etichette applicate ai ruoli. Se le etichette corrispondono, è possibile definire se l’accesso è autorizzato o meno.</li></ul>"

Puoi gestire le etichette di utilizzo dei dati utilizzando [!DNL Experience Platform] API o interfaccia utente. Per informazioni dettagliate su ciascuno di essi, consulta le sottosezioni seguenti.

### Utilizzo dell’interfaccia utente

Il **[!UICONTROL Criteri]** area di lavoro in [!DNL Experience Platform] L’interfaccia utente ti consente di visualizzare e gestire le etichette core e personalizzate per la tua organizzazione. È possibile utilizzare **[!UICONTROL Schemi]** area di lavoro a [applicare etichette agli schemi Experience Data Model (XDM)](../../xdm/tutorials/labels.md)o imparare a [creare e gestire etichette personalizzate nel **[!UICONTROL Criteri] UI](./user-guide.md) consultando invece la guida utente delle etichette di utilizzo dei dati.

>[!IMPORTANT]
>
>Le etichette non possono più essere applicate ai campi a livello di set di dati. Questo flusso di lavoro è stato dichiarato obsoleto a favore dell’applicazione di etichette a livello di schema. Eventuali etichette applicate in precedenza a livello di oggetto del set di dati continueranno a essere supportate tramite l’interfaccia utente di Platform fino al 31 maggio 2024. Per garantire che le etichette siano coerenti in tutti gli schemi, tutte le etichette precedentemente associate ai campi a livello di set di dati devono essere migrate a livello di schema da te nel corso dell’anno successivo. Consulta la sezione su [migrazione di etichette applicate in precedenza](../e2e.md#migrate-labels) per istruzioni su come eseguire questa operazione.

### Utilizzo delle API

Il `/labels` endpoint nella [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) consente di gestire in modo programmatico le etichette di utilizzo dei dati, inclusa la creazione di etichette personalizzate. Consulta la sezione [guida dell’endpoint &quot;labels&quot;](../api/labels.md) per ulteriori informazioni.

Il [API servizio set di dati](https://www.adobe.io/experience-platform-apis/references/dataset-service/) viene utilizzato per gestire le etichette per set di dati e campi. Consulta la guida su [gestione delle etichette dei set di dati](./dataset-api.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce un’introduzione alle etichette di utilizzo dei dati e al loro ruolo all’interno del framework di governance dei dati. Per ulteriori informazioni su come gestire le etichette in, consulta la documentazione accessibile dai collegamenti presenti in questa guida. [!DNL Experience Platform].
