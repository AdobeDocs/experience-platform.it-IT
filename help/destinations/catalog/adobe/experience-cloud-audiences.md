---
title: Experience Cloud Audiences
description: Scopri come condividere i tipi di pubblico da Real-time Customer Data Platform a varie app di Experience Cloud.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 1%

---


# [!UICONTROL Tipi di pubblico di Experience Cloud] connessione

>[!AVAILABILITY]
>
> Questa destinazione è disponibile per [Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

Utilizza questa destinazione per attivare i tipi di pubblico da Real-Time CDP ad Audienci Manager e Adobe Analytics. È necessaria una licenza Audienci Manager per inviare tipi di pubblico ad Adobe Analytics.

Per inviare tipi di pubblico ad altre soluzioni di Adobe, utilizza le connessioni dirette da Real-Time CDP a [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) e [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Questa destinazione sostituisce la [integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) da Real-time Customer Data Platform a varie soluzioni di Experience Cloud.
> 
>Se condividi già tipi di pubblico da Real-Time CDP a Audienci Manager e altre soluzioni di Experience Cloud tramite [integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), prima di utilizzare questa destinazione, contatta l’Assistenza clienti per disabilitare l’integrazione legacy.

![La destinazione Tipi di pubblico di Experience Cloud, evidenziata nel catalogo delle destinazioni.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Casi d’uso e vantaggi {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!UICONTROL Tipi di pubblico di Experience Cloud] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Real-Time CDP possono risolvere utilizzando questa destinazione.

### Abilitare i casi d’uso di Data Management Platform {#dmp-use-cases}

Ad Audience Manager, puoi utilizzare i tipi di pubblico di Real-Time CDP per i casi d’uso di Data Management Platform, ad esempio:

* Aggiunta [dati di terze parti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) ai tuoi segmenti;
* [Modellazione algoritmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Attivazione dei tipi di pubblico su destinazioni basate su cookie non ancora supportate nel catalogo delle destinazioni di Real-Time CDP.

### Controllo granulare dei tipi di pubblico esportati {#segments-control}

Utilizza la nuova integrazione self-service di condivisione del pubblico tramite la destinazione Tipi di pubblico di Experience Cloud per selezionare i tipi di pubblico da esportare in Audienci Manager e oltre. Questo consente di determinare quali tipi di pubblico desideri condividere con altre soluzioni di Experience Cloud e quali tipi di pubblico desideri mantenere esclusivamente in Real-Time CDP.

L’integrazione legacy di condivisione del pubblico non consentiva un controllo granulare dei tipi di pubblico da esportare in Audienci Manager e versioni successive.

### Condividere i tipi di pubblico di Real-Time CDP con altre soluzioni di Experience Cloud {#share-segments-with-other-solutions}

Oltre a condividere i tipi di pubblico con Audienci Manager, la scheda di destinazione Tipi di pubblico di Real-Time CDP consente di condividere i tipi di pubblico con qualsiasi altra soluzione di Experience Cloud per la quale disponi del provisioning, tra cui:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
> * È necessaria una licenza Audienci Manager per abilitare [Casi d’uso di Data Management Platform](#dmp-use-cases) di cui sopra.
> * Tu *non è necessario* una licenza di Audience Manager per condividere i tipi di pubblico di Real-Time CDP con Adobe Advertising Cloud, Adobe Target, Marketo e altre soluzioni di Experience Cloud, menzionate in [sezione precedente](#share-segments-with-other-solutions).

### Per i clienti che utilizzano la soluzione legacy di condivisione del pubblico

Se condividi già tipi di pubblico da Real-Time CDP a Audienci Manager e altre soluzioni di Experience Cloud tramite [integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), è necessario contattare l’Assistenza clienti per disabilitare l’integrazione legacy.

Il tempo di risposta per risolvere il ticket di deprovisioning è inferiore o pari a sei giorni lavorativi. Dopo aver disabilitato l’integrazione legacy esistente, puoi procedere con [creazione di una connessione](#connect) tramite la scheda di destinazione self-service.

>[!IMPORTANT]
>
>L’esportazione del pubblico da Real-Time CDP alle altre soluzioni verrà interrotta nel periodo compreso tra la risoluzione del ticket e il momento in cui viene stabilita una nuova connessione tramite la scheda di destinazione. Puoi ridurre al minimo questo downtime creando la connessione tramite la scheda di destinazione non appena il ticket viene chiuso.

## Limitazioni note e callout {#known-limitations}

Prendi nota delle seguenti limitazioni note e dei callout importanti durante l’utilizzo della scheda Tipi di pubblico di Experience Cloud:

* Attualmente, è supportata una singola destinazione Tipi di pubblico di Experience Cloud. Se si tenta di configurare una seconda connessione di destinazione, si verifica un errore.
* Quando ti connetti alla destinazione, puoi vedere un’opzione per [abilitare gli avvisi del flusso di dati](../../ui/alerts.md). Anche se visibile nell’interfaccia utente, il **l’opzione abilita avvisi non è attualmente supportata**.
* **Supporto per la retrocompilazione del pubblico**: la prima esportazione in Audienci Manager o in altre soluzioni Experience Cloud include una popolazione storica dei tipi di pubblico. Utenti di [integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) chi configura questa destinazione deve aspettarsi una differenza di backfill di circa 6 ore.

### Latenza durante l’attivazione dei tipi di pubblico {#audience-activation-latency}

Esiste una latenza di quattro ore tra il momento in cui i tipi di pubblico vengono attivati per la prima volta in Real-Time CDP e il momento in cui sono pronti per essere utilizzati in Audienci Manager e in altre soluzioni Experience Cloud per determinati casi d’uso.

Possono essere necessarie fino a 24 ore affinché i tipi di pubblico siano completamente disponibili in Audienci Manager per tutti i casi d’uso e fino a 48 ore affinché i tipi di pubblico di Experience Cloud Audiences vengano visualizzati nei rapporti di Audienci Manager.

I metadati, come i nomi del pubblico, sono disponibili in Audienci Manager entro pochi minuti dalla configurazione dell’esportazione nella destinazione Audiences di Experience Cloud.

## Identità supportate {#supported-identities}

I profili esportati in [!UICONTROL Tipi di pubblico di Experience Cloud] Le destinazioni sono mappate sulle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| GAID | Google Advertising ID | I profili acquisiti in Real-Time CDP con un’identità primaria di Google Advertising ID (GAID) possono essere esportati in questa destinazione. |
| IDFA | Apple ID per inserzionisti | I profili acquisiti in Real-Time CDP con un’identità primaria di Apple ID per inserzionisti (IDFA) possono essere esportati in questa destinazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | I profili acquisiti in Real-Time CDP con un’identità primaria dell’indirizzo e-mail con hash possono essere esportati in questa destinazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico ricavati dalle identità elencate nella sezione precedente. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Real-Time CDP in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, seleziona **[!UICONTROL Configurazione]** nella vista scheda di destinazione nel catalogo e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Vista dell’opzione Connetti alla destinazione per la destinazione Tipi di pubblico di Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Configura la nuova schermata di destinazione con le impostazioni richieste e facoltative per la connessione alla destinazione Tipi di pubblico di Experience Cloud.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione. Tieni presente che no [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) è obbligatorio e no [passaggio di pianificazione](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) è disponibile per questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per convalidare l’esportazione dei dati corretta, puoi verificare che i tipi di pubblico siano riusciti a passare alla soluzione di Experience Cloud desiderata.

### Convalidare i dati in Audienci Manager

I tipi di pubblico di Real-Time CDP vengono visualizzati in Audienci Manager come [Segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits), e [segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). Puoi verificare in Audienci Manager se i dati sono stati visualizzati come descritto nei collegamenti alla documentazione riportati sopra.

I nomi dei segmenti iniziano a essere popolati in Audienci Manager 15 minuti dopo l’invio dei tipi di pubblico da Real-Time CDP.

La popolazione del segmento inizia a fluire in Audienci Manager entro 6 ore dall’invio da Real-Time CDP e verrà aggiornata ogni 24 ore in Audienci Manager.

L’intera popolazione sarà visibile in Audienci Manager dopo 72 ore e le popolazioni continueranno a scorrere in Audienci Manager a meno che il pubblico non venga rimosso dalla destinazione in Real-Time CDP.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Real-Time CDP] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

La governance dei dati in Real-Time CDP viene applicata da entrambi [etichette di utilizzo dei dati](/help/data-governance/labels/reference.md) e azioni di marketing.
Le etichette di utilizzo dei dati verranno trasferite alle applicazioni, ma le azioni di marketing no. Ciò significa che una volta arrivati in Audienci Manager, i tipi di pubblico da Real-Time CDP possono essere esportati in qualsiasi destinazione disponibile. Ad Audience Manager, puoi utilizzare [controlli sull’esportazione dei dati](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) per bloccare l’esportazione di tipi di pubblico in determinate destinazioni.

Tipi di pubblico contrassegnati con [!DNL HIPAA] l’azione di marketing non verrà inviata da Real-Time CDP all’Audience Manager.

### Gestione delle autorizzazioni in Audienci Manager

I tipi di pubblico e le caratteristiche in Audienci Manager sono soggetti a [Controlli dell’accesso basati sul ruolo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

I tipi di pubblico esportati da Real-Time CDP vengono assegnati a un’origine dati specifica nell’Audience Manager denominato **[!UICONTROL Segmenti Experienci Platform]**.

Per consentire solo a determinati utenti di accedere ai tipi di pubblico, puoi applicare i controlli di accesso ai tipi di pubblico appartenenti all’origine dati. In Audienci Manager, devi impostare le nuove autorizzazioni di controllo degli accessi per questi tipi di pubblico e le caratteristiche create dai segmenti di Real-Time CDP.
