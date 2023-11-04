---
title: LiveRamp - Connessione di onboarding
description: Scopri come utilizzare il connettore LiveRamp per integrare i tipi di pubblico da Adobe Real-time Customer Data Platform a LiveRamp Connect.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: 9122159b3facf7952e6072d0b9e6f8d8d7d7c99c
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 4%

---

# Connessione [!DNL LiveRamp - Onboarding] {#liveramp-onboarding}

Utilizza il [!DNL LiveRamp - Onboarding] connessione ai tipi di pubblico onboarding da Adobe Real-time Customer Data Platform a [!DNL LiveRamp Connect].

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL LiveRamp - Onboarding] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

In qualità di esperto di marketing, voglio inviare tipi di pubblico da Adobe Experience Platform alle identità onboarding in [!DNL LiveRamp Connect] in modo da poter eseguire il targeting degli utenti su dispositivi mobili, open web, social e [!DNL CTV] piattaforme, utilizzando [!DNL Ramp ID] identificatore.

## Prerequisiti {#prerequisites}

Il [!DNL LiveRamp - Onboarding] connessione esporta file tramite [SFTP di LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) archiviazione.

Prima di poter inviare dati da Experienci Platform a [!DNL LiveRamp - Onboarding], è necessario [!DNL LiveRamp] credenziali. Contatta il tuo [!DNL LiveRamp] per ottenere le credenziali, se non le si dispone già.

## Identità supportate {#supported-identities}

[!DNL LiveRamp - Onboarding] supporta l’attivazione di identità come identificatori basati su PII, identificatori noti e ID personalizzati, descritti nella sezione [Documentazione di LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

In [passaggio di mappatura](#map) del flusso di lavoro di attivazione, devi definire le mappature target come attributi personalizzati.

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
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati in [!DNL LiveRamp - Onboarding] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Batch giornaliero]** | Poiché i profili vengono aggiornati in Experienci Platform in base alla valutazione del pubblico, i profili (identità) vengono aggiornati una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

**Autenticazione SFTP con password** {#sftp-password}

![Schermata di esempio che mostra come autenticare nella destinazione utilizzando SFTP con password](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Nome utente]**: nome utente per il [!DNL LiveRamp - Onboarding] percorso di archiviazione.
* **[!UICONTROL Password]**: password per il [!DNL LiveRamp - Onboarding] percorso di archiviazione.
* **[!UICONTROL Chiave di crittografia PGP/GPG]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.
  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL ID sottochiave]**:Se si fornisce una chiave di crittografia, è necessario fornire anche una crittografia **[!UICONTROL ID sottochiave]**. Consulta la [!DNL LiveRamp] [documentazione sulla crittografia](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) per scoprire come ottenere l’ID della sottochiave.

**SFTP con autenticazione della chiave SSH** {#sftp-ssh}

![Schermata di esempio che mostra come autenticare nella destinazione utilizzando la chiave SSH](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Nome utente]**: nome utente per il [!DNL LiveRamp - Onboarding] percorso di archiviazione.
* **[!UICONTROL Chiave SSH]**: privato [!DNL SSH] chiave utilizzata per accedere al [!DNL LiveRamp - Onboarding] percorso di archiviazione. La chiave privata deve essere formattata come [!DNL Base64]Stringa con codifica -e non deve essere protetta da password.

   * Per collegare [!DNL SSH] chiave per [!DNL LiveRamp - Onboarding] server, è necessario inviare un ticket tramite [!DNL LiveRamp]e fornisce la chiave pubblica. Per ulteriori informazioni, consulta [Documentazione di LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Chiave di crittografia PGP/GPG]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.
  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL ID sottochiave]**:Se si fornisce una chiave di crittografia, è necessario fornire anche una crittografia **[!UICONTROL ID sottochiave]**. Consulta la [!DNL LiveRamp] [documentazione sulla crittografia](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) per scoprire come ottenere l’ID della sottochiave.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID sottochiave di crittografia"
>abstract="ID della sottochiave utilizzato per la crittografia, in base alla chiave di crittografia pubblica LiveRamp. Questo campo è obbligatorio se hai fornito una chiave di crittografia nel passaggio di autenticazione."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Scopri come ottenere l’ID della sottochiave"

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dell’interfaccia utente di Platform che mostra come inserire i dettagli per la destinazione](../../assets/catalog/advertising/liveramp-onboarding/liveramp-connection-details.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Percorso cartella]**: percorso di [!DNL LiveRamp] `uploads` sottocartella che ospiterà i file esportati. Il `uploads` il prefisso viene aggiunto automaticamente al percorso della cartella. [!DNL LiveRamp] consiglia di creare una sottocartella dedicata per le consegne da Adobe Real-Time CDP per mantenere i file separati da tutti gli altri feed esistenti e garantire il corretto funzionamento di tutta l’automazione.
   * Ad esempio, se desideri esportare i file in `uploads/my_export_folder`, digitare `my_export_folder` nel **[!UICONTROL Percorso cartella]** campo.
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experienci Platform deve utilizzare per i file esportati. Le opzioni disponibili sono **[!UICONTROL GZIP]** o **[!UICONTROL Nessuno]**.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Pianificazione {#scheduling}

In [!UICONTROL Pianificazione] crea una pianificazione di esportazione per ogni pubblico, con le impostazioni mostrate di seguito.

* **[!UICONTROL Opzioni di esportazione file]**: [!UICONTROL Esporta file completi]. [Esportazioni file incrementali](../../ui/activate-batch-profile-destinations.md#export-incremental-files) non sono attualmente supportati per [!DNL LiveRamp] destinazione.
* **[!UICONTROL Frequenza]**: [!UICONTROL Giornaliero]
* **[!UICONTROL Data]**: seleziona l’ora di inizio e di fine dell’esportazione come desideri.

![Schermata dell’interfaccia utente di Platform che mostra il passaggio di pianificazione del pubblico.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

Il nome del file esportato non è attualmente configurabile dall&#39;utente. Tutti i file esportati in [!DNL LiveRamp - Onboarding] La destinazione viene automaticamente denominata in base al seguente modello:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Schermata dell’interfaccia utente di Platform che mostra il modello di nome file esportato.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

Ad esempio, il nome di un file esportato per un’organizzazione denominata [!DNL Luma] potrebbe assomigliare a questo:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** passaggio, puoi selezionare gli attributi e le identità da esportare per i profili.

>[!IMPORTANT]
>
>Questa destinazione supporta l’attivazione di uno spazio dei nomi dell’identità di origine per ogni flusso di attivazione. Se devi esportare più spazi dei nomi di identità, come `Email` e `Phone`, è necessario [creare un flusso di attivazione separato](../../ui/activate-batch-profile-destinations.md) per ogni identità.

In **[!UICONTROL Mappatura]** passaggio, il **[!UICONTROL Campo di destinazione]** la mappatura definisce il nome dell’intestazione di colonna nel file CSV esportato. Puoi modificare le intestazioni di colonna CSV nel file esportato con qualsiasi nome descrittivo, fornendo un nome personalizzato per il file **[!UICONTROL Campo di destinazione]**.

>[!IMPORTANT]
>
>Per eventuali modifiche apportate ai campi di destinazione dopo la consegna iniziale del file a [!DNL LiveRamp], notifica il tuo [!DNL LiveRamp] team dell’account o [invia un ticket al supporto LiveRamp](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) per garantire che le modifiche vengano applicate al processo di automazione.

1. In **[!UICONTROL Mappatura]** passaggio, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Viene visualizzata una nuova riga di mappatura.

   ![Experience Platform di schermate dell’interfaccia utente che mostrano la schermata Mappatura.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. In **[!UICONTROL Seleziona campo di origine]** finestra, scegli la **[!UICONTROL Seleziona attributi]** e selezionare l&#39;attributo XDM da mappare, oppure scegliere il **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona un’identità da mappare alla destinazione.

   ![Experience Platform di schermate dell’interfaccia utente che mostrano la schermata Mappatura sorgente.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. In **[!UICONTROL Seleziona campo di destinazione]** immettere il nome dell&#39;attributo che si desidera associare al campo di origine selezionato. Il nome dell’attributo qui definito si rifletterà nel file CSV esportato come intestazione di colonna.

   ![Experience Platform di schermate dell’interfaccia utente che mostrano la schermata Mappatura target.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   È inoltre possibile immettere il nome dell&#39;attributo digitandolo direttamente nel **[!UICONTROL Campo di destinazione]**.

   ![Experience Platform di schermate dell’interfaccia utente che mostrano la schermata Mappatura target.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Dopo aver aggiunto tutte le mappature desiderate, seleziona **[!UICONTROL Successivo]** e terminare il flusso di lavoro di attivazione.

## Dati esportati / Convalida esportazione dati {#exported-data}

I dati vengono esportati in [!DNL LiveRamp - Onboarding] percorso di archiviazione configurato come file CSV.

Durante l&#39;esportazione di file in [!DNL LiveRamp - Onboarding] di destinazione, Platform genera un file CSV per ogni [ID criterio di unione](../../../profile/merge-policies/overview.md).

Ad esempio, prendiamo in considerazione i seguenti tipi di pubblico:

* Pubblico A (criterio di unione 1)
* Pubblico B (criterio di unione 2)
* Pubblico C (criterio di unione 1)
* Pubblico D (criterio di unione 1)

Platform esporterà due file CSV in [!DNL LiveRamp - Onboarding]:

* Un file CSV contenente i tipi di pubblico A, C e D;
* Un file CSV contenente il pubblico B.

I file CSV esportati contengono profili con gli attributi selezionati e lo stato del pubblico corrispondente, in colonne separate, con il nome dell’attributo e `audience_namespace:audience_ID` coppie come intestazioni di colonna, come mostrato nell’esempio seguente:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

I profili inclusi nei file esportati possono corrispondere a uno dei seguenti stati di qualificazione del pubblico:

* `Active`: il profilo è attualmente qualificato per il pubblico.
* `Expired`: il profilo non è più qualificato per il pubblico, ma lo è già stato in passato.
* `""`(stringa vuota): il profilo non è mai qualificato per il pubblico.

Ad esempio, un file CSV esportato con `email` , due tipi di pubblico provenienti dall&#39;Experience Platform [Servizio di segmentazione](../../../segmentation/home.md), e uno [importato](../../../segmentation/ui/overview.md#importing-an-audience) pubblico esterno, potrebbe presentarsi così:

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Nell’esempio precedente, il `ups_aa2e3d98-974b-4f8b-9507-59f65b6442df` e `ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` descrivono i tipi di pubblico provenienti dal servizio di segmentazione, mentre `CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e` descrive un pubblico importato in Platform come [caricamento personalizzato](../../../segmentation/ui/overview.md#importing-an-audience).

Poiché Platform genera un file CSV per ogni [ID criterio di unione](../../../profile/merge-policies/overview.md), genera anche un flusso di dati separato eseguito per ogni ID del criterio di unione.

Ciò significa che **[!UICONTROL Identità attivate]** e **[!UICONTROL Profili ricevuti]** metriche in [il flusso di dati viene eseguito](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) Le pagine vengono aggregate per ogni gruppo di tipi di pubblico che utilizzano lo stesso criterio di unione, anziché essere visualizzate per ogni pubblico.

In seguito alla generazione del flusso di dati per un gruppo di tipi di pubblico che utilizzano lo stesso criterio di unione, i nomi dei tipi di pubblico non vengono visualizzati in [dashboard di monitoraggio](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Screeshot dell’interfaccia utente di Experience Platform che mostra la metrica delle identità attivate.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Caricare i dati esportati su LiveRamp {#upload-to-liveramp}

Dopo che i dati sono stati esportati correttamente in [!DNL LiveRamp - Onboarding] archiviazione, devi caricare i dati in [!DNL LiveRamp] piattaforma.

Per ulteriori informazioni su come caricare i file da [!DNL LiveRamp - Onboarding] archiviazione in un [!DNL LiveRamp] pubblico, consulta la seguente documentazione: [Considerazioni durante il caricamento del primo file in un pubblico](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli su come configurare [!DNL LiveRamp - Onboarding] di archiviazione, vedere [documentazione ufficiale](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
