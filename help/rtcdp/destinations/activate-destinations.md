---
title: Attivare profili e segmenti su una destinazione
seo-title: Attivare profili e segmenti su una destinazione
description: Attiva i dati di cui disponi in Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
seo-description: Attiva i dati di cui disponi in Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Attivare profili e segmenti su una destinazione

Attiva i dati di cui disponi in Adobe Real-time Customer Data Platform mappando i segmenti alle destinazioni. A questo scopo, attenetevi alla procedura indicata di seguito.

## Prerequisiti  {#prerequisites}

Per attivare i dati sulle destinazioni, è necessario aver [collegato correttamente una destinazione](/help/rtcdp/destinations/assets/connect-destination.png). Se non lo avete ancora fatto, andate al catalogo [delle](/help/rtcdp/destinations/destinations-catalog.md)destinazioni, sfogliate le destinazioni supportate e configurate una o più destinazioni.

## Attivare i dati {#activate-data}

1. In **[!UICONTROL Destinations > Browse]**, seleziona la destinazione in cui vuoi attivare i segmenti.
2. Fare clic sul nome della destinazione. Viene quindi visualizzato il flusso Activate (Attiva).
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Si noti che se esiste già un flusso di attivazione per una destinazione, è possibile visualizzare i segmenti attualmente inviati alla destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi descritti di seguito per modificare i dettagli di attivazione.
3. Seleziona **[!UICONTROL Activate]**;
4. Nel **[!UICONTROL Activate destination]** flusso di lavoro, nella **[!UICONTROL Select Segments]** pagina, seleziona i segmenti da inviare alla destinazione.
   ![segmenti-a-destinazione](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condizionale*. Questo passaggio si applica solo ai segmenti mappati a destinazioni di marketing e-mail. <br> Nella **[!UICONTROL Destination Attributes]** pagina, selezionate **[!UICONTROL Add new field]** e selezionate gli attributi che desiderate inviare alla destinazione.
È consigliabile che uno degli attributi sia un identificatore [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) univoco dello schema di unione. Per ulteriori informazioni sugli attributi obbligatori, vedi Identità nell&#39;articolo Destinazioni [di marketing](/help/rtcdp/destinations/email-marketing-destinations.md#identity) e-mail.
   ![destination-attribute](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Sulla **[!UICONTROL Segment schedule]** pagina è possibile visualizzare la data di inizio dell&#39;invio dei dati alla destinazione, nonché la frequenza dell&#39;invio dei dati alla destinazione.

   >[!IMPORTANT]
   >
   >Per le destinazioni social, devi selezionare l&#39;origine del pubblico in questo passaggio. Puoi passare al passaggio successivo solo dopo aver selezionato una delle opzioni nell’immagine sottostante.

   ![scegli origine dati](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Nella **[!UICONTROL Review]** pagina viene visualizzato un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** modificare le impostazioni o **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](/help/rtcdp/destinations/assets/confirm-selection.png)

## Modifica attivazione {#edit-activation}

Per modificare i flussi di attivazione esistenti nel CDP in tempo reale, effettuate le seguenti operazioni:

1. Selezionate **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, fate clic sulla **[!UICONTROL Browse]** scheda e quindi sul nome della destinazione.
2. Seleziona **[!UICONTROL Edit activation]** nella barra a destra per cambiare i segmenti da inviare alla destinazione.

## Verificare che l&#39;attivazione del segmento sia stata eseguita correttamente {#verify-activation}

### Destinazioni di marketing e-mail e destinazioni di archiviazione cloud

Per le destinazioni di e-mail marketing e di archiviazione cloud, Adobe Real-time CDP crea un `.txt` `.csv` file o un file delimitato da tabulazioni nel percorso di archiviazione specificato. È previsto che ogni giorno venga creato un nuovo file nel percorso di archiviazione. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

I file che si riceverebbero per tre giorni consecutivi potrebbero essere come segue:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La presenza di questi file nel percorso di memorizzazione conferma l’avvenuta riuscita dell’attivazione.

### Destinazioni pubblicitarie

Controllate la rispettiva destinazione pubblicitaria a cui state attivando i dati. Se l&#39;attivazione ha avuto esito positivo, i tipi di pubblico vengono popolati nella piattaforma pubblicitaria.

### Destinazioni social network

Per Facebook, un&#39;attivazione di successo significa che un&#39;audience personalizzata di Facebook verrà creata in modo programmatico in [Facebook Ads Manager](https://www.facebook.com/adsmanager/manage/). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

## Disattiva attivazione {#disable-activation}

Per disattivare un flusso di attivazione esistente, effettuate le seguenti operazioni:

1. Selezionate **[!UICONTROL Destinations]** nella barra di navigazione a sinistra, fate clic sulla **[!UICONTROL Browse]** scheda e quindi sul nome della destinazione.
2. Fate clic sul **[!UICONTROL Enabled]** controllo nella barra a destra per modificare lo stato del flusso di attivazione.
3. Nella finestra **Aggiorna stato** flusso dati, selezionare **Conferma** per disattivare il flusso di attivazione.

