---
title: ' [!DNL Google Ad Manager 360] connessione(Beta)'
description: Google Ad Manager 360 è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci sui loro siti web, tramite video e app mobili.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 4%

---

# [!DNL Google Ad Manager 360]connessione(Beta)

## Panoramica {#overview}

Il [!DNL Google Ad Manager 360] la connessione abilita il caricamento batch per [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], tramite [!DNL Google Cloud Storage].

Per ulteriori dettagli sul funzionamento degli identificatori forniti da Publisher in Google Ad Manager 360, vedi [documentazione ufficiale di Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso a [!DNL Google Ad Manager 360] connessione, contatta il tuo rappresentante di Adobe e fornisci [!DNL organization ID].

Il [!DNL Google Ad Manager 360] esportazioni di destinazione [!DNL CSV] file nel tuo [!DNL Google Cloud Storage] secchio. Dopo aver esportato [!DNL CSV] file, è necessario importarli nel file [!DNL Google Ad Manager 360] account.

## Specifiche della destinazione {#specifics}

Tieni presente i seguenti dettagli specifici di [!DNL Google Ad Manager 360] destinazioni.

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google e popolati nel file CSV.

## Identità supportate {#supported-identities}

[!DNL This integration] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleziona questa identità di destinazione a cui inviare i tipi di pubblico [!DNL Google Ad Manager 360] |

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
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

L’inserimento nell’elenco Consentiti è obbligatorio prima di impostare la prima [!DNL Google Ad Manager 360] in Platform. Prima di creare la destinazione, assicurati di completare il processo di inserimento nell’elenco Consentiti descritto di seguito.

>[!NOTE]
>
>L&#39;eccezione a questa regola è per esistente [Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) clienti. Se hai già creato una connessione a questa destinazione Google in Audienci Manager, non è necessario ripetere nuovamente la procedura di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

1. Segui i passaggi descritti in [Documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere un Adobe come DMP (Data Management Platform) collegato.
2. In [!DNL Google Ad Manager] , vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Impostazioni globali]** > **[!UICONTROL Impostazioni di rete]**, e abilita **[!UICONTROL Accesso API]** cursore.


## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: stringa alfanumerica di 61 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform.
* **[!UICONTROL Chiave di accesso segreta]**: stringa con codifica base64 di 40 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform.

Per ulteriori informazioni su questi valori, vedere [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica dell’origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Inserisci i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Aggiungi ID pubblico al nome del pubblico"
>abstract="Seleziona questa opzione per fare in modo che il nome del pubblico in Google Ad Manager 360 includa l’ID del pubblico da Experience Platform, come riportato di seguito: `Audience Name (Audience ID)`"

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Nome bucket]**: immetti il nome del [!DNL Google Cloud Storage] bucket da utilizzare per questa destinazione.
* **[!UICONTROL ID account]**: immetti il [!DNL Audience Link ID] dal tuo [!DNL Google] account. Questo è un identificatore specifico associato al tuo [!DNL Google Ad Manager] rete (non la tua [!DNL Network code]). Puoi trovarlo in **[!UICONTROL Admin > Global settings (Amministrazione > Impostazioni globali)]** nel [!DNL Google Ad Manager] di rete.
* **[!UICONTROL Tipo di account]**: seleziona un’opzione, a seconda del [!DNL Google] account:
   * Utilizzare `AdX buyer` per [!DNL Google AdX]
   * Utilizzare `DFP by Google` per [!DNL DoubleClick] per editori
* **[!UICONTROL Aggiungi ID pubblico al nome del pubblico]**: seleziona questa opzione affinché il nome del pubblico in Google Ad Manager 360 includa l’ID del pubblico di un Experience Platform, come segue: `Audience Name (Audience ID)`.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

Nel passaggio di mappatura identità puoi visualizzare le seguenti mappature precompilate:

| Mappatura precompilata | Descrizione |
|---------|----------|
| `ECID` -> `ppid` | Questa è l’unica mappatura precompilata modificabile dall’utente. Puoi selezionare uno qualsiasi degli attributi o degli spazi dei nomi delle identità da Platform e mapparli su `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mappa i nomi degli Experienci Platform di pubblico agli ID del pubblico nella piattaforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica alla piattaforma Google quando rimuovere gli utenti non qualificati dai segmenti. |

Queste mappature sono richieste da [!DNL Google Ad Manager 360] e vengono creati automaticamente da Adobe Experience Platform per tutti [!DNL Google Ad Manager 360] connessioni.

![Immagine dell’interfaccia utente che mostra il passaggio di mappatura per Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Risoluzione dei problemi {#troubleshooting}

Nel caso in cui si verifichino errori durante l’utilizzo di questa destinazione e si debba contattare Adobe o Google, tieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL ID account]**: 87933855
* **[!UICONTROL ID cliente]**: 89690775