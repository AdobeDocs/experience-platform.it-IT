---
title: Attivare il pubblico dell’account nelle destinazioni
type: Tutorial
description: Scopri come attivare i tipi di pubblico dell’account nelle destinazioni
badgeB2B: label="Edizione B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: f07eb12b4625bce117e1fe524727c00b7188aa5e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Attiva il pubblico dell’account

>[!AVAILABILITY]
>
>La funzionalità per attivare il pubblico dell’account nelle destinazioni è disponibile per le aziende che acquistano [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2b) edizioni Real-time Customer Data Platform.

Questo articolo spiega il flusso di lavoro necessario per esportare [pubblico dell’account](/help/segmentation/ui/account-audiences.md) da Adobe Experience Platform alla destinazione preferita.

## Destinazioni supportati {#supported-destinations}

Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda. Utilizza il **[!UICONTROL Tipi di dati]** filtra e seleziona **[!UICONTROL Account]** per visualizzare le destinazioni che supportano l’attivazione dei tipi di pubblico dell’account. Attualmente, l’esportazione del pubblico dell’account è disponibile solo per alcune destinazioni di archiviazione cloud ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Archiviazione BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), e [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) e [(Aziende) Tipi di pubblico LinkedIn corrispondenti](/help/destinations/catalog/social/linkedin.md) destinazione.

![Destinazioni che supportano i tipi di pubblico dell’account.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Prerequisiti {#prerequisites}

* Devi prima acquisire [profili account](/help/rtcdp/accounts/account-profile-overview.md) e creare [pubblico dell’account](/help/segmentation/ui/account-audiences.md) prima di attivarli nelle destinazioni a valle.
* Per attivare i tipi di pubblico dell’account nelle destinazioni, è necessario essersi collegati correttamente a una destinazione. Se non lo hai già fatto, accedi al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare. Leggi l’esercitazione sull’interfaccia utente su [connessione alle destinazioni](./connect-destination.md) per ulteriori informazioni.

### Autorizzazioni necessarie {#permissions}

Per attivare i tipi di pubblico dell’account, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Attivare le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per assicurarti di disporre delle autorizzazioni necessarie per attivare i tipi di pubblico dell’account, sfoglia il catalogo delle destinazioni. Se una destinazione ha **[!UICONTROL Attiva]** , quindi si dispone delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui puoi esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda.

   ![Scheda Catalogo di destinazione con il controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva]** nella scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

>[!TIP]
>
>Le destinazioni che possono esportare i tipi di pubblico dell’account sono indicate da un’icona nell’angolo superiore destro della scheda, simile alla destinazione evidenziata di seguito, oppure puoi utilizzare il filtro del tipo di dati per visualizzare solo le destinazioni che possono esportare i tipi di pubblico dell’account, come [mostrato più in alto nella pagina](#supported-destinations).

![Pagina di destinazione di Amazon S3 in cui è possibile esportare i tipi di pubblico di profilo evidenziati.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Seleziona **[!UICONTROL Account tipo dati]**, seguito dalla connessione di destinazione in cui desideri esportare i set di dati, quindi seleziona **[!UICONTROL Successivo]**.

>[!TIP]
> 
>Se desideri impostare una nuova destinazione per attivare i tipi di pubblico dell’account, seleziona **[!UICONTROL Configurare una nuova destinazione]** per attivare [Connetti alla destinazione](/help/destinations/ui/connect-destination.md) workflow e [seleziona account come tipo di dati](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Flusso di lavoro di attivazione della destinazione con il controllo account evidenziato.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Procedi alla sezione successiva per [seleziona il pubblico del tuo account](#select-profile-audiences) per l&#39;esportazione.

## Seleziona il pubblico del tuo account {#select-account-audiences}

Utilizza le caselle di controllo a sinistra dei nomi dei tipi di pubblico dell’account per selezionare i tipi di pubblico da esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**. Tieni presente che *pubblico dell’account* In questa visualizzazione non sono visualizzati altri tipi di pubblico.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona tipi di pubblico in cui è possibile selezionare i tipi di pubblico dell’account da esportare.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Pianificazione e passaggi successivi

Per il resto del flusso di lavoro di attivazione per esportare i tipi di pubblico dell’account, leggi l’esercitazione sull’attivazione dei dati in destinazioni basate su file. Continua da [pianifica passaggio esportazione pubblico](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Se si attivano i tipi di pubblico dell’account per **[!UICONTROL (Aziende) Tipi di pubblico LinkedIn corrispondenti]** destinazione, leggi l’esercitazione sull’attivazione delle destinazioni di streaming. Continua da [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Tieni presente che nel passaggio di pianificazione, durante l’esportazione dei tipi di pubblico dell’account nelle destinazioni di archiviazione cloud, il flusso di lavoro per attivare tali tipi di pubblico ti consente solo di esportare [file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _su base giornaliera_. Le esportazioni orarie non sono supportate. Tieni presente anche che **[!UICONTROL Dopo la valutazione del pubblico]** è l’unico tipo di valutazione supportato.

## Callout importanti e limitazioni note {#important-callouts-known-limitations}

Tieni presente i seguenti callout importanti e le limitazioni note per la versione con disponibilità generale della funzionalità di attivazione dei tipi di pubblico dell’account.

### Coppie di mappatura necessarie nella fase di mappatura quando si attivano i tipi di pubblico dell’account per **[!UICONTROL (Aziende) Tipi di pubblico LinkedIn corrispondenti]** destinazione {#required-mappings}

Quando si attivano i tipi di pubblico dell’account per **[!UICONTROL (Aziende) Tipi di pubblico LinkedIn corrispondenti]** destinazione, tieni presente che le due coppie di mappatura seguenti sono obbligatorie per esportare correttamente i dati:

![Mappatura dei campi obbligatori in linkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo di origine | Campo di destinazione |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (seleziona questo campo nella sezione **[!UICONTROL Seleziona lo spazio dei nomi delle identità]** visualizzazione, quando si seleziona la **[!UICONTROL Campo di destinazione]**). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell’account nelle destinazioni.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell’account nelle destinazioni."){width="100" zoomable="yes"} |

### Applicazione della governance dei dati {#data-governance-enforcement}

Il consenso viene applicato a livello di persona o profilo per *pubblico cliente e potenziale cliente*. Pertanto,  [valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportato quando si attivano i tipi di pubblico dell’account nelle destinazioni. Nel passaggio di revisione del flusso di lavoro di attivazione, è possibile visualizzare un controllo disattivato per **[!UICONTROL Visualizza i criteri di consenso applicabili]**.

![Passaggio di revisione del flusso di lavoro attiva tipi di pubblico per l’account con il controllo dell’applicazione del consenso disattivato.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Altri meccanismi di governance dei dati in Real-Time CDP, come [controlli dei criteri di utilizzo dati](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) e [controllo degli accessi basato su attributi](/help/destinations/home.md#attribute-based-access) sono supportati.
