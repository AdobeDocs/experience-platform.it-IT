---
title: Experience Cloud Audiences
description: Scopri come condividere i tipi di pubblico da Real-time Customer Data Platform a varie app di Experience Cloud.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 2%

---


# Connessione [!UICONTROL Experience Cloud Audiences]

>[!AVAILABILITY]
>
> Questa destinazione è disponibile per [i clienti Adobe Real-time Customer Data Platform Prime e Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

Utilizza questa destinazione per attivare i tipi di pubblico da Real-Time CDP ad Audience Manager e Adobe Analytics.

Per inviare dei tipi di pubblico ad Adobe Analytics, è necessaria una licenza Audience Manager. Per ulteriori dettagli, vedi l&#39;[panoramica dell&#39;Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=en).

Per inviare tipi di pubblico ad altre soluzioni Adobe, utilizza le connessioni dirette da Real-Time CDP a [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) e [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Questa destinazione sostituisce l&#39;[integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) da Real-time Customer Data Platform a varie soluzioni di Experience Cloud.
> 
>Se stai già condividendo tipi di pubblico da Real-Time CDP a Audience Manager e altre soluzioni Experience Cloud tramite l&#39;[integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), devi contattare l&#39;Assistenza clienti per disabilitare l&#39;integrazione legacy prima di utilizzare questa destinazione.

![Destinazione tipi di pubblico Experience Cloud, evidenziata nel catalogo delle destinazioni.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Casi d’uso e vantaggi {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!UICONTROL Experience Cloud Audiences], ecco alcuni esempi di casi d&#39;uso che i clienti Real-Time CDP possono risolvere utilizzando questa destinazione.

### Abilitare i casi d’uso di Data Management Platform {#dmp-use-cases}

Ad Audience Manager, puoi utilizzare i tipi di pubblico di Real-Time CDP per i casi d’uso di Data Management Platform, ad esempio:

* Aggiunta di [dati di terze parti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) ai segmenti;
* [Modellazione algoritmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Attivazione dei tipi di pubblico su destinazioni basate su cookie non ancora supportate nel catalogo delle destinazioni di Real-Time CDP.

### Controllo granulare dei tipi di pubblico esportati {#segments-control}

Per selezionare i tipi di pubblico da esportare in Audience Manager e oltre, utilizza la nuova integrazione self-service di condivisione del pubblico tramite la destinazione Experience Cloud Audiences.  Questo consente di determinare quali tipi di pubblico desideri condividere con altre soluzioni di Experience Cloud e quali tipi di pubblico desideri mantenere esclusivamente in Real-Time CDP.

L’integrazione legacy di condivisione del pubblico non consentiva un controllo granulare dei tipi di pubblico da esportare in Audience Manager e versioni successive.

### Condividere tipi di pubblico di Real-Time CDP con Adobe Analytics {#share-audiences-with-analytics}

I tipi di pubblico inviati alla destinazione Tipi di pubblico di Experience Cloud non vengono visualizzati automaticamente in Adobe Analytics.

Prima di poter inviare tipi di pubblico ad Adobe Analytics, devi [implementare il servizio Experience Cloud Identity per Analytics e Audience Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=en).

>[!IMPORTANT]
>
>Per inviare tipi di pubblico da Real-Time CDP ad Adobe Analytics tramite la destinazione Tipi di pubblico di Experience Cloud, è necessario disporre di una licenza Audience Manager.

### Condividere i tipi di pubblico di Real-Time CDP con altre soluzioni di Experience Cloud {#share-segments-with-other-solutions}

Puoi utilizzare la scheda di destinazione Tipi di pubblico di Real-Time CDP per condividere i tipi di pubblico con altre soluzioni di Experience Cloud.

Tuttavia, Adobe consiglia vivamente di utilizzare le seguenti schede di destinazione dedicate se desideri condividere i tipi di pubblico con queste soluzioni:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
> * È necessaria una licenza Audience Manager per abilitare i [casi d&#39;uso di Data Management Platform](#dmp-use-cases) menzionati più sopra.
> * *hai* bisogno di una licenza Audience Manager per condividere i tipi di pubblico di Real-Time CDP con Adobe Analytics.
> * *non hai bisogno* di una licenza Audience Manager per condividere i tipi di pubblico di Real-Time CDP con Adobe Advertising Cloud, Adobe Target, Marketo e altre soluzioni Experience Cloud, menzionate nella [sezione precedente](#share-segments-with-other-solutions).

### Per i clienti che utilizzano la soluzione legacy di condivisione del pubblico

Se stai già condividendo tipi di pubblico da Real-Time CDP a Audience Manager e altre soluzioni Experience Cloud tramite l&#39;[integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), devi contattare l&#39;Assistenza clienti per disabilitare l&#39;integrazione legacy.

Il tempo di risposta per risolvere il ticket di deprovisioning è inferiore o pari a sei giorni lavorativi. Dopo aver disabilitato l&#39;integrazione legacy esistente, puoi passare a [creare una connessione](#connect) tramite la scheda di destinazione self-service.

>[!IMPORTANT]
>
>L’esportazione del pubblico da Real-Time CDP alle altre soluzioni viene interrotta nel periodo di tempo che intercorre tra la risoluzione del ticket e il momento in cui viene stabilita una nuova connessione tramite la scheda di destinazione. Puoi ridurre al minimo i tempi di inattività creando la connessione tramite la scheda di destinazione dopo la chiusura del ticket.

## Limitazioni note e callout {#known-limitations}

Prendi nota delle seguenti limitazioni note e dei callout importanti durante l’utilizzo della scheda Tipi di pubblico di Experience Cloud:

* Attualmente, è supportata una singola destinazione Tipi di pubblico di Experience Cloud. Il tentativo di configurare una seconda connessione di destinazione genera un errore.
* Quando ti connetti alla destinazione, puoi visualizzare un&#39;opzione per [abilitare gli avvisi del flusso di dati](../../ui/alerts.md). Anche se visibile nell&#39;interfaccia utente, l&#39;opzione **abilita avvisi non è attualmente supportata**.
* **Supporto per la retrocompilazione del pubblico**: la prima esportazione in Audience Manager o in altre soluzioni Experience Cloud include una popolazione cronologica dei tipi di pubblico. Gli utenti della [integrazione legacy di condivisione del pubblico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) che configurano questa destinazione devono aspettarsi una differenza di backfill di circa sei ore.
* I tipi di pubblico provenienti da [Composizione pubblico](../../../segmentation/ui/audience-composition.md) non sono supportati direttamente. Per attivare il pubblico composito in questa destinazione è necessario creare una definizione di pubblico tramite [Segment Builder](../../../segmentation/ui/segment-builder.md) in base al pubblico composito e attivare il pubblico appena creato.

### Latenza durante l’attivazione dei tipi di pubblico {#audience-activation-latency}

Esiste una latenza di quattro ore tra il momento in cui i tipi di pubblico vengono attivati per la prima volta in Real-Time CDP e il momento in cui sono pronti per essere utilizzati in Audience Manager e in altre soluzioni Experience Cloud.

Possono essere necessarie fino a 24 ore affinché i tipi di pubblico siano completamente disponibili, ad Audience Manager per tutti i casi d’uso. La visualizzazione dei tipi di pubblico di Experience Cloud Audiences nei rapporti di Audience Manager può richiedere fino a 48 ore.

I metadati, come i nomi del pubblico, sono disponibili in Audience Manager entro pochi minuti dalla configurazione dell’esportazione nella destinazione Audiences di Experience Cloud.

## Identità supportate {#supported-identities}

I profili esportati nella destinazione [!UICONTROL Experience Cloud Audiences] sono mappati alle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/features/ecid.md). |
| GAID | GOOGLE ADVERTISING ID | I profili acquisiti in Real-Time CDP con un’identità primaria di Google Advertising ID (GAID) possono essere esportati in questa destinazione. |
| IDFA | Apple ID per inserzionisti | I profili acquisiti in Real-Time CDP con un’identità primaria di Apple ID per inserzionisti (IDFA) possono essere esportati in questa destinazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | I profili acquisiti in Real-Time CDP con un’identità primaria dell’indirizzo e-mail con hash possono essere esportati in questa destinazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico ricavati dalle identità elencate nella sezione precedente. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Real-Time CDP in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Configura]** nella vista a schede di destinazione nel catalogo e selezionare **[!UICONTROL Connetti alla destinazione]**.

![Visualizzazione dell&#39;opzione Connetti a destinazione per la destinazione Tipi di pubblico Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Configura la nuova schermata di destinazione con le impostazioni obbligatorie e facoltative per la connessione alla destinazione Tipi di pubblico Experience Cloud.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione. Nessun [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) richiesto e nessun [passaggio di pianificazione](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) disponibile per questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per convalidare l’esportazione dei dati corretta, puoi verificare che i tipi di pubblico siano riusciti a passare alla soluzione di Experience Cloud desiderata.

### Convalidare i dati in Audience Manager

I tipi di pubblico di Real-Time CDP vengono visualizzati in Audience Manager come [segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits) e [segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). Puoi verificare in Audience Manager se i dati sono stati visualizzati come descritto nei collegamenti alla documentazione riportati sopra.

I nomi dei segmenti iniziano a essere popolati in Audience Manager 15 minuti dopo l’invio dei tipi di pubblico da Real-Time CDP.

La popolazione del segmento inizia a fluire in Audience Manager entro 6 ore dall’invio da Real-Time CDP e viene aggiornata ogni 24 ore in Audience Manager.

L’intera popolazione sarà visibile in Audience Manager dopo 72 ore e le popolazioni continueranno a scorrere in Audience Manager a meno che il pubblico non venga rimosso dalla destinazione in Real-Time CDP.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Real-Time CDP] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

La governance dei dati in Real-Time CDP viene applicata sia dalle [etichette di utilizzo dei dati](/help/data-governance/labels/reference.md) che dalle azioni di marketing.
Le etichette di utilizzo dei dati vengono trasferite alle applicazioni, ma le azioni di marketing no. Ciò significa che una volta arrivati in Audience Manager, i tipi di pubblico da Real-Time CDP possono essere esportati in qualsiasi destinazione disponibile. Ad Audience Manager, puoi utilizzare [controlli di esportazione dei dati](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) per bloccare l&#39;esportazione di tipi di pubblico in determinate destinazioni.

I tipi di pubblico contrassegnati con l&#39;azione di marketing [!DNL HIPAA] non vengono inviati da Real-Time CDP a Audience Manager.

### Gestione delle autorizzazioni in Audience Manager

I tipi di pubblico e le caratteristiche in Audience Manager sono soggetti ai [controlli di accesso basati sul ruolo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

I tipi di pubblico esportati da Real-Time CDP vengono assegnati a un&#39;origine dati specifica nell&#39;Audience Manager denominata **[!UICONTROL Segmenti Experienci Platform]**.

Per consentire solo a determinati utenti l&#39;accesso ai tipi di pubblico, utilizzare [Controlli di accesso basati sul ruolo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) per configurare l&#39;accesso degli utenti ai tipi di pubblico e alle caratteristiche creati dai tipi di pubblico di Real-Time CDP.
