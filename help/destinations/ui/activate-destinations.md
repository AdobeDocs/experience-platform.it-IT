---
keywords: attivazione destinazione;attivazione destinazioni;attivazione dati
title: Attivare profili e segmenti su una destinazione
type: Tutorial
seo-title: Attivare profili e segmenti su una destinazione
description: Attiva i dati in Adobe Experience Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
seo-description: Attiva i dati in Adobe Experience Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
translation-type: tm+mt
source-git-commit: d1f357659313aba0811b267598deda9770d946a1
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 0%

---


# Attivare profili e segmenti su una destinazione

Attiva i dati in Adobe Experience Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.

## Prerequisiti {#prerequisites}

Per attivare i dati sulle destinazioni, è necessario che [sia stata collegata correttamente a una destinazione](./connect-destination.md). Se non lo avete già fatto, andate al [catalogo delle destinazioni](../catalog/overview.md), individuate le destinazioni supportate e configurate una o più destinazioni.

## Attivare i dati {#activate-data}

I passaggi nel flusso di lavoro di attivazione variano leggermente tra i tipi di destinazione. Il flusso di lavoro completo per tutti i tipi di destinazione è descritto di seguito.

### Selezionare la destinazione per l&#39;attivazione dei dati in {#select-destination}

Si applica a: Tutte le destinazioni

Nell&#39;interfaccia utente di Adobe Experience Platform, andate a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** e selezionate la destinazione in cui desiderate attivare i segmenti.

![passa alla destinazione](../assets/ui/activate-destinations/connect.png)

Selezionate il nome della destinazione per passare al flusso di lavoro di attivazione.

![activate-flow](../assets/ui/activate-destinations/activate-flow.png)

Se esiste già un flusso di lavoro di attivazione per una destinazione, puoi vedere i segmenti attualmente attivati per la destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi indicati di seguito per modificare i dettagli di attivazione.

Dopo aver selezionato una destinazione, selezionare **[!UICONTROL Activate]**.

### [!UICONTROL Select Segments] step  {#select-segments}

Si applica a: Tutte le destinazioni

![Seleziona il passaggio dei segmenti](../assets/ui/activate-destinations/select-segments-icon.png)

Nel flusso di lavoro **[!UICONTROL Activate destination]**, nella pagina **[!UICONTROL Select Segments]**, selezionare uno o più segmenti da attivare nella destinazione. Selezionare **[!UICONTROL Next]** per passare al passaggio successivo.

![segmenti-a-destinazione](../assets/ui/activate-destinations/email-select-segments.png)

### [!UICONTROL Identity mapping] step  {#identity-mapping}

Si applica a: destinazioni social e destinazione pubblicitaria di Google Customer Match

![Passaggio mappatura identità](../assets/ui/activate-destinations/identity-mapping-icon.png)

Per le destinazioni social, è necessario selezionare gli attributi di origine o gli spazi dei nomi di identità da mappare come identità di destinazione nella destinazione.

#### Esempio: attivazione dei dati sul pubblico in [!DNL Facebook] {#example-facebook}

Questo è un esempio di mappatura identità corretta durante l&#39;attivazione dei dati dell&#39;audience in [!DNL Facebook].

Selezione dei campi di origine:

* Selezionare lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono crittografati.
* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di origine se gli indirizzi e-mail del cliente durante l&#39;inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing e-mail](../catalog/social/facebook.md#email-hashing-requirements).
* Selezionare lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono composti da numeri di telefono non crittografati. [!DNL Platform] eseguirà l&#39;hash dei numeri di telefono per soddisfare  [!DNL Facebook] i requisiti.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di origine se i numeri di telefono sono stati crittografati durante l&#39;inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing dei numeri di telefono](../catalog/social/facebook.md#phone-number-hashing-requirements).
* Selezionare lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Selezionare lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Selezionare lo spazio dei nomi `Custom` come identità di origine se i dati sono composti da altri tipi di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Selezionare gli spazi dei nomi `IDFA` o `GAID` come identità di destinazione quando gli spazi dei nomi di origine sono `IDFA` o `GAID`.
* Selezionare lo spazio dei nomi `Extern_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mapping identità](../assets/ui/activate-destinations/identity-mapping.png)

I dati provenienti dagli spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] al momento dell&#39;attivazione.

I dati origine attributo non vengono automaticamente crittografati. Se il campo di origine contiene attributi non crittografati, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.
![Trasformazione mapping identità](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

#### Esempio: attivazione dei dati sul pubblico in [!DNL Google Customer Match] {#example-gcm}

Questo è un esempio di mappatura identità corretta durante l&#39;attivazione dei dati dell&#39;audience in [!DNL Google Customer Match].

Selezione dei campi di origine:

* Selezionare lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono crittografati.
* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di origine se gli indirizzi e-mail del cliente durante l&#39;inserimento dei dati in [!DNL Platform], in base ai [!DNL Google Customer Match] [requisiti di hashing e-mail](../catalog/social/../advertising/google-customer-match.md).
* Selezionare lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono composti da numeri di telefono non crittografati. [!DNL Platform] eseguirà l&#39;hash dei numeri di telefono per soddisfare  [!DNL Google Customer Match] i requisiti.
* Selezionare lo spazio dei nomi `Phone_SHA256_E.164` come identità di origine se i numeri di telefono sono stati crittografati durante l&#39;inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing dei numeri di telefono](../catalog/social/../advertising/google-customer-match.md).
* Selezionare lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Selezionare lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Selezionare lo spazio dei nomi `Custom` come identità di origine se i dati sono composti da altri tipi di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256_E.164` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256_E.164`.
* Selezionare gli spazi dei nomi `IDFA` o `GAID` come identità di destinazione quando gli spazi dei nomi di origine sono `IDFA` o `GAID`.
* Selezionare lo spazio dei nomi `User_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mapping identità](../assets/ui/activate-destinations/identity-mapping-gcm.png)

I dati provenienti dagli spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] al momento dell&#39;attivazione.

I dati origine attributo non vengono automaticamente crittografati. Se il campo di origine contiene attributi non crittografati, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.
![Trasformazione mapping identità](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

<!-- 
`IDFA` IDs will be mapped to:

* [MADID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#hash) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [mobileId](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#mobileid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md).

Select `GAID` as target identity if your data consists of Android device IDs. `GAID` IDs will be mapped to:

* [MADID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#hash) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [mobileId](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#mobileid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md).

If you are using another ID, such as "Rewards ID" or "Loyalty ID", as primary identity in your schema, you need to map it to the following target identities:

* [EXTERN_ID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#external_identifiers) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [USER_ID](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#userid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md). -->

### **[!UICONTROL Configure]** step  {#configure}

Si applica a: Destinazioni di marketing e-mail e destinazioni di archiviazione cloud

![Configura passaggio](../assets/ui/activate-destinations/configure-icon.png)

Nel passaggio **[!UICONTROL Configure]** potete configurare la pianificazione e i nomi dei file per ciascun segmento da esportare. La configurazione della pianificazione è obbligatoria, ma la configurazione del nome del file è facoltativa.

Per aggiungere una pianificazione per il segmento, selezionare **[!UICONTROL Create schedule]**.

![](../assets/ui/activate-destinations/configure-destination-schedule.png)

Viene visualizzato un profilo che mostra le opzioni per creare la pianificazione dei segmenti.

* **Esportazione** file: Potete esportare file completi o incrementali. Quando si esporta un file completo, viene pubblicata un’istantanea completa di tutti i profili idonei per tale segmento. Quando si esporta un file incrementale, viene pubblicato il delta di profili idonei per tale segmento dall’ultima esportazione.
* **Frequenza**: Se  **[!UICONTROL Export full files]** è selezionata, è possibile esportare  **[!UICONTROL Once]** o  **[!UICONTROL Daily]**. Se è selezionato **[!UICONTROL Export incremental files]**, è possibile esportare solo **[!UICONTROL Daily]**. Se si esporta un file **[!UICONTROL Once]**, il file viene esportato una volta. L&#39;esportazione di un file **[!UICONTROL Daily]** esporta il file ogni giorno dalla data di inizio alla data di fine alle 12:00 UTC (7:00 PM EST) se sono selezionati file completi e alle 12:00 UTC (7:00 AM EST) se sono selezionati file incrementali.
* **Data**: Se  **[!UICONTROL Once]** è selezionata, potete selezionare la data per l&#39;esportazione una tantum. Se è selezionata l&#39;opzione **[!UICONTROL Daily]**, è possibile selezionare le date di inizio e fine per le esportazioni.

![](../assets/ui/activate-destinations/export-full-file.png)

I nomi di file predefiniti sono costituiti dal nome di destinazione, dall’ID segmento e da un indicatore di data e ora. Ad esempio, è possibile modificare i nomi dei file esportati per distinguere tra campagne diverse o per fare in modo che il tempo di esportazione dei dati venga aggiunto ai file.

Selezionate l’icona matita per aprire una finestra modale e modificare i nomi dei file. I nomi dei file possono contenere un massimo di 255 caratteri.

![configura nome file](../assets/ui/activate-destinations/configure-name.png)

Nell’editor dei nomi file potete selezionare diversi componenti da aggiungere al nome file. Impossibile rimuovere il nome di destinazione e l&#39;ID del segmento dai nomi dei file. Oltre a questi, potete aggiungere quanto segue:

* **[!UICONTROL Segment name]**: Potete aggiungere il nome del segmento al nome del file.
* **[!UICONTROL Date and time]**: Selezionate tra l’aggiunta di un  `MMDDYYYY_HHMMSS` formato o di una marca temporale Unix di 10 cifre relativa all’ora in cui i file vengono generati. Scegliete una di queste opzioni se desiderate che i file abbiano un nome file dinamico generato con ogni esportazione incrementale.
* **[!UICONTROL Custom text]**: Aggiungere testo personalizzato ai nomi dei file.

Selezionare **[!UICONTROL Apply changes]** per confermare la selezione.

>[!IMPORTANT]
> 
>Se non si seleziona il componente **[!UICONTROL Date and Time]**, i nomi dei file saranno statici e il nuovo file esportato sovrascriverà il file precedente nel percorso di archiviazione con ogni esportazione. Quando si esegue un processo di importazione periodico da una posizione di archiviazione in una piattaforma di e-mail marketing, questa è l&#39;opzione consigliata.

![modificare le opzioni del nome del file](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

Al termine della configurazione di tutti i segmenti, selezionare **[!UICONTROL Next]** per continuare.

### **[!UICONTROL Segment schedule]** step  {#segment-schedule}

Si applica a: destinazioni pubblicitarie, destinazioni social

![fase di pianificazione del segmento](../assets/ui/activate-destinations/segment-schedule-icon.png)

Nella pagina **[!UICONTROL Segment schedule]** è possibile impostare la data di inizio per l&#39;invio dei dati alla destinazione, nonché la frequenza di invio dei dati alla destinazione.

>[!IMPORTANT]
>
>Per le destinazioni social, devi selezionare l&#39;origine del pubblico in questo passaggio. Puoi passare al passaggio successivo solo dopo aver selezionato una delle opzioni nell’immagine sottostante.

![Facebook Origin of Audience](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>Per Google Customer Match, è necessario fornire il [!UICONTROL App ID] in questo passaggio, quando si attivano i segmenti [!DNL IDFA] o [!DNL GAID].

![enter app id](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

### **[!UICONTROL Scheduling]** step  {#scheduling}

Si applica a: destinazioni di e-mail marketing e archiviazione cloud

![fase di pianificazione del segmento](../assets/ui/activate-destinations/scheduling-icon.png)

Nella pagina **[!UICONTROL Scheduling]** è possibile visualizzare la data di inizio per l&#39;invio dei dati alla destinazione e la frequenza di invio dei dati alla destinazione. Questi valori non possono essere modificati.

### **[!UICONTROL Select attributes]** step  {#select-attributes}

Si applica a: destinazioni di e-mail marketing e archiviazione cloud

![seleziona passaggio attributi](../assets/ui/activate-destinations/select-attributes-icon.png)

Nella pagina **[!UICONTROL Select attributes]**, selezionare **[!UICONTROL Add new field]** e scegliere gli attributi che si desidera inviare alla destinazione.

>[!NOTE]
>
> Adobe Experience Platform precompila la selezione con quattro attributi consigliati e comunemente utilizzati dallo schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Le esportazioni di file variano nei seguenti modi, a seconda che `segmentMembership.status` sia selezionato:
* Se il campo `segmentMembership.status` è selezionato, i file esportati includono i membri **[!UICONTROL Active]** nello snapshot completo iniziale e i membri **[!UICONTROL Active]** e **[!UICONTROL Expired]** nelle esportazioni incrementali successive.
* Se il campo `segmentMembership.status` non è selezionato, i file esportati includono solo i membri **[!UICONTROL Active]** nello snapshot completo iniziale e nelle esportazioni incrementali successive.

![attributi consigliati](../assets/ui/activate-destinations/mark-mandatory.png)

Inoltre, potete contrassegnare attributi diversi come obbligatori. Se un attributo è contrassegnato come obbligatorio, viene impostato in modo che il segmento esportato contenga tale attributo. Di conseguenza, può essere utilizzato come ulteriore forma di filtro. La marcatura di un attributo come obbligatorio è **non** obbligatoria.

È consigliabile che uno degli attributi sia un [identificatore univoco](../../destinations/catalog/email-marketing/overview.md#identity) dallo schema. Per ulteriori informazioni sugli attributi obbligatori, vedi la sezione relativa all&#39;identità nella documentazione [Destinazioni di marketing e-mail](../../destinations/catalog/email-marketing/overview.md#identity).

>[!NOTE]
> 
>Se sono state applicate etichette di utilizzo dei dati a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione avviene alle seguenti condizioni:
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.

>
> 
Ad esempio, se nel campo `person.name.firstName` sono presenti delle etichette di utilizzo dei dati in conflitto con il caso di utilizzo marketing della destinazione, nel passaggio della revisione viene visualizzata una violazione del criterio di utilizzo dei dati. Per ulteriori informazioni, vedere [Governance dei dati in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

### **[!UICONTROL Review]** step  {#review}

Si applica a: tutte le destinazioni

![fase di revisione](../assets/ui/activate-destinations/review-icon.png)

Nella pagina **[!UICONTROL Review]** è possibile visualizzare un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** per modificare le impostazioni, oppure **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedere [Applicazione dei criteri](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione della documentazione sulla governance dei dati.

![violazione dei criteri di dati](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](../assets/ui/activate-destinations/confirm-selection.png)

## Modifica attivazione {#edit-activation}

Per modificare i flussi di attivazione esistenti in Adobe Experience Platform, effettuate le seguenti operazioni:

1. Selezionare **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, quindi fare clic sulla scheda **[!UICONTROL Browse]** e quindi sul nome della destinazione.
2. Selezionate **[!UICONTROL Edit activation]** nella barra a destra per cambiare i segmenti da inviare alla destinazione.

## Verificare che l&#39;attivazione del segmento sia stata eseguita correttamente{#verify-activation}

### Destinazioni di marketing e-mail e destinazioni di archiviazione cloud {#esp-and-cloud-storage}

Per le destinazioni di e-mail marketing e di archiviazione cloud, Adobe Experience Platform crea un file `.csv` o `.txt` delimitato da tabulazioni nel percorso di archiviazione fornito. È previsto che ogni giorno venga creato un nuovo file nel percorso di archiviazione. Il formato predefinito del file è:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

È possibile modificare il formato del file. Per ulteriori informazioni, vai al passaggio [Configura](#configure) per le destinazioni di archiviazione cloud e di marketing tramite e-mail.

Con il formato di file predefinito, i file che si riceverebbero per tre giorni consecutivi potrebbero essere simili al seguente:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presenza di questi file nel percorso di memorizzazione conferma l’avvenuta riuscita dell’attivazione. Per comprendere la struttura dei file esportati, è possibile [scaricare un file .csv di esempio](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Questo file di esempio include gli attributi di profilo `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` e `personalEmail.address`.

### Destinazioni pubblicitarie

Controlla il tuo account nella rispettiva destinazione pubblicitaria a cui stai attivando i tuoi dati. Se l&#39;attivazione ha avuto esito positivo, i tipi di pubblico vengono popolati nella piattaforma pubblicitaria.

### Destinazioni social network

Per [!DNL Facebook], un&#39;attivazione riuscita implica la creazione di un&#39;audience [!DNL Facebook] personalizzata a livello di programmazione in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L&#39;integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta i backfill storici del pubblico. Tutte le qualifiche del segmento storico vengono inviate a [!DNL Facebook] quando si attivano i segmenti nella destinazione.

## Disattiva attivazione {#disable-activation}

Per disattivare un flusso di attivazione esistente, effettuate le seguenti operazioni:

1. Selezionare **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, quindi fare clic sulla scheda **[!UICONTROL Browse]** e quindi sul nome della destinazione.
2. Fate clic sul controllo **[!UICONTROL Enabled]** nella barra a destra per modificare lo stato del flusso di attivazione.
3. Nella finestra **Aggiorna stato flusso dati**, selezionare **Conferma** per disattivare il flusso di attivazione.
