---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci pubblicitari sui loro siti web, tramite video e nelle app per dispositivi mobili.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: ec4d064f90348f9eafb1d0fe4b9df5e102295507
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 2%

---

# (Beta) [!DNL Google Ad Manager 360] connection

## Panoramica {#overview}

La [!DNL Google Ad Manager 360] la connessione abilita il caricamento batch per [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], tramite [!DNL Google Cloud Storage].

Per ulteriori dettagli sul funzionamento degli identificatori forniti dall&#39;editore in Google Ad Manager 360, consulta la sezione [documentazione ufficiale di Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso al [!DNL Google Ad Manager 360] contatta il tuo rappresentante di Adobe e fornisci [!DNL IMS Organization ID].

La [!DNL Google Ad Manager 360] esportazioni di destinazione [!DNL CSV] file nel tuo [!DNL Google Cloud Storage] secchio. Una volta esportato il [!DNL CSV] file, è necessario importarli nel [!DNL Google Ad Manager 360] conto.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici per [!DNL Google Ad Manager 360] destinazioni.

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google e compilati nel file CSV.

## Identità supportate {#supported-identities}

[!DNL This integration] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleziona questa identità target a cui inviare i tipi di pubblico [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata Seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

L’inserimento nell’elenco Consentiti è obbligatorio prima di configurare il primo [!DNL Google Ad Manager 360] in Platform. Prima di creare la destinazione, completa il processo di inserimento nell’elenco Consentiti descritto di seguito.

>[!NOTE]
>
>L&#39;eccezione a questa regola è per esistente [Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) clienti. Se hai già creato una connessione a questa destinazione Google in Audience Manager, non è necessario rivedere il processo di inserimento nell’elenco Consentiti e procedere con i passaggi successivi.

1. Segui i passaggi descritti in [Documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere Adobe come piattaforma di gestione dati (DMP, Data Management Platform) collegata.
2. In [!DNL Google Ad Manager] interfaccia, vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Impostazioni globali]** > **[!UICONTROL Impostazioni di rete]** e abilita **[!UICONTROL Accesso API]** cursore.


## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il tuo [!DNL Google Cloud Storage] a Platform.
* **[!UICONTROL Chiave di accesso segreta]**: Una stringa con codifica base64 a 40 caratteri utilizzata per l&#39;autenticazione della [!DNL Google Cloud Storage] a Platform.

Per ulteriori informazioni su questi valori, consulta la sezione [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il tuo ID chiave di accesso e la chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica di origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Percorso cartella]**: Immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Nome blocco]**: Immetti il nome della [!DNL Google Cloud Storage] bucket utilizzato da questa destinazione.
* **[!UICONTROL ID account]**: Inserisci il tuo [!DNL Audience Link ID] dal [!DNL Google] conto. Questo è un identificatore specifico associato al [!DNL Google Ad Manager] rete (non il [!DNL Network code]). Puoi trovarlo in **[!UICONTROL Amministratore > Impostazioni globali]** in [!DNL Google Ad Manager] interfaccia.
* **[!UICONTROL Tipo di conto]**: Seleziona un’opzione a seconda del [!DNL Google] account:
   * Utilizzo `AdX buyer` per [!DNL Google AdX]
   * Utilizzo `DFP by Google` per [!DNL DoubleClick] per gli editori

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

Nel passaggio di mappatura identità , puoi vedere le seguenti mappature precompilate:

| Mappatura precompilata | Descrizione |
|---------|----------|
| `ECID` -> `ppid` | Questa è l’unica mappatura precompilata modificabile dall’utente. Puoi selezionare uno qualsiasi degli attributi o dei namespace di identità da Platform e mapparli su `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mappa i nomi dei segmenti di Experience Platform agli ID dei segmenti nella piattaforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica alla piattaforma Google quando rimuovere utenti squalificati dai segmenti. |

Queste mappature sono richieste da [!DNL Google Ad Manager 360] e vengono create automaticamente da Adobe Experience Platform per tutti [!DNL Google Ad Manager 360] connessioni.

![Immagine dell’interfaccia utente che mostra il passaggio di mappatura per Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il tuo [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Risoluzione dei problemi {#troubleshooting}

Nel caso in cui si verifichino errori durante l&#39;utilizzo di questa destinazione e sia necessario contattare Adobe o Google, mantieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL ID account]**: 87933855
* **[!UICONTROL ID cliente]**: 89690775