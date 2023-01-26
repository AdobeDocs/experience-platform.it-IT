---
title: (Beta) Tipi di pubblico di Experience Cloud
description: Scopri come condividere segmenti da Experience Platform a diverse soluzioni Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---


# (Beta) [!UICONTROL Tipi di pubblico di Experience Cloud] connection

Questa destinazione ti consente di condividere segmenti da Experience Platform a diverse soluzioni di Experience Cloud, come ad Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo.

![La destinazione Experience Cloud Audiences, evidenziata nel catalogo delle destinazioni.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Questa destinazione sostituisce la [integrazione della condivisione dei segmenti legacy](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) dall&#39;Experience Platform a diverse soluzioni Experience Cloud.
>* Questa destinazione è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.


## Casi d’uso e vantaggi {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!UICONTROL Tipi di pubblico di Experience Cloud] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Abilita casi d’uso di Data Management Platform {#dmp-use-cases}

Ad Audience Manager, puoi utilizzare segmenti di Experience Platform per casi d’uso di Data Management Platform, ad esempio:

* Aggiungi [dati di terze parti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) ai segmenti;
* [Modellazione algoritmica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Attiva i segmenti nelle destinazioni basate su cookie che non sono ancora supportate nel catalogo delle destinazioni Experience Platform.

### Controllo granulare dei segmenti esportati {#segments-control}

Utilizza la nuova integrazione di condivisione del segmento self-service tramite la destinazione Experience Cloud Audiences per selezionare i segmenti da esportare in Audience Manager e oltre. Questo ti consente di determinare quali segmenti vuoi condividere con altre soluzioni Experience Cloud e quali segmenti desideri mantenere esclusivamente in Experience Platform.

L’integrazione legacy per la condivisione dei segmenti non consentiva un controllo granulare sui segmenti da esportare in Audience Manager e oltre.

### Condivisione di segmenti di Experience Platform con altre soluzioni Experience Cloud {#share-segments-with-other-solutions}

Oltre a condividere i segmenti con l’Audience Manager, la scheda di destinazione Tipi di pubblico di Experience Platform consente di condividere i segmenti con qualsiasi altra soluzione di Experience Cloud per la quale sei abilitato, tra cui:

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
> * È necessaria una licenza di Audience Manager per abilitare i casi d’uso di Data Management Platform menzionati nella sezione precedente.
> * You *non è necessario* una licenza di Audience Manager per condividere segmenti di Experience Platform con Adobe Advertising Cloud, Adobe Target, Marketo e altre soluzioni di Experience Cloud tramite l’integrazione di Experience Cloud Audiences.


### Per i clienti che utilizzano la soluzione legacy di condivisione dei segmenti

Se stai già condividendo segmenti da Experience Platform ad Audience Manager e altre soluzioni di Experience Cloud tramite [integrazione della condivisione dei segmenti legacy](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam), per disabilitare l’integrazione legacy devi contattare l’Assistenza clienti o il Customer Success Manager. Per disabilitare l’integrazione, i team di assistenza clienti e di gestione dell’assistenza clienti devono creare un ticket Jira (consulta il ticket modello AAM-52354).

Il tempo di consegna per risolvere il ticket di deprovisioning per i clienti beta è di sei giorni lavorativi o meno. Dopo aver disabilitato l&#39;integrazione legacy esistente, puoi procedere a [creazione di una connessione](#connect) tramite la scheda di destinazione self-service.

>[!IMPORTANT]
>
>L’esportazione del segmento da Experience Platform alle altre soluzioni verrà interrotta nel periodo tra la risoluzione del ticket Jira e il momento in cui viene stabilita una nuova connessione tramite la scheda di destinazione. È possibile ridurre al minimo i tempi di inattività creando la connessione tramite la scheda di destinazione non appena il biglietto Jira viene chiuso.

## Limitazioni note e callout {#known-limitations}

Nota le seguenti limitazioni note e callout importanti nella versione beta della scheda Experience Cloud Audiences :

* [Monitoraggio dei flussi di dati](/help/dataflows/ui/monitor-destinations.md) non è supportato.
* Quando ti connetti alla destinazione, puoi visualizzare un’opzione per [abilitare gli avvisi del flusso di dati](#enable-alerts). Sebbene sia visibile nell’interfaccia utente, la **l&#39;opzione abilita avvisi non è supportata** nella versione beta.
* **Backfill non supportati**. La prima esportazione in Audience Manager o altre soluzioni di Experience Cloud non include una popolazione storica dei segmenti.
* Nella versione beta, puoi creare **una singola connessione di destinazione alla destinazione Experience Cloud Audiences**, in tutte le sandbox appartenenti all’organizzazione Experience Platform.
* C&#39;è una **latenza di quattro ore** tra il momento in cui i dati vengono attivati in Experience Platform e il momento in cui i dati sono pronti per essere utilizzati in Audience Manager e in altre soluzioni di Experience Cloud.

## Identità supportate {#supported-identities}

I profili esportati nel [!UICONTROL Tipi di pubblico di Experience Cloud] La destinazione è mappata alle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| ECID | Experience Cloud ID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| GAID | Google Advertising ID | I profili acquisiti in Experience Platform con un’identità principale di Google Advertising ID (GAID) possono essere esportati in questa destinazione. |
| IDFA | Apple ID per gli inserzionisti | I profili acquisiti in Experience Platform con un’identità principale di Apple ID per gli inserzionisti (IDFA) possono essere esportati in questa destinazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | I profili acquisiti in Experience Platform con un&#39;identità principale di indirizzo e-mail con hash possono essere esportati in questa destinazione. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con chiave delle identità elencate nella sezione precedente. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

>[!IMPORTANT]
> 
>Nella versione beta, puoi creare una singola connessione di destinazione alla destinazione Experience Cloud Audiences, in tutte le sandbox appartenenti alla tua organizzazione Experience Platform.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Configurazione]** nella vista scheda di destinazione nel catalogo e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Visualizzazione dell&#39;opzione Connetti a destinazione per la destinazione Pubblico di Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Configura la nuova schermata di destinazione che mostra le impostazioni richieste e facoltative per la connessione alla destinazione Experience Cloud Audiences.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.


## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione. Nota che no [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) è richiesto e no [fase di pianificazione](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) è disponibile per questa destinazione.

## Convalida esportazione dati {#exported-data}

Per convalidare l’esportazione dei dati riuscita, puoi verificare che i segmenti siano riusciti a inviarli alla soluzione di Experience Cloud desiderata.

### Convalidare dati in Audience Manager

I segmenti di Experience Platform vengono visualizzati in Audience Manager come [segnali](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [caratteristiche](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)e [segmenti](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Puoi verificare in Audience Manager se i dati sono stati visualizzati come descritto nei collegamenti alla documentazione di cui sopra.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

La governance dei dati in Experience Platform è applicata da entrambi [etichette di utilizzo dei dati](/help/data-governance/labels/reference.md) e le azioni di marketing.
Le etichette di utilizzo dei dati verranno trasferite alle applicazioni, ma le azioni di marketing no. Ciò significa che una volta arrivati nell’Audience Manager, i segmenti da Experience Platform possono essere esportati in qualsiasi destinazione disponibile. Ad Audience Manager, puoi utilizzare [controlli per l&#39;esportazione dei dati](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) per impedire l’esportazione di segmenti in determinate destinazioni.

### Gestione delle autorizzazioni in Audience Manager

Segmenti e caratteristiche in Audience Manager sono soggetti a [Controlli di accesso basati sul ruolo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=it) (RBAC).

I segmenti esportati da Experience Platform vengono assegnati a una specifica origine dati in un Audience Manager denominato **[!UICONTROL Segmenti di Experience Platform]**.

Per consentire l’accesso ai segmenti solo a determinati utenti, puoi applicare controlli di accesso ai segmenti appartenenti all’origine dati. È necessario impostare nuove autorizzazioni di controllo accessi in Audience Manager per questi segmenti e caratteristiche create dai segmenti di Experience Platform.