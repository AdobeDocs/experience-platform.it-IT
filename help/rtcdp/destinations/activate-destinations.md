---
title: Attivare profili e segmenti su una destinazione
seo-title: Attivare profili e segmenti su una destinazione
description: Attiva i dati di cui disponi  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
seo-description: Attiva i dati di cui disponi  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
translation-type: tm+mt
source-git-commit: be4cf64c89a189a09a4a7774c8fadc76c6ee8458
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# Attivare profili e segmenti su una destinazione

Attiva i dati di cui disponi  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.

## Prerequisiti  {#prerequisites}

Per attivare i dati sulle destinazioni, è necessario aver [collegato correttamente una destinazione](/help/rtcdp/destinations/connect-destination.md). Se non lo avete ancora fatto, andate al catalogo [delle](/help/rtcdp/destinations/destinations-catalog.md)destinazioni, sfogliate le destinazioni supportate e configurate una o più destinazioni.

## Attivare i dati {#activate-data}

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**, seleziona la destinazione in cui vuoi attivare i segmenti.
2. Fare clic sul nome della destinazione. Viene quindi visualizzato il flusso Activate (Attiva).
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Si noti che se esiste già un flusso di attivazione per una destinazione, è possibile visualizzare i segmenti attualmente inviati alla destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi descritti di seguito per modificare i dettagli di attivazione.
3. Seleziona **[!UICONTROL Activate]**;
4. Nel **[!UICONTROL Activate destination]** flusso di lavoro, nella **[!UICONTROL Select Segments]** pagina, seleziona i segmenti da inviare alla destinazione.
   ![segmenti-a-destinazione](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *Condizionale*. Questo passaggio varia a seconda del tipo di destinazione in cui vengono attivati i segmenti. <br> Per le destinazioni *di marketing* e-mail e le destinazioni *di archiviazione* cloud, nella **[!UICONTROL Select Attributes]** pagina selezionate **[!UICONTROL Add new field]** e selezionate gli attributi che desiderate inviare alla destinazione.
È consigliabile che uno degli attributi sia un identificatore [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) univoco dello schema di unione. Per ulteriori informazioni sugli attributi obbligatori, vedi Identità nell&#39;articolo Destinazioni [di marketing](/help/rtcdp/destinations/email-marketing-destinations.md#identity) e-mail.

   >[!NOTE]
   > 
   >Se sono state applicate etichette di utilizzo dei dati a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione avviene alle seguenti condizioni:
   >* I campi vengono utilizzati nella definizione del segmento.
   >* I campi sono configurati come attributi proiettati per la destinazione di destinazione.

   >
   > Considerate lo screenshot riportato di seguito. Se, ad esempio, nel campo `person.name.first.Name` erano presenti alcune etichette di utilizzo dei dati in conflitto con il caso di utilizzo marketing della destinazione, nel passaggio 7 viene mostrata una violazione del criterio di utilizzo dei dati. Per ulteriori informazioni, consulta Governance dei [dati in CDP in tempo reale](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![destination-attribute](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Per le destinazioni ** social, nel **[!UICONTROL Identity mapping]** passaggio potete selezionare gli attributi di origine da mappare come identità di destinazione nella destinazione. Questo passaggio è facoltativo o obbligatorio, a seconda dell&#39;identità primaria utilizzata nello schema. <br> 

   *Indirizzo e-mail come identità* principale: Se nello schema si utilizza l&#39;indirizzo e-mail come identità principale, è possibile ignorare il passaggio di mappatura identità, come illustrato di seguito:

   ![Indirizzo e-mail come identità](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Un altro ID come identità* principale: Se si utilizza un altro ID, ad esempio *Rewards ID* o *Loyalty ID*, come identità primaria nello schema, è necessario mappare manualmente l&#39;indirizzo e-mail dallo schema di identità come identità di destinazione nella destinazione social, come illustrato di seguito:

   ![ID fedeltà come identità](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Selezionate `Email_LC_SHA256` come identità di destinazione se avete hashing gli indirizzi e-mail dei clienti durante l&#39;inserimento di dati in  Adobe Experience Platform, in base ai requisiti [!DNL Facebook] di hashing [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)e-mail. <br> Selezionate `Email` come identità di destinazione se gli indirizzi e-mail utilizzati non sono crittografati.  CDP in tempo reale Adobe eseguirà l&#39;hash degli indirizzi e-mail per soddisfare [!DNL Facebook] i requisiti.

   ![mappatura identità dopo la compilazione dei campi](/help/rtcdp/destinations/assets/identity-mapping.png)

6. Sulla **[!UICONTROL Segment schedule]** pagina è possibile visualizzare la data di inizio dell&#39;invio dei dati alla destinazione, nonché la frequenza dell&#39;invio dei dati alla destinazione.

   >[!IMPORTANT]
   >
   >Per le destinazioni social, devi selezionare l&#39;origine del pubblico in questo passaggio. Puoi passare al passaggio successivo solo dopo aver selezionato una delle opzioni nell’immagine sottostante.

   ![scegli origine dati](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Nella **[!UICONTROL Review]** pagina viene visualizzato un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** modificare le impostazioni o **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

   >[!IMPORTANT]
   >
   >In questo passaggio, la funzione CDP in tempo reale verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione](/help/rtcdp/privacy/data-governance-overview.md#enforcement) dei criteri nella sezione relativa alla governance dei dati.

![conferma selezione](/help/rtcdp/destinations/assets/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionate **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](/help/rtcdp/destinations/assets/confirm-selection.png)



## Modifica attivazione {#edit-activation}

Per modificare i flussi di attivazione esistenti nel CDP in tempo reale, effettuate le seguenti operazioni:

1. Selezionate **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, fate clic sulla **[!UICONTROL Browse]** scheda e quindi sul nome della destinazione.
2. Seleziona **[!UICONTROL Edit activation]** nella barra a destra per cambiare i segmenti da inviare alla destinazione.

## Verificare che l&#39;attivazione del segmento sia stata eseguita correttamente {#verify-activation}

### Destinazioni di marketing e-mail e destinazioni di archiviazione cloud {#esp-and-cloud-storage}

Per le destinazioni di e-mail marketing e per l’archiviazione cloud,  CDP in tempo reale crea un file `.csv` `.txt` o delimitato da tabulazioni nel percorso di archiviazione specificato. È previsto che ogni giorno venga creato un nuovo file nel percorso di archiviazione. The file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

I file che si riceverebbero per tre giorni consecutivi potrebbero essere come segue:

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presenza di questi file nel percorso di memorizzazione conferma l’avvenuta riuscita dell’attivazione. Per comprendere la struttura dei file esportati, potete [scaricare un file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv di esempio. Questo file di esempio include gli attributi di profilo `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`e `personalEmail.address`.

### Destinazioni pubblicitarie

Controlla il tuo account nella rispettiva destinazione pubblicitaria a cui stai attivando i tuoi dati. Se l&#39;attivazione ha avuto esito positivo, i tipi di pubblico vengono popolati nella piattaforma pubblicitaria.

### Destinazioni social network

Ad [!DNL Facebook]esempio, un&#39;attivazione riuscita implica la creazione di un&#39;audience personalizzata a livello di programmazione in [!DNL Facebook] [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L&#39;integrazione tra  CDP in tempo reale del Adobe e [!DNL Facebook] supporta le ricadute storiche del pubblico. Tutte le qualifiche del segmento storico vengono inviate a [!DNL Facebook] quando si attivano i segmenti alla destinazione.

## Disattiva attivazione {#disable-activation}

Per disattivare un flusso di attivazione esistente, effettuate le seguenti operazioni:

1. Selezionate **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, fate clic sulla **[!UICONTROL Browse]** scheda e quindi sul nome della destinazione.
2. Fate clic sul **[!UICONTROL Enabled]** controllo nella barra a destra per modificare lo stato del flusso di attivazione.
3. Nella finestra **Aggiorna stato** flusso dati, selezionare **Conferma** per disattivare il flusso di attivazione.
