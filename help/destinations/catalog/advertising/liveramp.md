---
title: (Alfa) [!DNL LiveRamp SFTP] connection
description: Scopri come utilizzare il connettore LiveRamp per integrare i tipi di pubblico da Adobe Real-time Customer Data Platform a LiveRamp Connect.
hidefromtoc: true
hide: true
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: d7625018b7b36d8e9516f7884fc00b726d391103
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 3%

---

# (Alfa) [!DNL LiveRamp - SFTP] connection {#liveramp-destination}

Utilizzare la connessione LiveRamp ai tipi di pubblico integrati da Adobe Real-time Customer Data Platform a [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Questa connessione di destinazione è attualmente in fase alfa e disponibile solo per una selezione limitata di clienti. La funzionalità e la documentazione sono soggette a modifiche.</p>
&gt;<p>La versione finale di questa connessione di destinazione potrebbe richiedere la migrazione dei clienti.</p>


## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL LiveRamp SFTP] destinazione, ecco un esempio di caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

In qualità di addetto al marketing, voglio inviare tipi di pubblico da Adobe Experience Platform alle identità integrate [!DNL LiveRamp Connect] in modo da poter eseguire il targeting degli utenti su [!DNL CTV] piattaforme, utilizzando [!DNL Ramp ID] identificatore .

## Prerequisiti {#prerequisites}

La [!DNL LiveRamp - SFTP] file di esportazione delle connessioni utilizzando [SFTP di LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) archiviazione.

Prima di poter inviare dati da Experience Platform a [!DNL LiveRamp SFTP], è necessario [!DNL LiveRamp] credenziali. Rivolgiti al tuo [!DNL LiveRamp] rappresentante per ottenere le tue credenziali, se non le hai già.

## Identità supportate {#supported-identities}

LiveRamp SFTP supporta l’attivazione di identità come identificatori basati su PII, identificatori noti e ID personalizzati, descritti nella [Documentazione LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

In [fase di mappatura](#map) del flusso di lavoro di attivazione, devi definire le mappature di destinazione come attributi personalizzati.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nel [!DNL LiveRamp SFTP] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Batch giornaliero]** | Poiché i profili vengono aggiornati in Experience Platform in base alla valutazione dei segmenti, i profili (identità) vengono aggiornati una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

**Autenticazione SFTP con password** {#sftp-password}

![Schermata di esempio che mostra come eseguire l’autenticazione nella destinazione utilizzando SFTP con password](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Nome utente]**: Nome utente per il tuo [!DNL LiveRamp SFTP] posizione di archiviazione.
* **[!UICONTROL Password]**: La password [!DNL LiveRamp SFTP] posizione di archiviazione.
* **[!UICONTROL Chiave di crittografia PGP/GPG]**: Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente. Se fornisci una chiave di crittografia, devi anche fornire un **[!UICONTROL ID della sottochiave di crittografia]** in [dettagli di destinazione](#destination-details) sezione .

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP con autenticazione a chiave SSH** {#sftp-ssh}

![Schermata di esempio che mostra come eseguire l’autenticazione nella destinazione utilizzando la chiave SSH](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Nome utente]**: Nome utente per il tuo [!DNL LiveRamp SFTP] posizione di archiviazione.
* **[!UICONTROL Chiave SSH]**: Il privato [!DNL SSH] chiave utilizzata per accedere al [!DNL LiveRamp SFTP] posizione di archiviazione. La chiave privata deve essere formattata come [!DNL Base64]Stringa con codifica -e non deve essere protetta da password.

   * Per collegare il [!DNL SSH] chiave per [!DNL LiveRamp SFTP] server, è necessario inviare un ticket [!DNL LiveRamp]Portale di supporto tecnico e specifica la chiave pubblica. Per ulteriori informazioni, consulta la sezione [Documentazione LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Chiave di crittografia PGP/GPG]**: Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Se fornisci una chiave di crittografia, devi anche fornire un **[!UICONTROL ID della sottochiave di crittografia]** in [dettagli di destinazione](#destination-details) sezione . Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Compila i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID sottochiave di crittografia"
>abstract="ID della sottochiave utilizzato per la crittografia, in base alla chiave di crittografia pubblica LiveRamp. Questo campo è obbligatorio se hai fornito una chiave di crittografia nel passaggio di autenticazione."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Scopri come ottenere l’ID della sottochiave"

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dell’interfaccia utente di Platform che mostra come inserire i dettagli della destinazione](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Percorso cartella]**: Il percorso del [!DNL LiveRamp] `uploads` sottocartella che ospiterà i file esportati. La `uploads` Il prefisso viene aggiunto automaticamente al percorso della cartella.
   * Ad esempio, per esportare i file in `uploads/my_export_folder`, digita in `my_export_folder` in **[!UICONTROL Percorso cartella]** campo .
* **[!UICONTROL Formato di compressione]**: Selezionare il tipo di compressione che l&#39;Experience Platform deve utilizzare per i file esportati. Le opzioni disponibili sono **[!UICONTROL GZIP]** o **[!UICONTROL Nessuno]**.
* **[!UICONTROL ID della sottochiave di crittografia]**: La sottochiave utilizzata per la crittografia, in base alla variabile [!DNL LiveRamp] chiave di crittografia pubblica. Questo campo è obbligatorio se è stata fornita una chiave di crittografia nel [autenticazione](#authenticate) passo. Consulta la sezione [!DNL LiveRamp] [documentazione di crittografia](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) per scoprire come ottenere l’ID della sottochiave.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Pianificazione {#scheduling}

In [!UICONTROL Pianificazione] crea una pianificazione per l’esportazione per ciascun segmento, con le impostazioni mostrate di seguito.

>[!IMPORTANT]
>
>Tutti i segmenti attivati a questa destinazione devono essere configurati con la stessa pianificazione, come mostrato di seguito.

* **[!UICONTROL Opzioni di esportazione file]**: [!UICONTROL Esportare file completi]. [Esportazioni incrementali di file](../../ui/activate-batch-profile-destinations.md#export-incremental-files) al momento non sono supportati per [!DNL LiveRamp] destinazione.
* **[!UICONTROL Frequenza]**: [!UICONTROL Giornaliero]
* Imposta il tempo di esportazione su **[!UICONTROL Dopo la valutazione dei segmenti]**. Esportazioni di segmenti programmate e [esportazioni di file on-demand](../../ui/export-file-now.md) al momento non sono supportati per [!DNL LiveRamp] destinazione.
* **[!UICONTROL Data]**: Seleziona gli orari di inizio e fine dell’esportazione come desideri.

![Schermata dell’interfaccia utente della piattaforma che mostra la fase di pianificazione dei segmenti.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

Il nome file esportato non è attualmente configurabile dall&#39;utente. Tutti i file esportati in [!DNL LiveRamp SFTP] Le destinazioni vengono denominate automaticamente in base al seguente modello:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Schermata dell’interfaccia utente della piattaforma che mostra il modello di nome file esportato.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Ad esempio, il nome di un file esportato per un&#39;organizzazione denominata [!DNL Luma] potrebbe essere simile al seguente:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** puoi selezionare gli attributi e le identità da esportare per i profili.

>[!IMPORTANT]
>
>Questa destinazione supporta l’attivazione di uno spazio dei nomi dell’identità sorgente per ogni flusso di attivazione. Se devi esportare più spazi dei nomi di identità, come `Email` e `Phone`, devi [creare un flusso di attivazione separato](../../ui/activate-batch-profile-destinations.md) per ogni identità.

In **[!UICONTROL Mappatura]** step, **[!UICONTROL Campo di destinazione]** la mappatura definisce il nome dell’intestazione della colonna nel file CSV esportato. Puoi modificare le intestazioni di colonna CSV nel file esportato con qualsiasi nome descrittivo, fornendo un nome personalizzato per il **[!UICONTROL Campo di destinazione]**.

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la schermata Mapping (Mappatura).](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM da mappare, oppure scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità da mappare alla destinazione.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la schermata Mappatura origine.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. In **[!UICONTROL Selezionare il campo di destinazione]** immettere il nome dell&#39;attributo a cui si desidera mappare il campo di origine selezionato. Il nome dell’attributo qui definito si riflette nel file CSV esportato come intestazione di colonna.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la schermata di mappatura della destinazione.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Puoi anche immettere il nome dell’attributo digitandolo direttamente nel **[!UICONTROL Campo di destinazione]**.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la schermata di mappatura della destinazione.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Dopo aver aggiunto tutte le mappature desiderate, seleziona **[!UICONTROL Successivo]** e terminare il flusso di lavoro di attivazione.

## Esportazione di dati / Convalida esportazione dati {#exported-data}

I dati vengono esportati in [!DNL LiveRamp SFTP] percorso di archiviazione configurato come file CSV.

Quando si esportano file in [!DNL LiveRamp SFTP] destinazione, Platform genera un file CSV per ogni [ID criterio unione](../../../profile/merge-policies/overview.md).

Ad esempio, prendiamo in considerazione i seguenti segmenti:

* Segmento A (Criteri di unione 1)
* Segmento B (Criteri di unione 2)
* Segmento C (Criteri di unione 1)
* Segmento D (Criteri di unione 1)

Platform esporta due file CSV in [!DNL LiveRamp SFTP]:

* Un file CSV contenente i segmenti A, C e D;
* Un file CSV contenente il segmento B.

I file CSV esportati contengono profili con gli attributi selezionati e lo stato del segmento corrispondente, su colonne separate, con il nome dell’attributo e gli ID del segmento come intestazioni di colonna.

I profili inclusi nei file esportati possono corrispondere a uno dei seguenti stati di qualificazione dei segmenti:

* `Active`: Il profilo è attualmente qualificato per il segmento.
* `Expired`: Il profilo non è più qualificato per il segmento, ma in passato è qualificato.
* `""`(stringa vuota): Il profilo non è mai qualificato per il segmento.


Ad esempio, un file CSV esportato con un file `email` l’attributo e 3 segmenti possono avere un aspetto simile al seguente:

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Poiché Platform genera un file CSV per ogni [ID criterio unione](../../../profile/merge-policies/overview.md), genera anche un’esecuzione separata del flusso di dati per ogni ID criterio di unione.

Ciò significa che **[!UICONTROL Identità attivate]** e **[!UICONTROL Profili ricevuti]** nelle metriche [esecuzioni di dataflow](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) Le pagine vengono aggregate per ogni gruppo di segmenti che utilizzano lo stesso criterio di unione, anziché essere visualizzate per ciascun segmento.

A seguito della generazione di un flusso di dati per un gruppo di segmenti che utilizzano lo stesso criterio di unione, i nomi dei segmenti non vengono visualizzati nella [dashboard di monitoraggio](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Schermata dell’interfaccia utente di Experience Platform che mostra le identità attivate dalla metrica.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Carica i dati esportati in LiveRamp {#upload-to-liveramp}

Dopo l’esportazione dei dati in [!DNL LiveRamp - SFTP] , è necessario caricare i dati nel [!DNL LiveRamp] piattaforma.

Per ulteriori informazioni su come caricare i file da [!DNL LiveRamp - SFTP] archiviazione su un [!DNL LiveRamp] pubblico, consulta la seguente documentazione: [Considerazioni sul caricamento del primo file su un pubblico](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per maggiori dettagli su come configurare l&#39;archiviazione SFTP LiveRamp, vedi la [documentazione ufficiale](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
