---
title: Pubblico Experience Cloud (Beta)
description: Scopri come condividere segmenti da Experience Platform a varie soluzioni di Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---

# (Beta) [!UICONTROL Tipi di pubblico di Experience Cloud] connessione

Questa destinazione consente di condividere segmenti da Experience Platform a varie soluzioni di Experience Cloud, come Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo.

![La destinazione Tipi di pubblico di Experience Cloud, evidenziata nel catalogo delle destinazioni.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Questa destinazione sostituisce la [integrazione legacy di condivisione dei segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) da Experience Platform a varie soluzioni di Experience Cloud.
>* Questa destinazione è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.


## Casi d’uso e vantaggi {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!UICONTROL Tipi di pubblico di Experience Cloud] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Abilitare i casi d’uso di Data Management Platform {#dmp-use-cases}

Ad Audience Manager, puoi utilizzare i segmenti Experience Platform per i casi di utilizzo di Data Management Platform, ad esempio:

* Aggiungi [dati di terze parti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) ai tuoi segmenti;
* [Modellazione algoritmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Attiva i segmenti in destinazioni basate su cookie non ancora supportate nel catalogo delle destinazioni Experience Platform.

### Controllo granulare dei segmenti esportati {#segments-control}

Utilizza la nuova integrazione self-service di condivisione dei segmenti tramite la destinazione Tipi di pubblico di Experience Cloud per selezionare i segmenti da esportare in Audience Manager e oltre. Questo consente di determinare quali segmenti desideri condividere con altre soluzioni Experience Cloud e quali segmenti desideri mantenere esclusivamente in Experience Platform.

L’integrazione legacy di condivisione dei segmenti non consentiva un controllo granulare dei segmenti da esportare in Audience Manager e versioni successive.

### Condividere segmenti di Experience Platform con altre soluzioni di Experience Cloud {#share-segments-with-other-solutions}

Oltre a condividere i segmenti con Audience Manager, la scheda di destinazione Tipi di pubblico di Experience Platform consente di condividere i segmenti con qualsiasi altra soluzione di Experience Cloud per la quale disponi del provisioning, tra cui:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
> * Questa destinazione è disponibile per [Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clienti.
> * È necessaria una licenza Audience Manager per abilitare [Casi d’uso di Data Management Platform](#dmp-use-cases) di cui sopra.
> * Tu *non è necessario* una licenza di Audience Manager per condividere segmenti di Experience Platform con Adobe Advertising Cloud, Adobe Target, Marketo e altre soluzioni di Experience Cloud, menzionata in [sezione precedente](#share-segments-with-other-solutions).


### Per i clienti che utilizzano la soluzione legacy di condivisione dei segmenti

Se condividi già segmenti da Experience Platform a Audience Manager e altre soluzioni di Experience Cloud tramite [integrazione legacy di condivisione dei segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), per disabilitare l’integrazione legacy, contatta l’Assistenza clienti o il team dell’account Adobe. Per disabilitare l’integrazione, i team dell’Assistenza clienti e dell’account Adobe devono inviare un ticket Jira (vedi il ticket modello AAM-52354).

Il tempo di risposta per risolvere il ticket di deprovisioning per i clienti beta è inferiore o pari a sei giorni lavorativi. Dopo aver disabilitato l’integrazione legacy esistente, puoi procedere con [creazione di una connessione](#connect) tramite la scheda di destinazione self-service.

>[!IMPORTANT]
>
>L’esportazione del segmento da Experience Platform alle altre soluzioni verrà interrotta nel periodo di tempo che intercorre tra la risoluzione del ticket Jira e il momento in cui viene stabilita una nuova connessione tramite la scheda di destinazione. Puoi ridurre al minimo questo downtime creando la connessione tramite la scheda di destinazione non appena il ticket Jira viene chiuso.

## Limitazioni note e callout {#known-limitations}

Osserva le seguenti limitazioni note e callout importanti nella versione beta della scheda Tipi di pubblico di Experience Cloud:

* [Controllo dei flussi di dati](/help/dataflows/ui/monitor-destinations.md) non è supportato.
* Quando ti connetti alla destinazione, puoi vedere un’opzione per [abilitare gli avvisi del flusso di dati](#enable-alerts). Anche se visibile nell’interfaccia utente, il **l’opzione abilita avvisi non è supportata** nella versione beta.
* **Backfill non supportati**. La prima esportazione nell’Audience Manager o in altre soluzioni di Experience Cloud non include una popolazione storica dei segmenti.
* Nella versione beta, puoi creare **una singola connessione di destinazione alla destinazione Experience Cloud Audiences**, in tutte le sandbox appartenenti alla tua organizzazione Experience Platform.
* È presente un **latenza di quattro ore** tra il momento in cui i dati vengono attivati in Experience Platform e il momento in cui i dati sono pronti per essere utilizzati in Audience Manager e in altre soluzioni Experience Cloud.

## Identità supportate {#supported-identities}

I profili esportati in [!UICONTROL Tipi di pubblico di Experience Cloud] Le destinazioni sono mappate sulle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| GAID | Google Advertising ID | I profili acquisiti in Experience Platform con un’identità primaria di Google Advertising ID (GAID) possono essere esportati in questa destinazione. |
| IDFA | Apple ID per inserzionisti | I profili acquisiti in Experience Platform con un’identità primaria di Apple ID per inserzionisti (IDFA) possono essere esportati in questa destinazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | I profili acquisiti in Experience Platform con un’identità primaria dell’indirizzo e-mail con hash possono essere esportati in questa destinazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) ricavato dalle identità elencate nella sezione precedente. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

>[!IMPORTANT]
> 
>Nella versione beta, puoi creare una singola connessione di destinazione alla destinazione Tipi di pubblico di Experience Cloud, su tutte le sandbox appartenenti alla tua organizzazione di Experienci Platform.

### Autentica nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, seleziona **[!UICONTROL Configurazione]** nella vista scheda di destinazione nel catalogo e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Vista dell’opzione Connetti alla destinazione per la destinazione Tipi di pubblico di Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Configura la nuova schermata di destinazione con le impostazioni richieste e facoltative per la connessione alla destinazione Tipi di pubblico di Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.


## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione. Tieni presente che no [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) è obbligatorio e no [passaggio di pianificazione](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) è disponibile per questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per convalidare l’esportazione dei dati corretta, puoi verificare che i segmenti siano stati correttamente inseriti nella soluzione di Experience Cloud desiderata.

### Convalidare i dati in Audience Manager

I segmenti di Experience Platform vengono visualizzati in Audience Manager come [Segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), e [segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Puoi verificare in Audience Manager se i dati sono stati visualizzati come descritto nei collegamenti alla documentazione riportati sopra.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

La governance dei dati in Experience Platform viene applicata da entrambi [etichette di utilizzo dei dati](/help/data-governance/labels/reference.md) e azioni di marketing.
Le etichette di utilizzo dei dati verranno trasferite alle applicazioni, ma le azioni di marketing no. Ciò significa che una volta arrivati in Audience Manager, i segmenti da Experience Platform possono essere esportati in qualsiasi destinazione disponibile. Ad Audience Manager, puoi utilizzare [controlli sull’esportazione dei dati](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) per bloccare l’esportazione di segmenti in determinate destinazioni.

### Gestione delle autorizzazioni in Audience Manager

Segmenti e caratteristiche in Audience Manager sono soggetti a [Controlli dell’accesso basati sul ruolo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=it) (RBAC).

I segmenti esportati da Experience Platform vengono assegnati a un’origine dati specifica nell’Audience Manager denominato **[!UICONTROL Segmenti Experience Platform]**.

Per consentire l’accesso ai segmenti solo a determinati utenti, puoi applicare i controlli di accesso ai segmenti appartenenti all’origine dati. In Audience Manager, devi impostare le nuove autorizzazioni di controllo degli accessi per questi segmenti e caratteristiche create da segmenti Experience Platform.
