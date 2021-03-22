---
keywords: attivare destinazione;attivare destinazioni;attivare dati
title: Attivare profili e segmenti in una destinazione
type: Tutorial
seo-title: Attivare profili e segmenti in una destinazione
description: Attiva i dati in Adobe Experience Platform mappando i segmenti sulle destinazioni. A questo scopo, segui i passaggi seguenti.
seo-description: Attiva i dati in Adobe Experience Platform mappando i segmenti sulle destinazioni. A questo scopo, segui i passaggi seguenti.
translation-type: tm+mt
source-git-commit: 0992b223a96b77446a9f9c2823f5195541dd93fa
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# Attivare profili e segmenti in una destinazione

## Panoramica {#overview}

Attiva i dati in [!DNL Adobe Experience Platform] mappando i segmenti sulle destinazioni. A questo scopo, segui i passaggi seguenti.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario aver collegato correttamente [una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura una o più destinazioni.

## Attiva i dati {#activate-data}

I passaggi nel flusso di lavoro di attivazione variano leggermente tra i tipi di destinazione. Il flusso di lavoro completo per tutti i tipi di destinazione è descritto di seguito.

## Selezionare la destinazione in cui attivare i dati in {#select-destination}

Si applica a: Tutte le destinazioni

Nell’interfaccia utente di Adobe Experience Platform, passa a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** e fai clic sul pulsante **[!UICONTROL Activate]** corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato nell’immagine seguente.

![attiva nella destinazione](../assets/ui/activate-destinations/browse-tab-activate.png)

Segui i passaggi della sezione successiva per selezionare i segmenti da attivare.

## [!UICONTROL Select Segments] step  {#select-segments}

Si applica a: Tutte le destinazioni

![Passaggio Seleziona segmenti](../assets/ui/activate-destinations/select-segments-icon.png)

Nel flusso di lavoro **[!UICONTROL Activate destination]**, nella pagina **[!UICONTROL Select Segments]** , seleziona uno o più segmenti da attivare nella destinazione. Seleziona **[!UICONTROL Next]** per passare al passaggio successivo.

![da segmenti a destinazione](../assets/ui/activate-destinations/email-select-segments.png)

## [!UICONTROL Identity mapping] step  {#identity-mapping}

Si applica a: destinazioni social e destinazione pubblicitaria Google Customer Match

![Passaggio di mappatura identità](../assets/ui/activate-destinations/identity-mapping-icon.png)

Per le destinazioni social, devi selezionare gli attributi di origine o i namespace di identità da mappare come identità di destinazione nella destinazione.

## Esempio: attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Facebook].

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se hai hashing gli indirizzi e-mail dei clienti durante l’inserimento dei dati in [!DNL Platform], in base a [!DNL Facebook] [requisiti di hashing e-mail](../catalog/social/facebook.md#email-hashing-requirements).
* Seleziona lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per conformarsi ai  [!DNL Facebook] requisiti.
* Seleziona lo spazio dei nomi `Phone_SHA256` come identità di origine se hai hashing i numeri di telefono durante l’inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing del numero di telefono](../catalog/social/facebook.md#phone-number-hashing-requirements).
* Seleziona lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Selezionare i namespace `IDFA` o `GAID` come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona lo spazio dei nomi `Extern_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mappatura identità](../assets/ui/activate-destinations/identity-mapping.png)

I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.

I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione.
![Trasformazione mappatura identità](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

## Esempio: attivazione dei dati sul pubblico in [!DNL Google Customer Match] {#example-gcm}

Questo è un esempio di mappatura corretta dell&#39;identità durante l&#39;attivazione dei dati sul pubblico in [!DNL Google Customer Match].

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se hai hashing gli indirizzi e-mail dei clienti durante l’inserimento dei dati in [!DNL Platform], in base a [!DNL Google Customer Match] [requisiti di hashing e-mail](../catalog/social/../advertising/google-customer-match.md).
* Seleziona lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono non crittografati. [!DNL Platform] cancellerà i numeri di telefono per conformarsi ai  [!DNL Google Customer Match] requisiti.
* Seleziona lo spazio dei nomi `Phone_SHA256_E.164` come identità di origine se hai hashing i numeri di telefono durante l’inserimento dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing del numero di telefono](../catalog/social/../advertising/google-customer-match.md).
* Seleziona lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da un altro tipo di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256_E.164` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256_E.164`.
* Selezionare i namespace `IDFA` o `GAID` come identità di destinazione quando i namespace di origine sono `IDFA` o `GAID`.
* Seleziona lo spazio dei nomi `User_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

![Mappatura identità](../assets/ui/activate-destinations/identity-mapping-gcm.png)

I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.

I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione.
![Trasformazione mappatura identità](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

## **[!UICONTROL Configure]** step  {#configure}

Si applica a: Destinazioni e-mail marketing e archiviazione cloud

![Configura passaggio](../assets/ui/activate-destinations/configure-icon.png)

[!DNL Adobe Experience Platform] esporta dati per destinazioni di marketing e archiviazione cloud e-mail sotto forma di  [!DNL CSV] file. Nel passaggio **[!UICONTROL Configure]** puoi configurare la pianificazione e i nomi dei file per ciascun segmento che stai esportando. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente i file di esportazione a 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo.
>
>I nomi dei file divisi vengono aggiunti con un numero che indica che il file fa parte di un’esportazione più grande, in quanto tale: `filename.csv`, `filename_2.csv`, `filename_3.csv`.


Per aggiungere una pianificazione per il segmento, seleziona **[!UICONTROL Create schedule]**.

![](../assets/ui/activate-destinations/configure-destination-schedule.png)

Viene visualizzata una finestra di dialogo che mostra le opzioni per creare la pianificazione dei segmenti.

* **Esportazione** file: È possibile esportare file completi o incrementali. L’esportazione di un file completo pubblica un’istantanea completa di tutti i profili idonei per quel segmento. L’esportazione di un file incrementale pubblica il delta di profili idonei per quel segmento dall’ultima esportazione.
* **Frequenza**: Se  **[!UICONTROL Export full files]** è selezionato, puoi esportare  **[!UICONTROL Once]** o  **[!UICONTROL Daily]**. Se è selezionato **[!UICONTROL Export incremental files]**, è possibile esportare solo **[!UICONTROL Daily]**. L’esportazione di un file **[!UICONTROL Once]** esporta il file una sola volta. L’esportazione di un file **[!UICONTROL Daily]** esporta il file ogni giorno dalla data di inizio alla data di fine alle 12:00 UTC (7:00 PM EST) se sono selezionati file completi e alle 12:00 UTC (7:00 AM EST) se sono selezionati file incrementali.
* **Data**: Se  **[!UICONTROL Once]** è selezionata, puoi selezionare la data dell’esportazione una tantum. Se è selezionato **[!UICONTROL Daily]**, puoi selezionare le date di inizio e di fine per le esportazioni.

![](../assets/ui/activate-destinations/export-full-file.png)

I nomi file predefiniti sono costituiti dal nome di destinazione, dall’ID del segmento e da un indicatore di data e ora. Ad esempio, puoi modificare i nomi dei file esportati per distinguere tra campagne diverse o per far sì che il tempo di esportazione dei dati sia aggiunto ai file.

Seleziona l’icona a forma di matita per aprire una finestra modale e modificare i nomi dei file. I nomi dei file sono limitati a 255 caratteri.

![configura nome file](../assets/ui/activate-destinations/configure-name.png)

Nell’editor dei nomi dei file, puoi selezionare diversi componenti da aggiungere al nome del file. Impossibile rimuovere il nome di destinazione e l’ID del segmento dai nomi dei file. Oltre a questi, puoi aggiungere quanto segue:

* **[!UICONTROL Segment name]**: Puoi aggiungere il nome del segmento al nome del file.
* **[!UICONTROL Date and time]**: Seleziona tra l’aggiunta di un  `MMDDYYYY_HHMMSS` formato o di una marca temporale Unix a 10 cifre dell’ora in cui vengono generati i file. Scegliere una di queste opzioni se si desidera che i file abbiano un nome file dinamico generato con ogni esportazione incrementale.
* **[!UICONTROL Custom text]**: Aggiungi testo personalizzato ai nomi dei file.

Seleziona **[!UICONTROL Apply changes]** per confermare la selezione.

>[!IMPORTANT]
> 
>Se non selezioni il componente **[!UICONTROL Date and Time]**, i nomi dei file saranno statici e il nuovo file esportato sovrascriverà il file precedente nel percorso di archiviazione con ogni esportazione. Quando esegui un processo di importazione ricorrente da un percorso di archiviazione in una piattaforma di marketing e-mail, questa è l’opzione consigliata.

![modifica opzioni nome file](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

Al termine della configurazione di tutti i segmenti, seleziona **[!UICONTROL Next]** per continuare.

## **[!UICONTROL Segment schedule]** step  {#segment-schedule}

Si applica a: destinazioni pubblicitarie, destinazioni social

![passo della pianificazione del segmento](../assets/ui/activate-destinations/segment-schedule-icon.png)

Nella pagina **[!UICONTROL Segment schedule]** puoi impostare la data di inizio dell’invio dei dati alla destinazione e la frequenza dell’invio dei dati alla destinazione.

>[!IMPORTANT]
>
>Per le destinazioni social, in questo passaggio devi selezionare l’origine del pubblico. Puoi passare al passaggio successivo solo dopo aver selezionato una delle opzioni nell’immagine seguente.

![Origine del pubblico su Facebook](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>Per Customer Match di Google, è necessario fornire [!UICONTROL App ID] in questo passaggio, quando si attivano i segmenti [!DNL IDFA] o [!DNL GAID].

![entrare in app id](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

## **[!UICONTROL Scheduling]** step  {#scheduling}

Si applica a: destinazioni e-mail marketing e cloud storage

![passo della pianificazione del segmento](../assets/ui/activate-destinations/scheduling-icon.png)

Nella pagina **[!UICONTROL Scheduling]** è possibile visualizzare la data di inizio dell’invio dei dati alla destinazione e la frequenza dell’invio dei dati alla destinazione. Questi valori non possono essere modificati.

## **[!UICONTROL Select attributes]** step  {#select-attributes}

Si applica a: destinazioni e-mail marketing e cloud storage

![passaggio seleziona attributi](../assets/ui/activate-destinations/select-attributes-icon.png)

Nella pagina **[!UICONTROL Select attributes]** , seleziona **[!UICONTROL Add new field]** e scegli gli attributi che desideri inviare alla destinazione.

>[!NOTE]
>
> Adobe Experience Platform precompila la selezione con quattro attributi consigliati e di uso comune dallo schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Le esportazioni di file variano nei seguenti modi, a seconda che sia selezionato `segmentMembership.status`:
* Se il campo `segmentMembership.status` è selezionato, i file esportati includono i membri **[!UICONTROL Active]** nello snapshot completo iniziale e i membri **[!UICONTROL Active]** e **[!UICONTROL Expired]** nelle esportazioni incrementali successive.
* Se il campo `segmentMembership.status` non è selezionato, i file esportati includono solo i membri **[!UICONTROL Active]** nello snapshot completo iniziale e nelle esportazioni incrementali successive.

![attributi consigliati](../assets/ui/activate-destinations/mark-mandatory.png)

Inoltre, puoi contrassegnare attributi diversi come obbligatori. Contrassegnando un attributo come obbligatorio, questo viene reso in modo che il segmento esportato debba contenere tale attributo. Di conseguenza, può essere utilizzato come ulteriore forma di filtro. La marcatura di un attributo come obbligatorio è **non** obbligatoria.

È consigliabile che uno degli attributi sia un [identificatore univoco](../../destinations/catalog/email-marketing/overview.md#identity) dallo schema. Per ulteriori informazioni sugli attributi obbligatori, consulta la sezione identità nella documentazione [Destinazioni di marketing e-mail](../../destinations/catalog/email-marketing/overview.md#identity) .

>[!NOTE]
> 
>Se sono state applicate etichette di utilizzo dei dati a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione si verifica nelle seguenti condizioni:
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.

>
> 
Ad esempio, se nel campo `person.name.firstName` sono presenti alcune etichette di utilizzo dei dati in conflitto con l’azione di marketing della destinazione, nel passaggio di revisione viene visualizzata una violazione dei criteri di utilizzo dei dati. Per ulteriori informazioni, consulta [Governance dei dati in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## **[!UICONTROL Review]** step  {#review}

Si applica a: tutte le destinazioni

![passaggio di revisione](../assets/ui/activate-destinations/review-icon.png)

Nella pagina **[!UICONTROL Review]** è disponibile un riepilogo della selezione. Seleziona **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** per modificare le impostazioni oppure **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione dei criteri](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione relativa alla governance dei dati .

![violazione dei criteri dei dati](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, seleziona **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![confirm-selection](../assets/ui/activate-destinations/confirm-selection.png)

## Modifica attivazione {#edit-activation}

Per modificare i flussi di attivazione esistenti in Adobe Experience Platform, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, quindi fai clic sulla scheda **[!UICONTROL Browse]** e fai clic sul nome della destinazione.
2. Seleziona **[!UICONTROL Edit activation]** nella barra a destra per modificare i segmenti da inviare alla destinazione.

## Verifica che l&#39;attivazione del segmento sia avvenuta correttamente {#verify-activation}

### Destinazioni e-mail marketing e destinazioni di archiviazione cloud {#esp-and-cloud-storage}

Per le destinazioni di e-mail marketing e l’archiviazione cloud, Adobe Experience Platform crea un file `.csv` o `.txt` delimitato da tabulazioni nel percorso di archiviazione fornito. Attendi la creazione di un nuovo file nel percorso di archiviazione ogni giorno. Il formato predefinito del file è:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

È possibile modificare il formato del file. Per ulteriori informazioni, passa al passaggio [Configura](#configure) per le destinazioni di archiviazione cloud e di marketing e-mail.

Con il formato di file predefinito, i file che si riceverebbero in tre giorni consecutivi potrebbero essere così:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presenza di questi file nel percorso di archiviazione è la conferma di un&#39;attivazione riuscita. Per comprendere come sono strutturati i file esportati, è possibile [scaricare un file .csv di esempio](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Questo file di esempio include gli attributi del profilo `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` e `personalEmail.address`.

## Destinazioni pubblicitarie

Controlla il tuo account nella rispettiva destinazione pubblicitaria a cui stai attivando i tuoi dati. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono popolati nella piattaforma pubblicitaria.

## Destinazioni social network

Per [!DNL Facebook], una corretta attivazione implica la creazione programmatica di un pubblico personalizzato [!DNL Facebook] in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) a livello di programmazione. L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta le versioni precedenti del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL Facebook] quando attivi i segmenti nella destinazione.

## Disattiva attivazione {#disable-activation}

Per disabilitare un flusso di attivazione esistente, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, quindi fai clic sulla scheda **[!UICONTROL Browse]** e fai clic sul nome della destinazione.
2. Fai clic sul controllo **[!UICONTROL Enabled]** nella barra a destra per modificare lo stato del flusso di attivazione.
3. Nella finestra **Aggiorna stato flusso dati**, selezionare **Conferma** per disabilitare il flusso di attivazione.
