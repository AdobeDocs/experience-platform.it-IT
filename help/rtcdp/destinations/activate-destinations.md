---
title: Attivare profili e segmenti su una destinazione
seo-title: Attivare profili e segmenti su una destinazione
description: Attiva i dati di cui disponi in  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
seo-description: Attiva i dati di cui disponi in  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
translation-type: tm+mt
source-git-commit: 5387959496da3b1a6323f173154d769090a1fd40
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---


# Attivare profili e segmenti su una destinazione

Attiva i dati di cui disponi in  Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.

## Prerequisiti  {#prerequisites}

Per attivare i dati sulle destinazioni, è necessario aver [collegato correttamente una destinazione](/help/rtcdp/destinations/connect-destination.md). Se non lo avete ancora fatto, andate al catalogo [delle](/help/rtcdp/destinations/destinations-catalog.md)destinazioni, sfogliate le destinazioni supportate e configurate una o più destinazioni.

## Attivare i dati {#activate-data}

I passaggi del flusso di lavoro di attivazione variano leggermente tra i tipi di destinazione. Il flusso di lavoro completo per tutti i tipi di destinazione è descritto di seguito.

### Selezionare la destinazione a cui attivare i dati {#select-destination}

Si applica a: Tutte le destinazioni

1. Nell’interfaccia utente CDP in tempo reale del Adobe , andate a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**, quindi selezionate la destinazione in cui desiderate attivare i segmenti.
   ![passa alla destinazione](assets/oracle-eloqua-connect.png)
2. Fare clic sul nome della destinazione. Consente di passare al flusso di lavoro di attivazione.
   ![activate-flow](assets/activate-flow.png)Nota: se esiste già un flusso di lavoro di attivazione per una destinazione, puoi vedere i segmenti attualmente attivati nella destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi descritti di seguito per modificare i dettagli di attivazione.
3. Seleziona **[!UICONTROL Activate]**.

<br> 

### **[!UICONTROL Select Segments]** step {#select-segments}

Si applica a: Tutte le destinazioni

![Seleziona il passaggio dei segmenti](/help/rtcdp/destinations/assets/select-segments-icon.png)


Nel **[!UICONTROL Activate destination]** flusso di lavoro, nella **[!UICONTROL Select Segments]** pagina, seleziona uno o più segmenti da attivare nella destinazione. Premere **[!UICONTROL Next]** per passare al passaggio successivo.
![segmenti-a-destinazione](assets/email-select-segments.png)

<br> 

### **[!UICONTROL Identity mapping]** step {#identity-mapping}

![Passaggio mappatura identità](/help/rtcdp/destinations/assets/identity-mapping-icon.png)

Si applica a: destinazioni social e destinazione pubblicitaria di Google Customer Match

Per le destinazioni ** social, nel **[!UICONTROL Identity mapping]** passaggio potete selezionare gli attributi di origine da mappare come identità di destinazione nella destinazione. Questo passaggio è facoltativo o obbligatorio, a seconda dell&#39;identità primaria utilizzata nello schema. <br> 

*Indirizzo e-mail come identità* principale: Se nello schema si utilizza l&#39;indirizzo e-mail come identità principale, è possibile ignorare il passaggio di mappatura identità, come illustrato di seguito:

![Indirizzo e-mail come identità](assets/email-as-identity.gif)

<br> 

*Un altro ID come identità* principale: Se si utilizza un altro ID, ad esempio *Rewards ID* o *Loyalty ID*, come identità primaria nello schema, è necessario mappare manualmente l&#39;indirizzo e-mail dallo schema di identità come identità di destinazione nella destinazione social, come illustrato di seguito:

![ID fedeltà come identità](assets/rewardsid-as-identity.gif)


Selezionate `Email_LC_SHA256` come identità di destinazione se avete hashing gli indirizzi e-mail dei clienti durante l&#39;inserimento di dati in Adobe Experience Platform, in base ai requisiti [!DNL Facebook] di hashing delle [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)e-mail. <br> Selezionate `Email` come identità di destinazione se gli indirizzi e-mail utilizzati non sono crittografati.  CDP in tempo reale Adobe eseguirà l&#39;hash degli indirizzi e-mail per soddisfare [!DNL Facebook] i requisiti.

![mappatura identità dopo la compilazione dei campi](assets/identity-mapping.png)

<br> 

### **[!UICONTROL Configure]** step {#configure}

Si applica a: Destinazioni di marketing e-mail e destinazioni di archiviazione cloud

![Configura passaggio](/help/rtcdp/destinations/assets/configure-icon.png)

Questo passaggio è facoltativo. Nel **[!UICONTROL Configure]** passaggio, puoi configurare i nomi dei file per ogni segmento che stai esportando. I nomi di file predefiniti sono costituiti dal nome di destinazione, dall’ID segmento e da un indicatore di data e ora. Ad esempio, è possibile modificare i nomi dei file esportati per distinguere tra campagne diverse o per fare in modo che il tempo di esportazione dei dati venga aggiunto ai file.

Selezionare **[!UICONTROL Next]** per utilizzare i nomi file predefiniti oppure fare clic sull&#39;icona matita per aprire una finestra modale e modificare i nomi dei file. I nomi dei file possono contenere un massimo di 255 caratteri.

![configura nome file](assets/activation-workflow-configure-step.png)

Nell’editor dei nomi file potete selezionare diversi componenti da aggiungere al nome file. Impossibile rimuovere il nome di destinazione e l&#39;ID del segmento dai nomi dei file. Oltre a questi, potete aggiungere quanto segue:

* **[!UICONTROL Segment name]**: Potete aggiungere il nome del segmento al nome del file.
* **[!UICONTROL Date and time]**: Selezionate tra l’aggiunta di un `MMDDYYYY_HHMMSS` formato o di una marca temporale Unix di 10 cifre relativa all’ora in cui i file vengono generati. Selezionare una di queste opzioni se si desidera che i file abbiano un nome di file dinamico generato con ogni esportazione incrementale.
* **[!UICONTROL Custom text]**: Aggiungere testo personalizzato ai nomi dei file.

Select **[!UICONTROL Apply changes]** to confirm your selection.

>[!IMPORTANT]
> 
>Se non selezionate il **[!UICONTROL Date and Time]** componente, i nomi dei file saranno statici e il nuovo file esportato sovrascriverà il file precedente nel percorso di memorizzazione con ogni esportazione. Quando si esegue un processo di importazione periodico da una posizione di archiviazione in una piattaforma di e-mail marketing, questa è l&#39;opzione consigliata.

![modificare le opzioni del nome del file](assets/activate-workflow-configure-step-2.png)

<br> 

### **[!UICONTROL Segment Schedule]** step {#segment-schedule}

Si applica a: destinazioni pubblicitarie, destinazioni social

![fase di pianificazione del segmento](/help/rtcdp/destinations/assets/segment-schedule-icon.png)

Sulla **[!UICONTROL Segment schedule]** pagina è possibile impostare la data iniziale per l&#39;invio dei dati alla destinazione, nonché la frequenza di invio dei dati alla destinazione.

>[!IMPORTANT]
>
>Per le destinazioni social, devi selezionare l&#39;origine del pubblico in questo passaggio. Puoi passare al passaggio successivo solo dopo aver selezionato una delle opzioni nell’immagine sottostante.

![scegli origine dati](assets/choose-data-origin.png)

<br> 

### **[!UICONTROL Scheduling]** step {#scheduling}

Si applica a: destinazioni di e-mail marketing e archiviazione cloud

![fase di pianificazione del segmento](assets/scheduling-icon.png)

Sulla **[!UICONTROL Scheduling]** pagina è possibile visualizzare la data di inizio per l&#39;invio dei dati alla destinazione e la frequenza di invio dei dati alla destinazione. Questi valori non possono essere modificati.

<br> 

### **[!UICONTROL Select attributes]** step {#select-attributes}

Si applica a: destinazioni di e-mail marketing e archiviazione cloud

![seleziona passaggio attributi](/help/rtcdp/destinations/assets/select-attributes-icon.png)


Nella **[!UICONTROL Select Attributes]** pagina, selezionate **[!UICONTROL Add new field]** e selezionate gli attributi che desiderate inviare alla destinazione.

>[!NOTE]
>
>  CDP in tempo reale precompila la selezione con quattro attributi consigliati e comunemente utilizzati dallo schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Le esportazioni di file variano come segue, a seconda che `segmentMembership.status` sia selezionato o meno:
* Se il `segmentMembership.status` campo è selezionato, i file esportati includono i membri **Attivo** nello snapshot completo iniziale e i membri **Attivo** e **Scaduto** nelle esportazioni incrementali successive.
* Se il `segmentMembership.status` campo non è selezionato, i file esportati includono solo i membri **attivi** nello snapshot completo iniziale e nelle esportazioni incrementali successive.

![attributi consigliati](/help/rtcdp/destinations/assets/recommended-attributes.png)


È consigliabile che uno degli attributi sia un identificatore [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) univoco dello schema. Per ulteriori informazioni sugli attributi obbligatori, vedi Identità nell&#39;articolo Destinazioni [di marketing](/help/rtcdp/destinations/email-marketing-destinations.md#identity) e-mail.

>[!NOTE]
> 
>Se sono state applicate etichette di utilizzo dei dati a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione avviene alle seguenti condizioni:
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.

>
> 
Considerate lo screenshot riportato di seguito. Se, ad esempio, nel campo `person.name.firstName` erano presenti alcune etichette di utilizzo dei dati in conflitto con il caso di utilizzo marketing della destinazione, nel passaggio della revisione viene mostrata una violazione del criterio di utilizzo dei dati (passaggio 9). Per ulteriori informazioni, vedi [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations)in tempo reale.

![destination-attribute](assets/select-attributes-step.png)

<br> 

### **[!UICONTROL Review]** step {#review}

Si applica a: tutte le destinazioni

![fase di revisione](/help/rtcdp/destinations/assets/review-icon.png)

Nella **[!UICONTROL Review]** pagina viene visualizzato un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** modificare le impostazioni o **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, la funzione CDP in tempo reale verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione](/help/rtcdp/privacy/data-governance-overview.md#enforcement) dei criteri nella sezione relativa alla governance dei dati.

![violazione dei criteri di dati](assets/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionate **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](assets/confirm-selection.png)


## Modifica attivazione {#edit-activation}

Per modificare i flussi di attivazione esistenti nel CDP in tempo reale, effettuate le seguenti operazioni:

1. Selezionate **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, fate clic sulla **[!UICONTROL Browse]** scheda e quindi sul nome della destinazione.
2. Seleziona **[!UICONTROL Edit activation]** nella barra a destra per cambiare i segmenti da inviare alla destinazione.

## Verificare che l&#39;attivazione del segmento sia stata eseguita correttamente {#verify-activation}

### Destinazioni di marketing e-mail e destinazioni di archiviazione cloud {#esp-and-cloud-storage}

Per le destinazioni di e-mail marketing e per l’archiviazione cloud,  CDP in tempo reale crea un file `.csv` `.txt` o delimitato da tabulazioni nel percorso di archiviazione specificato. È previsto che ogni giorno venga creato un nuovo file nel percorso di archiviazione. Il formato predefinito del file è:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

È possibile modificare il formato del file. Per ulteriori informazioni, vai al passaggio [Configura](/help/rtcdp/destinations/activate-destinations.md#configure) per le destinazioni di archiviazione cloud e di marketing e-mail.

Con il formato di file predefinito, i file che si riceverebbero per tre giorni consecutivi potrebbero essere simili al seguente:

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presenza di questi file nel percorso di memorizzazione conferma l’avvenuta riuscita dell’attivazione. Per comprendere la struttura dei file esportati, potete [scaricare un file](assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv di esempio. Questo file di esempio include gli attributi di profilo `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`e `personalEmail.address`.

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
