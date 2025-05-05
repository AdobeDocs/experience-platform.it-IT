---
title: (Beta) [!DNL Google Ad Manager 360] connessione
description: Google Ad Manager 360 è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci sui loro siti web, tramite video e app mobili.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 6%

---

# (Beta) Connessione [!DNL Google Ad Manager 360]

>[!IMPORTANT]
>
> Google sta rilasciando modifiche all&#39;API [Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html?lang=it) e all&#39;API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) per supportare i requisiti relativi alla conformità e al consenso definiti nel [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_it) (DMA) nell&#39;Unione Europea ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso è attiva dal 6 marzo 2024.
><br/>
>Per aderire alla politica di consenso degli utenti dell’UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso degli utenti finali durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi del regolamento DMA dell’Unione Europea.
><br/>
>I clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non devono intraprendere alcuna azione.
><br/>
>I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare le funzionalità [segment definition](../../../segmentation/home.md#segment-definitions) all&#39;interno di [Segment Builder](../../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati e continuare a utilizzare senza interruzioni le destinazioni Real-Time CDP Google esistenti.

La connessione [!DNL Google Ad Manager 360] abilita il caricamento batch per [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360] tramite [!DNL Google Cloud Storage].

Per ulteriori dettagli sul funzionamento degli identificatori forniti da Publisher in Google Ad Manager 360, consulta la [documentazione ufficiale di Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Questa destinazione è attualmente in Beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l&#39;accesso alla connessione [!DNL Google Ad Manager 360], contatta il tuo rappresentante Adobe e fornisci [!DNL organization ID].

La [!DNL Google Ad Manager 360] destinazione esporta [!DNL CSV] i file nel tuo [!DNL Google Cloud Storage] bucket. Una volta esportati i [!DNL CSV] file, è necessario importarli nel account [!DNL Google Ad Manager 360] .

## Specifiche della destinazione {#specifics}

Prendere nota dei dettagli seguenti specifici per [!DNL Google Ad Manager 360] destinazioni.

* Questa destinazione non supporta attualmente la funzionalità [esporta file on-demand](../../ui/export-file-now.md).
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google e popolati nel file CSV.

## Identità supportate {#supported-identities}

[!DNL This integration] supporta l&#39;attivazione delle identità descritte nella tabella seguente.

| Identità Target | Descrizione | Considerazioni |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selezionare questa identità di destinazione per inviare tipi di pubblico a [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata Seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

L&#39;inserimento nell&#39;elenco Consentiti è obbligatorio prima di configurare la prima destinazione [!DNL Google Ad Manager 360] in Experience Platform. Prima di creare la destinazione, assicurati di completare il processo di inserimento nell’elenco Consentiti descritto di seguito.

>[!NOTE]
>
>L&#39;eccezione a questa regola è per i clienti [Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) esistenti. Se hai già creato una connessione a questa destinazione di Google in Audience Manager, non è necessario eseguire nuovamente il processo di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

1. Segui i passaggi descritti nella [documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere Adobe come piattaforma di gestione dati collegata (DMP).
2. Nell&#39;interfaccia [!DNL Google Ad Manager], vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Impostazioni globali]** > **[!UICONTROL Impostazioni di rete]** e abilita il cursore **[!UICONTROL Accesso API]**.


## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: stringa alfanumerica di 61 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Experience Platform.
* **[!UICONTROL Chiave di accesso segreta]**: una stringa con codifica base64 di 40 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Experience Platform.

Per ulteriori informazioni su questi valori, consulta la guida delle [chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica sull&#39;origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Aggiungi ID del pubblico al nome del pubblico"
>abstract="Seleziona questa opzione per fare in modo che il nome del pubblico in questa destinazione includa l’ID del pubblico da Experience Platform, come riportato di seguito: `Audience Name (Audience ID)`"

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Percorso cartella]**: immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Nome bucket]**: immettere il nome del bucket [!DNL Google Cloud Storage] da utilizzare per questa destinazione.
* **[!UICONTROL ID account]**: immetti [!DNL Audience Link ID] dal tuo account [!DNL Google]. Questo è un identificatore specifico associato alla rete [!DNL Google Ad Manager] (non alla tua [!DNL Network code]). Puoi trovarlo in **[!UICONTROL Impostazioni globali di amministrazione >]** nell&#39;interfaccia [!DNL Google Ad Manager] .
* **[!UICONTROL Tipo di]** account: seleziona un&#39;opzione, a seconda [!DNL Google] account:
   * Usa `AdX buyer` per [!DNL Google AdX]
   * Usa `DFP by Google` per [!DNL DoubleClick] per gli editori
* **[!UICONTROL Aggiungi ID pubblico al nome del pubblico]**: seleziona questa opzione per fare in modo che il nome del pubblico in Google Ad Manager 360 includa l&#39;ID pubblico da Experience Platform, come segue: `Audience Name (Audience ID)`.

### Abilitare gli avvisi {#enable-alerts}

È possibile abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la destinazione. Seleziona un avviso dall&#39;elenco a cui iscriverti per ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida sulla [sottoscrizione agli avvisi relativi alle destinazioni utilizzando il interfaccia](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, selezionare **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[[!UICONTROL autorizzazioni]](/help/access-control/home.md#permissions) Visualizza Destinazioni&rbrack;**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Profili]** Visualizza e **[!UICONTROL Segmenti]** &lbrack;Visualizza accesso controllo. Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

Nel passaggio di mappatura identità puoi visualizzare le seguenti mappature precompilate:

| Mappatura precompilata | Descrizione |
|---------|----------|
| `ECID` -> `ppid` | Questa è l&#39;unica mappatura precompilata utente modificabile. È possibile selezionare qualsiasi spazio dei nomi di attributi o identità da Experience Platform e mapparli a `ppid`. |
| `metadata.segment.alias` -> `list_id` | Associa i nomi del pubblico di Experience Platform agli ID del pubblico nella piattaforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica alla piattaforma Google quando rimuovere gli utenti squalificati dai segmenti. |

Queste mappature sono richieste e [!DNL Google Ad Manager 360] create automaticamente da Adobe Experience Platform per tutte le [!DNL Google Ad Manager 360] connessioni.

![interfaccia&#39;immagine che mostra il passaggio di mappatura per Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il bucket [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Risoluzione dei problemi {#troubleshooting}

Nel caso riscontrassi errori durante l’utilizzo di questa destinazione e avessi bisogno di contattare Adobe o Google, tieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL ID account]**: 87933855
* **[!UICONTROL ID cliente]**: 89690775