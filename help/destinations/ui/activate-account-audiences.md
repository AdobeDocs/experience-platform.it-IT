---
title: Attivare il pubblico dell’account nelle destinazioni
type: Tutorial
description: Scopri come attivare i tipi di pubblico dell’account nelle destinazioni
badgeB2B: label="Edizione B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Attiva il pubblico dell’account

>[!AVAILABILITY]
>
>La funzionalità per attivare i tipi di pubblico dell&#39;account nelle destinazioni è disponibile per le aziende che acquistano le edizioni [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) di Real-time Customer Data Platform.

Questo articolo spiega il flusso di lavoro necessario per esportare [tipi di pubblico dell&#39;account](/help/segmentation/ui/account-audiences.md) da Adobe Experience Platform nella destinazione preferita.

## Destinazioni supportati {#supported-destinations}

Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**. Utilizza il filtro **[!UICONTROL Tipi di dati]** e seleziona **[!UICONTROL Account]** per visualizzare le destinazioni che supportano l&#39;attivazione dei tipi di pubblico dell&#39;account. Attualmente, l&#39;esportazione dei tipi di pubblico dell&#39;account è disponibile solo per alcune destinazioni di archiviazione cloud ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md) e [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) e per la destinazione [(Aziende) LinkedIn Matched Audiences](/help/destinations/catalog/social/linkedin.md).

![Destinazioni che supportano i tipi di pubblico dell&#39;account.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Panoramica video

Guarda il video seguente per una panoramica sulla creazione e l’attivazione dei tipi di pubblico per gli account e sui casi d’uso supportati per l’attivazione di tali tipi di pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Prerequisiti {#prerequisites}

* Prima di poter essere attivati nelle destinazioni a valle, devi acquisire [profili account](/help/rtcdp/accounts/account-profile-overview.md) e creare [tipi di pubblico account](/help/segmentation/ui/account-audiences.md).
* Per attivare i tipi di pubblico dell’account nelle destinazioni, è necessario essersi collegati correttamente a una destinazione. Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare. Per ulteriori informazioni, leggi l&#39;esercitazione dell&#39;interfaccia utente su [connessione alle destinazioni](./connect-destination.md).

### Autorizzazioni richieste {#permissions}

Per attivare i tipi di pubblico dell&#39;account, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Attiva destinazioni]** [Autorizzazioni per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per assicurarti di disporre delle autorizzazioni necessarie per attivare i tipi di pubblico dell’account, sfoglia il catalogo delle destinazioni. Se una destinazione dispone di un controllo **[!UICONTROL Attiva]**, si dispone delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui puoi esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**.

   ![Scheda Catalogo di destinazione con il controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva]** nella scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

>[!TIP]
>
>Le destinazioni che possono esportare i tipi di pubblico dell&#39;account sono indicate da un&#39;icona nell&#39;angolo superiore destro della scheda, simile alla destinazione evidenziata di seguito, oppure è possibile utilizzare il filtro del tipo di dati per visualizzare solo le destinazioni che possono esportare i tipi di pubblico dell&#39;account, come [mostrato più in alto nella pagina](#supported-destinations).

![Pagina di destinazione di Amazon S3 in grado di esportare i tipi di pubblico del profilo evidenziati.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Seleziona **[!UICONTROL Account tipo dati]**, seguito dalla connessione di destinazione in cui desideri esportare i set di dati, quindi seleziona **[!UICONTROL Avanti]**.

>[!TIP]
> 
>Se desideri impostare una nuova destinazione per attivare i tipi di pubblico dell&#39;account, seleziona **[!UICONTROL Configura nuova destinazione]** per attivare il flusso di lavoro [Connetti alla destinazione](/help/destinations/ui/connect-destination.md) e [seleziona gli account come tipo di dati](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Flusso di lavoro di attivazione della destinazione con controllo account evidenziato.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Procedi alla sezione successiva per [selezionare i tipi di pubblico del tuo account](#select-profile-audiences) per l&#39;esportazione.

## Seleziona il pubblico del tuo account {#select-account-audiences}

Utilizza le caselle di controllo a sinistra dei nomi dei tipi di pubblico dell&#39;account per selezionare i tipi di pubblico che desideri esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**. In questa visualizzazione vengono visualizzati solo *tipi di pubblico dell&#39;account* e non vengono visualizzati altri tipi di pubblico.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona tipi di pubblico in cui è possibile selezionare i tipi di pubblico dell&#39;account da esportare.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Pianificazione e passaggi successivi

Per il resto del flusso di lavoro di attivazione per esportare i tipi di pubblico dell’account, leggi l’esercitazione sull’attivazione dei dati in destinazioni basate su file. Continua dal passaggio [pianifica esportazione pubblico](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Se stai attivando i tipi di pubblico dell&#39;account nella destinazione **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, leggi l&#39;esercitazione sull&#39;attivazione delle destinazioni di streaming. Continua dal [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Tieni presente che nel passaggio di pianificazione, durante l&#39;esportazione dei tipi di pubblico dell&#39;account nelle destinazioni di archiviazione cloud, il flusso di lavoro per attivare i tipi di pubblico dell&#39;account ti consente di esportare solo [file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _con una pianificazione giornaliera_. Le esportazioni orarie non sono supportate. Si noti inoltre che **[!UICONTROL Dopo la valutazione del pubblico]** è l&#39;unico tipo di valutazione supportato.

## Callout importanti e limitazioni note {#important-callouts-known-limitations}

Tieni presente i seguenti callout importanti e le limitazioni note per la versione con disponibilità generale della funzionalità di attivazione dei tipi di pubblico dell’account.

### Coppie di mappatura necessarie nel passaggio di mappatura durante l&#39;attivazione dei tipi di pubblico dell&#39;account nella destinazione **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Quando si attivano i tipi di pubblico dell&#39;account nella destinazione **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, si noti che le due coppie di mapping seguenti sono obbligatorie per esportare correttamente i dati:

![Campi obbligatori per la mappatura di LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo di origine | Campo di destinazione |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (seleziona questo campo nella visualizzazione **[!UICONTROL Seleziona spazio dei nomi identità]**, quando selezioni il **[!UICONTROL campo di destinazione]**). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selezionare lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni."){width="100" zoomable="yes"} |

### Applicazione della governance dei dati {#data-governance-enforcement}

Il consenso viene applicato a livello di persona o profilo per *tipi di pubblico cliente e potenziale*. Pertanto, la [valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportata quando si attivano i tipi di pubblico dell&#39;account nelle destinazioni. Nel passaggio di revisione del flusso di lavoro di attivazione, puoi visualizzare un controllo disattivato per **[!UICONTROL Visualizza i criteri di consenso applicabili]**.

![Passaggio di revisione del flusso di lavoro attiva tipi di pubblico per l&#39;account con il controllo dell&#39;applicazione del consenso disattivato.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Sono supportati altri meccanismi di governance dei dati in Real-Time CDP, ad esempio [controlli dei criteri di utilizzo dei dati](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) e [controllo dell&#39;accesso basato sugli attributi](/help/destinations/home.md#attribute-based-access).
